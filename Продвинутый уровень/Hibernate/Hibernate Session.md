---
tags:
  - undone
---
```java
public class UtilHibernate() {  
    private static final SessionFactory sessionFactory = buildSessionFactory();  
  
    private static SessionFactory buildSessionFactory() {  
        try {  
            StandardServiceRegistry standardRegistry = new StandardServiceRegistryBuilder().configure().build();  
            Metadata metadata = new MetadataSources(standardRegistry).getMetadataBuilder().build();  
            return metadata.getSessionFactoryBuilder().build();  
        } catch (Throwable ex) {  
            System.err.println("Initial sessionFactory creation failed." + ex);  
            throw new ExceptionInInitializerError(ex);  
        }  
    }
```