# iPay88
[![Build Status](https://img.shields.io/packagist/dt/karyamedia/ipay88.svg?maxAge=2592000)](https://packagist.org/packages/karyamedia/ipay88) [![Join the chat at https://gitter.im/karyamedia/ipay88](https://badges.gitter.im/karyamedia/ipay88.svg)](https://gitter.im/karyamedia/ipay88?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

iPay88 payment gateway module.

**NOTE**: You are required to request demo account from support@ipay88.com.my

## Installation

I've make this project available to install via [Composer](https://getcomposer.org/) with following command:

```bash
$ composer require karyamedia/ipay88 dev-master
```

## Example Controller

```php
<?php

class Payment {

	protected $_merchantCode;
	protected $_merchantKey;

	public function __construct(){
		parent::__construct();
		/**
		 * MerchantCode confidential
		 * MerchantKey confidential
		 */
		$this->_merchantCode = 'xxxxxx';
		$this->_merchantKey = 'xxxxxxxxx';
	}

	public function index(){
		$request = new IPay88\Payment\Request($this->_merchantKey);
		
		$this->_data['merchantCode'] 		= $request->setMerchantCode($this->_merchantCode);
		$this->_data['paymentId'] 		= $request->setPaymentId(1);
		$this->_data['refNo'] 			= $request->setRefNo('EXAMPLE0001');
		$this->_data['amount'] 			= $request->setAmount('0.50');
		$this->_data['currency'] 		= $request->setCurrency('MYR');
		$this->_data['prodDesc'] 		= $request->setProdDesc('Testing');
		$this->_data['userName'] 		= $request->setUserName('Your name');
		$this->_data['userEmail'] 		= $request->setUserEmail('email@example.com');
		$this->_data['userContact'] 		= $request->setUserContact('0123456789');
		$this->_data['remark'] 			= $request->setRemark('Some remarks here..');
		$this->_data['lang'] 			= $request->setLang('UTF-8');
		$this->_data['signatureType']		= $request->getSignatureType('HMACSHA256'),
		$this->_data['signature'] 		= $request->getSignature();
		$this->_data['responseUrl'] 		= $request->setResponseUrl('http://example.com/response');
		$this->_data['backendUrl'] 		= $request->setBackendUrl('http://example.com/backend');

		IPay88\Payment\Request::make($this->_merchantKey, $this->_data);
	}

	public function response(){	
		$response = (new IPay88\Payment\Response)->init($this->_merchantCode);
		echo "<pre>";
		print_r($response);
	}
}
```

## Important Update from iPay88
Dear Valued Merchant,

We hope this message finds you well.

We are reaching out to notify you of an important update to the security of our iPay88 API payment system. As part
of our ongoing efforts to enhance the security and integrity of all transactions, we have upgraded our signature encryption algorithm from SHA-256 to HMAC-SHA512.

What this means for you:

All API requests to iPay88 will now require HMAC-SHA512 for signature generation and validation.

This upgrade provides an additional layer of security, enhancing resilience against potential vulnerabilities and safeguarding sensitive payment data.

Please update your integration to support the HMAC-SHA512 encryption algorithm before the deadline of
31st January 2025.

## Credits

[Shiro Amada](https://github.com/shiroamada)

[Leow Kah Thong](https://github.com/ktleow)

[Fikri Marhan](https://github.com/fikri-marhan)

[Pijoe](https://github.com/pijoe86)

[aa6my](https://github.com/aa6my)

## Reference
https://github.com/cchitsiang/ipay88

https://github.com/fastsafety/ipay88

## Lisence

MIT © [Karyamedia](https://github.com/karyamedia/karya). Please see [License File](LICENSE.md) for more information.
