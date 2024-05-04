---
tags:
  - undone
---
--
компонент в архитектуре Apache Tomcat, он отвечает за обработку JSP-страниц (JavaServer Pages). В простейших терминах, Jasper представляет собой JSP-движок для Tomcat. Он компилирует JSP-страницы в сервлеты для их выполнения.

Работа Jasper включает в себя следующие шаги:

  

1. **Чтение JSP-страницы**: при получении запроса на JSP-страницу, Jasper начинает свою работу с чтения самой страницы. Исходный код JSP-страницы состоит из HTML-тегов и Java-кода, который встроен в эти теги.
    
2. **Компиляция JSP-страницы в Java-сервлет**: Jasper затем превращает эту JSP-страницу в Java-сервлет. HTML-теги преобразуются в строки вывода в сервлете, а встроенный Java-код становится частью логики сервлета.
    
3. **Компиляция сервлета**: после того как сервлет был сформирован, Jasper компилирует его в байт-код Java, который может быть выполнен JVM (Java Virtual Machine).
    
4. **Исполнение сервлета**: в конце концов, когда сервлет будет скомпилирован, он будет выполнен в контейнере сервлетов Catalina.
    


Таким образом, Jasper играет важную роль в Tomcat, обеспечивая поддержку JSP-страниц, которые являются основой для многих веб-приложений Java.

## Пример
взаимодействие с Jasper происходит каждый раз, когда вы создаете JSP-страницу. Допустим, у вас есть JSP-страница с именем `example.jsp`, которая выглядит так:

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %> 
<html> 
	<head>
		 <title>Привет, мир!</title> 
	</head> 
	<body> 
		<h1>${message}</h1> 
	</body>
</html>
```

```java
@WebServlet(name = "HelloServlet", urlPatterns = {"/hello"}) 
public class HelloServlet extends HttpServlet { protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException { 
	request.setAttribute("message", "Привет, мир!"); 
	request.getRequestDispatcher("/example.jsp").forward(request, response); 
	} 
}
```
При обращении к URL `/hello`, сервлет устанавливает атрибут `message`, а затем перенаправляет запрос на `example.jsp`. Jasper автоматически обрабатывает `example.jsp`, компилирует его в сервлет и выполняет его. В браузере вы увидите заголовок `Привет, мир!`. Это взаимодействие с Jasper, но все детали работы Jasper скрыты от вас.