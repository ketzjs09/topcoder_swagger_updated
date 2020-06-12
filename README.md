# Topcoder API Swagger Composition Reference
#### General Overview:
In the following document, each component of a swagger documentation has been described in terms of their generic utility as well as some additional details related to the additional adaptations that might be required to adhere to the expected guidelines for composing Topcoder API documentation.

_How to interpret indentations_ - Attention should be paid to the indentation of various components described below. The relative indentation of the components below are meant to reflect the expected indentation of the actual properties in the swagger file. For reference, in the following description, the properties 'version', 'title' etc have been indented under 'info'; this reflects the fact that these properties the properties 'version', 'title' etc are properties of the nested object, which is in turn the value of the 'info' property, which itself is a root-level property.

#### Component Descriptions:
**swagger:** This should be set to the swagger version in use. The value should be left as is unless the swagger version is updated.
*Example:*
  >"'swagger: 2.0'"

**info:** Value should be left empty. As discussed in the section above, this is a root-level property, and everything that is indented under this is effectively a sub-property, as it is the property of the nested object that forms the value of this particular property. _The same applied to every root level property._
  * **version:** This should contain the proper version of the swagger file with exactly reflects its current iteration. For every update, the version should be updated using the basic rule of - 
  x - major release
  y - minor release
  z - build number, where the version is x.y.z 
  For more guidelines on versioning, this resource can be referenced: https://semver.org/

    *Example:*
      >"version: 1.2.9"


  - **title:** This should contain the title of the API. For new APIs and in APIs where change in the title can be considered, the title should be assigned after proper consideration. It should clearly reflect the core use-case of the API. Practically, for most pre-existing APIs, the title Value should be left as is, i.e identical to the legacy title to avoid any confusion for developers acquainted with previous versions. 
  For new APIs, the title should be succinct but highly relevant and to the point, and should give the reader a clear idea of what the API is about at a high-level. 
  In addition to textual information, versioning and revision details can also be appended at the end of the title. For instance, in the following example the term 'v5' denotes the version of the challenge API.

    *Example:*
      >"title: Challenge API v5"

  - **description:**
    This should provide a clear and concise description of the API and a high level overview of the concept and model encapsulated by the API. Additional overarching information such as pagination and access controls etc should be shared if available. Here, detailed information should be provided at a high level about all the components discussed in the API documentation, in addition to any background/contextual information. Each specific component should then be discussed in detail in its own section. <br/>
    _Some qualitative guidelines_ - In terms of the qualitative nature of the description, it must be ensured that the description is long enough to contain all required information for a developer who's entirely unacquainted with the assets being discussed. 
    In fact, the description should be treated as somewhat of an education mini-tool to help the developer understand the context comprehensively. Yet, the text should not be too verbose and longer than required. In general however, the writers are expected to be slightly biased towards comprehensiveness (vs succinctness) when it comes to writing informative descriptions. <br/><br/>
  
    _On readability of the composition_ - It should be ensured that the description and the entire documentation in general should be easily readable by a developer who has a reasonable proficiency in English but not necessarily very high or native-level proficiency. Hence, it should be ensure that the readability level of the documentations are approachable as possible. To help with this, several readability metrics are available on the Internet, such as https://app.readable.com/text/. This particular resource helps measure the text's [Flesch-Kinaid Grade Level](https://en.wikipedia.org/wiki/Flesch%E2%80%93Kincaid_readability_tests#Flesch%E2%80%93Kincaid_grade_level) and [Gunning Fog Index](https://en.wikipedia.org/wiki/Gunning_fog_index). _Whenever possible, a Gunning Fox Index of less than 10.5 should be attempted for the entire documentation text._<br/><br/>

    *Example:*
      >_"description: Topcoder is a platform that engages talented people working remotely from around the world in order to deliver high-level software, design and data science services to its clients. One of the formats it does so is via the 'challenge format'.<br/>
      A 'challenge' is basically a contest where various contestants compete for a pre-defined set of prizes, which is awarded to the highest scoring contestants based on some pre-defined reference scorecard.
      Most challenges are open to the public for participation. Most challenges are comprised of several stages such as: registration, submission, review, appeals etc. The contestants submit during the submission phase, which is then reviewed by one or more reviewers. The results of the review are privately visible to the contestants, as in, a contestant who has submitted can only see their own submission. In most challenges, particularly 'development' track challenge of type 'Code', there is an option to appeal, where the contestants can appeal against any apparent error in review by the reviewer. After the appeals, the reviewers are required to respond to appeals made by the contestants in the appeal response phase, and once this phase is complete, the challenge is considered complete. The contestants' submissions are reverse sorted by their final review score, and the top N submissions receive the pre-defined prizes."_<br/>
      In the above toy example, notice how most relevant high-level details about the challenge process is shared with the developer who might be reading the documentation, so that are able to understand most aspects of the documentation. For instance, if some part of the documentation talks about 'appeals', they will have enough high level knowledge to readily understand what the endpoint/information is about, which can be further elaborate via more specific information in the relevant section.<br> 
      Note that this example is just for reference, an actual description might contain considerably more details based on the endpoints the API documentation needs to cover. After the above introduction has been composed, any additional information such as pagination, or any additional relevant information should be communicated. <br/>

