# PhoneNumberUtil

`APIVERSION: 46`

`STATUS: ACTIVE`
## Methods
### `static extractPossibleNumber(String thePhoneNumber)`

Attempts to extract a possible number from the string passed in. This currently strips all leading characters that cannot be used to start a phone number. Characters that can be used to start a phone number are defined in the VALID_START_CHAR_PATTERN. If none of these characters are found in the number passed in, an empty string is returned. This function also attempts to strip off any alternative extensions or endings if two or more are present, such as in the case of: (530) 583-6985 x302/x2303. The second extension here makes this actually two phone numbers, (530) 583-6985 x302 and (530) 583-6985 x2303. We remove the second extension so that the first number is parsed correctly.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the string that might contain a phone number|

#### Return

**Type**

String

**Description**

the number, stripped of any non-phone-number prefix (such as "Tel:") or an empty     string if no character used to start phone numbers (such as + or any digit) is found in the     number

### `static normalizeDigitsOnly(String thePhoneNumber)`

Normalizes a string of characters representing a phone number. This converts wide-ascii and arabic-indic numerals to European numerals, and strips punctuation and alpha characters.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|a string of characters representing a phone number|

#### Return

**Type**

String

**Description**

the normalized string version of the phone number

### `static normalizeDiallableCharsOnly(String thePhoneNumber)`

Normalizes a string of characters representing a phone number. This strips all characters which are not diallable on a mobile phone keypad (including all non-ASCII digits).

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|a string of characters representing a phone number|

#### Return

**Type**

String

**Description**

the normalized string version of the phone number

### `static convertAlphaCharactersInNumber(String thePhoneNumber)`

Converts all alpha characters in a number to their respective digits on a keypad, but retains existing formatting.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|String|

#### Return

**Type**

String

**Description**

String

### `getLengthOfGeographicalAreaCode(PhoneNumber thePhoneNumber)`

Gets the length of the geographical area code from the PhoneNumber object passed in, so that clients could use it to split a national significant number into geographical area code and subscriber number. It works in such a way that the resultant subscriber number should be diallable, at least on some devices. An example of how this could be used: <pre>{@code * PhoneNumberUtil phoneUtil = PhoneNumberUtil.getInstance(); * PhoneNumber number = phoneUtil.parse("16502530000", "US"); * String nationalSignificantNumber = phoneUtil.getNationalSignificantNumber(number); * String areaCode; * String subscriberNumber; * Integer areaCodeLength = phoneUtil.getLengthOfGeographicalAreaCode(number); * if (areaCodeLength &gt; 0) { *   areaCode = nationalSignificantNumber.substring(0, areaCodeLength); *   subscriberNumber = nationalSignificantNumber.substring(areaCodeLength); * } else { *   areaCode = ""; *   subscriberNumber = nationalSignificantNumber; * } * }</pre> N.B.: area code is a very ambiguous concept, so the I18N team generally recommends against using it for most purposes, but recommends using the more general {@code national_number} instead. Read the following carefully before deciding to use this method: <ul> <li> geographical area codes change over time, and this method honors those changes; therefore, it doesn't guarantee the stability of the result it produces. <li> subscriber numbers may not be diallable from all devices (notably mobile devices, which typically requires the full national_number to be dialled in most regions). <li> most non-geographical numbers have no area codes, including numbers from non-geographical entities <li> some geographical numbers have no area codes. </ul>

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the PhoneNumber object for which clients     want to know the length of the area code|

#### Return

**Type**

Integer

**Description**

the length of area code of the PhoneNumber object     passed in

### `getLengthOfNationalDestinationCode(PhoneNumber thePhoneNumber)`
### `static getCountryMobileToken(Integer countryCallingCode)`

Returns the mobile token for the provided country calling code if it has one, otherwise returns an empty string. A mobile token is a number inserted before the area code when dialing a mobile number from that country from abroad.

#### Parameters

|Param|Description|
|---|---|
|`countryCallingCode`|the country calling code for which we want the mobile token|

#### Return

**Type**

String

**Description**

the mobile token, as a string, for the given country calling code

### `getSupportedRegions()`

Returns all regions the library has metadata for.

#### Return

**Type**

Set&lt;String&gt;

**Description**

an unordered set of the two-letter region codes for every geographical region the     library supports

