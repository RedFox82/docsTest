# Leniency

`APIVERSION: 46`

`STATUS: ACTIVE`

Leniency when finding potential phone numbers in text segments. The levels
here are ordered in increasing strictness.

## Methods
### `static POSSIBLE()`

Phone numbers accepted are possible, but not necessarily valid.

#### Return

**Type**

PossibleLeniency

**Description**

PossibleLeniency

### `static VALID()`

Phone numbers accepted are possible and valid.

#### Return

**Type**

ValidLeniency

**Description**

ValidLeniency

### `static STRICT_GROUPING()`

Phone numbers accepted are valid and are grouped in a possible way for this locale. For example, a US number written as "65 02 53 00 00" is not accepted at this leniency level, whereas "650 253 0000" or "6502530000" are. Numbers with more than one '/' symbol are also dropped at this level. Warning: The next two levels might result in lower coverage especially for regions outside of country code "+1". If you are not sure about which level to use, you can send an e-mail to the discussion group http://groups.google.com/group/libphonenumber-discuss/

#### Return

**Type**

StrictGroupingLeniency

**Description**

StrictGroupingLeniency

### `static EXACT_GROUPING()`

Phone numbers accepted are valid and are grouped in the same way that we would have formatted it, or as a single block. For example, a US number written as "650 2530000" is not accepted at this leniency level, whereas "650 253 0000" or "6502530000" are.

#### Return

**Type**

ExactGroupingLeniency

**Description**

ExactGroupingLeniency

---
