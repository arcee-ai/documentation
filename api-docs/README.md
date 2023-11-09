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

***