### `getSupportedGlobalNetworkCallingCodes()`

Returns all global network calling codes the library has metadata for.

#### Return

**Type**

Set&lt;Integer&gt;

**Description**

an unordered set of the country calling codes for every non-geographical entity the     library supports

### `getSupportedCallingCodes()`

Returns all country calling codes the library has metadata for, covering both non-geographical entities (global network calling codes) and those used for geographical entities. This could be used to populate a drop-down box of country calling codes for a phone-number widget, for instance.

#### Return

**Type**

Set&lt;Integer&gt;

**Description**

an unordered set of the country calling codes for every geographical and     non-geographical entity the library supports

### `getSupportedTypesForRegion(String regionCode)`

Returns the types for a given region which the library has metadata for. Will not include FIXED_LINE_OR_MOBILE (if numbers in this region could be classified as FIXED_LINE_OR_MOBILE, both FIXED_LINE and MOBILE would be present) and UNKNOWN. No types will be returned for invalid or unknown region codes.

#### Parameters

|Param|Description|
|---|---|
|`regionCode`|String|

#### Return

**Type**

Set&lt;PhoneNumberTypeEnum&gt;

**Description**

Set&lt;PhoneNumberTypeEnum&gt;

### `getSupportedTypesForNonGeoEntity(Integer countryCallingCode)`

Returns the types for a country-code belonging to a non-geographical entity which the library has metadata for. Will not include FIXED_LINE_OR_MOBILE (if numbers for this non-geographical entity could be classified as FIXED_LINE_OR_MOBILE, both FIXED_LINE and MOBILE would be present) and UNKNOWN. No types will be returned for country calling codes that do not map to a known non-geographical entity.

#### Parameters

|Param|Description|
|---|---|
|`countryCallingCode`|Integer|

#### Return

**Type**

Set&lt;PhoneNumberTypeEnum&gt;

**Description**

Set&lt;PhoneNumberTypeEnum&gt;

### `static getInstance()`

Gets a [PhoneNumberUtil](/Miscellaneous/PhoneNumberUtil.md) instance to carry out international phone number formatting, parsing, or validation. The instance is loaded with all phone number metadata. <p>The [PhoneNumberUtil](/Miscellaneous/PhoneNumberUtil.md) is implemented as a singleton. Therefore, calling getInstance multiple times will only result in one instance being created.

#### Return

**Type**

PhoneNumberUtil

**Description**

a PhoneNumberUtil instance

### `static createInstance(MetadataLoader metadataLoader)`

