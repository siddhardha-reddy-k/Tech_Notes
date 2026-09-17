# JSP — Interview-Focused Learning Index

> Goal: Learn JSP only to the level needed for fresher Java interviews.
>
> Focus on understanding concepts, flow, and common interview questions.
> Do not spend time going deep into outdated JSP coding styles.

---

## 1. JSP Introduction

- What is JSP?
- Why JSP was introduced
- JSP vs Servlet
- Where JSP fits in a Java web application
- JSP as the View layer
- `.jsp` file basics

**Priority:** High

---

## 2. How JSP Works Internally

- Browser → JSP → JSP/Servlet Container
- JSP is translated into a Servlet
- JSP → Generated Java Servlet → Compiled Class → Execution
- Translation phase
- Request processing phase

**Priority:** Very High

---

## 3. JSP Lifecycle

Know these three lifecycle methods:

```java
_jspInit()
_jspService()
_jspDestroy()
```

Understand:

- When each method executes
- Which method handles every request
- JSP lifecycle vs Servlet lifecycle

**Priority:** Very High

---

## 4. JSP Scripting Elements

Learn these three:

```jsp
<% ... %>       // Scriptlet

<%= ... %>      // Expression

<%! ... %>      // Declaration
```

Also know:

- JSP comments
- Why scriptlets are considered old-style JSP

**Priority:** High

---

## 5. JSP Directives

Learn:

```jsp
<%@ page ... %>
<%@ include ... %>
<%@ taglib ... %>
```

Important `page` directive attributes:

- `import`
- `contentType`
- `errorPage`
- `isErrorPage`
- `session`

**Priority:** High

---

## 6. JSP Implicit Objects

Know all 9 implicit objects:

```text
request
response
out
session
application
config
pageContext
page
exception
```

Focus more on:

- `request`
- `response`
- `session`
- `application`
- `out`
- `pageContext`
- `exception`

**Priority:** Very High

---

## 7. JSP Scopes

Know the four JSP scopes:

```text
page
request
session
application
```

Understand their lifetime:

- Page scope → current JSP page
- Request scope → current request
- Session scope → current user's session
- Application scope → entire web application

**Priority:** Very High

---

## 8. JSP Action Tags

Know these important action tags:

```jsp
<jsp:include>
<jsp:forward>
<jsp:useBean>
<jsp:setProperty>
<jsp:getProperty>
<jsp:param>
```

Understand what each one is used for.

**Priority:** High

---

## 9. Include vs Forward vs Redirect

Understand the difference between:

```text
<%@ include %>
<jsp:include>
<jsp:forward>
response.sendRedirect()
```

Prepare these interview comparisons:

- Include directive vs `<jsp:include>`
- Forward vs Redirect

**Priority:** Very High

---

## 10. JSP Exception Handling

Learn only the basics:

```jsp
errorPage
isErrorPage
```

Also understand:

```xml
<error-page>
```

inside `web.xml`.

**Priority:** Medium

---

## 11. JSP + JavaBean

Understand:

```jsp
<jsp:useBean>
<jsp:setProperty>
<jsp:getProperty>
```

Know how JSP communicates with a JavaBean.

You only need one simple example.

**Priority:** Medium

---

## 12. Expression Language (EL)

> Important topic to add beyond the institute notes.

Basic syntax:

```jsp
${user.name}
${requestScope.user}
${sessionScope.username}
${applicationScope.value}
${param.id}
```

Understand:

- What EL is
- Why EL was introduced
- Accessing JavaBean properties
- Accessing request/session/application attributes
- `param`

Example:

Old JSP:

```jsp
<%= user.getName() %>
```

Using EL:

```jsp
${user.name}
```

**Priority:** Very High

---

## 13. JSTL

> Important topic to add beyond the institute notes.

JSTL = JSP Standard Tag Library

Focus only on core tags:

```jsp
<c:out>
<c:set>
<c:if>
<c:choose>
<c:when>
<c:otherwise>
<c:forEach>
```

Example:

