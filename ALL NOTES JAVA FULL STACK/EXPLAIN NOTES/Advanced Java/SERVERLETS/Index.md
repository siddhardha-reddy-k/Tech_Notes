# Servlets — Learning Index

## Goal

Learn Servlets only to the level needed to:

- Understand Java web fundamentals
- Handle HTTP requests and responses
- Build a small Servlet + JDBC application
- Answer fresher interview questions
- Transition confidently into Spring MVC / Spring Boot
- Understand which older Servlet practices are only for awareness

Target flow:

```text
Browser
→ HTTP Request
→ Servlet Container
→ Servlet
→ Service
→ DAO
→ JDBC
→ Database
→ HTTP Response
→ Browser
```

---

# 1. Servlet Fundamentals

## 1.1 Web Application Basics
**Priority:** Good to Know

- Web application
- Static vs dynamic content
- Client-side vs server-side resources
- Deployment
- Web server vs Servlet container

## 1.2 What is a Servlet
**Priority:** Must Know

- What a Servlet is
- Why Servlets exist
- Server-side Java
- Servlet vs normal Java class
- Role of Servlet Container

## 1.3 Servlet Architecture
**Priority:** Must Know

- Browser / Client
- HTTP Request
- Tomcat / Servlet Container
- Servlet
- Service / DAO
- Database
- HTTP Response

## 1.4 HTTP Basics for Servlets
**Priority:** Must Know

- Request
- Response
- URL
- HTTP methods
- GET
- POST
- Headers
- Status codes
- HTTP is stateless

---

## Checkpoint 1

Be able to explain:

- What is a Servlet?
- Why do we need a Servlet Container?
- Web server vs Servlet container
- What happens when the browser sends a request?
- Where does a Servlet sit in the backend flow?
- Why is HTTP called stateless?

---

# 2. Servlet Setup and Mapping

## 2.1 `HttpServlet`
**Priority:** Must Know

- Extending `HttpServlet`
- Why `HttpServlet` is preferred for HTTP applications
- Container calls Servlet methods

## 2.2 `@WebServlet`
**Priority:** Must Know

- URL mapping
- Basic annotation configuration

## 2.3 URL Mapping Patterns
**Priority:** Good to Know

- Exact mapping

```text
/user
```

- Path / directory mapping

```text
/api/*
```

- Extension mapping

```text
*.do
```

Focus mainly on understanding how URLs are mapped to Servlets.

## 2.4 `web.xml`
**Priority:** Basic Awareness

- Deployment descriptor
- Old XML-based Servlet mapping
- Know what it is
- Do not study XML-heavy configuration deeply

---

## Checkpoint 2

Be able to:

- Create a basic `HttpServlet`
- Map it using `@WebServlet`
- Explain how a URL reaches the correct Servlet
- Recognize `web.xml` configuration

---

# 3. Handling HTTP Requests

## 3.1 `doGet()`
**Priority:** Must Know

- Handling GET requests
- Reading data
- Returning a response

## 3.2 `doPost()`
**Priority:** Must Know

- Handling POST requests
- Form submission
- Request body

## 3.3 GET vs POST
**Priority:** Must Know

Understand the practical difference:

- GET → generally retrieve/read data
- POST → generally submit/create/process data
- Query string vs request body
- Do not treat POST itself as encryption

## 3.4 HTML Form → Servlet
**Priority:** Must Know

- `action`
- `method`
- Input `name`
- Form submission flow

---

## Checkpoint 3

Be able to explain:

- When `doGet()` runs
- When `doPost()` runs
- GET vs POST
- How an HTML form reaches a Servlet
- Write a basic GET/POST Servlet from memory

---

# 4. Request and Response Objects

## 4.1 `HttpServletRequest`
**Priority:** Must Know

- Represents incoming request
- Request information
- Client data

## 4.2 Request Parameters
**Priority:** Must Know

- `getParameter()`
- Query parameters
- Form parameters

## 4.3 Request Headers
**Priority:** Must Know

- What headers are
- `getHeader()`
- Common HTTP headers

## 4.4 `HttpServletResponse`
**Priority:** Must Know

- Represents outgoing response
- Writing response data
- `getWriter()`

## 4.5 Content Type / MIME Type
**Priority:** Good to Know

Understand:

```java
response.setContentType("text/html");
```

Common examples:

```text
text/html
text/plain
application/json
```

Do not memorize old Word/Excel MIME examples deeply.

## 4.6 HTTP Status Codes
**Priority:** Must Know

Important codes:

- 200 OK
- 201 Created
- 302 Found / Redirect
- 400 Bad Request
- 401 Unauthorized
- 403 Forbidden
- 404 Not Found
- 500 Internal Server Error

---

## Checkpoint 4

Be able to explain:

- What `HttpServletRequest` contains
- What `HttpServletResponse` does
- How to read request parameters
- What headers are
- Why content type matters
- Why status codes matter

---

# 5. Navigation Between Resources

## 5.1 `RequestDispatcher`
**Priority:** Must Know

- What it does
- `forward()`
- `include()`

## 5.2 Forward
**Priority:** Must Know

