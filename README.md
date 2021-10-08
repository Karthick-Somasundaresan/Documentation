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
|[@length](#length)|specifies the expresion to evaluate length of an array parameter PARAM(can be other parameter name, or constant, or math expression)| | |
|[@maxlength](#maxlength)| | | |
|[@interface](#interface)| | | |
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
|[@param ](#param)|provide description for method/notification parameter or property/notification index METHOD| |
|[@retval ](#retval)|specifies possible return error codes for method/property (can be many) METHOD (JSON-ONLY)| No|Yes|
|[@text](#text)|renames identifier METHOD, PARAM, POD MEMBER, ENUM (JSON-ONLY)| No| Yes|

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
### Example

[top](#table)

<a name="out"></a>
# @out
### Description
### Example

[top](#table)

<a name="length"></a>
# @length
### Description
### Example

[top](#table)

<a name="maxlength"></a>
# @maxlength
### Description
### Example

[top](#table)

<a name="interface"></a>
# @interface
### Description
### Example

[top](#table)

<a name="inout"></a>
# @inout
### Description
### Example

[top](#table)

<a name="json"></a>
# @json
### Description
### Example

[top](#table)

<a name="json_omit"></a>
# @json:omit
### Description
### Example

[top](#table)

<a name="event"></a>
# @event
### Description
### Example

[top](#table)

<a name="extended"></a>
# @extended
### Description
### Example

[top](#table)

<a name="iterator"></a>
# @iterator
### Description
### Example

[top](#table)

<a name="deprecated"></a>
# @deprecated
### Description
### Example

[top](#table)

<a name="obsolete"></a>
# @obsolete
### Description
### Example

[top](#table)

<a name="index"></a>
# @index
### Description
### Example

[top](#table)

<a name="listener"></a>
# @listener
### Description
### Example

[top](#table)

<a name="brief"></a>
# @brief
### Description
### Example

[top](#table)

<a name="details"></a>
# @details
### Description
### Example

[top](#table)

<a name="param"></a>
# @param
### Description
### Example

[top](#table)

<a name="retval"></a>
# @retval
### Description
### Example

[top](#table)

<a name="text"></a>
# @text
### Description
### Example

[top](#table)
