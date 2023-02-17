# TriggerHandlerDispatcher

`APIVERSION: 54`

`STATUS: ACTIVE`

Dispatches trigger-based events to implementations of <code>TriggerHandler</code> based on the current trigger context.


**See** [Trigger](Trigger)


**See** [TriggerHandlerFactory](TriggerHandlerFactory)


**See** [TriggerHandler](TriggerHandler)

## Methods
### `static dispatch(Type factoryType)`

Dispatch the current trigger event to a trigger handler created using the specified factory.

#### Parameters

|Param|Description|
|---|---|
|`factoryType`|the class for the trigger handler factory used to create the trigger handler|

---
