- What is the difference between Normal API and REST API?

A **Normal API** (Application Programming Interface) is a general term for any interface that allows communication between different software applications. It can follow any protocol or architecture, such as SOAP, RPC, or custom protocols.

A **REST API** (Representational State Transfer API) is a specific type of API that adheres to the principles of REST architecture. REST APIs typically use HTTP methods (GET, POST, PUT, DELETE) and are designed to be stateless, scalable, and cacheable. REST APIs often return data in formats like JSON or XML.

### Key Differences:

1. **Architecture**:

   - Normal API: Can follow any architecture (e.g., SOAP, RPC).
   - REST API: Must follow REST principles.

2. **Protocol**:

   - Normal API: May use various protocols (e.g., HTTP, SMTP).
   - REST API: Primarily uses HTTP.

3. **Data Format**:

   - Normal API: Can use any data format.
   - REST API: Commonly uses JSON or XML.

4. **Statelessness**:

   - Normal API: May or may not be stateless.
   - REST API: Always stateless (no client context is stored on the server).

5. **Caching**:
   - Normal API: Caching depends on the implementation.
   - REST API: Designed to support caching for better performance.

---

- What are REST API best practices?

### REST API Best Practices:

1. **Use Proper HTTP Methods**

   - **GET**: Retrieve data.
   - **POST**: Create new resources.
   - **PUT**: Update existing resources.
   - **DELETE**: Remove resources.

2. **Use Meaningful Resource Names**

   - Use nouns instead of verbs for endpoints.
   - Example: `/users` instead of `/getUsers`.

3. **Statelessness**

   - Ensure the server does not store client context between requests. Each request should contain all necessary information.

4. **Use HTTP Status Codes**

   - Use standard status codes to indicate the result of operations:
     - `200 OK`: Success.
     - `201 Created`: Resource created.
     - `400 Bad Request`: Invalid input.
     - `404 Not Found`: Resource not found.
     - `500 Internal Server Error`: Server error.

5. **Version Your API**

   - Include versioning in the URL or headers.
   - Example: `/api/v1/users`.

6. **Support Filtering, Sorting, and Pagination**

   - Allow clients to filter, sort, and paginate data.
   - Example: `/users?sort=age&limit=10&page=2`.

7. **Use JSON for Data Format**

   - JSON is widely used due to its simplicity and compatibility.

8. **Secure Your API**

   - Use HTTPS to encrypt communication.
   - Implement authentication (e.g., OAuth, API keys).

9. **Provide Proper Documentation**

   - Use tools like Swagger or Postman to document your API.

10. **Handle Errors Gracefully**

- Return meaningful error messages with details about what went wrong.
