swagger: '2.0'

# basic metadata about our API
info:
  title: PizzaToppings API
  version: 1.0.1

# the host to call to interact with this server
host: api.irresistibleapis.com

# the basepath, which is appended to the host
basePath: /v1

# the schemes (http | https) to call with
schemes:
  - http

# what default mediatype we consume for put, post methods
consumes:
  - application/json

# what media type we produce
produces:
  - application/json

paths:
  /pizzas:
    get:
      description: Retrieves a list of pizzas in the system
      parameters:
        - description: String to match in the pizza name
          in: query
          name: nameString
          required: false
          type: string
      responses:
        '200':
          description: Pizza list
          examples:
            application/json:
              - id: 1
                name: "Maui Wowie"
                toppings:
                  - 2
                  - 3
              - id: 2
                name: "Kirsten's Pizza"
                toppings:
                  - 1
    post:
      description: Adds a new pizza to the list
      parameters:
        - description: ID for the pizza (only one per user)
          in: body
          name: pizza
          required: true
          schema:
              type: object
              required:
                - id
                - name
              properties:
                id:
                    type: string
                name:
                    type: string
                toppings:
                    type: array
                    items:
                        type: integer
      responses:
        '201':
          description: Pizza created
          examples:
            application/json:
              - id: 1
                location: /pizzas/1.2.3.4
                name: Maui Wowie
                toppings:
                  - 2
                  - 3
        '409':
          description: Duplicate pizza name or ID found
          examples:
            application/json:
              - message: Duplicate pizza ID found
  /pizzas/{pizzaid}:
    get:
      description: Retrieves an individual pizza
      responses:
        '200':
          description: 'Pizza '
          examples:
            application/json:
              id: 1
              name: Maui Wowie
              toppings:
                - 2
                - 3
          schema:
            type: object
        '404':
          description: Pizza not found
          examples:
            application/json:
              message: No pizza with that ID found
            schema:
              type: string
    put:
      description: Pizza update
      parameters:
        - description: ID for the pizza (only one per user)
          in: body
          name: pizza
          required: true
          schema:
              type: object
              required:
                - id
                - name
              properties:
                id:
                    type: string
                name:
                    type: string
                toppings:
                    type: array
                    items:
                        type: integer
      responses:
        '204':
          description: Pizza updated
        '404':
          description: Pizza not found
          examples:
            application/json:
              message: No pizza with that ID found
            schema:
              type: string
    delete:
      description: Deletes an individual pizza
      responses:
        '204':
          description: Pizza deleted
        '404':
          description: Pizza not found
          examples:
            application/json:
              message: No pizza with that ID found
  /toppings/:
    get:
      description: Retrieves a list of toppings in the system
      parameters:
        - description: String to match in the topping name
          in: query
          name: nameString
          required: false
          type: string
      responses:
        '200':
          description: Pizza list
          examples:
            application/json:
              - id: 1
                name: "pepperoni"
              - id: 2
                name: "ham"
              - id: 3
                name: "pineapple"
    post:
      description: Adds a new topping to the list
      parameters:
        - description: ID for the topping (only one per user)
          in: body
          name: pizza
          required: true
          schema:
              type: object
              required:
                - name
              properties:
                name:
                    type: string
      responses:
        '201':
          description: Pizza created
          examples:
            application/json:
              - id: 1
                location: /pizzas/1.2.3.4
                name: Maui Wowie
                toppings:
                  - 2
                  - 3

        '409':
          description: Duplicate pizza name or ID found
          examples:
            application/json:
              - message: Duplicate pizza ID found
  /toppings/{toppingid}:
    get:
      description: Retrieves an individual pizza
      responses:
        '200':
          description: 'Pizza '
          examples:
            application/json:
              id: 1
              name: Maui Wowie
              toppings:
                - 2
                - 3
          schema:
            type: object
        '404':
          description: Pizza not found
          examples:
            application/json:
              message: No pizza with that ID found
            schema:
              type: string
    put:
      description: Updates an individual pizza
      responses:
        '204':
          description: Pizza updated
        '404':
          description: Pizza not found
          examples:
            application/json:
              message: No pizza with that ID found
            schema:
              type: string
    delete:
      description: Deletes an individual pizza
      responses:
        '204':
          description: Pizza deleted
        '404':
          description: Pizza not found
          examples:
            application/json:
              message: No pizza with that ID found
            schema:
              type: object