<a name="table"> </a>
| Tag|Short Description|StubGen|JsonGen|
|--|--|:--:|:--:|
|[@stubgen:include](#stubgen_include)|insert another C++ file FILE|Yes| Yes|
|[@insert](#insert)|same as @stubgen:include FILE| Yes|Yes|
|[@stubgen:skip](#stubgen_skip)|stop processing current file, now deprecated FILE| Yes|Yes|
|[@stop](#stop)|same as @stubgen:skip, not deprecated, but also never advertised FILE|Yes| Yes|
|[@stubgen:omit](#stubgen_omit)|omit processing of the next class or method CLASS, METHOD (PROXYSTUB-ONLY)| Yes| No (but has side-effects)|
|[@omit](#omit)|same as @stubgen:omit CLASS, METHOD (PROXYSTUB-ONLY)| Yes| No (but has side-effects)|
|[@stubgen:stub](#stubgen_stub)|emit empty function stub instead of full proxy implementation METHOD (PROXYSTUB-ONLY)| Yes| No|
|[@stub](#stub)|same as @stubgen:stub METHOD (PROXYSTUB-ONLY)| Yes| No|
|[@in](#in)|marks an input parameter PARAM| Yes| Yes|
|[@out](#out)|marks an output parameter PARAM| Yes|Yes|
|[@length](#length)|specifies the expresion to evaluate length of an array parameter PARAM(can be other parameter name, or constant, or math expression)| No | Yes |
|[@maxlength](#maxlength)|specifies a maximum buffer length value (a constant, a parameter name or a math expression),") if not specified @length is used as maximum length, use round parenthesis for expressions",) e.g.: @length:bufferSize @length:(width * height * 4) | No | Yes |
|[@interface](#interface)| specifies a parameter holding interface ID value for void* interface passing | Yes | No |
|[@inout](#inout)|marks as input and output parameter (a.k.a @in @out) PARAM| Yes|Yes|
|[@json](#json)|marks a class as JsonGenerator input CLASS (JSON-ONLY)| No| Yes|
|[@json:omit](#json_omit)|marks a method/property/notification to omit METHOD (JSON-ONLY| No| Yes|
|[@event](#event)|marks a class as JSON notification CLASS (JSON-ONLY)| No| Yes|
|[@extended](#extended)|(JSON-ONLY)| No| Yes|
|[@iterator](#iterator)|marks a class as an iterator CLASS (JSON-ONLY)| Yes| Yes|
|[@deprecated](#deprecated)|marks a method/property/notification deprecated (i.e. obsolete and candidate for removal) METHOD (JSON-ONLY)| No| Yes|
|[@obsolete](#obsolete)|marks a method/property/notification as obsolete METHOD (JSON-ONLY)| No| Yes|
|[@index](#index)|marks an index parameter to a property or notification PARAM (JSON-ONLY)| No| Yes|
|[@listener](#listener)|marks the notification as a "status listener" METHOD (JSON-ONLY)| No| Yes|
|[@brief ](#brief)|specifies brief description of a method/property/notification or parameter or POD structure member METHOD, PARAM, POD MEMBER (JSON-ONLY)| No| Yes|
|[@details ](#details)|specifies detaild description of a method/property/notification METHOD (JSON-ONLY)| No| Yes|
|[@param ](#param)|provide description for method/notification parameter or property/notification index METHOD| No | Yes|
|[@retval ](#retval)|specifies possible return error codes for method/property (can be many) METHOD (JSON-ONLY)| No|Yes|
|[@text](#text)|renames identifier METHOD, PARAM, POD MEMBER, ENUM (JSON-ONLY)| No| Yes|
|[@property](#property)||No|Yes|
<a name="stubgen_include"></a>
# @stubgen:include
### Description
This tag is used when we need to include definitions from another file. This tag imports the contents of the file while creating json generation and as well as in stub generation. 
Like #include preprocessor the contents of the files are included before processing any other tags
### Example
IDeviceInfo.h [includes](https://github.com/rdkcentral/ThunderInterfaces/blob/master/interfaces/IDeviceInfo.h#L24) com/IIteratorType.h to get the definition for RPC::IIteratorType

`
// @stubgen:include <com/IIteratorType.h>
`

[top](#table)

<a name="insert"></a>
# @insert
### Description
This tag is same as [@stubgen:include](#stubgen_include). 
### Example
Test code, IJsonGeneratorCorpus.h [includes](https://github.com/rdkcentral/Thunder/blob/master/Tests/jsongenerator/IJsonGeneratorCorpus.h#L27) com/IIteratorType.h using insert tag.

`
// @insert <com/IIteratorType.h>
`

[top](#table)

<a name="stubgen_skip"></a>
# @stubgen:skip

### Description
Remaining portion of the file below this tag will be skipped from processing. If placed on top of the file, the complete file is skipped from processing.
This tag is currently deprecated. [@omit](#omit) is preferred over this tag.

### Example
[IDRM.h](https://github.com/rdkcentral/ThunderInterfaces/blob/master/interfaces/IDRM.h#L41) file is skipped from processing placing this tag at the top of this file.


`
// @stubgen:skip
`

[top](#table)

<a name="stop"></a>
# @stop
### Description
This tag is same as [@stubgen:skip](#stubgen_skip)

[top](#table)

<a name="stubgen_omit"></a>
# @stubgen:omit
### Description

This tag is applies to struct, class, functions. When the struct/class marked as omit, proxy stubs will not be created for those. 
Including its inner class/struct/enums. But [@json](#json) tag will still be applicable to the struct/class. 

### Example

[ITimeSync.h](https://github.com/rdkcentral/ThunderInterfaces/blob/master/interfaces/ITimeSync.h#L27) uses omit flag to skip the content of the whole file. 
This is the preferred way to skip the content.

[top](#table)

<a name="omit"></a>
# @omit
### Description

Same as [@stubgen:omit](#stubgen_omit)

[top](#table)

<a name="stubgen_stub"></a>
# @stubgen:stub
### Description

When we dont want to create a proxy implementation for a function we mark it with this tag.

??? May be those functions which doesnt make sense to call from the other side of the process boundary ???

### Example

In [IShell](https://github.com/rdkcentral/Thunder/blob/master/Source/plugins/IShell.h#L232) Submit function is marked as stub as it does not want that function to be called beyond WPEFramework process


[top](#table)

<a name="stub"></a>
# @stub
### Description

Same as [@stubgen:stub](#stubgen_stub)

[top](#table)

<a name="in"></a>
# @in
### Description

This tag will mark a parameter in a function as an input parameter. By default, all parameters in a function are treated as input paramter. 
All input paramters are expected to be const. If not, warning will be thrown during JSONRPC code generation.

### Example

In [IDolby.h](https://github.com/rdkcentral/ThunderInterfaces/blob/master/interfaces/IDolby.h#L77) enable parameter is marked as an input parameter.

[top](#table)

<a name="out"></a>
# @out
### Description
This tag will mark a parameter in a function as an output parameter. By default, all parameters in a function are treated as input parameter.
Output parameters should either be a reference or a pointer and should not be constant.
If these conditions are not met, Error will be thrown during JSONRPC code generation.

### Example
In [IDolby.h](https://github.com/rdkcentral/ThunderInterfaces/blob/master/interfaces/IDolby.h#L67) supported parameter is marked as output paramter.

[top](#table)

<a name="length"></a>
# @length
### Description

This tag should be associated with an array. It specifies the expresion to evaluate length of an array parameter PARAM(can be other parameter name, or constant, or math expression)


### Example

Possible usage of length tag

As another parameter

`/* @length:param1 */`

As a constant.

`/* @length:32 */`

As an expression

`/* @length:(param1+param2+16) */`

In IOCDM.h, 

function [StoreLicenseData](https://github.com/rdkcentral/ThunderInterfaces/blob/master/interfaces/IOCDM.h#L159) @length param is marked as constant.

function [SelectKeyId](https://github.com/rdkcentral/ThunderInterfaces/blob/master/interfaces/IOCDM.h#L163) @length tag is marked as another parameter.


[top](#table)

<a name="maxlength"></a>
# @maxlength
### Description
This tag is associated with [/* @inout */](#inout) tag. It specifies a maximum buffer length value (a constant, a parameter name or a math expression if not specified @length is used as maximum length, use round parenthesis for expressions, e.g.: @length:bufferSize @length:(width * height * 4)
It will use different buffer for output depending upon this tag. If not specified it will reuse the same input buffer for output as well.
### Example
In [IPerformance.h](https://github.com/rdkcentral/ThunderInterfaces/blob/5fa166bd17c6b910696c6113c5520141bcdea07b/interfaces/IPerformance.h#L32) it specifies, the maximum length for the buffer.

[top](#table)

<a name="interface"></a>
# @interface
### Description

This tag specifies a parameter holding interface ID value for void* interface passing. Functions like [Aquire](https://github.com/rdkcentral/Thunder/blob/master/Source/com/ICOM.h#L45) will return the pointer to the queried interface. For such functions, this tag will specify which field to look for to get the corresponding interface id.

### Example

In [ICOM.h](https://github.com/rdkcentral/Thunder/blob/master/Source/com/ICOM.h#L45) specifies parameter 3 interfaceId holds the interface id for the returned interface.

[top](#table)

<a name="inout"></a>
# @inout
### Description

In few methods, a parameter will act both as input as well as output parameter. Such parameters are marked using this tag. 

### Example
In [IDisplayInfo.h](https://github.com/rdkcentral/ThunderInterfaces/blob/5fa166bd17c6b910696c6113c5520141bcdea07b/interfaces/IDisplayInfo.h#L98) the parameter length acts both as input as well as the output. While calling this API, application will fill the buffer size in the length paramenter.
When the function returns, the parameter will have the modified length value. Thus acts as both input and output parameter

[top](#table)

<a name="json"></a>
# @json
### Description

This tag helps to generate JSONRPC files for the given Class/Struct/Enum.
It will creates files JsonData_<InterfaceName>Output.h, JsonEnum_<InterfaceName>Output.cpp, J<InterfaceName>Output.cpp

JsonData_<structname>Output.h will have definitions for structs that are used in JsonMethods.
JsonEnum_<Structname>Output.cpp will have definition for Enums
J<InterfaceFilename>Output.h will have definition for the methods for JSONRPC.

### Example

[IDisplayInfo.h](https://github.com/rdkcentral/ThunderInterfaces/blob/5fa166bd17c6b910696c6113c5520141bcdea07b/interfaces/IDisplayInfo.h#L121) uses this tag to generate JSONRPC files. 
It will create the following files
JsonEnum_HDRProperties.cpp
JHDRProperties.h


[top](#table)

<a name="json_omit"></a>
# @json:omit
### Description

This tag is used to leave out any Class/Struct/Enum from generating JSONRPC file.

### Example

[IBrowser.h](https://github.com/rdkcentral/ThunderInterfaces/blob/5fa166bd17c6b910696c6113c5520141bcdea07b/interfaces/IBrowser.h#L117) uses this tag to remove HeaderList function from JsonRPC file generation.

[top](#table)

<a name="event"></a>
# @event
### Description

This tag is used in JSONRPC file generation. This tag is used to mark a struct/class that will be called back as an notification by the framework.

### Example

[IDolby.h](https://github.com/rdkcentral/ThunderInterfaces/blob/5fa166bd17c6b910696c6113c5520141bcdea07b/interfaces/IDolby.h#L53) Whenever the audio mode changes AudioModeChanged API will be called. 

[top](#table)

<a name="extended"></a>
# @extended
### Description

This tag is deprecated.
By default, while creating the JSONRPC, if a method has a single POD paramenter, It's equivalent Json class is used.
If a class is marked with this tag, such conversion will not take place. It will still create a separate Data class to access that parameter.

???When to use???

### Example

In [IVolumeControl.h](https://github.com/rdkcentral/ThunderInterfaces/blob/5fa166bd17c6b910696c6113c5520141bcdea07b/interfaces/IVolumeControl.h#L31) INotification structure is marked with this tag.
The functions parameters for muted and volume will be implemented in expanded format meaning a JSON wrapper class will be created even if there is only one member present.

[top](#table)

<a name="iterator"></a>
# @iterator
### Description

This is a helper tag. This helps in generating helper functions to iterate through an array. 
The helper functions are defined in IIteratorType.h. 
The interfaces which needs iteration functionality should include that header using [@stubgen:include](#stubgen_include) tag.
In Json Generator,it will help to convert the class to JsonArray.
In Proxy generation, it will help in generating the helper function like Current, Next, Previous for iterating through the array.


### Example

[IDeviceInfo.h](https://github.com/rdkcentral/ThunderInterfaces/blob/5fa166bd17c6b910696c6113c5520141bcdea07b/interfaces/IDeviceInfo.h#L24) uses @stubgen:include to insert the IIteratorType to that file.
Which inturn used to iterate through iterators in function [AudioOutputs](https://github.com/rdkcentral/ThunderInterfaces/blob/5fa166bd17c6b910696c6113c5520141bcdea07b/interfaces/IDeviceInfo.h#L83), [VideoOutputs](https://github.com/rdkcentral/ThunderInterfaces/blob/5fa166bd17c6b910696c6113c5520141bcdea07b/interfaces/IDeviceInfo.h#L84), [Resolutions](https://github.com/rdkcentral/ThunderInterfaces/blob/5fa166bd17c6b910696c6113c5520141bcdea07b/interfaces/IDeviceInfo.h#L85)

[top](#table)

<a name="deprecated"></a>
# @deprecated
### Description

This tag is used to mark a Method, Property as deprecated in the generated document.

### Example

When a method is marked with this tag, in the generated .md, it will be marked with the below Message 
>This API is **deprecated** and may be removed in the future. It is no longer recommended for use in new implementations.

[top](#table)

<a name="obsolete"></a>
# @obsolete
### Description

This tag is used to mark a Method, Property as obolete in the generated document.

### Example

When a method is marked with this tag, in the generated .md, it will be marked with the below Message 
> This API is **obsolete**. It is no longer recommended for use in new implementations

[top](#table)

<a name="index"></a>
# @index
### Description
In some cases, clients are interested only in certain events. In such cases, we can use this tag.
Index should be the first parameter in the function. 

??? Not able to find an example ??? 

### Example

[top](#table)

<a name="listener"></a>
# @listener
### Description

??? Not able to find an example ???

### Example

[top](#table)

<a name="brief"></a>
# @brief
### Description

This is a short description about the function. This description will be appeneded to the method description in the JSONRPC generated file.

??? From the code, it is understood that it can extract the example following the text e.g. but not able to find a working example???

### Example

[IDolby.h](https://github.com/rdkcentral/ThunderInterfaces/blob/5fa166bd17c6b910696c6113c5520141bcdea07b/interfaces/IDolby.h#L65) mentions a brief descrption using this tag.
JsonGenerator.py will create a file JDolbyOutput.h. In that file the method AtmosMetadata. It adds that description.

```

// Property: dolby_atmosmetadata - Atmos capabilities of Sink (r/o)

    module.Register<void, Core::JSON::Boolean>(_T("dolby_atmosmetadata"),

        [_destination](Core::JSON::Boolean& Result) -> uint32_t {

            uint32_t _errorCode;

            // read-only property get

            bool result{};

            _errorCode = _destination->AtmosMetadata(result);

            if (_errorCode == Core::ERROR_NONE) {

                Result = result;

            }

            return (_errorCode);

        });

```

[top](#table)

<a name="details"></a>
# @details
### Description
Just like @brief starts a brief description, @details starts the detailed description. This tag will be used while creating markdown documents for the header.
There it will be captured in the description section for the method. This description will not be added in the code generation. 
It will be added only in the document generation.

[top](#table)

<a name="param"></a>
# @param
### Description
The syntax for this tag is @param <PARAMETER>. It is associated with a function/property.
This tag adds the description about the specified parameter in the generated code and in the generated document.

### Example

[IDolby.h](https://github.com/rdkcentral/ThunderInterfaces/blob/5fa166bd17c6b910696c6113c5520141bcdea07b/interfaces/IDolby.h#L76) add description about enable parameter using this tag.

[top](#table)

<a name="retval"></a>
# @retval
### Description

This tag is used in document creation.
The syntax for this tag is @retval <ErrorCode>: <Description>. It is associated with function/property
This tag adds description about each return codes specified in the generated markdown document.

### Example

In [IVolumeControl.h](https://github.com/rdkcentral/ThunderInterfaces/blob/5fa166bd17c6b910696c6113c5520141bcdea07b/interfaces/IVolumeControl.h#L54), it uses this tag to add description about the returned error code.

[top](#table)

<a name="text"></a>
# @text
### Description

This tag is applicable to Enums, function names and function parameters. 
When used with ENUMS, it will associate the Enum values to the given text in the JSON code.
When used in function names like below, it will replace the actual function name with the text that is given.
When used in function parameter like below, it will replace the parameter name with the text that is given in the tag.

### Example

[IBrowser.h](https://github.com/rdkcentral/ThunderInterfaces/blob/5fa166bd17c6b910696c6113c5520141bcdea07b/interfaces/IBrowser.h#L61) uses this tag for ENUMS. The generated code for this header will map the text for these 
enums as allowed and not as Allowed, blocked and not as Blocked. Without these tags the string equivalent of the enums will be first letter caps followed by all small. Now with this tag, we have changed it to all small.

[top](#table)


<a name="property"></a>
# @property
### Description

We mark a method to be a property when we intented to simple get and set. It cannot have more than one parameter. 
A method which does more than get and set should not be marked as property even if it is having a single parameter.
A property is said to be write only if its parameter is const and there no ther method definition with non const is given for reading.
A property is said to be read only if its parameter is non-const and there no ther method definition with const is given for setting.
A property is said to be both if it has both const and non-const version present.

### Example

[IDolby.h](https://github.com/rdkcentral/ThunderInterfaces/blob/5fa166bd17c6b910696c6113c5520141bcdea07b/interfaces/IDolby.h#L64) is a read only property as it does not have a const version for setting the property.

[IBrowser.h](https://github.com/rdkcentral/ThunderInterfaces/blob/5fa166bd17c6b910696c6113c5520141bcdea07b/interfaces/IBrowser.h#L140) is a write only property as it has only const version and not non const version is available.

[IBrowser.h](https://github.com/rdkcentral/ThunderInterfaces/blob/5fa166bd17c6b910696c6113c5520141bcdea07b/interfaces/IBrowser.h#L100) is a read write property as it has both const and non const version defined.


[top](#table)