- Server-side transfer
- Same request and response
- Browser usually does not know about the internal transfer

## 5.3 Include
**Priority:** Good to Know

- Includes output of another resource
- Understand concept only

## 5.4 Redirect
**Priority:** Must Know

- `sendRedirect()`
- Browser receives redirect
- Browser sends a new request
- URL changes

## 5.5 Forward vs Redirect
**Priority:** Must Know

Compare:

- Server-side vs client-side
- Same request vs new request
- URL behavior
- Request attributes/data
- Use cases

---

## Checkpoint 5

Be able to explain:

- Forward vs Redirect
- Why `RequestDispatcher` exists
- What `include()` does
- When a new HTTP request is created

---

# 6. State Management

## 6.1 Why Session Tracking Exists
**Priority:** Must Know

- HTTP is stateless
- Need to remember users across requests

## 6.2 Cookies
**Priority:** Must Know

- What a cookie is
- Create cookie
- Read cookie
- Client-side storage
- Common use cases

## 6.3 `HttpSession`
**Priority:** Must Know

- `getSession()`
- Session ID
- `setAttribute()`
- `getAttribute()`
- `removeAttribute()`
- `invalidate()`

## 6.4 Cookies vs Sessions
**Priority:** Must Know

- Client-side vs server-side state
- Session ID relationship
- Login/session example

## 6.5 Other Session Tracking Techniques
**Priority:** Basic Awareness

- URL rewriting
- Hidden form fields

---

## Checkpoint 6

Be able to explain:

- Why HTTP is stateless
- Why cookies exist
- Why sessions exist
- Cookies vs Sessions
- How login state can be maintained

---

# 7. Servlet Lifecycle and Container Management

## 7.1 Servlet Lifecycle
**Priority:** Must Know

Correct flow:

```text
Servlet object created
→ init()
→ service()
→ doGet() / doPost()
→ destroy()
```

Understand:

- `init()` → initialization
- `service()` → handles incoming requests
- `destroy()` → cleanup before removal

## 7.2 `service()`
**Priority:** Good to Know

- `HttpServlet.service()` dispatches requests to methods such as `doGet()` and `doPost()`
- Normally override `doGet()` / `doPost()`, not `service()`

## 7.3 `loadOnStartup`
**Priority:** Good to Know

- Normally Servlet may be created when first needed
- `loadOnStartup` allows initialization during application/server startup

## 7.4 Servlet Threading Concept
**Priority:** Good to Know

- Usually one Servlet instance handles multiple requests
- Requests may be handled by multiple threads
- Avoid unsafe shared mutable instance variables

---

## Checkpoint 7

Be able to explain:

- Who creates the Servlet object
- Servlet lifecycle
- `service()` vs `doGet()` / `doPost()`
- What `loadOnStartup` means
- Why Servlet instance variables require care

---

# 8. Servlet Configuration Objects

## 8.1 `ServletConfig`
**Priority:** Good to Know

- Configuration specific to one Servlet
- Initialization parameters
- `getInitParameter()`

## 8.2 `ServletContext`
**Priority:** Good to Know

- One context for the web application
- Application-wide information
- Shared attributes
- Context parameters

## 8.3 `ServletConfig` vs `ServletContext`
**Priority:** Good to Know

Understand scope:

```text
ServletConfig  → one Servlet
ServletContext → whole web application
```

Do not spend too much time on XML configuration.

---

# 9. Servlet Filters

## 9.1 What is a Filter
**Priority:** Must Know Concept

A Filter can process requests/responses before or after a Servlet.

Flow:

```text
Browser
→ Filter
→ Servlet
→ Filter
→ Browser
```

## 9.2 Filter API
**Priority:** Good to Know

- `Filter`
- `FilterChain`
- `doFilter()`
- `@WebFilter`

## 9.3 Common Uses
**Priority:** Must Know Concept

- Authentication
- Logging
- Validation
- Request/response preprocessing
- Security

Important later because Spring Security heavily uses filter-based request processing.

---

## Checkpoint 8

Be able to explain:

- What a Filter does
- What `FilterChain` means
- Why filters are useful
- How the concept connects to Spring Security

---

# 10. Servlet + JDBC

## 10.1 Connecting Servlet to JDBC
**Priority:** Must Know

Basic concept:

```text
Servlet
→ JDBC
→ Database
```

Preferred structure:

```text
Servlet
→ Service
→ DAO
→ JDBC
→ Database
```

## 10.2 Form → Servlet → Database
**Priority:** Must Know

- Read form data
- Validate/convert data
- Call DAO
- Execute database operation
- Send response

## 10.3 Display Database Data
**Priority:** Must Know

- Servlet receives request
- DAO retrieves records
- Data returned to controller
- Controller forwards to view

## 10.4 Resource Handling
**Priority:** Must Know

- `PreparedStatement`
- try-with-resources
- Connection handling
- SQLException handling

Avoid putting all SQL directly inside Servlet methods in the final application structure.

---

## Checkpoint 9

Be able to explain:

- How Servlets and JDBC connect
- Why DAO exists
- Why SQL should not be scattered through Servlets
- Request → Servlet → DAO → Database → Response

