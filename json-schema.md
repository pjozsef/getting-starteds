####JSON Schema

####Basics
* **`type`**<br>Defines what type of value is accepted for a given property.<br>Example: {"type": "object"}
* **`id`**<br>Declares a unique identifier for the schema.<br>Declares a base URL against which $ref URLs are resolved.<br>Example: {"id": "http://my.domain.com/schemas/address.json"}

####Types
* **`string`**
  * minLength [number]
  * maxLength [number]
  * pattern [regexString]
  * format ["date-time", "mail", "hostname", "ipv4", "ipv6", "uri"]
* **`number`**
  * multipleOf [number]
  * minimum [number]
  * maximum [number]
  * exclusiveMinimum [bool]
  * exclusiveMaximum [bool]
* **`integer`**<br>Same as {"type": "number", "multipleOf": 1.0}
* **`object`**
  * properties [object]
  * additoinalProperties [bool]/[object]<br> If it's an object, that object is a schema that will be used to validate any additional properties not listed in `properties`.
  * required [array]
  * minProperties [number]
  * maxProperties [number]
  * dependencies [object]<br>Defines how properties are dependent on each other.<br>Example: `"dependencies":{"a" : ["b", "c"]}`, meaning that if property `a` is present, property `b` and `c` must also be present.
  * patternProperties [object]<br>Example: Any additional properties whose names start with the prefix S_ must be strings, and any with the prefix I_ must be integers<br>```{"patternProperties": {"^S_": {"type": "string"}, "^I_": {"type": "integer"}}}```
* **`array`**
  * General validation
    * minItems [number]
    * maxItems [number]
    * uniqueItems [bool]
  * List validation
    * items [object]<br>The schema against which all items are validated.
  * Tuple validation
    * items [array]<br>Each element of the array is a schema, which validates each index of the document' array.
    * additionalItems [bool]
* **`boolean`**
* **`null`**

####Sources
http://spacetelescope.github.io/understanding-json-schema/
