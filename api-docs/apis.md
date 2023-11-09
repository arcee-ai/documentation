# 🔗 APIs

## API Endpoint Schemas

### POST /v2/organizations

**Summary:** Create Organization

**Description:** Create a new organization

#### Request Body

* `application/json`:

```json
{
  "properties": {
    "name": {
      "type": "string",
      "title": "Name"
    },
    "type": {
      "anyOf": [
        {
          "type": "string"
        },
        {
          "type": "null"
        }
      ],
      "title": "Type"
    }
  },
  "type": "object",
  "required": [
    "name"
  ],
  "title": "CreateOrganizationInput"
}
```

#### Responses

* `200`:
  * `application/json`:

```json
{
  "properties": {
    "organization": {
      "$ref": "#/components/schemas/Organization"
    }
  },
  "type": "object",
  "required": [
    "organization"
  ],
  "title": "CreateOrganizationOutput"
}
```

* `422`:
  * `application/json`:

```json
{
  "properties": {
    "detail": {
      "items": {
        "$ref": "#/components/schemas/ValidationError"
      },
      "type": "array",
      "title": "Detail"
    }
  },
  "type": "object",
  "title": "HTTPValidationError"
}
```

### POST /v2/organizations/{org}/invite

**Summary:** Invite Member

**Description:** Invite up to 10 new users to an organization

#### Request Body

* `application/json`:

```json
{
  "properties": {
    "invitees": {
      "items": {
        "$ref": "#/components/schemas/Invitee"
      },
      "type": "array",
      "title": "Invitees"
    }
  },
  "type": "object",
  "required": [
    "invitees"
  ],
  "title": "InviteMemberInput"
}
```

#### Responses

* `200`:
* `422`:
  * `application/json`:

```json
{
  "properties": {
    "detail": {
      "items": {
        "$ref": "#/components/schemas/ValidationError"
      },
      "type": "array",
      "title": "Detail"
    }
  },
  "type": "object",
  "title": "HTTPValidationError"
}
```

### GET /v2/tokens

**Summary:** List Tokens

**Description:** List a user's api tokens

#### Responses

* `200`:
  * `application/json`:

```json
{
  "properties": {
    "tokens": {
      "items": {
        "$ref": "#/components/schemas/ApiToken"
      },
      "type": "array",
      "title": "Tokens"
    }
  },
  "type": "object",
  "required": [
    "tokens"
  ],
  "title": "ListTokensOutput"
}
```

### POST /v2/tokens

**Summary:** Create Token

**Description:** Create a new API token. An expiry date must be given in "YYYY-MM-DD" format.

#### Request Body

* `application/json`:

```json
{
  "properties": {
    "expiry": {
      "type": "string",
      "format": "date",
      "title": "Expiry"
    }
  },
  "type": "object",
  "required": [
    "expiry"
  ],
  "title": "CreateTokenInput"
}
```

#### Responses

* `201`:
  * `application/json`:

```json
{
  "properties": {
    "token": {
      "anyOf": [
        {
          "type": "string"
        },
        {
          "type": "string",
          "format": "uuid4"
        }
      ],
      "title": "Token"
    }
  },
  "type": "object",
  "required": [
    "token"
  ],
  "title": "CreateTokenOutput"
}
```

* `422`:
  * `application/json`:

```json
{
  "properties": {
    "detail": {
      "items": {
        "$ref": "#/components/schemas/ValidationError"
      },
      "type": "array",
      "title": "Detail"
    }
  },
  "type": "object",
  "title": "HTTPValidationError"
}
```

### DELETE /v2/tokens/{id}

**Summary:** Delete Token

**Description:** Delete a token by id

#### Responses

* `200`:
* `422`:
  * `application/json`:

```json
{
  "properties": {
    "detail": {
      "items": {
        "$ref": "#/components/schemas/ValidationError"
      },
      "type": "array",
      "title": "Detail"
    }
  },
  "type": "object",
  "title": "HTTPValidationError"
}
```

### POST /v2/models/train

**Summary:** Train Model

**Description:** None

#### Request Body

* `application/json`:

