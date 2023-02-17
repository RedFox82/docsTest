# PhoneNumberOfflineGeocoder

`APIVERSION: 47`

`STATUS: ACTIVE`

An offline geocoder which provides geographical information related to a phone number.

## Methods
### `static getInstance()`

Gets a [PhoneNumberOfflineGeocoder](/Miscellaneous/PhoneNumberOfflineGeocoder.md) instance to carry out international phone number geocoding. <p> The [PhoneNumberOfflineGeocoder](/Miscellaneous/PhoneNumberOfflineGeocoder.md) is implemented as a singleton. Therefore, calling this method multiple times will only result in one instance being created.

#### Return

**Type**

PhoneNumberOfflineGeocoder

**Description**

a [PhoneNumberOfflineGeocoder](/Miscellaneous/PhoneNumberOfflineGeocoder.md) instance

### `getDescriptionForValidNumber(PhoneNumber thePhoneNumber, Locale languageCode)`

Returns a text description for the given phone number, in the language provided. The description might consist of the name of the country where the phone number is from, or the name of the geographical area the phone number is from if more detailed information is available. <p>This method assumes the validity of the number passed in has already been checked, and that the number is suitable for geocoding. We consider fixed-line and mobile numbers possible candidates for geocoding.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|a valid phone number for which we want to get a text description|
|`languageCode`|the language code for which the description should be written|

#### Return

**Type**

String

**Description**

a text description for the given language code for the given phone number, or an     empty string if the number could come from multiple countries, or the country code is     in fact invalid

### `getDescriptionForValidNumber(PhoneNumber thePhoneNumber, Locale languageCode, String userRegion)`

As per [#getDescriptionForValidNumber(PhoneNumber, Locale)](#getDescriptionForValidNumber(PhoneNumber, Locale)) but also considers the region of the user. If the phone number is from the same region as the user, only a lower-level description will be returned, if one exists. Otherwise, the phone number's region will be returned, with optionally some more detailed information. <p>For example, for a user from the region "US" (United States), we would show "Mountain View, CA" for a particular number, omitting the United States from the description. For a user from the United Kingdom (region "GB"), for the same number we may show "Mountain View, CA, United States" or even just "United States". <p>This method assumes the validity of the number passed in has already been checked.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the phone number for which we want to get a text description|
|`languageCode`|the language code for which the description should be written|
|`userRegion`|the region code for a given user. This region will be omitted from the     description if the phone number comes from this region. It should be a two-letter     upper-case CLDR region code.|

#### Return

**Type**

String

**Description**

a text description for the given language code for the given phone number, or an     empty string if the number could come from multiple countries, or the country code is     in fact invalid

### `getDescriptionForNumber(PhoneNumber thePhoneNumber, Locale languageCode)`

As per [#getDescriptionForValidNumber(PhoneNumber, Locale)](#getDescriptionForValidNumber(PhoneNumber, Locale)) but explicitly checks the validity of the number passed in.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the phone number for which we want to get a text description|
|`languageCode`|the language code for which the description should be written|

#### Return

**Type**

String

**Description**

a text description for the given language code for the given phone number, or empty     string if the number passed in is invalid or could belong to multiple countries

### `getDescriptionForNumber(PhoneNumber thePhoneNumber, Locale languageCode, String userRegion)`

As per [#getDescriptionForValidNumber(PhoneNumber, Locale, String)](#getDescriptionForValidNumber(PhoneNumber, Locale, String)) but explicitly checks the validity of the number passed in.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the phone number for which we want to get a text description|
|`languageCode`|the language code for which the description should be written|
|`userRegion`|the region code for a given user. This region will be omitted from the     description if the phone number comes from this region. It should be a two-letter     upper-case CLDR region code.|

#### Return

**Type**

String

**Description**

a text description for the given language code for the given phone number, or empty     string if the number passed in is invalid or could belong to multiple countries

---
