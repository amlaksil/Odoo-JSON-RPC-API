# Odoo JSON-RPC API

### 1. Introduction to Odoo JSON-RPC API

Odoo's JSON-RPC API allows external applications to interact with Odoo databases remotely. It follows the JSON-RPC 2.0 specification and provides a range of services and methods for performing CRUD operations, executing actions, generating reports, and more.

### 2. Authentication and Session Management

Before making requests to the Odoo JSON-RPC API, you need to authenticate and establish a session. Authentication is typically done using the `authenticate()` method of the `common` service. This method takes the database name, username, and password as parameters and returns a session ID if authentication is successful.

Example:
```
{
  "jsonrpc": "2.0",
  "method": "call",
  "params": {
    "service": "common",
    "method": "authenticate",
    "args": ["database_name", "username", "password", {}]
  },
  "id": 1
}
```

### 3. Making Requests

Once authenticated, you can make requests to various services and methods provided by Odoo. The structure of a request includes the JSON-RPC version, method, parameters, and request ID.

Example Request:
```json
{
  "jsonrpc": "2.0",
  "method": "call",
  "params": {
    "service": "object",
    "method": "execute",
    "args": ["database_name", 1, "password", "model_name", "method_name", []]
  },
  "id": 2
}
```

### 4. Handling Responses

Responses from Odoo JSON-RPC API include a result field containing the response data or an error field containing error information if the request failed. It's important to handle responses appropriately based on the result or error.

Example Response (Success):
```json
{
  "jsonrpc": "2.0",
  "result": {
    "key": "value"
  },
  "id": 2
}
```

Example Response (Error):
```json
{
  "jsonrpc": "2.0",
  "error": {
    "code": 200,
    "message": "Error Message",
    "data": {}
  },
  "id": 2
}
```

### 5. Error Handling

Error handling in Odoo JSON-RPC API involves checking for error codes and messages in the response and handling them appropriately in your application logic. Common error codes include authentication errors, permission errors, and invalid parameters.

### 6. Available Services and Methods

Odoo JSON-RPC API provides several services and methods:

**Services:**

1. **Object Service (`object`):** This service deals with CRUD operations on Odoo models.

2. **Common Service (`common`):** Provides authentication and session management functionalities.

3. **Report Service (`report`):** Used for generating reports in various formats like PDF, Excel, etc.

4. **Workflow Service (`workflow`):** Handles workflow-related operations such as transitions, triggers, etc.

5. **Web Service (`web`):** Provides functionalities related to the Odoo web interface.

6. **Action Service (`action`):** Used for executing specific actions defined in Odoo.

7. **Wizard Service (`wizard`):** Deals with wizards, which are UI components used for data entry or task completion.

8. **Security Service (`security`):** Handles security-related operations such as access control, permissions, etc.

9. **Data Service (`data`):** Deals with data import/export operations.

10. **Utility Service (`utility`):** Provides various utility functions and helper methods.

**Methods:**

1. **Execute (`execute`):** Commonly used to execute CRUD operations on Odoo models.

2. **Search Read (`search_read`):** Used to search and read records from Odoo models based on specified criteria.

3. **Create (`create`):** Used to create new records in Odoo models.

4. **Write (`write`):** Used to update existing records in Odoo models.

5. **Unlink (`unlink`):** Used to delete records from Odoo models.

6. **Search (`search`):** Used to search for records in Odoo models based on specified criteria.

7. **Read (`read`):** Used to read specific fields of records from Odoo models.

8. **Name Get (`name_get`):** Used to fetch the human-readable name of records.

9. **Context Get (`context_get`):** Used to fetch the context for the current session.

10. **Action Execute (`action_execute`):** Used to execute actions defined in Odoo.

### 7. Best Practices

- Securely manage authentication credentials.
- Handle errors gracefully and provide meaningful error messages to users.
- Implement appropriate validation for input parameters.
- Use batch requests to optimize performance when making multiple calls.

### 8. Example Use Case:

Example of fetching Records from a Model

```
{
  "jsonrpc": "2.0",
  "method": "call",
  "params": {
    "service": "object",
    "method": "execute",
    "args": ["database_name", 1, "password", "model_name", "search_read", []]
  },
  "id": 3
}
```
Example of fetching records from the `hr.employee` model:

```
{
  "jsonrpc": "2.0",
  "method": "call",
  "params": {
    "service": "object",
    "method": "execute",
    "args": ["rd-demo", 2, "admin", "hr.employee", "search_read", [["company_id", "=", 3]], ["name", "job_title", "work_email", "work_phone", "mobile_phone"]]
  },
  "id": 456
}
```

Example of fetching product category from `product.template` model

```
{
  "jsonrpc": "2.0",
  "method": "call",
  "params": {
    "service": "object",
    "method": "execute",
    "args": ["rd-demo", 2, "admin", "product.template", "search_read", [["company_id", "=", 3]], ["categ_id"]]
  },
  "id": 1
}
```

Example of creating a record:

```
{
  "jsonrpc": "2.0",
  "method": "call",
  "params": {
    "service": "object",
    "method": "execute",
    "args": [
      "rd-demo",
      2,
      "admin",
      "product.template",
      "create",
      {
        "company_id": 3,
        "name": "Fire hydrant",
        "detailed_type": "product"
      }
    ]
  }

```

Example of updating a record:

```
{
  "jsonrpc": "2.0",
  "method": "call",
  "params": {
    "service": "object",
    "method": "execute",
    "args": [
      "rd-demo",
      2,
      "admin",
      "product.template",
      "write",
      [40],
      {"categ_id": 2}
    ]
  }
}
```

Example of deleting a record:

```
{
  "jsonrpc": "2.0",
  "method": "call",
  "params": {
    "service": "object",
    "method": "execute",
    "args": [
      "rd-demo",
      2,
      "admin",
      "product.template",
      "unlink",
      [46]
    ]
  }
}
```


### Conclusion

Odoo's JSON-RPC API provides a powerful way to integrate external applications with Odoo databases. By following best practices and understanding the available services and methods, you can efficiently build integrations and extend Odoo's functionality according to your business needs.
