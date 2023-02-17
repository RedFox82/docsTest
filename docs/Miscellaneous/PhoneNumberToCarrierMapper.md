# PhoneNumberToCarrierMapper

`APIVERSION: 47`

`STATUS: ACTIVE`
## Methods
### `static getInstance()`

Gets a [PhoneNumberToCarrierMapper](/Miscellaneous/PhoneNumberToCarrierMapper.md) instance to carry out international carrier lookup. <p> The [PhoneNumberToCarrierMapper](/Miscellaneous/PhoneNumberToCarrierMapper.md) is implemented as a singleton. Therefore, calling this method multiple times will only result in one instance being created.

#### Return

**Type**

PhoneNumberToCarrierMapper

**Description**

a [PhoneNumberToCarrierMapper](/Miscellaneous/PhoneNumberToCarrierMapper.md) instance

### `getNameForValidNumber(PhoneNumber thePhoneNumber, Locale languageCode)`

Returns a carrier name for the given phone number, in the language provided. The carrier name is the one the number was originally allocated to, however if the country supports mobile number portability the number might not belong to the returned carrier anymore. If no mapping is found an empty string is returned. <p>This method assumes the validity of the number passed in has already been checked, and that the number is suitable for carrier lookup. We consider mobile and pager numbers possible candidates for carrier lookup.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|a valid phone number for which we want to get a carrier name|
|`languageCode`|the language code in which the name should be written|

#### Return

**Type**

String

**Description**

a carrier name for the given phone number

### `getNameForNumber(PhoneNumber thePhoneNumber, Locale languageCode)`
### `getSafeDisplayName(PhoneNumber thePhoneNumber, Locale languageCode)`

Gets the name of the carrier for the given phone number only when it is 'safe' to display to users. A carrier name is considered safe if the number is valid and for a region that doesn't support &lt;a href="http://en.wikipedia.org/wiki/Mobile_number_portability"&gt;mobile number portability&lt;/a&gt;.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the phone number for which we want to get a carrier name|
|`languageCode`|the language code in which the name should be written|

#### Return

**Type**

String

**Description**

a carrier name that is safe to display to users, or the empty string

---
