####Swagger specification extract
[Swagger Object](#swaggerobject)<br>
[Info Object](#infoobject)<br>
[Contact Object](#contactobject)<br>
[License Object](#licenseobject)<br>
[Paths Object](#pathsobject)<br>
[Path Item Object](#pathitemobject)<br>
[Operation Object](#operationobject)<br>
[External Documentation Object](#externaldocumentationobject)<br>
[Parameter Object](#parameterobject)<br>
[Items Object](#itemsobject)<br>
[Responses Object](#responsesobject)<br>
[Response Object](#responseobject)<br>
[Headers Object](#headersobject)<br>
[Example Object](#exampleobject)<br>
[Header Object](#headerobject)<br>
[Tag Object](#tagobject)<br>
[Reference Object](#referenceobject)<br>
[Schema Object](#schemaobject)<br>
[Definitions Object](#definitionsobject)<br>
[Parameters Definitions Object](#parametersdefinitionsobject)<br>
[Responses Definitions Object](#responsesdefinitionsobject)<br>
[Security Definitions Object](#securitydefinitionsobject)<br>
[Security Scheme Object](#securityschemeobject)<br>
[Scopes Object](#scopesobject)<br>
[Security Requirement Object](#securityrequirementobject)<br>
<br>**Fields in bold are required.**

####<a name="swaggerobject">Swagger object</a>
Root document object.
* **swagger [string]**<br>Specifies the Swagger Specification version.
* **info [[Info Object]](#infoobject)**<br>Provides metadata about the API.
* **paths [Paths Object]**
* host [string]<br>The hostname or ip that serves tha API.<br>May include a port.
* basepath [string]<br>The base path on which the API is served, relative to `host`.<br>Starts with a leading slash.
* schemes [string[]]<br>The transfer protocol of the API. Values can only be `http`, `https`, `ws`, `wss`.
* consumes [string[]]<br>The list of MIME types the APIs can consume.
* produces [string[]]<br>The list of MIME types the APIs can produce.
* definitions [Definitions Object]<br>An object to hold data types produced and consumed by operations.
* parameters [Parameters Definitions Object]<br>An object to hold parameters that can be used across operations.
* responses [Responses Definitions Object]<br>An object to hold responses that can be used across operations.
* securityDefinitions [Security Definitions Object]<br>Security scheme definitions that can be used across the specifications.
* security [Security Requirement Object]<br> A declaration of which security schemes are applied for the API as a whole.
* tags [Tag Object]<br>A list of tags used by the specification with additional metadata.
* externalDocs [external Documentation Object]<br>Additional external documentation.

####<a name="infoobject">Info object</a>
Provides metadata about the API.
* **title [string]**
* **version [string]**
* description [string]
* termsOfService [string]
* contact [Contact Object]
* license [License Object]

####<a name="contactobject">Contact object</a>
* name [string]
* url [string]
* email [string]

####<a name="licenseobject">License object</a>
* **name [string]**<br>The name of the license used for the API.
* url [string]<br>An URL to the license used for the API.

####<a name="pathsobject">Paths object</a>
* /{path} [Path Item Object]<br>A relative path to an individual endpoint.

####<a name="pathitemobject">Path Item Object</a>