**tags:** Value should be left empty. Paths can be grouped into groups and each group can have a corresponding tag. These tags can be defined in the root level as follows. In general, groups and hence tags should reflect some kind of actual grouping of the concepts/paths being defined. Grouping shouldn't be arbitrary or contrived.

For more information, please refer to https://swagger.io/docs/specification/grouping-operations-with-tags/ 

Important - The groups will be rendered in any swagger viewer in the order in which it is defined here under the 'tags' section. So proper consideration should be given to desired order of the groupings, and they should be listed below in that order.


  * **- name:** Should contain the name of the group tag. This tag should be in use by at least one path in the current swagger file. If any tag is not required anymore after an update to the API/swagger file, that tag should be removed.
  **description:** Should contain a concise description of tag. This information will be displayed at the top of the group. 
  **externalDocs:**
    - **url:** Should contain a link to any external resource if available. This should be populated by the relevant links that contain further information about this group

  * **- name:** Should contain the name of the another group
    **description:** Should contain the description of the group
    **externalDocs:**
      - **url:** Should contain the link of the group

  *Example:*
  > **- name:** ChallengeTypes
    **description:** Paths concerning the different types of challenges at Topcoder.  
    **externalDocs:**
      - **url:** https://help.topcoder.com/hc/en-us/articles/217481558-Development-Challenge-Types"
  

**host:**  Should be set to the host address.
*Example:*
  >host: api.topcoder.com
  
**basePath:** Should be set to the base path under the host address. Most probably will continue to reflect the current version of the API
*Example:*
  >basePath: /v5

**schemes:** The value should be left empty. This should contain the transfer protocols used by the API. http, https, and WebSocket schemes ws and wss are supported by swagger. 
*Example:*
 > schemes:
  -http
 -https"

**securityDefinitions:** The value should be left empty.  This should encapsulate all security schemes (authentication types) supported by the API.
  * **bearer:** This value should be left empty. This should encapsulate properties related to bearer security schemes. For more information about authentication, refer to: https://swagger.io/docs/specification/2-0/authentication/
    * **type:** This should contain the type of authentication to be used.
    *Example:*
      >type: apiKey ()

    * **name:** This should contain a descriptive name of the  authentication.  
    *Example:*
      >name: API Key Authorization

    * **in:** This should contain the location where the API key should be looked for. 
    *Example:*
      >in: header