```jsp
<c:forEach var="user" items="${users}">
    ${user.name}
</c:forEach>
```

Main idea:

```text
Old JSP:
Scriptlets

Better JSP:
EL + JSTL
```

**Priority:** Very High

---

## 14. MVC with Servlet + JSP

Understand this flow:

```text
Browser
   ↓
Servlet / Controller
   ↓
Service / Java Code
   ↓
request.setAttribute(...)
   ↓
JSP
   ↓
HTML Response
```

Typical Servlet code:

```java
request.setAttribute("user", user);

request.getRequestDispatcher("user.jsp")
       .forward(request, response);
```

JSP:

```jsp
${user.name}
```

Understand:

- Servlet = Controller
- Java classes / DAO / Service = Model
- JSP = View

**Priority:** Very High

---

## 15. JSP + Database

Know that directly writing JDBC code inside JSP is a legacy / bad practice.

Avoid:

```text
JSP
 ↓
JDBC
 ↓
Database
```

Prefer:

```text
JSP
 ↑
Servlet / Controller
 ↑
Service / DAO
 ↑
Database
```

You do not need to practice JDBC directly inside JSP.

**Priority:** Concept Only

---

## 16. Custom JSP Tags / TLD

Know only:

- Custom Tag
- Tag Library
- `taglib` directive
- TLD = Tag Library Descriptor

Do not spend time writing:

- `TagSupport` classes
- Custom TLD files
- Complex custom tags

**Priority:** Very Low

---

## 17. JSP Configuration / WEB-INF

Know:

```text
WEB-INF
web.xml
JSP mapping
welcome-file
```

Important concept:

Files inside `WEB-INF` cannot normally be requested directly from the browser.

This is useful in MVC:

```text
Servlet / Controller
        ↓
JSP inside WEB-INF
```

Do not memorize large `web.xml` files.

**Priority:** Medium

---

## 18. JSP Deployment Basics

Know only:

```text
WAR
Tomcat
Deployment
src/main/webapp
WEB-INF
web.xml
```

Understand what a WAR file is and how a Java web application is deployed to Tomcat.

**Priority:** Low

---

## 19. JSP Best Practices

Know these interview points:

- Avoid business logic inside JSP
- Avoid JDBC inside JSP
- Avoid Scriptlets in modern JSP code
- Use Servlet / Controller for request processing
- Use JSP only as the View
- Use EL + JSTL for displaying data

**Priority:** High

---

## 20. JSP Interview Revision

Prepare these questions:

1. What is JSP?
2. Why was JSP introduced?
3. JSP vs Servlet?
4. How does JSP work internally?
5. Is JSP converted into a Servlet?
6. Explain the JSP lifecycle.
7. What are JSP scripting elements?
8. Scriptlet vs Expression vs Declaration?
9. What are JSP directives?
10. What are JSP implicit objects?
11. Name the 9 JSP implicit objects.
12. What are JSP scopes?
13. What is `pageContext`?
14. What is Expression Language?
15. What is JSTL?
16. Why are Scriptlets discouraged?
17. Include directive vs `<jsp:include>`?
18. Forward vs Redirect?
19. What are JSP action tags?
20. What is JavaBean in JSP?
21. What is `WEB-INF`?
22. Why are JSP files sometimes kept inside `WEB-INF`?
23. How are Servlets and JSP used together in MVC?
24. Why should JDBC not be written directly inside JSP?
25. What is the role of JSP in MVC?

---

# Final Learning Order

For interview preparation, follow this order:

```text
1. JSP Basics
2. Internal Working
3. Lifecycle
4. Scripting Elements
5. Directives
6. Implicit Objects
7. Scopes
8. Action Tags
9. Include / Forward / Redirect
10. JavaBean
11. Expression Language
12. JSTL
13. Servlet + JSP MVC
```

These are the main topics.

Everything else is secondary.

---

# Topics Outside JSP

The institute merged notes also contain topics such as:

- JUnit
- Maven
- Git
- GitHub

These are useful Java-development topics, but they should be studied separately and are not part of this JSP learning index.
