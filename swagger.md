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
* **paths [[Paths Object]](#pathsobject)**
* host [string]<br>The hostname or ip that serves tha API.<br>May include a port.
* basepath [string]<br>The base path on which the API is served, relative to `host`.<br>Starts with a leading slash.
* schemes [string[]]<br>The transfer protocol of the API. Values can only be `http`, `https`, `ws`, `wss`.
* consumes [string[]]<br>The list of MIME types the APIs can consume.
* produces [string[]]<br>The list of MIME types the APIs can produce.
* definitions [[Definitions Object]](#definitionsobject)<br>An object to hold data types produced and consumed by operations.
* parameters [[Parameters Definitions Object]](#parametersdefinitionsobject)<br>An object to hold parameters that can be used across operations.
* responses [[Responses Definitions Object]](#responsesdefinitionsobject)<br>An object to hold responses that can be used across operations.
* securityDefinitions [[Security Definitions Object]](#securitydefinitionsobject)<br>Security scheme definitions that can be used across the specifications.
* security [[Security Requirement Object]](#securityrequirementobject)<br> A declaration of which security schemes are applied for the API as a whole.
* tags [[Tag Object]](#tagobject)<br>A list of tags used by the specification with additional metadata.
* externalDocs [[External Documentation Object]](#externaldocumentationobject)<br>Additional external documentation.

####<a name="infoobject">Info object</a>
Provides metadata about the API.
* **title [string]**
* **version [string]**
* description [string]
* termsOfService [string]
* contact [[Contact Object]](#contactobject)
* license [[License Object]](#licenceobject)

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
* get [[Operation Object]](#operationobject)
* post [[Operation Object]](#operationobject)
* put [[Operation Object]](#operationobject)
* delete [[Operation Object]](#operationobject)
* options [[Operation Object]](#operationobject)
* head [[Operation Object]](#operationobject)
* patch [[Operation Object]](#operationobject)
* parameters [[Parameter Object][]](#parameterobject)/[[Reference Object][]](#referenceobject)
<br>A list of parameters that are applicable for all the operations described under this path.
* $ref [string]<br>External definition of this path item.

####<a name="operationobject">Operation Object</a>
* tags [string]<br>List of tags for API documentation, logical grouping of operations by resources, etc.
* summary [string]
* description [string]
* operationId [string]<br>Unique string used to identify the operation. Must be unique among all operations in tha API.
* consumes [string]
* produces [string]
* parameters [[Parameter Object]](#parameterobject)/[[Reference Object]](#referenceobject)
* responses [[Responses Object]](#responsesobject)
* schemes [string[]]<br>Trasnfer protocol of the operation, values can only be `http`, `https`, `ws`, `wss`
* deprecated [boolean]
* security [[Security Requirement Object]](#securityrequirementobject)

####<a name="externaldocumentationobject">External Documentation Object</a>
* description [string]
* url [string]

####<a name="parameterobject">Parameter Object</a>
Describes a single operation parameter. A unique parameter id sdefined by a combination of a name and location.<br>
* **name [string]**
* **in [string]**<br>Location of the parameter. Possible values are `query`, `header`, `path`, `formData`, `body`.
* description [string]
* required [boolean]

If `in` is `body`:
* schema [[Schema Object]](#schemaobject)

Otherwise:
* type, format, allowEmptyValue, items, collectionFormat, default, maximum, minimum, exclusiveMaximum, exclusiveMinimum, maxLength, minLength, pattern, maxItems, minItems, uniqueItems, enum, multipleOf

Collection format:
* csv<br>foo,bar
* ssv<br>foo bar
* tsv<br>foo\tbar
* pipes<br>foo|bar
* multi<br>Multiple parameter instances of the same name<br>foo=bar&foo=baz

####<a name="itemsobject">Items Object</a>
A limited subset of JSON-Schema's items object. It is used by parameter definitions that are not located in `body`.

####<a name="responsesobject">Responses Object</a>
* default [[Response Object]](#responseobject)/[[Reference Object]](#referenceobject)
* {HTTP status code} [[Response Object]](#responseobject)/[[Reference Object]](#referenceobject)

####<a name="responseobject">Response Object</a>
* **description [string]**
* schema [[Schema Object]](#schemaobject)<br>Definition of the response structure. If this field is absent, it means no content is returned as part of the response.
* headers [[Headers Object]](#headersobject)
* examples [[Example Object]](#exampleobject)

####<a name="headersobject">Headers Object</a>
* {name} [[Header Object]](#headerobject)<br>The name of the property corresponds to the name of the header. The value describes the type of the header.

####<a name="headerobject">Header Object</a>
* type [string]<br>Must be any of `string`, `number`, `integer`, `boolean`, `array`.
* **items [[Items Object]](#itemsobject)**<br>Required if `type` is `array`.
* format [string]
* description [string]
* collectionFormat, default, maximum, minimum, exclusiveMaximum, exclusiveMinimum, maxLength, minLength, pattern, maxItems, minItems, uniqueItems, enum, multipleOf

####<a name="exampleobject">Example Object</a>
* {mime type} [*]<br>{The name of the property must be one of the `Operation`'s `produces` values. The value should be an example of what such a response would look like.

####<a name="tagobject">Tag Object</a>
* name [string]<br>
* description [string]<br>
* externalDocs [[External Documentation Object]](#externaldocumentationobject)

####<a name="referenceobject">Reference Object</a>
* **$ref [string]**<br>Must be a JSON pointer.

####<a name="schemaobject">Schema Object</a>
The same as described in the JSON Schema specification, extended by the following properties:
* discriminator [string]<br>Adds support for polymorph8ism.
* readOnly [boolean]<br>Declared the property as read only, meaning it ma be sent as part of a response, but must not be sent as part of the request.
* xml [[XML Object]](#xmlobject)
* externalDocs [[External Documentation Object]](#externaldocumentationobject)
* example [*]

####<a name="definitionsobject">Definitions Object</a>
An object to hold data types that can be consumed and produced by operations.
* {name} [[Schema Object}}(#schemaobject)

####<a name="parametersdefinitionsobject">Parameters Definitions Object</a>
An object to hold parameters to be reused across operations.
* {name} [[Parameter Object]](#parameterobject)

####<a name="responsesdefinitionsobject">Responses Definitions Object</a>
An object to holds responses to be reused accross operations.
* {name} [[Response Object]](#responseobject)

####<a name="securitydefinitionsobject">Security Definitions Object</a>
A declaration of the security schemes available to be used in the specifications.
* {name} [[Security Scheme Object]](#securityschemeobject)

####<a name="securityschemeobject">Security Scheme Object</a>
Allows the definition of a security scheme that can be used by the operations. Supported schemes are basic authentication, an API key and OAuth2's common flows.
* **type [string]**<br>Value must be `basic`, `apiKey` or `oauth2`.
* description [string]
* **name [string]** *ApiKey*<br>The name of the header or query parameter to be used.
* **in [string]** *ApiKey*<br>The location of the API key. Value must be `query` or `header`.
* **flow [string]** *Oauth2*<br>The flow used by the OAuth2 security scheme, Value must be `implicit`, `password`, `application` or `accessCode`.
* **authorizationUrl [string]** *Oauth2(implicit, accessCode)*
* **tokenUrl [string]** *Oauth2(password, application, accessCode)*
* **scopes [[Scopes Object]](#scopesobject)** *Oauth2*

####<a name="scopesobject">Scopes Object</a>
Lists the available scopes for an OAuth2 security scheme.
* {name} [string]<br>Maps between a name of a scope to a short description of it.

####<a name="securityrequirementobject">Security Requirement Object</a>
Lists the required security schemes to execute this operation. The object can have multiple security schemes declared in it which are all required.
The name used for each property must correspond to a security scheme declared in the [[Security Definitions]](#securitydefinitionsobject).
* {name} [string]<br>If the security scheme is of type `Oauth2`, then the value is a list of scope names required for the execution. For other security scheme types, the array must be empty.

####Sources
http://swagger.io/specification
