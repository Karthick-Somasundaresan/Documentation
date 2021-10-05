### Table of Contents

- [Introduction](#head.Introduction)
- [Description](#head.Description)
- [Configuration](#head.Configuration)
- [Methods](#head.Methods)
- [Notifications](#head.Notifications)

|Tag|Description|StubGen|JsonGen|
|--|--|--|--|
|[@stubgen:include](stubgen_include)|insert another C++ file FILE|Yes| Yes|
|@insert|same as @stubgen:include FILE| Yes|Yes|
|@stubgen:skip|stop processing current file, now deprecated FILE| Yes|Yes|
|@stop|same as @stubgen:skip, not deprecated, but also never advertised FILE|Yes| Yes|
|@stubgen:omit|omit processing of the next class or method CLASS, METHOD (PROXYSTUB-ONLY)| Yes| No (but has side-effects)|
|@omit|same as @stubgen:omit CLASS, METHOD (PROXYSTUB-ONLY)| Yes| No (but has side-effects)|
|@stubgen:stub|emit empty function stub instead of full proxy implementation METHOD (PROXYSTUB-ONLY)| Yes| No|
|@stub|same as @stubgen:stub METHOD (PROXYSTUB-ONLY)| Yes| No|
|@in|marks an input parameter PARAM| Yes| Yes|
|@out|marks an output parameter PARAM| Yes|Yes|
|@length:<expr>|specifies the expresion to evaluate length of an array parameter PARAM(can be other parameter name, or constant, or math expression)| | |
|@maxlength:<expr>PARAM| | | |
|@interface:<id>PARAM| | | |
|@inout|marks as input and output parameter (a.k.a @in @out) PARAM| Yes|Yes|
|@json|marks a class as JsonGenerator input CLASS (JSON-ONLY)| No| Yes|
|@json:omit|marks a method/property/notification to omit METHOD (JSON-ONLY| No| Yes|
|@event|marks a class as JSON notification CLASS (JSON-ONLY)| No| Yes|
|@extended|(JSON-ONLY)| No| Yes|
|@iterator|marks a class as an iterator CLASS (JSON-ONLY)| Yes| Yes|
|@deprecated|marks a method/property/notification deprecated (i.e. obsolete and candidate for removal) METHOD (JSON-ONLY)| No| Yes|
|@obsolete|marks a method/property/notification as obsolete METHOD (JSON-ONLY)| No| Yes|
|@index|marks an index parameter to a property or notification PARAM (JSON-ONLY)| No| Yes|
|@listener|marks the notification as a "status listener" METHOD (JSON-ONLY)| No| Yes|
|@brief <text>|specifies brief description of a method/property/notification or parameter or POD structure member METHOD, PARAM, POD MEMBER (JSON-ONLY)| No| Yes|
|@details <text>|specifies detaild description of a method/property/notification METHOD (JSON-ONLY)| No| Yes|
|@param <param> <text>|provide description for method/notification parameter or property/notification index METHOD| |
|@retval <code> <text>|specifies possible return error codes for method/property (can be many) METHOD (JSON-ONLY)| No|Yes|
|@text <text>|renames identifier METHOD, PARAM, POD MEMBER, ENUM (JSON-ONLY)| No| Yes|


<a name="stubgen_include"></a>
# @stubgen:include
<a name="head.Introduction"></a>
# Introduction
<a name="head.description"></a>
# Description