```json
{
  "properties": {
    "id": {
      "anyOf": [
        {
          "type": "string"
        },
        {
          "type": "string",
          "format": "uuid4"
        },
        {
          "type": "null"
        }
      ],
      "title": "Id"
    },
    "name": {
      "anyOf": [
        {
          "type": "string"
        },
        {
          "type": "null"
        }
      ],
      "title": "Name"
    },
    "context": {
      "anyOf": [
        {
          "type": "string"
        },
        {
          "type": "null"
        }
      ],
      "title": "Context"
    },
    "generator": {
      "anyOf": [
        {
          "type": "string"
        },
        {
          "type": "null"
        }
      ],
      "title": "Generator"
    }
  },
  "type": "object",
  "title": "TrainModelInput"
}
```

#### Responses

* `200`:
  * `application/json`:

```json
{
  "properties": {
    "id": {
      "anyOf": [
        {
          "type": "string"
        },
        {
          "type": "string",
          "format": "uuid4"
        }
      ],
      "title": "Id"
    },
    "message": {
      "type": "string",
      "title": "Message"
    }
  },
  "type": "object",
  "required": [
    "id",
    "message"
  ],
  "title": "TrainModelOutput"
}
```

* `422`:
  * `application/json`:

```json
{
  "properties": {
    "detail": {
      "items": {
        "$ref": "#/components/schemas/ValidationError"
      },
      "type": "array",
      "title": "Detail"
    }
  },
  "type": "object",
  "title": "HTTPValidationError"
}
```

### GET /v2/models/status/{id\_or\_name}

**Summary:** Training Status

**Description:** None

#### Responses

* `200`:
  * `application/json`:

```json
{
  "properties": {
    "id": {
      "type": "string",
      "title": "Id"
    },
    "model_id": {
      "type": "string",
      "title": "Model Id"
    },
    "status": {
      "type": "string",
      "title": "Status"
    }
  },
  "type": "object",
  "required": [
    "id",
    "model_id",
    "status"
  ],
  "title": "TrainModelStatus"
}
```

* `422`:
  * `application/json`:

```json
{
  "properties": {
    "detail": {
      "items": {
        "$ref": "#/components/schemas/ValidationError"
      },
      "type": "array",
      "title": "Detail"
    }
  },
  "type": "object",
  "title": "HTTPValidationError"
}
```

### POST /v2/models/generate

**Summary:** Generate Model

**Description:** None

#### Request Body

* `application/json`:

```json
{
  "properties": {
    "query": {
      "type": "string",
      "title": "Query"
    },
    "size": {
      "anyOf": [
        {
          "type": "integer"
        },
        {
          "type": "null"
        }
      ],
      "title": "Size",
      "default": 5
    },
    "filters": {
      "anyOf": [
        {
          "items": {
            "$ref": "#/components/schemas/QueryFilter"
          },
          "type": "array"
        },
        {
          "type": "null"
        }
      ],
      "title": "Filters"
    },
    "id": {
      "anyOf": [
        {
          "type": "string"
        },
        {
          "type": "string",
          "format": "uuid4"
        }
      ],
      "title": "Id"
    }
  },
  "type": "object",
  "required": [
    "query",
    "id"
  ],
  "title": "GenerateModelInput"
}
```

#### Responses

* `200`:
  * `application/json`:

```json
{
  "properties": {
    "text": {
      "type": "string",
      "title": "Text"
    },
    "context": {
      "items": {
        "type": "string"
      },
      "type": "array",
      "title": "Context"
    }
  },
  "type": "object",
  "required": [
    "text",
    "context"
  ],
  "title": "GenerateModelOutput"
}
```

* `422`:
  * `application/json`:

```json
{
  "properties": {
    "detail": {
      "items": {
        "$ref": "#/components/schemas/ValidationError"
      },
      "type": "array",
      "title": "Detail"
    }
  },
  "type": "object",
  "title": "HTTPValidationError"
}
```

### POST /v2/models/retrieve

**Summary:** Retrieve Model

**Description:** None

#### Request Body

* `application/json`:

