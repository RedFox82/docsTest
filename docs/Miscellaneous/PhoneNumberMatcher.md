# PhoneNumberMatcher

`APIVERSION: 46`

`STATUS: ACTIVE`

A stateful class that finds and extracts telephone numbers from {@linkplain String text}.
Instances can be created using the {@linkplain PhoneNumberUtil#findNumbers factory methods} in
[PhoneNumberUtil](/Miscellaneous/PhoneNumberUtil.md).
Vanity numbers (phone numbers using alphabetic digits such as &lt;tt&gt;1-800-SIX-FLAGS&lt;/tt&gt; are
not found.
This class is not thread-safe.


**Implemented types**

[Iterator&lt;PhoneNumberMatch&gt;](Iterator&lt;PhoneNumberMatch&gt;)

## Methods
### `hasNext()`
### `next()`
---
