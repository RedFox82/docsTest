---
layout: default
---
# Classes
## Miscellaneous

### [AbstractLeniency](./Miscellaneous/AbstractLeniency.md)


### [AsYouTypeFormatter](./Miscellaneous/AsYouTypeFormatter.md)




### [CustomPhoneFormattingAction](./Miscellaneous/CustomPhoneFormattingAction.md)


### [ExactGroupingLeniency](./Miscellaneous/ExactGroupingLeniency.md)


### [GenericTriggerHandler](./Miscellaneous/GenericTriggerHandler.md)


### [Leniency](./Miscellaneous/Leniency.md)

Leniency when finding potential phone numbers in text segments. The levels
here are ordered in increasing strictness.



### [Locale](./Miscellaneous/Locale.md)


### [MetadataLoader](./Miscellaneous/MetadataLoader.md)

Interface for clients to specify a customized phone metadata loader.
Note that implementation owners have the responsibility to ensure this is
thread-safe.



### [NumberFormat](./Miscellaneous/NumberFormat.md)


### [NumberParseException](./Miscellaneous/NumberParseException.md)


### [PhoneFormattingRequest](./Miscellaneous/PhoneFormattingRequest.md)


### [PhoneMetadata](./Miscellaneous/PhoneMetadata.md)


### [PhoneNumber](./Miscellaneous/PhoneNumber.md)


### [PhoneNumberMatch](./Miscellaneous/PhoneNumberMatch.md)




### [PhoneNumberMatcher](./Miscellaneous/PhoneNumberMatcher.md)

A stateful class that finds and extracts telephone numbers from {@linkplain String text}.
Instances can be created using the {@linkplain PhoneNumberUtil#findNumbers factory methods} in
[PhoneNumberUtil](./Miscellaneous/PhoneNumberUtil.md).
Vanity numbers (phone numbers using alphabetic digits such as &lt;tt&gt;1-800-SIX-FLAGS&lt;/tt&gt; ar&hellip;


### [PhoneNumberOfflineGeocoder](./Miscellaneous/PhoneNumberOfflineGeocoder.md)

An offline geocoder which provides geographical information related to a phone number.



### [PhoneNumberToCarrierMapper](./Miscellaneous/PhoneNumberToCarrierMapper.md)


### [PhoneNumberToTimeZonesMapper](./Miscellaneous/PhoneNumberToTimeZonesMapper.md)

An offline mapper from phone numbers to time zones.



### [PhoneNumberUtil](./Miscellaneous/PhoneNumberUtil.md)


### [PossibleLeniency](./Miscellaneous/PossibleLeniency.md)


### [ShortNumberInfo](./Miscellaneous/ShortNumberInfo.md)




### [StrictGroupingLeniency](./Miscellaneous/StrictGroupingLeniency.md)


### [StringBuilder](./Miscellaneous/StringBuilder.md)

Implementation of StringBuilder that can manipulate strings.
Based on Java implementation where String is immutable and
StringBuilder is mutable type. Internally it's just uses
Apex strings and their methods



### [TriggerHandlerDispatcher](./Miscellaneous/TriggerHandlerDispatcher.md)

Dispatches trigger-based events to implementations of <code>TriggerHandler</code> based on the current trigger context.



### [ValidLeniency](./Miscellaneous/ValidLeniency.md)