```json
{
  "properties": {
    "query": {
      "type": "string",
      "title": "Query"
    },
    "size": {
      "anyOf": [
        {
          "type": "integer"
        },
        {
          "type": "null"
        }
      ],
      "title": "Size",
      "default": 5
    },
    "filters": {
      "anyOf": [
        {
          "items": {
            "$ref": "#/components/schemas/QueryFilter"
          },
          "type": "array"
        },
        {
          "type": "null"
        }
      ],
      "title": "Filters"
    },
    "id": {
      "anyOf": [
        {
          "type": "string"
        },
        {
          "type": "string",
          "format": "uuid4"
        }
      ],
      "title": "Id"
    }
  },
  "type": "object",
  "required": [
    "query",
    "id"
  ],
  "title": "RetrieveModelInput"
}
```

#### Responses

* `200`:
  * `application/json`:

```json
{
  "properties": {
    "results": {
      "items": {
        "$ref": "#/components/schemas/RetrieveModelResult"
      },
      "type": "array",
      "title": "Results"
    }
  },
  "type": "object",
  "required": [
    "results"
  ],
  "title": "RetrieveModelOutput"
}
```

* `422`:
  * `application/json`:

```json
{
  "properties": {
    "detail": {
      "items": {
        "$ref": "#/components/schemas/ValidationError"
      },
      "type": "array",
      "title": "Detail"
    }
  },
  "type": "object",
  "title": "HTTPValidationError"
}
```

### POST /v2/contexts

**Summary:** Upload Context

**Description:** None

#### Request Body

* `application/json`:

```json
{
  "properties": {
    "context_name": {
      "type": "string",
      "title": "Context Name"
    },
    "documents": {
      "items": {
        "$ref": "#/components/schemas/UploadContextDocument"
      },
      "type": "array",
      "title": "Documents"
    }
  },
  "type": "object",
  "required": [
    "context_name",
    "documents"
  ],
  "title": "UploadContextInput"
}
```

#### Responses

* `200`:
  * `application/json`:

```json
{
  "properties": {
    "message": {
      "type": "string",
      "title": "Message",
      "default": "Processing context..."
    },
    "context_name": {
      "type": "string",
      "title": "Context Name"
    },
    "context_id": {
      "type": "string",
      "title": "Context Id"
    }
  },
  "type": "object",
  "required": [
    "context_name",
    "context_id"
  ],
  "title": "UploadContextOutput"
}
```

* `422`:
  * `application/json`:

```json
{
  "properties": {
    "detail": {
      "items": {
        "$ref": "#/components/schemas/ValidationError"
      },
      "type": "array",
      "title": "Detail"
    }
  },
  "type": "object",
  "title": "HTTPValidationError"
}
```

### POST /v2/contexts/{context\_name}/csv

**Summary:** Upload Context Csv

**Description:** None

#### Request Body

* `multipart/form-data`:

```json
{
  "properties": {
    "file": {
      "type": "string",
      "format": "binary",
      "title": "File",
      "description": "A CSV file containing ['doc', 'title'] or ['answer', 'doc', 'question', 'title'] columns, including a header. Extra columns are allowed."
    }
  },
  "type": "object",
  "required": [
    "file"
  ],
  "title": "Body_upload_context_csv_v2_contexts__context_name__csv_post"
}
```

#### Responses

* `201`:
  * `application/json`:

```json
{
  "properties": {
    "message": {
      "type": "string",
      "title": "Message",
      "default": "Processing context..."
    },
    "context_name": {
      "type": "string",
      "title": "Context Name"
    },
    "context_id": {
      "type": "string",
      "title": "Context Id"
    }
  },
  "type": "object",
  "required": [
    "context_name",
    "context_id"
  ],
  "title": "UploadContextOutput"
}
```

* `202`:
  * `application/json`:

```json
{
  "properties": {
    "message": {
      "type": "string",
      "title": "Message",
      "default": "Processing context..."
    },
    "context_name": {
      "type": "string",
      "title": "Context Name"
    },
    "context_id": {
      "type": "string",
      "title": "Context Id"
    }
  },
  "type": "object",
  "required": [
    "context_name",
    "context_id"
  ],
  "title": "UploadContextOutput"
}
```

