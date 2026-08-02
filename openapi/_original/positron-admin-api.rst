::

  openapi: 3.1.0
  info:
    title: Olivaw Admin API
    description: API for olivaw administative layer
    version: '1.0'
  security:
  - bearer:
    - API key
  paths:
    "/models":
      get:
        summary: Gets a list of all models.
        description: |
          Lists the currently available models, providing basic information about each model.
        tags: [models]
        operationId: listModels
        responses:
          '200':
            description: returns a list of all models.
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Models'
    "/models/{model}":
      get:
        summary: Gets a specific model by model id.
        description: |
          Retrieves a model instance, providing basic information about the model such as
          the creation time.
        tags: [models]
        operationId: getModel
        parameters:
          - name: model
            in: path
            description: The ID of the model to use for this request
            required: true
            schema:
              type: string
        responses:
          '200':
            description: returns a list of all models.
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Model'
          '404':
            description: The model was not found.
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'
      patch:
        summary: Updates a specific model by model id.
        description: Alters information about the model
        tags: [models]
        operationId: updateModel
        parameters:
          - name: model
            in: path
            description: The ID of the model to use for this request
            required: true
            schema:
              type: string
        requestBody:
          required: true
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Model'
        responses:
          '200':
            description: successful update
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Model'
          '400':
            description: invalid information provided to update
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'
          '404':
            description: The model was not found.
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'
      delete:
        summary: Deletes a specific model by model id.
        description: Removes a model from the list of available models
        tags: [models]
        operationId: deleteModel
        parameters:
          - name: model
            in: path
            description: The ID of the model to use for this request
            required: true
            schema:
              type: string
        responses:
          '200':
            description: successful deletion
          '404':
            description: The model was not found.
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'
    "/models/new":
      post:
        summary: Populate information about a model
        description: |
          Creates a model entry
        tags: [models]
        operationId: createModel
        requestBody:
          required: true
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Model'
        responses:
          '201':
            description: successful
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Model'
          '400':
            description: invalid information provided to server
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'
    "/serviceNodes":
      get:
        summary: Gets a list of all service nodes.
        description: |
          Lists the currently available service nodes, providing basic information about each node.
        tags: [service_nodes]
        operationId: listServiceNodes
        responses:
          '200':
            description: returns a list of all service nodes.
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/ServiceNodes'
    "/serviceNodes/{node}":
      get:
        summary: Gets a specific service node by node id.
        description: |
          Retrieves a service node instance, providing basic information about the node.
        tags: [service_nodes]
        operationId: getServiceNode
        parameters:
          - name: node
            in: path
            description: The ID of the node to use for this request
            required: true
            schema:
              type: string
        responses:
          '200':
            description: successful retrieval of service node information
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/ServiceNode'
          '404':
            description: The service node was not found.
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'
      patch:
        summary: Updates a specific service node by service node id.
        description: Alters information about the service node
        tags: [service_nodes]
        operationId: updateServiceNode
        parameters:
          - name: node
            in: path
            description: The ID of the service node to use for this request
            required: true
            schema:
              type: string
        requestBody:
          required: true
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ServiceNode'
        responses:
          '200':
            description: successful update
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/ServiceNode'
          '400':
            description: invalid information provided to update
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'
          '404':
            description: The model was not found.
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'
      delete:
        summary: Deletes a service node by node id.
        description: |
          Removes a service node from the list of available service nodes.
          If the service node is currently servicing requests, those requests
          will be drained before halting service, unless `halt=true` is provided
          in the query.
        tags: [models]
        operationId: deleteServiceNode
        parameters:
          - name: node
            in: path
            description: The ID of the node to use for this request
            required: true
            schema:
              type: string
          - name: halt
            in: query
            description: |
              forces the deletion operation to halt requests being serviced
              by these service nodes.
        responses:
          '200':
            description: successful deletion
          '404':
            description: The service node was not found.
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'
    "/serviceNodes/new":
      post:
        summary: Populate information about a service node
        description: |
          Creates a service node entry
        tags: [models]
        operationId: createServiceNode
        requestBody:
          required: true
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ServiceNode'
        responses:
          '201':
            description: successful
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/ServiceNode'
          '400':
            description: invalid information provided to server
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'

    "/users":
      get:
        summary: Gets a list of all users.
        description: |
          Lists the currently available users, providing basic information about each user.
        tags: [users]
        operationId: listUsers
        responses:
          '200':
            description: returns a list of all users.
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Users'
    "/users/{user}":
      get:
        summary: Gets a information about a single user.
        description: |
          Shows the selected users, providing basic information about each user.
        tags: [users]
        parameters:
          - name: user
            in: path
            description: The ID of the user to use for this request
            required: true
            schema:
              type: string
        operationId: getUser
        responses:
          '200':
            description: returns information about of a single user.
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/User'
          '404':
            description: The user was not found.
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'
      patch:
        summary: Updates a specific user by user id.
        description: Alters information about the user
        tags: [users]
        operationId: updateUser
        parameters:
          - name: user
            in: path
            description: The ID of the user to update
            required: true
            schema:
              type: string
        requestBody:
          required: true
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
        responses:
          '200':
            description: successful update
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/User'
          '400':
            description: invalid information provided to update
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'
          '404':
            description: The user was not found.
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'
      delete:
        summary: Deletes a specific user by user id.
        description: Removes a user from the list of available users
        tags: [users]
        operationId: deleteUser
        parameters:
          - name: user
            in: path
            description: The ID of the user to use for this request
            required: true
            schema:
              type: string
        responses:
          '200':
            description: successful deletion
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/User'
          '404':
            description: The user was not found.
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'
    "/users/new":
      post:
        summary: Create a new user
        description: |
          Creates a user entry
        tags: [users]
        operationId: createUser
        requestBody:
          required: true
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
        responses:
          '201':
            description: successful
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/User'
          '400':
            description: invalid information provided to server
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'
    "/accessTokens":
      get:
        summary: Gets a list of all access tokens.
        description: |
          Lists the currently available access tokens, providing basic information about each user.
        tags: [access_tokens]
        operationId: listAccessTokens
        parameters:
          - name: user
            in: query
            description: The ID of the user to filter access tokens
            required: true
            schema:
              type: string
        responses:
          '200':
            description: returns a list of all users.
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/AccessTokens'
    "/accessTokens/{token}":
      get:
        summary: Gets a information about a single access token.
        description: |
          Shows the selected access token, providing basic information about the token.
        tags: [access_tokens]
        parameters:
          - name: token
            in: path
            description: The ID of the token to request info about
            required: true
            schema:
              type: string
        operationId: getAccessToken
        responses:
          '200':
            description: Successful retrieval of the access token
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/AccessToken'
          '404':
            description: The access token was not found.
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'
      delete:
        summary: Deletes an access token by token id.
        description: |
          Removes an access token from the list of available tokens.  The
          access token will also be purged from the caches of all nodes
          in the cluster
        tags: [access_tokens]
        operationId: deleteAccessToken
        parameters:
          - name: token
            in: path
            description: The ID of the access token to delete
            required: true
            schema:
              type: string
        responses:
          '200':
            description: successful deletion
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/AccessToken'
          '404':
            description: The user was not found.
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'
    "/accessTokens/new":
      post:
        summary: Create a new access token
        description: |
          Creates a new access token.  This is not directly populated into the
          token cache until it has been used.  Note that the response contains
          fields which are not stored in the database in plaintext and cannot
          be retrieved at a future date.
        tags: [access_tokens]
        operationId: createAccessToken
        requestBody:
          required: true
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/CreateAccessToken'
        responses:
          '201':
            description: successful creation of an access token
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/AccessToken'
          '400':
            description: invalid information provided to server
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'
  components:
    schemas:
      Error:
        type: object
        properties:
          status:
            type: integer
            description: The HTTP status code associated with this error.
          error:
            type: string
            description: The error message.
      Models:
        type: array
        items:
          $ref: '#/components/schemas/Model'
      Model:
        type: object
        properties:
          id:
            type: string
            description: The model identifier, which can be referenced in the API endpoints.
          created:
            type: integer
            description: The Unix timestamp (in seconds) when the model was created.
          owned_by:
            type: string
            description: The organization that owns the model
      ServiceNodes:
        type: array
        items:
          $ref: '#/components/schemas/ServiceNode'
      ServiceNode:
        type: object
        properties:
          id:
            format: uuid
            type: string
          name:
            type: string
            description: human-readable name for the service node
          backend:
            enum:
              - OpenAINode
              - VllmNode
              - GiskardNode
          config:
            type: object
          models:
            # TODO: split into two, using JsonSchema inheritance techniques
            oneOf:
              - $ref: '#/components/schemas/Models'
              - $ref: '#/components/schemas/IdList'
      Users:
        type: array
        items:
          $ref: '#/components/schemas/User'
      User:
        type: object
        properties:
          id:
            type: string
            format: uuid
          name:
            type: string
            description: human-readable name for the service node
          email:
            type: string
          avatar:
            type: string
            format: url
          level:
            enum:
              - superuser
              - admin
              - user
      AccessTokens:
        type: array
        items:
          $ref: '#/components/schemas/AccessToken'
      AccessToken:
        type: object
        properties:
          id:
            type: string
            format: uuid
          name:
            type: string
          redacted:
            type: string
          expires_at:
            type: string
            format: date-time
          users:
            # TODO: split into two, using JsonSchema inheritance techniques
            oneOf:
              - $ref: '#/components/schemas/Users'
              - $ref: '#/components/schemas/IdList'
      IdList:
        type: array
        items:
          type: string
          format: uuid
