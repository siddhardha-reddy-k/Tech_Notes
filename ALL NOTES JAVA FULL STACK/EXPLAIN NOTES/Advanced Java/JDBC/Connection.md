
## 3. Connection

`Connection` represents an active database session.

Important imports:

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
```

### Creating a Connection

```java
Connection con = DriverManager.getConnection(
        url,
        username,
        password
);
```

Example:

```java
String url =
        "jdbc:oracle:thin:@//localhost:1521/FREEPDB1";

String username = "SYSTEM";
String password = "admin";

Connection con =
        DriverManager.getConnection(
                url,
                username,
                password
        );
```

### DriverManager

`DriverManager` helps Java find the JDBC driver and establish the database connection.

Main method:

```java
DriverManager.getConnection(...)
```

It returns:

```java
Connection
```

### JDBC URL

Current Oracle JDBC URL:

```text
jdbc:oracle:thin:@//localhost:1521/FREEPDB1
```

Breakdown:

```text
jdbc:oracle:thin:@//localhost:1521/FREEPDB1
│     │      │        │       │       │
│     │      │        │       │       └─ Service name
│     │      │        │       └───────── Port
│     │      │        └───────────────── Host
│     │      └────────────────────────── Driver type
│     └───────────────────────────────── Database
└─────────────────────────────────────── JDBC
```

### What Happens Internally?

```text
Java
 ↓
DriverManager
 ↓
Oracle JDBC Driver
 ↓
Oracle Database
 ↓
Authentication
 ↓
Connection object returned
```

### SQLException

Database operations can fail because of:

- Wrong username/password
- Wrong JDBC URL
- Missing JDBC driver
- Database not running
- Network problems
- SQL errors

JDBC commonly throws:

```java
SQLException
```

Example:

```java
try {

    Connection con =
            DriverManager.getConnection(
                    url,
                    username,
                    password
            );

} catch (SQLException e) {
    e.printStackTrace();
}
```

### Closing the Connection

```java
con.close();
```

Connections should not be left open unnecessarily.

---