**paths:** Value should be left empty. This encapsulates the paths in the API. This is the heart of the API definition, where individual paths in the API are defined. Attention should be paid that to the correctness of all the path names, and the subsequent properties of the paths.
  * **/<path_name>:** Value should be left empty. The name of this property should reflect the actual name of the path of the API. The name should be descriptive, and if it is a multi-word name, the words should be separated by dashes.
  *Examples:*
    > /challenge-types:

    > /challenge-phases:

    > /challenge-timelines
    * **<request_type>:** Value should be left empty. The name of this property should indicate the type of request - i.e. get/post/put/delete
    *Examples:*
      > get:

      > put:

      > post:
      * **tags:** Value should be left empty. This encapsulted the tag under which this path should be encapsulated when rendering by a viewer.

        - <tag_name> Only property name should be set.Value should be empty.
          *Example:*
          >ChallengeTypes

      * **description:** Should contain a detailed enough description of the API path. 
        *Example:*
          > description: Returns a list of all challenge types hosted at Topcoder
      * **produces:**
          - Should contain the format of response to be expected from the path.
          *Example:*
            > produces : application/json
      * **parameters:** Value should be left empty. This should encapsulate the different parameters inside the path /<path_name>. For further reference: https://swagger.io/docs/specification/2-0/describing-parameters/
        * **\$ref:** One or more of these $ref references can be used to refer to existing parameters that need to be defined at the root level parameter. Parameters have been described later.
        *Example:*
          > '$ref: #/parameters/perPage'
        * **name:** Should contain the name of the parameter. Names should be chosen to be concise and precisely indicating the intended parameter.
                *Example:*
          > name: description
        * **in:** Should contain the the location where the parameter should be found. That is, whether the parameter should be looked for in the query section or the path. Possible values can be query/path/header/cookie. For further reference: https://swagger.io/docs/specification/2-0/describing-parameters/
        *Example:*
          > in: query

        * **description:** Should contain detailed enough information about the intended use of the parameter, in addition other details such case-sensitivity, whether partial matches are allowed, etc.
        *Example:*
          > description: Name of the specific challenge type that's required. Can case-sensitive and partial matches are allowed.

        * **required:** Should contain the boolean value indicating whether the parameter is required or not.
        *Example:*
          > required: false
        
        * **type:** Should contain the datatype of the value to be entered for this parameter.
        *Example:*
          > type: string
      * **responses:** Value should be left empty. This should encapsulate the attributes related to the responses. For further reference, please refer to: https://swagger.io/docs/specification/2-0/describing-responses/
        * **<response_code>**: The value should be left empty. The name of this property should indicate the potential response code that has been implemented by the API. All response codes that are implemented should be listed using similar structures described below. List of response codes can be found here: https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html
          *Example:*
          > '200':

            **description:** Description/interpretation of the response code mentioned above. The definitions can be found here: https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html
            **schema:** The value should be empty. This will encapsulate the information about the schema of the response.
            *  **type:** Should contain the datatype of the schema. For the complete list of types, refer to the link shared above.
            * **items:** Should contain the schema that describes the type and format of array items.
            * **\$ref:** Should contain the the internal link to the definition that should be referenced. When a definition is reference, the schema defined in it is adopted by the intended schema of this response.
              *Example:*
              > $ref: #/definitions/ChallengeType

            **headers:** The value should be empty. This should encapsulate any custom headers to provide additional information in addition to the response body. For example, a rate-limited API may provide the rate limit status via response headers as follows:
            - **<header_name>** The value should be empty. This should encapsulate the name of the header, which in should be a hypher separate phrase or a word, generally starting with an 'X-'.
                *Example:*
              > **X-Page:**
              or 
              **X-RateLimit-Limit:**

            - **type:** This should describe the datatype of the response header. 
            *Example:*
              > type: integer

            - **description:** This should contain a clear and if required elaborate description of the response header, considering that the response header along with the response body might be one of the most read parts of the API reference.
  
**parameters:**
* **<parameter_name>** The value should be left empty. This should encapsulate the different parameters inside the path /<path_name>. These parameters can be referenced using \$ref by the parameter definitions under the 'parameter' property of path definitions. The string used for parameter_name should be concise and descriptive and should reflect the overall intention of the parameter. For particularly parameter names other than extremely generic ones like 'id', 'name' etc, copious amounts of details must be provided via the description sub-property. 
<br>For further reference: https://swagger.io/docs/specification/2-0/describing-parameters/.
    *Example:*
    > perPage:

    * **name:** Should contain the name of the parameter. Names should be chosen to be concise and precisely indicating the intended parameter.
    *Example:*
        > name: perPage
    * **in:** Should contain the the location where the parameter should be found. That is, whether the parameter should be looked for in the query section or the path. Possible values can be query/path/header/cookie. For further reference: https://swagger.io/docs/specification/2-0/describing-parameters/
    *Example:*
        > in: query
    * **description:** Should contain detailed enough information about the intended use of the parameter, in addition other details such case-sensitivity, whether partial matches are allowed, etc. In case of non-generic parameter names, ensure to provide enough context and background about the parameter.
    *Example:*
        > description: Name of the specific challenge type that's required. A challenge type be of type 'Code', 'F2F', 'Assembly' etc. For the entire list of eligible challenge type, refer to the resource http://www.topcoder.com/example_link. Can case-sensitive and partial matches are allowed.
    * **required:** Should contain the boolean value indicating whether the parameter is required or not.
    *Example:*
        > required: false
    * **type:** Should contain the datatype of the value to be entered for this parameter.
        > type: integer
    * **default:** Should contain the default value of the parameter in consideration.
    *Example:*
        > default: 20
    * **maximum:** Should contain the maximum permissible value of the parameter in consideration.
    *Example:*
        > maximum: 100
    
**definitions:** The value should be empty. This should encapsulate the data model definitions. These data models can be leveraged by the other parts of the swagger definitions above. Here, each model can be thought of a class in an object-oriented language, which can be referred as a data-type in the documentation, just like any other data type like a string, number, object etc. Although, it should be noted that the model should not necessarily be of object type. It can be of any usual type supported by Swagger, such as a number, string, boolean etc. For further details, refer to the 'type' sub-property below.