Create a new [PhoneNumberUtil](/Miscellaneous/PhoneNumberUtil.md) instance to carry out international phone number formatting, parsing, or validation. The instance is loaded with all metadata by using the metadataLoader specified. <p>This method should only be used in the rare case in which you want to manage your own metadata loading. Calling this method multiple times is very expensive, as each time a new instance is created from scratch. When in doubt, use [#getInstance](#getInstance).

#### Parameters

|Param|Description|
|---|---|
|`metadataLoader`|customized metadata loader. This should not be null|

#### Return

**Type**

PhoneNumberUtil

**Description**

a PhoneNumberUtil instance

### `static formattingRuleHasFirstGroupOnly(String nationalPrefixFormattingRule)`

Helper function to check if the national prefix formatting rule has the first group only, i.e., does not start with the national prefix.

#### Parameters

|Param|Description|
|---|---|
|`nationalPrefixFormattingRule`|String|

#### Return

**Type**

Boolean

**Description**

Boolean

### `isNumberGeographical(PhoneNumber phoneNumber)`

Tests whether a phone number has a geographical association. It checks if the number is associated with a certain region in the country to which it belongs. Note that this doesn't verify if the number is actually in use.

#### Parameters

|Param|Description|
|---|---|
|`phoneNumber`|PhoneNumber|

#### Return

**Type**

Boolean

**Description**

Boolean

### `isNumberGeographical(PhoneNumberTypeEnum phoneNumberType, Integer countryCallingCode)`

Overload of isNumberGeographical(PhoneNumber), since calculating the phone number type is expensive; if we have already done this, we don't want to do it again.

#### Parameters

|Param|Description|
|---|---|
|`phoneNumberType`|PhoneNumberTypeEnum|
|`countryCallingCode`|Integer|

#### Return

**Type**

Boolean

**Description**

Boolean

### `format(PhoneNumber thePhoneNumber, PhoneNumberFormat numberFormat)`

Formats a phone number in the specified format using default rules. Note that this does not promise to produce a phone number that the user can dial from where they are - although we do format in either 'national' or 'international' format depending on what the client asks for, we do not currently support a more abbreviated format, such as for users in the same "area" who could potentially dial the number without area code. Note that if the phone number has a country calling code of 0 or an otherwise invalid country calling code, we cannot work out which formatting rules to apply so we return the national significant number with no formatting applied.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the phone number to be formatted|
|`numberFormat`|the format the phone number should be formatted into|

#### Return

**Type**

String

**Description**

the formatted phone number

### `format(PhoneNumber thePhoneNumber, PhoneNumberFormat numberFormat, StringBuilder formattedNumber)`

Same as [#format(PhoneNumber, PhoneNumberFormat)](#format(PhoneNumber, PhoneNumberFormat)), but accepts a mutable StringBuilder as a parameter to decrease object creation when invoked many times.

### `formatByPattern(PhoneNumber thePhoneNumber, PhoneNumberFormat numberFormat, List<NumberFormat> userDefinedFormats)`

Formats a phone number in the specified format using client-defined formatting rules. Note that if the phone number has a country calling code of zero or an otherwise invalid country calling code, we cannot work out things like whether there should be a national prefix applied, or how to format extensions, so we return the national significant number with no formatting applied.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the phone number to be formatted|
|`numberFormat`|the format the phone number should be formatted into|
|`userDefinedFormats`|formatting rules specified by clients|

#### Return

**Type**

String

**Description**

the formatted phone number

### `formatNationalNumberWithCarrierCode(PhoneNumber thePhoneNumber, String carrierCode)`
### `formatNationalNumberWithPreferredCarrierCode(PhoneNumber thePhoneNumber, String fallbackCarrierCode)`
### `formatNumberForMobileDialing(PhoneNumber thePhoneNumber, String regionCallingFrom, Boolean withFormatting)`

Returns a number formatted in such a way that it can be dialed from a mobile phone in a specific region. If the number cannot be reached from the region (e.g. some countries block toll-free numbers from being called outside of the country), the method returns an empty string.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the phone number to be formatted|
|`regionCallingFrom`|the region where the call is being placed|
|`withFormatting`|whether the number should be returned with formatting symbols, such as     spaces and dashes.|

#### Return

**Type**

String

**Description**

the formatted phone number

### `formatOutOfCountryCallingNumber(PhoneNumber thePhoneNumber, String regionCallingFrom)`

Formats a phone number for out-of-country dialing purposes. If no regionCallingFrom is supplied, we format the number in its INTERNATIONAL format. If the country calling code is the same as that of the region where the number is from, then NATIONAL formatting will be applied. <p>If the number itself has a country calling code of zero or an otherwise invalid country calling code, then we return the number with no formatting applied. <p>Note this function takes care of the case for calling inside of NANPA and between Russia and Kazakhstan (who share the same country calling code). In those cases, no international prefix is used. For regions which have multiple international prefixes, the number in its INTERNATIONAL format will be returned instead.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the phone number to be formatted|
|`regionCallingFrom`|the region where the call is being placed|

#### Return

**Type**

String

**Description**

the formatted phone number

### `formatInOriginalFormat(PhoneNumber thePhoneNumber, String regionCallingFrom)`

Formats a phone number using the original phone number format (e.g. INTERNATIONAL or NATIONAL) that the number is parsed from, provided that the number has been parsed with [* parseAndKeepRawInput](* parseAndKeepRawInput). Otherwise the number will be formatted in NATIONAL format. <p>The original format is embedded in the country_code_source field of the PhoneNumber object passed in, which is only set when parsing keeps the raw input. When we don't have a formatting pattern for the number, the method falls back to returning the raw input. <p>Note this method guarantees no digit will be inserted, removed or modified as a result of formatting.

#### Parameters

|Param|Description|
|---|---|
|`number`|the phone number that needs to be formatted in its original number format|
|`regionCallingFrom`|the region whose IDD needs to be prefixed if the original number has     one|

#### Return

**Type**

String

**Description**

the formatted phone number in its original number format

### `formatOutOfCountryKeepingAlphaChars(PhoneNumber thePhoneNumber, String regionCallingFrom)`

Formats a phone number for out-of-country dialing purposes. Note that in this version, if the number was entered originally using alpha characters and this version of the number is stored in raw_input, this representation of the number will be used rather than the digit representation. Grouping information, as specified by characters such as "-" and " ", will be retained. <p>&lt;b&gt;Caveats:&lt;/b&gt;</p> <ul> <li> This will not produce good results if the country calling code is both present in the raw input _and_ is the start of the national number. This is not a problem in the regions which typically use alpha numbers. <li> This will also not produce good results if the raw input has any grouping information within the first three digits of the national number, and if the function needs to strip preceding digits/words in the raw input before these digits. Normally people group the first three digits together so this is not a huge problem - and will be fixed if it proves to be so. </ul>

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the phone number that needs to be formatted|
|`regionCallingFrom`|the region where the call is being placed|

#### Return

**Type**

String

**Description**

the formatted phone number

### `getNationalSignificantNumber(PhoneNumber thePhoneNumber)`

Gets the national significant number of a phone number. Note a national significant number doesn't contain a national prefix or any formatting.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the phone number for which the national significant number is needed|

#### Return

**Type**

String

**Description**

the national significant number of the PhoneNumber object passed in

### `chooseFormattingPatternForNumber(List<NumberFormat> availableFormats, String nationalNumber)`
### `formatNsnUsingPattern(String nationalNumber, NumberFormat formattingPattern, PhoneNumberFormat numberFormat)`
### `getExampleNumber(String regionCode)`

Gets a valid number for the specified region.

#### Parameters

|Param|Description|
|---|---|
|`regionCode`|the region for which an example number is needed|

#### Return

**Type**

PhoneNumber

**Description**

a valid fixed-line number for the specified region. Returns null when the metadata    does not contain such information, or the region 001 is passed in. For 001 (representing    non-geographical numbers), call [#getExampleNumberForNonGeoEntity](#getExampleNumberForNonGeoEntity) instead.

### `getInvalidExampleNumber(String regionCode)`
### `getExampleNumberForType(String regionCode, PhoneNumberTypeEnum type)`

Gets a valid number for the specified region and number type.

#### Parameters

|Param|Description|
|---|---|
|`regionCode`|the region for which an example number is needed|
|`type`|the type of number that is needed|

#### Return

**Type**

PhoneNumber

**Description**

a valid number for the specified region and type. Returns null when the metadata     does not contain such information or if an invalid region or region 001 was entered.     For 001 (representing non-geographical numbers), call     [#getExampleNumberForNonGeoEntity](#getExampleNumberForNonGeoEntity) instead.

### `getExampleNumberForType(PhoneNumberTypeEnum type)`

Gets a valid number for the specified number type (it may belong to any country).

#### Parameters

|Param|Description|
|---|---|
|`type`|the type of number that is needed|

#### Return

**Type**

PhoneNumber

**Description**

a valid number for the specified type. Returns null when the metadata     does not contain such information. This should only happen when no numbers of this type are     allocated anywhere in the world anymore.

### `getExampleNumberForNonGeoEntity(Integer countryCallingCode)`

Gets a valid number for the specified country calling code for a non-geographical entity.

#### Parameters

|Param|Description|
|---|---|
|`countryCallingCode`|the country calling code for a non-geographical entity|

#### Return

**Type**

PhoneNumber

**Description**

a valid number for the non-geographical entity. Returns null when the metadata    does not contain such information, or the country calling code passed in does not belong    to a non-geographical entity.

### `getNumberType(PhoneNumber thePhoneNumber)`

Gets the type of a valid phone number.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the phone number that we want to know the type|

#### Return

**Type**

PhoneNumberTypeEnum

**Description**

the type of the phone number, or UNKNOWN if it is invalid

### `getMetadataForRegion(String regionCode)`

Returns the metadata for the given region code or {@code null} if the region code is invalid or unknown.

### `getMetadataForNonGeographicalRegion(Integer countryCallingCode)`
### `isValidNumber(PhoneNumber thePhoneNumber)`

Tests whether a phone number matches a valid pattern. Note this doesn't verify the number is actually in use, which is impossible to tell by just looking at a number itself. It only verifies whether the parsed, canonicalised number is valid: not whether a particular series of digits entered by the user is diallable from the region provided when parsing. For example, the number +41 (0) 78 927 2696 can be parsed into a number with country code "41" and national significant number "789272696". This is valid, while the original string is not diallable.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the phone number that we want to validate|

#### Return

**Type**

Boolean

**Description**

a Boolean that indicates whether the number is of a valid pattern

### `isValidNumberForRegion(PhoneNumber thePhoneNumber, String regionCode)`

Tests whether a phone number is valid for a certain region. Note this doesn't verify the number is actually in use, which is impossible to tell by just looking at a number itself. If the country calling code is not the same as the country calling code for the region, this immediately exits with false. After this, the specific number pattern rules for the region are examined. This is useful for determining for example whether a particular number is valid for Canada, rather than just a valid NANPA number. Warning: In most cases, you want to use [#isValidNumber](#isValidNumber) instead. For example, this method will mark numbers from British Crown dependencies such as the Isle of Man as invalid for the region "GB" (United Kingdom), since it has its own region code, "IM", which may be undesirable.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the phone number that we want to validate|
|`regionCode`|the region that we want to validate the phone number for|

#### Return

**Type**

Boolean

**Description**

a Boolean that indicates whether the number is of a valid pattern

### `getRegionCodeForNumber(PhoneNumber thePhoneNumber)`

Returns the region where a phone number is from. This could be used for geocoding at the region level. Only guarantees correct results for valid, full numbers (not short-codes, or invalid numbers).

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the phone number whose origin we want to know|

#### Return

**Type**

String

**Description**

the region where the phone number is from, or null if no region matches this calling     code

### `getRegionCodeForCountryCode(Integer countryCallingCode)`

Returns the region code that matches the specific country calling code. In the case of no region code being found, ZZ will be returned. In the case of multiple regions, the one designated in the metadata as the "main" region for this calling code will be returned. If the countryCallingCode entered is valid but doesn't match a specific region (such as in the case of non-geographical calling codes like 800) the value "001" will be returned (corresponding to the value for World in the UN M.49 schema).

### `getRegionCodesForCountryCode(Integer countryCallingCode)`

Returns a list with the region codes that match the specific country calling code. For non-geographical country calling codes, the region code 001 is returned. Also, in the case of no region code being found, an empty list is returned.

### `getCountryCodeForRegion(String regionCode)`

Returns the country calling code for a specific region. For example, this would be 1 for the United States, and 64 for New Zealand.

#### Parameters

|Param|Description|
|---|---|
|`regionCode`|the region that we want to get the country calling code for|

#### Return

**Type**

Integer

**Description**

the country calling code for the region denoted by regionCode

### `getNddPrefixForRegion(String regionCode, Boolean stripNonDigits)`

Returns the national dialling prefix for a specific region. For example, this would be 1 for the United States, and 0 for New Zealand. Set stripNonDigits to true to strip symbols like "~" (which indicates a wait for a dialling tone) from the prefix returned. If no national prefix is present, we return null. <p>Warning: Do not use this method for do-your-own formatting - for some regions, the national dialling prefix is used only for certain types of numbers. Use the library's formatting functions to prefix the national prefix when required.

#### Parameters

|Param|Description|
|---|---|
|`regionCode`|the region that we want to get the dialling prefix for|
|`stripNonDigits`|true to strip non-digits from the national dialling prefix|

#### Return

**Type**

String

**Description**

the dialling prefix for the region denoted by regionCode

### `isNANPACountry(String regionCode)`

Checks if this is a region under the North American Numbering Plan Administration (NANPA).

#### Return

**Type**

Boolean

**Description**

true if regionCode is one of the regions under NANPA

### `isAlphaNumber(String thePhoneNumber)`
### `isPossibleNumber(PhoneNumber thePhoneNumber)`

Convenience wrapper around [#isPossibleNumberWithReason](#isPossibleNumberWithReason). Instead of returning the reason for failure, this method returns true if the number is either a possible fully-qualified number (containing the area code and country code), or if the number could be a possible local number (with a country code, but missing an area code). Local numbers are considered possible if they could be possibly dialled in this format: if the area code is needed for a call to connect, the number is not considered possible without it.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the number that needs to be checked|

#### Return

**Type**

Boolean

**Description**

true if the number is possible

### `isPossibleNumberForType(PhoneNumber thePhoneNumber, PhoneNumberTypeEnum type)`

Convenience wrapper around [#isPossibleNumberForTypeWithReason](#isPossibleNumberForTypeWithReason). Instead of returning the reason for failure, this method returns true if the number is either a possible fully-qualified number (containing the area code and country code), or if the number could be a possible local number (with a country code, but missing an area code). Local numbers are considered possible if they could be possibly dialled in this format: if the area code is needed for a call to connect, the number is not considered possible without it.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the number that needs to be checked|
|`type`|the type we are interested in|

#### Return

**Type**

Boolean

**Description**

true if the number is possible for this particular type

### `isPossibleNumberWithReason(PhoneNumber thePhoneNumber)`
### `isPossibleNumberForTypeWithReason(PhoneNumber thePhoneNumber, PhoneNumberTypeEnum type)`

Check whether a phone number is a possible number of a particular type. For types that don't exist in a particular region, this will return a result that isn't so useful; it is recommended that you use [#getSupportedTypesForRegion](#getSupportedTypesForRegion) or [#getSupportedTypesForNonGeoEntity](#getSupportedTypesForNonGeoEntity) respectively before calling this method to determine whether you should call it for this number at all. This provides a more lenient check than [#isValidNumber](#isValidNumber) in the following sense: &lt;ol&gt; <li> It only checks the length of phone numbers. In particular, it doesn't check starting digits of the number. <li> For some numbers (particularly fixed-line), many regions have the concept of area code, which together with subscriber number constitute the national significant number. It is sometimes okay to dial only the subscriber number when dialing in the same area. This function will return IS_POSSIBLE_LOCAL_ONLY if the subscriber-number-only version is passed in. On the other hand, because isValidNumber validates using information on both starting digits (for fixed line numbers, that would most likely be area codes) and length (obviously includes the length of area codes for fixed line numbers), it will return false for the subscriber-number-only version. &lt;/ol&gt;

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the number that needs to be checked|
|`type`|the type we are interested in|

#### Return

**Type**

ValidationResultEnum

**Description**

a ValidationResult object which indicates whether the number is possible

### `isPossibleNumber(String thePhoneNumber, String regionDialingFrom)`
### `truncateTooLongNumber(PhoneNumber thePhoneNumber)`

Attempts to extract a valid number from a phone number that is too long to be valid, and resets the PhoneNumber object passed in to that valid version. If no valid number could be extracted, the PhoneNumber object passed in will not be modified.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|a PhoneNumber object which contains a number that is too long to be valid|

#### Return

**Type**

Boolean

**Description**

true if a valid phone number can be successfully extracted

### `getAsYouTypeFormatter(String regionCode)`

Gets an [com.google.i18n.phonenumbers.AsYouTypeFormatter](com.google.i18n.phonenumbers.AsYouTypeFormatter) for the specific region.

#### Parameters

|Param|Description|
|---|---|
|`regionCode`|the region where the phone number is being entered|

#### Return

**Type**

AsYouTypeFormatter

**Description**

an [com.google.i18n.phonenumbers.AsYouTypeFormatter](com.google.i18n.phonenumbers.AsYouTypeFormatter) object, which can be used     to format phone numbers in the specific region "as you type"

### `extractCountryCode(StringBuilder fullNumber, StringBuilder nationalNumber)`
### `maybeStripNationalPrefixAndCarrierCode(StringBuilder thePhoneNumber, PhoneMetadata metadata, StringBuilder carrierCode)`

Strips any national prefix (such as 0, 1) present in the number provided.

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the normalized telephone number that we wish to strip any national     dialing prefix from|
|`metadata`|the metadata for the region that we think this number is from|
|`carrierCode`|a place to insert the carrier code if one is extracted|

#### Return

**Type**

Boolean

**Description**

true if a national prefix or carrier code (or both) could be extracted

### `parse(String numberToParse, String defaultRegion)`

Parses a string and returns it as a phone number in proto buffer format. The method is quite lenient and looks for a number in the input text (raw input) and does not check whether the string is definitely only a phone number. To do this, it ignores punctuation and white-space, as well as any text before the number (e.g. a leading "Tel: ") and trims the non-number bits. It will accept a number in any format (E164, national, international etc), assuming it can be interpreted with the defaultRegion supplied. It also attempts to convert any alpha characters into digits if it thinks this is a vanity number of the type "1800 MICROSOFT". <p> This method will throw a [com.google.i18n.phonenumbers.NumberParseException](com.google.i18n.phonenumbers.NumberParseException) if the number is not considered to be a possible number. Note that validation of whether the number is actually a valid number for a particular region is not performed. This can be done separately with [#isValidNumber](#isValidNumber). <p> Note this method canonicalizes the phone number such that different representations can be easily compared, no matter what form it was originally entered in (e.g. national, international). If you want to record context about the number being parsed, such as the raw input that was entered, how the country code was derived etc. then call [* #parseAndKeepRawInput](* #parseAndKeepRawInput) instead.

#### Parameters

|Param|Description|
|---|---|
|`numberToParse`|number that we are attempting to parse. This can contain formatting such     as +, ( and -, as well as a phone number extension. It can also be provided in RFC3966     format.|
|`defaultRegion`|region that we are expecting the number to be from. This is only used if     the number being parsed is not written in international format. The country_code for the     number in this case would be stored as that of the default region supplied. If the number     is guaranteed to start with a '+' followed by the country calling code, then RegionCode.ZZ     or null can be supplied.|

#### Return

**Type**

PhoneNumber

**Description**

a phone number proto buffer filled with the parsed number

#### Throws

|Exception|Description|
|---|---|
|`NumberParseException`|if the string is not considered to be a viable phone number (e.g.     too few or too many digits) or if no default region was supplied and the number is not in     international format (does not start with +)|

### `parse(String numberToParse, String defaultRegion, PhoneNumber phoneNumber)`

Same as [#parse(CharSequence, String)](#parse(CharSequence, String)), but accepts mutable PhoneNumber as a parameter to decrease object creation when invoked many times.

### `parseAndKeepRawInput(String numberToParse, String defaultRegion)`

Parses a string and returns it in proto buffer format. This method differs from [#parse](#parse) in that it always populates the raw_input field of the protocol buffer with numberToParse as well as the country_code_source field.

#### Parameters

|Param|Description|
|---|---|
|`numberToParse`|number that we are attempting to parse. This can contain formatting such     as +, ( and -, as well as a phone number extension.|
|`defaultRegion`|region that we are expecting the number to be from. This is only used if     the number being parsed is not written in international format. The country calling code     for the number in this case would be stored as that of the default region supplied.|

#### Return

**Type**

PhoneNumber

**Description**

a phone number proto buffer filled with the parsed number

#### Throws

|Exception|Description|
|---|---|
|`NumberParseException`|if the string is not considered to be a viable phone number or if     no default region was supplied|

### `parseAndKeepRawInput(String numberToParse, String defaultRegion, PhoneNumber phoneNumber)`

Same as[#parseAndKeepRawInput(CharSequence, String)](#parseAndKeepRawInput(CharSequence, String)), but accepts a mutable PhoneNumber as a parameter to decrease object creation when invoked many times.

### `findNumbers(String text, String defaultRegion)`

Returns an iterable over all [PhoneNumberMatch PhoneNumberMatches](PhoneNumberMatch PhoneNumberMatches) in {@code text}. This is a shortcut for [#findNumbers(CharSequence, String, Leniency, long) * getMatcher(text, defaultRegion, Leniency.VALID, Long.MAX_VALUE)](#findNumbers(CharSequence, String, Leniency, long) * getMatcher(text, defaultRegion, Leniency.VALID, Long.MAX_VALUE)).

#### Parameters

|Param|Description|
|---|---|
|`text`|the text to search for phone numbers, null for no text|
|`defaultRegion`|region that we are expecting the number to be from. This is only used if     the number being parsed is not written in international format. The country_code for the     number in this case would be stored as that of the default region supplied. May be null if     only international numbers are expected.|

### `findNumbers(String text, String defaultRegion, AbstractLeniency leniency, Long maxTries)`

Returns an iterable over all [PhoneNumberMatch PhoneNumberMatches](PhoneNumberMatch PhoneNumberMatches) in {@code text}.

#### Parameters

|Param|Description|
|---|---|
|`text`|the text to search for phone numbers, null for no text|
|`defaultRegion`|region that we are expecting the number to be from. This is only used if     the number being parsed is not written in international format. The country_code for the     number in this case would be stored as that of the default region supplied. May be null if     only international numbers are expected.|
|`leniency`|the leniency to use when evaluating candidate phone numbers|
|`maxTries`|the maximum number of invalid numbers to try before giving up on the text.     This is to cover degenerate cases where the text has a lot of false positives in it. Must     be {@code >= 0}.|

### `isNumberMatch(PhoneNumber firstNumberIn, PhoneNumber secondNumberIn)`

Takes two phone numbers and compares them for equality. <p>Returns EXACT_MATCH if the country_code, NSN, presence of a leading zero for Italian numbers and any extension present are the same. Returns NSN_MATCH if either or both has no region specified, and the NSNs and extensions are the same. Returns SHORT_NSN_MATCH if either or both has no region specified, or the region specified is the same, and one NSN could be a shorter version of the other number. This includes the case where one has an extension specified, and the other does not. Returns NO_MATCH otherwise. For example, the numbers +1 345 657 1234 and 657 1234 are a SHORT_NSN_MATCH. The numbers +1 345 657 1234 and 345 657 are a NO_MATCH.

#### Parameters

|Param|Description|
|---|---|
|`firstNumberIn`|first number to compare|
|`secondNumberIn`|second number to compare|

#### Return

**Type**

MatchType

**Description**

NO_MATCH, SHORT_NSN_MATCH, NSN_MATCH or EXACT_MATCH depending on the level of equality     of the two numbers, described in the method definition.

### `isNumberMatch(String firstNumber, String secondNumber)`

Takes two phone numbers as strings and compares them for equality. This is a convenience wrapper for [#isNumberMatch(PhoneNumber, PhoneNumber)](#isNumberMatch(PhoneNumber, PhoneNumber)). No default region is known.

#### Parameters

|Param|Description|
|---|---|
|`firstNumber`|first number to compare. Can contain formatting, and can have country     calling code specified with + at the start.|
|`secondNumber`|second number to compare. Can contain formatting, and can have country     calling code specified with + at the start.|

#### Return

**Type**

MatchType

**Description**

NOT_A_NUMBER, NO_MATCH, SHORT_NSN_MATCH, NSN_MATCH, EXACT_MATCH. See     [#isNumberMatch(PhoneNumber, PhoneNumber)](#isNumberMatch(PhoneNumber, PhoneNumber)) for more details.

### `isNumberMatch(PhoneNumber firstNumber, String secondNumber)`
### `canBeInternationallyDialled(PhoneNumber thePhoneNumber)`

Returns true if the number can be dialled from outside the region, or unknown. If the number can only be dialled from within the region, returns false. Does not check the number is a valid number. Note that, at the moment, this method does not handle short numbers (which are currently all presumed to not be diallable from outside their country).

#### Parameters

|Param|Description|
|---|---|
|`thePhoneNumber`|the phone-number for which we want to know whether it is diallable from     outside the region|

#### Return

**Type**

Boolean

**Description**

Boolean

### `isMobileNumberPortableRegion(String regionCode)`

Returns true if the supplied region supports mobile number portability. Returns false for invalid, unknown or regions that don't support mobile number portability.

#### Parameters

|Param|Description|
|---|---|
|`regionCode`|the region for which we want to know whether it supports mobile number     portability or not|

#### Return

**Type**

Boolean

**Description**

Boolean

---
## Enums
### MatchType

Types of phone number matches. See detailed description beside the isNumberMatch() method.


### PhoneNumberFormat

INTERNATIONAL and NATIONAL formats are consistent with the definition in ITU-T Recommendation
E.123. However we follow local conventions such as using '-' instead of whitespace as
separators. For example, the number of the Google Switzerland office will be written as
"+41 44 668 1800" in INTERNATIONAL format, and as "044 668 1800" in NATIONAL format. E164
format is as per INTERNATIONAL format but with no formatting applied, e.g. "+41446681800".
RFC3966 is as per INTERNATIONAL format, but with all spaces and other separating symbols
replaced with a hyphen, and with any phone number extension appended with ";ext=". It also
will have a prefix of "tel:" added, e.g. "tel:+41-44-668-1800".
Note: If you are considering storing the number in a neutral format, you are highly advised to
use the PhoneNumber class.


### PhoneNumberTypeEnum

Type of phone numbers.


### ValidationResultEnum

Possible outcomes when testing if a PhoneNumber is possible.


---
