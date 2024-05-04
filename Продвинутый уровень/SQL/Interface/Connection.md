---
tags:
  - undone
---
```java
public Util() {  
    try {  
        connection = DriverManager.getConnection(URL, USERNAME, PASSWORD);  
        if (connection != null && !connection.isClosed()) {  
            System.out.println("We are connected!");  
        }  
    } catch (SQLException e) {  
        System.out.println("there is no connection... Exception!");  
    }  
}  
  
// Метод для получения соединения с базой данных  
public Connection getConnection() {  
    return connection;  
}
```
