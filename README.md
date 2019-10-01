Twilio SDK for PHP
==================

An ultra-lightweight PHP SDK for accessing Twilio APIs and emitting valid TwiML verbs in response to webhook calls.  Also works with [SignalWire](https://signalwire.com/).

[![Donate](https://cubiclesoft.com/res/donate-shield.png)](https://cubiclesoft.com/donate/)

Features
--------

* Does what it says on the tin in a mere 7KB of code.
* Works with [Twilio](https://www.twilio.com/) and [SignalWire](https://signalwire.com/).
* Has a liberal open source license.  MIT or LGPL, your choice.
* Designed for relatively painless integration into your project.
* Sits on GitHub for all of that pull request and issue tracker goodness to easily submit changes and ideas respectively.

Getting Started
---------------

Send a SMS message:

```php
<?php
	require_once "support/sdk_twilio.php";

	// Twilio Account Sid and Token.
	$twilio_sid = "YOUR_ACCOUNT_SID";
	$twilio_token = "YOUR_ACCOUNT_TOKEN";

	$twilio = new TwilioSDK();
	$twilio->SetAccessInfo($twilio_sid, $twilio_token);

	// For SignalWire, use:
//	$twilio->SetAccessInfo($twilio_sid, $twilio_token, "https://YOUR_SPACE.signalwire.com/api/laml/2010-04-01");

	$postvars = array(
		"From" => "+13145557878",  // Twilio phone number
		"To" => "+13145551212",    // Destination phone number
		"Body" => "SMS message to send."
	);

	$result = $twilio->RunAPI("POST", "Messages", $postvars);
	if (!$result["success"])
	{
		var_dump($result);

		exit();
	}
?>
```

Handle an incoming webhook call:

```php
<?php
	require_once "support/sdk_twilio.php";

	// Twilio Account Sid and Token.
	$twilio_sid = "YOUR_ACCOUNT_SID";
	$twilio_token = "YOUR_ACCOUNT_TOKEN";

	$twilio = new TwilioSDK();
	$twilio->SetAccessInfo($twilio_sid, $twilio_token);

	// Secure the request.
	$twilio->ValidateWebhookRequest();

	$twilio->StartXMLResponse();

	if (isset($_REQUEST["CallSid"]))
	{
		if (isset($_REQUEST["Digits"]) && $_REQUEST["Digits"] == "1")
		{
			$twilio->OutputXMLTag("Say", array(), "It's sunny and warm outside.");
		}
		else if (isset($_REQUEST["Digits"]) && $_REQUEST["Digits"] == "2")
		{
			$twilio->OutputXMLTag("Say", array(), "It's going to be a balmy 72 degrees outside today with a very slight chance of delicious pie falling from the sky.");
		}

		$options = array();
		$options[] = "Press 1 to get the weather.";
		$options[] = "Press 2 to get the forecast.";

		$twilio->OpenXMLTag("Gather", array("numDigits" => "1"));
		$twilio->OutputXMLTag("Say", array(), implode("  ", $options));
		$twilio->CloseXMLTag("Gather");

		$twilio->OutputXMLTag("Redirect", array(), Request::GetFullURLBase());
	}

	$twilio->EndXMLResponse();
?>
```

More Information
----------------

* [SDK documentation](https://github.com/cubiclesoft/php-twilio-sdk/blob/master/docs/sdk_twilio.md) - The TwilioSDK class documentation.
