# PhoneNumberToTimeZonesMapper

`APIVERSION: 47`

`STATUS: ACTIVE`

An offline mapper from phone numbers to time zones.

## Methods
### `static getInstance()`

Gets a [PhoneNumberToTimeZonesMapper](/Miscellaneous/PhoneNumberToTimeZonesMapper.md) instance. <p> The [PhoneNumberToTimeZonesMapper](/Miscellaneous/PhoneNumberToTimeZonesMapper.md) is implemented as a singleton. Therefore, calling this method multiple times will only result in one instance being created.

#### Return

**Type**

PhoneNumberToTimeZonesMapper

**Description**

PhoneNumberToTimeZonesMapper instance

### `getTimeZonesForGeographicalNumber(PhoneNumber thePhoneNumber)`

Returns a list of time zones to which a phone number belongs. <p>This method assumes the validity of the number passed in has already been checked, and that the number is geo-localizable. We consider fixed-line and mobile numbers possible candidates for geo-localization.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|a valid phone number for which we want to get the time zones to which it belongs|

#### Return

**Type**

List&lt;String&gt;

**Description**

a list of the corresponding time zones or a single element list with the default     unknown time zone if no other time zone was found or if the number was invalid

### `getTimeZonesForNumber(PhoneNumber thePhoneNumber)`

As per [#getTimeZonesForGeographicalNumber(PhoneNumber)](#getTimeZonesForGeographicalNumber(PhoneNumber)) but explicitly checks the validity of the number passed in.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the phone number for which we want to get the time zones to which it belongs|

#### Return

**Type**

List&lt;String&gt;

**Description**

a list of the corresponding time zones or a single element list with the default     unknown time zone if no other time zone was found or if the number was invalid

### `static getUnknownTimeZone()`

Returns a String with the ICU unknown time zone.

---
