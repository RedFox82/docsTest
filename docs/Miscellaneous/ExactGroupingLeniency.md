# ExactGroupingLeniency

`APIVERSION: 46`

`STATUS: ACTIVE`

**Inheritance**

[AbstractLeniency](/Miscellaneous/AbstractLeniency.md)
 &gt; 
ExactGroupingLeniency

## Methods
### `override verify(PhoneNumber thePhoneNumber, String candidate, PhoneNumberUtil util, PhoneNumberMatcher numberMatcher)`

Phone numbers accepted are PhoneNumberUtil::isValidNumber() valid and are grouped in the same way that we would have formatted it, or as a single block. For example, a US number written as "650 2530000" is not accepted at this leniency level, whereas "650 253 0000" or "6502530000" are. Numbers with more than one '/' symbol are also dropped at this level. Warning: This level might result in lower coverage especially for regions outside of country code "+1". If you are not sure about which level to use, email the discussion group libphonenumber-discuss

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|PhoneNumber|
|`candidate`|String|
|`util`|PhoneNumberUtil|
|`numberMatcher`|PhoneNumberMatcher|

#### Return

**Type**

Boolean

**Description**

Boolean


**Googlegroups** .com.

---
