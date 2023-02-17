# AsYouTypeFormatter

`APIVERSION: 48`

`STATUS: ACTIVE`


## Methods
### `clear()`

Clears the internal state of the formatter, so it can be reused.

### `inputDigit(String nextChar)`

Formats a phone number on-the-fly as each digit is entered.

#### Parameters

|Param|Description|
|---|---|
|`nextChar`|the most recently entered digit of a phone number. Formatting characters are     allowed, but as soon as they are encountered this method formats the number as entered and     not 'as you type' anymore. Full width digits and Arabic-indic digits are allowed, and will     be shown as they are.|

#### Return

**Type**

String

**Description**

the partially formatted phone number.

### `inputDigitAndRememberPosition(String nextChar)`

Same as [#inputDigit](#inputDigit), but remembers the position where {@code nextChar} is inserted, so that it can be retrieved later by using [#getRememberedPosition](#getRememberedPosition). The remembered position will be automatically adjusted if additional formatting characters are later inserted/removed in front of {@code nextChar}.

### `getRememberedPosition()`

Returns the current position in the partially formatted phone number of the character which was previously passed in as the parameter of [#inputDigitAndRememberPosition](#inputDigitAndRememberPosition).

---
