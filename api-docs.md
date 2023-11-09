---
description: >-
  If you're planning on consuming Arcee's API docs, here's a quickstart for
  using our APIs.
---

# API docs

Here is a summary of some key endpoints:

1. **Create Organization (`/v2/organizations`):**
   * POST method to create a new organization.
   * Requires a JSON request body that matches the `CreateOrganizationInput` schema.
   * Responses include a `200` for success and `422` for validation errors.
2. **Invite Member (`/v2/organizations/{org}/invite`):**
   * POST method to invite up to 10 new users to an organization.
   * Requires the organization slug in the path and `InviteMemberInput` in the request body.
   * Responses include a `200` for success and `422` for validation errors.
3. **List Tokens (`/v2/tokens`):**
   * GET method to list a user's API tokens.
   * The response will include a `200` status code for success.
4. **Create Token (`/v2/tokens`):**
   * POST method to create a new API token.
   * Requires a JSON request body with an expiry date using the `CreateTokenInput` schema.
   * Responses include a `201` for success and `422` for validation errors.
5. **Train Model (`/v2/models/train`):**
   * POST method to train a model with specific parameters defined by `TrainModelInput`.
   * Responses include a `200` for success and `422` for validation errors.
6. **Retrieve Model (`/v2/models/retrieve`):**
   * POST method to retrieve the output of a model using `RetrieveModelInput`.
   * Responses include a `200` for success and `422` for validation errors.
7. **Upload Context CSV (`/v2/contexts/{context_name}/csv`):**
   * POST method to upload a CSV to a context.
   * Requires the context name and CSV file in the form-data request body.
   * Responses include a `201` for successful upload, `202` for accepted but processing, and `422` for validation errors.
8. **Retriever Status (`/v2/retrievers/status/{context_name}`):**
   * GET method to get the status of the retriever for a given context.
   * Response includes a `200` for successful retrieval of status.
9. **Submit Feedback (`/v2/feedback`):**
   * POST method to submit feedback.
   * Requires `SubmitFeedbackInput` in the request body.
   * Responses include a `202` for successful acceptance of feedback and `422` for validation errors.
10. **Whoami (`/v2/whoami`):**
    * GET method that returns the current user and organization details.
    * Response includes a `200` for success and `422` for validation errors.

\


### Endpoint: `/v2/organizations`

#### POST

**Summary:** Create Organization

**Description:** Create a new organization

**Tags:** v2

**Request Body**

* `application/json`: Reference: #/components/schemas/CreateOrganizationInput

**Responses**

* `200`: Successful Response
* `application/json`: Reference: #/components/schemas/CreateOrganizationOutput

***

### Endpoint: `/v2/organizations/{org}/invite`

#### POST

**Summary:** Invite Member

**Description:** Invite up to 10 new users to an organization

**Tags:** v2, org\_admin

**Parameters**

* `org` (path): The organization slug to invite members to
  * Required: Yes
  * Type: string
* `x-arcee-org` (header): If provided, scope a request to an organization by slug
  * Required: No
  * Complex schema (Please refer to the schema definition)

**Request Body**

* `application/json`: Reference: #/components/schemas/InviteMemberInput

**Responses**

* `200`: Successful Response
* `application/json`: Complex schema (Please refer to the schema definition)

***

### Endpoint: `/v2/tokens`

#### GET

**Summary:** List Tokens

**Description:** List a user's api tokens

**Tags:** v2

**Responses**

* `200`: Successful Response
* `application/json`: Reference: #/components/schemas/ListTokensOutput

#### POST

**Summary:** Create Token

**Description:** Create a new API token. An expiry date must be given in "YYYY-MM-DD" format.

**Tags:** v2

**Request Body**

* `application/json`: Reference: #/components/schemas/CreateTokenInput

**Responses**

* `201`: Successful Response
* `application/json`: Reference: #/components/schemas/CreateTokenOutput

***

### Endpoint: `/v2/tokens/{id}`

#### DELETE

**Summary:** Delete Token

**Description:** Delete a token by id

**Tags:** v2

**Parameters**

* `id` (path):
  * Required: Yes
  * Complex schema (Please refer to the schema definition)

**Responses**

* `200`: Successful Response
* `application/json`: Complex schema (Please refer to the schema definition)

***

### Endpoint: `/v2/models/train`

#### POST

**Summary:** Train Model

**Tags:** v2

**Parameters**

* `x-arcee-org` (header): If provided, scope a request to an organization by slug
  * Required: No
  * Complex schema (Please refer to the schema definition)

**Request Body**

* `application/json`: Reference: #/components/schemas/TrainModelInput

**Responses**

* `200`: Successful Response
* `application/json`: Reference: #/components/schemas/TrainModelOutput

***

### Endpoint: `/v2/models/status/{id_or_name}`

#### GET

**Summary:** Training Status

**Tags:** v2

**Parameters**