*  **<model_name>** The value should be empty. The property name itself should contain the name of the model. The name should generally be written with camel-casing and the name should be descriptive and yet not too long. Multiple models/schema can be listed. The name should should reflect the most relevant actual intention or the major use-case of the model. Generic model names, like Model1 should be avoided, and more descriptive model names should be preferred instead.
*Examples:*
    > ChallengeType:

    > ChallengeTypeTimelineTemplate

    * **type:** This should contain the type of the model schema being defined. As discussed in the 'definitions' section above, the data type of a model should not necessarily be of 'object' type, it can be of any supported Swagger datatype, such as string, number, array, boolean, integer and of course 'object'.
    
    For additional reference of datatypes, refer: https://swagger.io/docs/specification/data-models/data-types/
    *Examples:*
      > type: object

      > type: string

    * **<schema_selector_keyword>:** In case two or more models need to be combined in some manner. Alternatively, the following selectors can also be used to validate a particular value against multiple criteria. We need to define the manner in which the combination needs to be done. OpenAI provides several keywords, which can be used to create these combinations. This should be one of the following: 
    *oneOf* – validates the value against exactly one of the subschemas
*allOf* – validates the value against all the subschemas
*anyOf* – validates the value against any (one or more) of the subschemas<br/>
    *Examples:*
        > allOf:

        > anyOf:
      * **\- type:**  This should contain the type of the sub-schema being defined. The potential values that can be entered here are entirely identical to those mentioned in the 'type' section mentioned a level above. To reiterate, the possible values are: string, number, integer, object, array.
      *Examples:*
        > type: object

        > type: number
       *  **properties:** The value should be empty. This is to indicate that the following object value will encapsulate the list of properties of the current model being defined. Here each property will be represented as as object, with properties as described below. 
          * **<property_name>** The value should be empty. The property should be named based on the internal implementation of the API. The name of the property should be selected as required, and in general should be succinct.
          *Example:*
            > id:
            * **type:** This should contain the type of the model schema being defined. As discussed in the 'definitions' section above, the data type of a model should not necessarily be of 'object' type, it can be of any supported Swagger datatype, such as string, number, array, boolean, integer and of course 'object'.<br>
            *Examples:*
                > type: string

                > type: number
            * **description:** This should contain an informative yet concise description of the property name. The point is that the reader should be able to get an idea of what the use of this particular property of the Model is going to be. In case the property name is not extremely obvious (such as 'id' or 'name'), consider adding an elaborate enough information that ensures that the reader understands the context and the intention of the property.
            *Example:*
                > _"description: The challenge type ID. A challenge ID is a unique identifier that is automatically generated and assigned to each challenge by Topcoder's internal systems. <br> A challenge ID is usually 8 characters long and is numeric, mostly starting with 30. An example Challenge ID: 30129443. The specific challenge web page can be accessed via HTTP by appending the challenge ID after the string 'https://www.topcoder.com/challenges/'. Hence for the provided example, the resultant link would be https://www.topcoder.com/challenges/30129443.<br>The challenge ID is used by the challenge API to refer the challenge for a majority intents and purposes."_ <br>
                Note - This kind of terse descriptions should be used only if the term (challenge type ID in this case) has already been discussed in the document. Otherwise, use a more detailed description.
            * **format:** This should contain the string format of the property. For further details, refer to the String Formats section here: https://swagger.io/docs/specification/data-models/data-types/. A string can have any one of the many possible string formats, such as 'EMAIL', 'UUID', 'URI' etc. This ensure that the correct validation is ensured whenever the model is referenced. 

              
              *Examples:*
                > format: UUID

                > format: URI


        * **- $ref:** This should contain references to other definitions of models. The keyword \$ref imports an existing model to the location from where it is invoked. In this particular context, when the \$ref keyword is used in the Model definition, the model being referenced will be imported into this Model and will be available for use, and extensions. It works somewhat similar to how inheritance works in Object Oriented Programming.
        <br>Though care should be taken that complex cyclical references are not created. 
        For more information on \$ref, including additional syntax details, refer to the documentation here: https://swagger.io/docs/specification/using-ref/ (Note - The documentation is listed under Swagger version 3.0, but are largely applicable to version 2.0)
      *Example:*
             > \- $ref: '#/definitions/ChallengeTypeData'

        * **required:** The value should be left empty. Only the sub-properties below need to be modified/defined. The subsequent sub-properties should contain the list of properties are essential for the model.<br>
      **- <required_property_name>** - This should contain the name of the mandatory property. Multiple mandatory properties can be listed in order under the the 'required' property. The list of properties mentioned here should be a subset of the list of the properties defined under the 'properties' section, which need to be entered mandatorily for reference of the Model.
      *Example:*
            > \- id
            > \- name
        

