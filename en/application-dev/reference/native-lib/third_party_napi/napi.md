# Node-API

## Introduction

Node-API (NAPI) provides APIs to encapsulate JavaScript capabilities as a native plug-in. It is independent of the underlying JavaScript and is maintained as part of Node.js.


## Supported Capabilities

NAPI eliminates the differences between underlying JavaScript engines and provides a set of stable interfaces.

The OpenHarmony Native API component optimizes the NAPI interface implementation and provides connection to underlying engines such as ArkJS. Currently, some APIs in the [Node-API](https://nodejs.org/docs/v14.9.0/api/n-api.html) standard library are supported.

## Symbols Extended by the OpenHarmony API Component 

|Type|Symbol|Description|
| --- | --- | --- |
|FUNC|napi_run_script_path|Runs a JavaScript file.|

** Symbols Exported from the NAPI Library**

|Type|Symbol|Description|
| --- | --- | --- |
|FUNC|napi_module_register|Registers the NAPI native module.|
|FUNC|napi_get_last_error_info|Obtains the **napi_extended_error_info** structure, which contains the latest error information.|
|FUNC|napi_throw|Throws a JavaScript value.|
|FUNC|napi_throw_error|Throws a JavaScript **Error** with text information.|
|FUNC|napi_throw_type_error|Throws a JavaScript **TypeError** with text information.|
|FUNC|napi_throw_range_error|Throws a JavaScript **RangeError** with text information.|
|FUNC|napi_is_error|Checks whether **napi_value** indicates an error object.|
|FUNC|napi_create_error|Creates and obtains a JavaScript **Error** with text information.|
|FUNC|napi_create_type_error|Creates and obtains a JavaScript **TypeError** with text information.|
|FUNC|napi_create_range_error|Creates and obtains a JavaScript **RangeError** with text information.|
|FUNC|napi_get_and_clear_last_exception|Obtains and clears the latest exception.|
|FUNC|napi_is_exception_pending|Checks whether an exception occurs.|
|FUNC|napi_fatal_error|Raises a fatal error to terminate the process immediately.|
|FUNC|napi_open_handle_scope|Creates a context environment.|
|FUNC|napi_close_handle_scope|Closes the context environment. After the context environment is closed, all references declared in it are closed.|
|FUNC|napi_open_escapable_handle_scope|Creates an escapable handle scope from which the declared values can be returned to the parent scope.|
|FUNC|napi_close_escapable_handle_scope|Closes the escapable handle scope passed in.|
|FUNC|napi_escape_handle|Promotes the handle to the input JavaScript object so that it is valid for the lifespan of its parent scope.|
|FUNC|napi_create_reference|Creates a reference for an **Object** to extend its lifespan. The caller needs to manage the reference lifespan.|
|FUNC|napi_delete_reference|Deletes the reference passed in.|
|FUNC|napi_reference_ref|Increments the reference count for the reference passed in and returns the count.|
|FUNC|napi_reference_unref|Decrements the reference count for the reference passed in and returns the count.|
|FUNC|napi_get_reference_value|Obtains the JavaScript **Object** associated with the reference.|
|FUNC|napi_create_array|Creates and obtains a JavaScript **Array**.|
|FUNC|napi_create_array_with_length|Creates and obtains a JavaScript **Array** of the specified length.|
|FUNC|napi_create_arraybuffer|Creates and obtains a JavaScript **ArrayBuffer** of the specified size.|
|FUNC|napi_create_external|Allocates a JavaScript value with external data.|
|FUNC|napi_create_external_arraybuffer|Allocates a JavaScript **ArrayBuffer** with external data.|
|FUNC|napi_create_object|Creates a default JavaScript **Object**.|
|FUNC|napi_create_symbol|Create a JavaScript **Symbol**.|
|FUNC|napi_create_typedarray|Creates a JavaScript **TypeArray** from an existing **ArrayBuffer**.|
|FUNC|napi_create_dataview|Creates a JavaScript **DataView** from an existing **ArrayBuffer**.|
|FUNC|napi_create_int32|Creates a JavaScript **Number** from C **int32_t** data.|
|FUNC|napi_create_uint32|Creates a JavaScript **Number** from C **uint32_t** data.|
|FUNC|napi_create_int64|Creates a JavaScript **Number** from C **int64_t** data.|
|FUNC|napi_create_double|Creates a JavaScript **Number** from C **double** data.|
|FUNC|napi_create_string_latin1|Creates a JavaScript **String** from an ISO-8859-1-encoded C string.|
|FUNC|napi_create_string_utf8|Creates a JavaScript **String** from a UTF8-encoded C string.|
|FUNC|napi_get_array_length|Obtains the length of an array.|
|FUNC|napi_get_arraybuffer_info|Obtains the underlying data buffer of the **ArrayBuffer** and its length.|
|FUNC|napi_get_prototype|Obtains the prototype of the specified JavaScript **Object**.|
|FUNC|napi_get_typedarray_info|Obtains properties of the specified **TypedArray**.|
|FUNC|napi_get_dataview_info|Obtains properties of the specified **DataView**.|
|FUNC|napi_get_value_bool|Obtains the C Boolean equivalent of the given JavaScript **Boolean**.|
|FUNC|napi_get_value_double|Obtains the C double equivalent of the given JavaScript **Number**.|
|FUNC|napi_get_value_external|Obtains the external data pointer previously passed through **napi_create_external()**.|
|FUNC|napi_get_value_int32|Obtains the C int32 equivalent of the given JavaScript **Number**.|
|FUNC|napi_get_value_int64|Obtains the C int64 equivalent of the given JavaScript **Number**.|
|FUNC|napi_get_value_string_latin1|Obtains the ISO-8859-1-encoded string corresponding to the given JavaScript value.|
|FUNC|napi_get_value_string_utf8|Obtains the UTF8-encoded string corresponding to the given JavaScript value.|
|FUNC|napi_get_value_uint32|Obtains the C uint32 equivalent of the given JavaScript **Number**.|
|FUNC|napi_get_boolean|Obtains the JavaScript Boolean object based on the given C Boolean value.|
|FUNC|napi_get_global|Obtains the **global** object.|
|FUNC|napi_get_null|Obtains the **null** object.|
|FUNC|napi_get_undefined|Obtains the **undefined** object.|
|FUNC|napi_coerce_to_bool|Forcibly converts the given JavaScript value to a JavaScript Boolean value.|
|FUNC|napi_coerce_to_number|Forcibly converts the given JavaScript value to a JavaScript number.|
|FUNC|napi_coerce_to_object|Forcibly converts the given JavaScript value to a JavaScript object.|
|FUNC|napi_coerce_to_string|Forcibly converts the given JavaScript value to a JavaScript string.|
|FUNC|napi_typeof|Obtains the JavaScript type of the given JavaScript value.|
|FUNC|napi_instanceof|Checks whether the given object is an instance of the specified constructor.|
|FUNC|napi_is_array|Checks whether the given JavaScript value is an array.|
|FUNC|napi_is_arraybuffer|Checks whether the given JavaScript value is a `ArrayBuffer`.|
|FUNC|napi_is_typedarray|Checks whether the given JavaScript value is a **TypedArray**.|
|FUNC|napi_is_dataview|Checks whether the given JavaScript value is a **DataView**.|
|FUNC|napi_is_date|Checks whether the given JavaScript value is a JavaScript **Date** object.|
|FUNC|napi_strict_equals|Checks whether two JavaScript values are strictly equal.|
|FUNC|napi_get_property_names|Obtains the names of the enumerable properties of **Object** in an array of strings.|
|FUNC|napi_set_property|Sets a property for the given **Object**.|
|FUNC|napi_get_property|Obtains the requested property of the given **Object**.|
|FUNC|napi_has_property|Checks whether the given **Object** has the specified property.|
|FUNC|napi_delete_property|Deletes the **key** property from the given **Object**.|
|FUNC|napi_has_own_property|Checks whether the given **Object** has the own property named **key**.|
|FUNC|napi_set_named_property|Sets a property with the specified name for the given **Object**.|
|FUNC|napi_get_named_property|Obtains the property with the specified name in the given **Object**.|
|FUNC|napi_has_named_property|Checks whether the given **Object** has the property with the specified name.|
|FUNC|napi_set_element|Sets an element at the specified index of the given **Object**.|
|FUNC|napi_get_element|Obtains the element at the specified index of the given **Object**.|
|FUNC|napi_has_element|Obtains the element if the given **Object** has an element at the specified index.|
|FUNC|napi_delete_element|Deletes the element at the specified index of the given **Object**.|
|FUNC|napi_define_properties|Defines multiple properties for the given **Object**.|
|FUNC|napi_call_function|Calls a JavaScript function in a native method, that is, native call JavaScript.|
|FUNC|napi_create_function|Creates a native method for JavaScript to call.|
|FUNC|napi_get_cb_info|Obtains detailed information about the call, such as the parameters and **this** pointer, from the given callback info.|
|FUNC|napi_get_new_target|Obtains the **new.target** of the constructor call.|
|FUNC|napi_new_instance|Creates an instance based on the given constructor.|
|FUNC|napi_define_class|Defines a JavaScript class corresponding to the C++ class.|
|FUNC|napi_wrap|Wraps a native instance in a JavaScript object.|
|FUNC|napi_unwrap|Obtains the native instance that was previously wrapped in a JavaScript object.|
|FUNC|napi_remove_wrap|Obtains the native instance that was previously wrapped in a JavaScript object and removes the wrapping.|
|FUNC|napi_create_async_work|Creates a work object that executes logic asynchronously.|
|FUNC|napi_delete_async_work|Releases an asynchronous work object.|
|FUNC|napi_queue_async_work|Adds an asynchronous work object to the queue so that it can be scheduled for execution.|
|FUNC|napi_cancel_async_work|Cancels the queued asynchronous work if it has not been started.|
|FUNC|napi_get_node_version|Obtains the current Node-API version.|
|FUNC|napi_get_version|Obtains the latest Node-API version supported when the Node.js runtime.|
|FUNC|napi_create_promise|Creates a deferred object and a JavaScript promise.|
|FUNC|napi_resolve_deferred|Resolves a deferred object that is associated with a JavaScript promise.|
|FUNC|napi_reject_deferred|Rejects a deferred object that is associated with a JavaScript promise.|
|FUNC|napi_is_promise|Checks whether the given JavaScript value is a promise object.|
|FUNC|napi_run_script|Executes a string of JavaScript code.|
|FUNC|napi_get_uv_event_loop|Obtains the current libuv loop instance.|