* `id_or_name` (path):
  * Required: Yes
  * Type: string
* `allow_demo` (query):
  * Required: No
  * Complex schema (Please refer to the schema definition)
* `x-arcee-org` (header): If provided, scope a request to an organization by slug
  * Required: No
  * Complex schema (Please refer to the schema definition)

**Responses**

* `200`: Successful Response
* `application/json`: Reference: #/components/schemas/TrainModelStatus

***

### Endpoint: `/v2/models/generate`

#### POST

**Summary:** Generate Model

**Tags:** v2

**Parameters**

* `x-arcee-org` (header): If provided, scope a request to an organization by slug
  * Required: No
  * Complex schema (Please refer to the schema definition)

**Request Body**

* `application/json`: Reference: #/components/schemas/GenerateModelInput

**Responses**

* `200`: Successful Response
* `application/json`: Reference: #/components/schemas/GenerateModelOutput

***

### Endpoint: `/v2/models/retrieve`

#### POST

**Summary:** Retrieve Model

**Tags:** v2

**Parameters**

* `x-arcee-org` (header): If provided, scope a request to an organization by slug
  * Required: No
  * Complex schema (Please refer to the schema definition)

**Request Body**

* `application/json`: Reference: #/components/schemas/RetrieveModelInput

**Responses**

* `200`: Successful Response
* `application/json`: Reference: #/components/schemas/RetrieveModelOutput

***

### Endpoint: `/v2/contexts`

#### POST

**Summary:** Upload Context

**Tags:** v2

**Parameters**

* `x-arcee-org` (header): If provided, scope a request to an organization by slug
  * Required: No
  * Complex schema (Please refer to the schema definition)

**Request Body**

* `application/json`: Reference: #/components/schemas/UploadContextInput

**Responses**

* `200`: Successful Response
* `application/json`: Reference: #/components/schemas/UploadContextOutput

***

### Endpoint: `/v2/contexts/{context_name}/csv`

#### POST

**Summary:** Upload Context Csv

**Tags:** v2

**Parameters**

* `context_name` (path):
  * Required: Yes
  * Type: string
* `x-arcee-org` (header): If provided, scope a request to an organization by slug
  * Required: No
  * Complex schema (Please refer to the schema definition)

**Request Body**

* `multipart/form-data`: Reference: #/components/schemas/Body\_upload\_context\_csv\_v2\_contexts\_\_context\_name\_\_csv\_post

**Responses**

* `201`: Successful Response
* `application/json`: Reference: #/components/schemas/UploadContextOutput

***

### Endpoint: `/v2/retrievers/train`

#### POST

**Summary:** Train Retriever

**Tags:** v2

**Parameters**

* `x-arcee-org` (header): If provided, scope a request to an organization by slug
  * Required: No
  * Complex schema (Please refer to the schema definition)

**Request Body**

* `application/json`: Reference: #/components/schemas/TrainRetrieverInput

**Responses**

* `200`: Successful Response
* `application/json`: Complex schema (Please refer to the schema definition)

***

### Endpoint: `/v2/retrievers/retrain`

#### POST

**Summary:** Retrain Retriever

**Tags:** v2

**Parameters**

* `data` (query):
  * Required: Yes
  * Complex schema (Please refer to the schema definition)
* `x-arcee-org` (header): If provided, scope a request to an organization by slug
  * Required: No
  * Complex schema (Please refer to the schema definition)

**Responses**

* `200`: Successful Response
* `application/json`: Complex schema (Please refer to the schema definition)

***

### Endpoint: `/v2/retrievers/status/{context_name}`

#### GET

**Summary:** Retriever Status

**Tags:** v2

**Parameters**

* `context_name` (path):
  * Required: Yes
  * Type: string
* `x-arcee-org` (header): If provided, scope a request to an organization by slug
  * Required: No
  * Complex schema (Please refer to the schema definition)

**Responses**

* `200`: Successful Response
* `application/json`: Reference: #/components/schemas/RetrieverStatus

***

### Endpoint: `/v2/feedback`

#### POST

**Summary:** Submit Feedback

**Tags:** v2

**Parameters**

* `x-arcee-org` (header): If provided, scope a request to an organization by slug
  * Required: No
  * Complex schema (Please refer to the schema definition)

**Request Body**

* `application/json`: Reference: #/components/schemas/SubmitFeedbackInput

**Responses**

* `202`: Successful Response
* `application/json`: Reference: #/components/schemas/SubmitFeedbackOutput

***

### Endpoint: `/v2/whoami`

#### GET

**Summary:** Whoami

**Description:** Get current user and org detail

**Tags:** v2

**Parameters**

* `x-arcee-org` (header): If provided, scope a request to an organization by slug
  * Required: No
  * Complex schema (Please refer to the schema definition)

**Responses**

* `200`: Successful Response
* `application/json`: Reference: #/components/schemas/WhoamiOutput

***
