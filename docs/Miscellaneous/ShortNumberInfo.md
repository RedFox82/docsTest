# ShortNumberInfo

`APIVERSION: 47`

`STATUS: ACTIVE`


## Methods
### `static getInstance()`

Returns the singleton instance of the ShortNumberInfo.

#### Return

**Type**

ShortNumberInfo

**Description**

ShortNumberInfo

### `isPossibleShortNumberForRegion(PhoneNumber thePhoneNumber, String regionDialingFrom)`

Check whether a short number is a possible number when dialed from the given region. This provides a more lenient check than [#isValidShortNumberForRegion](#isValidShortNumberForRegion).

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the short number to check|
|`regionDialingFrom`|the region from which the number is dialed|

#### Return

**Type**

Boolean

**Description**

whether the number is a possible short number

### `isPossibleShortNumber(PhoneNumber thePhoneNumber)`

Check whether a short number is a possible number. If a country calling code is shared by multiple regions, this returns true if it's possible in any of them. This provides a more lenient check than [#isValidShortNumber](#isValidShortNumber). See [#isPossibleShortNumberForRegion(PhoneNumber, String)](#isPossibleShortNumberForRegion(PhoneNumber, String)) for details.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the short number to check|

#### Return

**Type**

Boolean

**Description**

whether the number is a possible short number

### `isValidShortNumberForRegion(PhoneNumber thePhoneNumber, String regionDialingFrom)`

Tests whether a short number matches a valid pattern in a region. Note that this doesn't verify the number is actually in use, which is impossible to tell by just looking at the number itself.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the short number for which we want to test the validity|
|`regionDialingFrom`|the region from which the number is dialed|

#### Return

**Type**

Boolean

**Description**

whether the short number matches a valid pattern

### `isValidShortNumber(PhoneNumber thePhoneNumber)`

Tests whether a short number matches a valid pattern. If a country calling code is shared by multiple regions, this returns true if it's valid in any of them. Note that this doesn't verify the number is actually in use, which is impossible to tell by just looking at the number itself. See [#isValidShortNumberForRegion(PhoneNumber, String)](#isValidShortNumberForRegion(PhoneNumber, String)) for details.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the short number for which we want to test the validity|

#### Return

**Type**

Boolean

**Description**

whether the short number matches a valid pattern

### `getExpectedCostForRegion(PhoneNumber thePhoneNumber, String regionDialingFrom)`

Gets the expected cost category of a short number when dialed from a region (however, nothing is implied about its validity). If it is important that the number is valid, then its validity must first be checked using [#isValidShortNumberForRegion](#isValidShortNumberForRegion). Note that emergency numbers are always considered toll-free. Example usage: <pre>{@code // The region for which the number was parsed and the region we subsequently check against // need not be the same. Here we parse the number in the US and check it for Canada. PhoneNumber number = phoneUtil.parse("110", "US"); ... String regionCode = "CA"; ShortNumberInfo shortInfo = ShortNumberInfo.getInstance(); if (shortInfo.isValidShortNumberForRegion(shortNumber, regionCode)) {   ShortNumberCost cost = shortInfo.getExpectedCostForRegion(number, regionCode);   // Do something with the cost information here. }}</pre>

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the short number for which we want to know the expected cost category|
|`regionDialingFrom`|the region from which the number is dialed|

#### Return

**Type**

ShortNumberCost

**Description**

the expected cost category for that region of the short number. Returns UNKNOWN_COST if     the number does not match a cost category. Note that an invalid number may match any cost     category.

### `getExpectedCost(PhoneNumber thePhoneNumber)`

Gets the expected cost category of a short number (however, nothing is implied about its validity). If the country calling code is unique to a region, this method behaves exactly the same as [#getExpectedCostForRegion(PhoneNumber, String)](#getExpectedCostForRegion(PhoneNumber, String)). However, if the country calling code is shared by multiple regions, then it returns the highest cost in the sequence PREMIUM_RATE, UNKNOWN_COST, STANDARD_RATE, TOLL_FREE. The reason for the position of UNKNOWN_COST in this order is that if a number is UNKNOWN_COST in one region but STANDARD_RATE or TOLL_FREE in another, its expected cost cannot be estimated as one of the latter since it might be a PREMIUM_RATE number. <p> For example, if a number is STANDARD_RATE in the US, but TOLL_FREE in Canada, the expected cost returned by this method will be STANDARD_RATE, since the NANPA countries share the same country calling code. <p> Note: If the region from which the number is dialed is known, it is highly preferable to call [#getExpectedCostForRegion(PhoneNumber, String)](#getExpectedCostForRegion(PhoneNumber, String)) instead.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the short number for which we want to know the expected cost category|

#### Return

**Type**

ShortNumberCost

**Description**

the highest expected cost category of the short number in the region(s) with the given     country calling code

### `connectsToEmergencyNumber(String phoneNumber, String regionCode)`

Returns true if the given number, exactly as dialed, might be used to connect to an emergency service in the given region. <p> This method accepts a string, rather than a PhoneNumber, because it needs to distinguish cases such as "+1 911" and "911", where the former may not connect to an emergency service in all cases but the latter would. This method takes into account cases where the number might contain formatting, or might have additional digits appended (when it is okay to do that in the specified region).

#### Parameters

|Param|Description|
|---|---|
|`phoneNumber`|the phone number to test|
|`regionCode`|the region where the phone number is being dialed|

#### Return

**Type**

Boolean

**Description**

whether the number might be used to connect to an emergency service in the given region

### `isEmergencyNumber(String phoneNumber, String regionCode)`

Returns true if the given number exactly matches an emergency service number in the given region. <p> This method takes into account cases where the number might contain formatting, but doesn't allow additional digits to be appended. Note that {@code isEmergencyNumber(number, region)} implies {@code connectsToEmergencyNumber(number, region)}.

#### Parameters

|Param|Description|
|---|---|
|`phoneNumber`|the phone number to test|
|`regionCode`|the region where the phone number is being dialed|

#### Return

**Type**

Boolean

**Description**

whether the number exactly matches an emergency services number in the given region

### `isCarrierSpecific(PhoneNumber thePhoneNumber)`

Given a valid short number, determines whether it is carrier-specific (however, nothing is implied about its validity). Carrier-specific numbers may connect to a different end-point, or not connect at all, depending on the user's carrier. If it is important that the number is valid, then its validity must first be checked using [#isValidShortNumber](#isValidShortNumber) or [#isValidShortNumberForRegion](#isValidShortNumberForRegion).

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the valid short number to check|

#### Return

**Type**

Boolean

**Description**

whether the short number is carrier-specific, assuming the input was a valid short     number

### `isCarrierSpecificForRegion(PhoneNumber thePhoneNumber, String regionDialingFrom)`

Given a valid short number, determines whether it is carrier-specific when dialed from the given region (however, nothing is implied about its validity). Carrier-specific numbers may connect to a different end-point, or not connect at all, depending on the user's carrier. If it is important that the number is valid, then its validity must first be checked using [#isValidShortNumber](#isValidShortNumber) or [#isValidShortNumberForRegion](#isValidShortNumberForRegion). Returns false if the number doesn't match the region provided.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the valid short number to check|
|`regionDialingFrom`|the region from which the number is dialed|

#### Return

**Type**

Boolean

**Description**

whether the short number is carrier-specific in the provided region, assuming the     input was a valid short number

### `isSmsServiceForRegion(PhoneNumber thePhoneNumber, String regionDialingFrom)`

Given a valid short number, determines whether it is an SMS service (however, nothing is implied about its validity). An SMS service is where the primary or only intended usage is to receive and/or send text messages (SMSs). This includes MMS as MMS numbers downgrade to SMS if the other party isn't MMS-capable. If it is important that the number is valid, then its validity must first be checked using [#isValidShortNumber](#isValidShortNumber) or [#isValidShortNumberForRegion](#isValidShortNumberForRegion). Returns false if the number doesn't match the region provided.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the valid short number to check|
|`regionDialingFrom`|the region from which the number is dialed|

#### Return

**Type**

Boolean

**Description**

whether the short number is an SMS service in the provided region, assuming the input     was a valid short number

---
## Enums
### ShortNumberCost

Cost categories of short numbers.


---
