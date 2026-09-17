# 19. JDBC DAO Pattern

DAO means:

```text
Data Access Object
```

Its purpose is to keep database access logic separate from business logic.

## Without DAO

SQL and JDBC code may become scattered across:

```text
main()
service()
controller()
```

## With DAO

Database operations stay in one dedicated layer.

Example interface:

```java
public interface EmployeeDAO {

    void save(Employee employee);

    Employee findById(int id);

    List<Employee> findAll();

    void update(Employee employee);

    void delete(int id);
}
```

## DAO Implementation

```java
public class EmployeeDAOImpl
        implements EmployeeDAO {

    public void save(Employee employee) {
        // JDBC INSERT
    }

    public Employee findById(int id) {
        // JDBC SELECT
        return null;
    }

    public void update(Employee employee) {
        // JDBC UPDATE
    }

    public void delete(int id) {
        // JDBC DELETE
    }
}
```

## Flow

```text
Service
  ↓
EmployeeDAO
  ↓
JDBC
  ↓
Database
```

## Why DAO?

```text
Separates database code
Keeps SQL/JDBC in one place
Improves maintainability
Keeps business logic cleaner
```

The same separation remains useful when moving later to Spring, JPA, or Hibernate.

## Core Idea

```text
DAO
→ separates database access logic
→ contains CRUD methods
→ keeps JDBC code away from business logic
```