* `422`:
  * `application/json`:

```json
{
  "properties": {
    "detail": {
      "items": {
        "$ref": "#/components/schemas/ValidationError"
      },
      "type": "array",
      "title": "Detail"
    }
  },
  "type": "object",
  "title": "HTTPValidationError"
}
```

### POST /v2/retrievers/train

**Summary:** Train Retriever

**Description:** None

#### Request Body

* `application/json`:

```json
{
  "properties": {
    "context_name": {
      "type": "string",
      "title": "Context Name"
    }
  },
  "type": "object",
  "required": [
    "context_name"
  ],
  "title": "TrainRetrieverInput"
}
```

#### Responses

* `200`:
* `422`:
  * `application/json`:

```json
{
  "properties": {
    "detail": {
      "items": {
        "$ref": "#/components/schemas/ValidationError"
      },
      "type": "array",
      "title": "Detail"
    }
  },
  "type": "object",
  "title": "HTTPValidationError"
}
```

### POST /v2/retrievers/retrain

**Summary:** Retrain Retriever

**Description:** None

#### Responses

* `200`:
* `422`:
  * `application/json`:

```json
{
  "properties": {
    "detail": {
      "items": {
        "$ref": "#/components/schemas/ValidationError"
      },
      "type": "array",
      "title": "Detail"
    }
  },
  "type": "object",
  "title": "HTTPValidationError"
}
```

### GET /v2/retrievers/status/{context\_name}

**Summary:** Retriever Status

**Description:** None

#### Responses

* `200`:
  * `application/json`:

```json
{
  "properties": {
    "context_name": {
      "type": "string",
      "title": "Context Name"
    },
    "status": {
      "type": "string",
      "title": "Status"
    },
    "context_id": {
      "type": "string",
      "title": "Context Id"
    }
  },
  "type": "object",
  "required": [
    "context_name",
    "status",
    "context_id"
  ],
  "title": "RetrieverStatus"
}
```

* `422`:
  * `application/json`:

```json
{
  "properties": {
    "detail": {
      "items": {
        "$ref": "#/components/schemas/ValidationError"
      },
      "type": "array",
      "title": "Detail"
    }
  },
  "type": "object",
  "title": "HTTPValidationError"
}
```

### POST /v2/feedback

**Summary:** Submit Feedback

**Description:** None

#### Request Body

* `application/json`:

```json
{
  "properties": {
    "message": {
      "type": "string",
      "title": "Message"
    },
    "location": {
      "anyOf": [
        {
          "type": "string"
        },
        {
          "type": "null"
        }
      ],
      "title": "Location"
    }
  },
  "type": "object",
  "required": [
    "message"
  ],
  "title": "SubmitFeedbackInput"
}
```

#### Responses

* `202`:
  * `application/json`:

```json
{
  "properties": {
    "message": {
      "type": "string",
      "title": "Message"
    }
  },
  "type": "object",
  "required": [
    "message"
  ],
  "title": "SubmitFeedbackOutput"
}
```

* `422`:
  * `application/json`:

```json
{
  "properties": {
    "detail": {
      "items": {
        "$ref": "#/components/schemas/ValidationError"
      },
      "type": "array",
      "title": "Detail"
    }
  },
  "type": "object",
  "title": "HTTPValidationError"
}
```

### GET /v2/whoami

**Summary:** Whoami

**Description:** Get current user and org detail

#### Responses

* `200`:
  * `application/json`:

```json
{
  "properties": {
    "email": {
      "type": "string",
      "title": "Email"
    },
    "org": {
      "type": "string",
      "title": "Org"
    }
  },
  "type": "object",
  "required": [
    "email",
    "org"
  ],
  "title": "WhoamiOutput"
}
```

* `422`:
  * `application/json`:

```json
{
  "properties": {
    "detail": {
      "items": {
        "$ref": "#/components/schemas/ValidationError"
      },
      "type": "array",
      "title": "Detail"
    }
  },
  "type": "object",
  "title": "HTTPValidationError"
}
```