---

# 11. Basic MVC Structure

## 11.1 MVC Concept
**Priority:** Must Know

```text
Model
→ Data / business logic

View
→ UI

Controller
→ Handles requests
```

## 11.2 Servlet as Controller
**Priority:** Must Know

```text
Browser
→ Servlet Controller
→ Service
→ DAO
→ Database
→ View / Response
```

## 11.3 Separation of Concerns
**Priority:** Must Know

Avoid:

```text
Servlet
→ SQL
→ HTML
→ Business Logic
```

Prefer:

```text
Servlet
→ Service
→ DAO
→ Database
```

---

# 12. Simple CRUD Web Application

Build one small application.

## 12.1 Create
**Priority:** Must Know

```text
Form
→ POST
→ Servlet
→ DAO
→ INSERT
```

## 12.2 Read
**Priority:** Must Know

```text
GET
→ Servlet
→ DAO
→ SELECT
→ Display
```

## 12.3 Update
**Priority:** Must Know

- Load record
- Edit form
- Submit update
- Update database

## 12.4 Delete
**Priority:** Must Know

- Receive ID
- Delete record
- Redirect back to list page

## 12.5 Session Example
**Priority:** Must Know

Add simple login/session handling.

---

## Final Servlet Project

### Student / Employee CRUD Application

Features:

- List records
- Add record
- Edit record
- Delete record
- Basic login
- `HttpSession`
- Servlet controllers
- Service layer
- DAO layer
- JDBC
- Oracle Database
- Forward / Redirect
- Basic MVC structure

Architecture:

```text
Browser
   ↓
Servlet
   ↓
Service
   ↓
DAO
   ↓
JDBC
   ↓
Oracle Database
```

---

# 13. Servlets → Spring MVC

## 13.1 Problems with Raw Servlets
**Priority:** Must Know

- Repetitive request handling
- Manual parameter extraction
- Manual mappings
- Boilerplate
- More infrastructure code

## 13.2 `DispatcherServlet`
**Priority:** Must Know

Understand:

```text
Servlet API
      ↓
DispatcherServlet
      ↓
Spring MVC
      ↓
Controller
```

## 13.3 Raw Servlet vs Spring MVC
**Priority:** Must Know

Servlet:

```java
@WebServlet("/users")
public class UserServlet extends HttpServlet {

    @Override
    protected void doGet(
            HttpServletRequest request,
            HttpServletResponse response) {
    }
}
```

Spring MVC:

```java
@GetMapping("/users")
public List<User> getUsers() {
}
```

The goal is to understand what Spring is simplifying.

---

# 14. Low-Priority / Legacy Topics

## GenericServlet
**Priority:** Basic Awareness

Know that it exists.

For HTTP web applications, focus on `HttpServlet`.

## Deep `web.xml`
**Priority:** Basic Awareness

Know old XML mapping/configuration.

Do not spend time memorizing large XML files.

## Old Manual JAR Setup
**Priority:** Basic Awareness

Institute notes may manually add:

```text
servlet-api.jar
ojdbc14.jar
```

Understand why dependencies exist, but use modern dependency/project management when building current applications.

## Old File Upload Libraries
**Priority:** Skip

Do not study old JavaZoom / `uploadbean.jar` based file-upload examples.

Modern Servlet APIs support multipart/file upload.

## Rare Servlet APIs
**Priority:** Basic Awareness

Study only if required by an interview or project.

## Deep Container Internals
**Priority:** Basic Awareness

Do not over-invest here.

---

# Final Interview Revision

Before interviews, be comfortable answering:

- What is a Servlet?
- Why are Servlets used?
- What is a Servlet Container?
- Web server vs Servlet container
- What is `HttpServlet`?
- `doGet()` vs `doPost()`
- GET vs POST
- What are `HttpServletRequest` and `HttpServletResponse`?
- How do you read request parameters?
- What are HTTP headers?
- What is MIME/content type?
- Important HTTP status codes
- What is `@WebServlet`?
- What is URL mapping?
- Forward vs Redirect
- What is `RequestDispatcher`?
- Cookies vs Sessions
- Why is HTTP stateless?
- Servlet lifecycle
- `service()` vs `doGet()` / `doPost()`
- What is `ServletConfig`?
- What is `ServletContext`?
- What is a Servlet Filter?
- How do Servlets connect with JDBC?
- Why use DAO?
- What is MVC?
- What role does a Servlet play in MVC?
- What is `DispatcherServlet`?
- How is Spring MVC related to Servlets?

---

# End Goal

Do **not** become an expert in legacy Servlet development.

Reach this level:

```text
Understand Web + HTTP Basics
          ↓
Understand Servlet Container
          ↓
Understand HttpServlet
          ↓
Handle Request / Response
          ↓
Understand Navigation + Sessions
          ↓
Understand Lifecycle + Filters
          ↓
Connect Servlet with JDBC
          ↓
Build CRUD using DAO + MVC
          ↓
Understand DispatcherServlet
          ↓
Move to Spring MVC / Spring Boot
```
