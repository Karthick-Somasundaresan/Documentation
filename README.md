
|Tag|Description|StubGen|JsonGen|
|--|--|--|--|
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
|[@length:<expr>](#length)|specifies the expresion to evaluate length of an array parameter PARAM(can be other parameter name, or constant, or math expression)| | |
|[@maxlength:<expr>PARAM](#maxlength)| | | |
|[@interface:<id>PARAM](#interface)| | | |
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
|[@brief <text>](#brief)|specifies brief description of a method/property/notification or parameter or POD structure member METHOD, PARAM, POD MEMBER (JSON-ONLY)| No| Yes|
|[@details <text>](#details)|specifies detaild description of a method/property/notification METHOD (JSON-ONLY)| No| Yes|
|[@param <param> <text>](#param)|provide description for method/notification parameter or property/notification index METHOD| |
|[@retval <code> <text>](#retval)|specifies possible return error codes for method/property (can be many) METHOD (JSON-ONLY)| No|Yes|
|[@text <text>](#text)|renames identifier METHOD, PARAM, POD MEMBER, ENUM (JSON-ONLY)| No| Yes|

<a name="#stubgen_include"></a>
# stubgen_include

<a name="insert"></a>
# insert

<a name="stubgen_skip"></a>
# stubgen_skip

<a name="stop"></a>
# stop

<a name="stubgen_omit"></a>
# stubgen_omit

<a name="omit"></a>
# omit

<a name="stubgen_stub"></a>
# stubgen_stub

<a name="stub"></a>
# stub

<a name="in"></a>
# in

<a name="out"></a>
# out

<a name="length"></a>
# length

<a name="maxlength"></a>
# maxlength

<a name="interface"></a>
# interface

<a name="inout"></a>
# inout

<a name="json"></a>
# json

<a name="json_omit"></a>
# json_omit

<a name="event"></a>
# event

<a name="extended"></a>
# extended

<a name="iterator"></a>
# iterator

<a name="deprecated"></a>
# deprecated

<a name="obsolete"></a>
# obsolete

<a name="index"></a>
# index

<a name="listener"></a>
# listener

<a name="brief"></a>
# brief

<a name="details"></a>
# details

<a name="param"></a>
# param

<a name="retval"></a>
# retbal

<a name="text"></a>
# text
