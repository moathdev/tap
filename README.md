# Laravel Tap payment

[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.md) 
[![Latest Version on Packagist](https://img.shields.io/packagist/v/Moathdev/tap?style=flat-square)](https://packagist.org/packages/moathdev/tap) 
[![Total Downloads](https://img.shields.io/packagist/dt/Moathdev/tap.svg?style=flat-square)](https://packagist.org/packages/thujohn/twitter) 
![GitHub Release Date](https://img.shields.io/github/release-date/moathdev/tap?label=latest%20release&style=flat-square)

Pay payment API for Laravel  7.x & 8.x

You need to create an Account and create your access token in the [Tap Payment website](https://www.tap.company/).

## Installation

```
composer require  moathdev/tap
```

## Configuration 

Just set the below environment variables in your `.env`. 

```
TAP_SECRET_KEY_LIVE=
TAP_SECRET_KEY_SANDBOX=
```

### Advanced configuration

Run `php artisan vendor:publish --provider="Moathdev\Tap\TapServiceProvider"`
```
/config/tap.php
```



# Usage

## Functions

### Charges

* `getCharge()` - Retrieves the details of a charge that has previously been created. Supply the unique charge id that was returned from your  previous request, and Tap will return the corresponding charge information. The same information is returned when creating the charge.
* `CreateCharge()` - To charge a credit card or debit card (Knet, mada, Visa, MasterCard) or an existing authorized transactions, you create a charge request. If your API key is in test mode, the card won't actually be charged, though everything else will occur as if in live mode.
* `UpdateCharge()` - Updates the specified charge by setting the values of the parameters passed. Any parameters not provided will be left unchanged.
* `getAllCharges()` - Returns a list of charges you’ve previously created. The charges are returned in sorted order, with the most recent charges appearing first.

## Examples

- Retrieve a Charge
```php
Route::get('/getCharge/{charge_id}', function($charge_id)
{
	$res = Tap::getCharge(['charge_id' => $charge_id]);

    dd($res);
});
```

- Create a Charge
```php
Route::get('/CreateCharge', function()
{
	    $res  = Tap::CreateCharge([
            'amount'=> 1,
            'currency' => 'SAR',
            'threeDSecure' => true,
            'save_card' => false,
            'description' => 'Test Description',
            'statement_descriptor' => 'Sample',
            'metadata' => [
                'udf1' => 'test 1',
                'udf2' => 'test 2',
            ],
            'reference' => [
                'transaction' => 'txn_0001',
                'order' => 'ord_0001',
            ],
            'receipt' => [
                'email' => false,
                'sms' => false,
            ],
            'customer' => [
                'first_name' => "test",
                'middle_name' => "test",
                'last_name' => "test",
                'email' => "test@test.com",
                'phone' => [
                    'country_code' => "965",
                    'number' => "50000000",
                ],
            ],
            'merchant' => [
                'id' => ''
            ],
            'source' => [
                'id' => 'src_all',
            ],
            'post' => [
                'url' => 'http://your_website.com/post_url'
            ],
            'redirect' => [
                'url' => 'http://your_website.com/post_url'
            ]
        ]);
        
        dd($res);
});
```

