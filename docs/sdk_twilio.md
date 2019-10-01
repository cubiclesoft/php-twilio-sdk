TwilioSDK Class:  'support/sdk_twilio.php'
==========================================

An ultra-lightweight PHP SDK for accessing Twilio APIs and emitting valid TwiML verbs in response to webhook calls.  Also works with [SignalWire](https://signalwire.com/)..

Examples can be found here:

https://github.com/cubiclesoft/php-twilio-sdk/

TwilioSDK::SetAccessInfo($sid, $token, $apibase = "https://api.twilio.com/2010-04-01")
--------------------------------------------------------------------------------------

Access:  public

Parameters:

* $sid - A string containing a Twilio Account Sid.
* $token - A string containing a Twilio Account Token.
* $apibase - A string containing the base URL of a Twilio-compatible API.

Returns:  Nothing.

This function sets the baseline access information for later calls.

TwilioSDK::hash_hmac_internal($algo, $data, $key, $raw_output = false)
----------------------------------------------------------------------

Access:  _internal_ static

Parameters:  Same as the PHP function `hash_hmac()`.

Returns:  A string containing the HMAC.

This mostly internal static function implements an equivalent `hash_hmac()` function if the Hash extension is not available.  Only implements HMAC-MD5 and HMAC-SHA1 as a fallback.

TwilioSDK::ValidateWebhookRequest($checksig = true)
---------------------------------------------------

Access:  public

Parameters:

* $checksig - A boolean to indicate whether or not to check the incoming `X-Twilio-Signature` header (Default is true).

Returns:  Nothing.  Will exit with an error message if validation fails.

This function validates incoming webhook requests.  It checks the supplied Account Sid and, by default, the incoming signature on the request.  Validates that Twilio is the source of the request.

TwilioSDK::StartXMLResponse()
-----------------------------

Access:  public static

Parameters:  None.

Returns:  Nothing.

This static function emits the start of a TwiML response.

TwilioSDK::OpenXMLTag($tagname, $attrs = array(), $void = false)
----------------------------------------------------------------

Access:  public static

Parameters:

* $tagname - A string containing a TwiML verb.
* $attrs - An array containing key-value attributes (Default is array()).
* $void - A boolean that indicates whether or not this is a void tag (Default is false).

Returns:  Nothing.

This static function emits a new XML tag in the TwiML response.  For every call to this function that does not set `$void` to true, there must be a matching `CloseXMLTag()` call to emit correct XML.

TwilioSDK::AppendXMLData($str)
------------------------------

Access:  public static

Parameters:

* $str - A string to encode and emit.

Returns:  Nothing.

This static function encodes and emits the input string as valid content.

TwilioSDK::CloseXMLTag($tagname)
--------------------------------

Access:  public static

Parameters:

* $tagname - A string containing a TwiML verb.

Returns:  Nothing.

This static function emits a closing XML tag in the TwiML response.

TwilioSDK::OutputXMLTag($tagname, $attrs = array(), $str = "")
--------------------------------------------------------------

Access:  public static

Parameters:

* $tagname - A string containing a TwiML verb.
* $attrs - An array containing key-value attributes (Default is array()).
* $str - A string to encode and emit (Default is "").

Returns:  Nothing.

This static function emits a void tag when `$str` is empty and an open tag, appended string, and close tag when it `$str` is not empty.  Basically an all-in-one convenience function for most TwiML verbs.

TwilioSDK::EndXMLResponse()
---------------------------

Access:  public static

Parameters:  None.

Returns:  Nothing.

This static function emits the end of a TwiML response.

TwilioSDK::Internal_DownloadRecordingCallback($response, $data, $opts)
----------------------------------------------------------------------

Access:  _internal_

Parameters:

* $response - An array containing the current HTTP response line information.
* $body - A string containing the retrieve body content.
* $opts - An array containing file resource or callback information.

Returns:  A boolean of true.

This internal function processes downloaded file data as it is retrieved from the API.

TwilioSDK::DownloadRecording($sid, $format = ".wav", $filename = false)
-----------------------------------------------------------------------

Access:  public

Parameters:

* $sid - A string containing a Recording Sid.
* $format - A string containing one of '.wav' or '.mp3' (Default is ".wav").
* $filename - A boolean of false or a string containing a filename to write the downloaded file to (Default is false).

Returns:  A standard array of information.

This function downloads the specified recording as either a WAV or MP3 file.

TwilioSDK::RunAPI($method, $apipath, $postvars = array(), $options = array(), $expected = 200, $decodebody = true, $extension = ".json")
----------------------------------------------------------------------------------------------------------------------------------------

Access:  public

Parameters:

* $method - A string containing the API HTTP method (e.g. "GET", "POST", "DELETE").
* $apipath - A string containing the API to use (e.g. "Messages", "Recordings").
* $postvars - An array containing key-value pairs to use for a POST request (Default is array()).
* $options - An array containing additional options to pass to the underlying WebBrowser class (Default is array()).
* $expected - An integer containing the expected HTTP response code (Default is 200).
* $decodebody - A boolean indicating whether or not to decode the response body as JSON (Default is true).
* $extension - A string containing the request extension to use (Default is ".json").

Returns:  A standard array of information.

This function makes a single API call to the configured Twilio-compatible API.

TwilioSDK::Twilio_Translate($format, ...)
-----------------------------------------

Access:  _internal_ static

Parameters:

* $format - A string containing valid sprintf() format specifiers.

Returns:  A string containing a translation.

This internal static function takes input strings and translates them from English to some other language if CS_TRANSLATE_FUNC is defined to be a valid PHP function name.
