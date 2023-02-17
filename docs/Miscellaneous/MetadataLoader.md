# MetadataLoader

`APIVERSION: 46`

`STATUS: ACTIVE`

Interface for clients to specify a customized phone metadata loader.
Note that implementation owners have the responsibility to ensure this is
thread-safe.

## Methods
### `loadMetadata(String resourceName, String metadataFileName)`

Returns a PhoneMetadata. This method may be called concurrently so implementations must be thread-safe.

#### Parameters

|Param|Description|
|---|---|
|`resourceName`|- name of the resource zip file containing the metadata files.|
|`metadataFileName`|file name of metadata to load.|

#### Return

**Type**

PhoneMetadata

**Description**

metadata as PhoneMetadata. Return null in case the metadata file could not be found

---
