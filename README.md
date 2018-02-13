Savano Payment
================
Savano Payment Gateway Extension For Yii2

Installation
==============
The preferred way to install this extension is through composer.

Either run
```
php composer.phar require amirkhh/savano
```
or add
```
"amirkhh/savano": "dev-master"
```
to the require section of your ``composer.json`` file.
    
How to use this extension
=========================
For example, imagine that you have a controller called this PaymentController at first you need 2 actions,
one of them is for request payment and another is verify payment.

you need to use an storage to save your payments and payments status.

``PaymentController.php``
```
..... 

<?php
public function actionVerify($au, $order_id)
{
    $pin = 'Your Pin';

    /* Fetch Price, OrderId and Authority in Your Storage */
    $authority = $au;
    $price     = 100;
    $orderId   = $order_id;

    $savano = new Savano;
    $savano->pin = $pin;

    if(($verify = $savano->verify($authority, $price, $orderId)->getResult()) === 1)
    {
        // Payment Successfully
        echo 'Payment Successfully';
    }
    else
    {
	// Show Error
        echo $savano->getErrorMessage();
    }
}

public function actionVerify($au, $order_id)
{
    $pin = 'Your Pin';

    /* Fetch Price, OrderId and Authority in Your Storage */
    $authority = $au;
    $price     = 100;
    $orderId   = $order_id;

    $savano = new Savano;
    $savano->pin = $pin;

    if(($verify = $savano->verify($authority, $price, $orderId)->getResult()) === 1)
    {
        // Payment Successfully
        echo 'Payment Successfully';
    }
    else
    {
	// Show Error
        echo $savano->getErrorMessage();
    }
}

public function beforeAction($action)
{
    if ($action->id == 'verify') {
        $this->enableCsrfValidation = false;
    }

    return parent::beforeAction($action);
}

.....
```
