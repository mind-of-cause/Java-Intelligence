---
tags:
  - undone
---

--
 это один из компонентов в архитектуре Tomcat, который служит HTTP-коннектором. Задачей Coyote является прослушивание входящих запросов, передача их на обработку в Catalina (сердце Tomcat) и возвращение ответа клиенту после его обработки.
 Рассмотрим его задачи подробнее: 
 1. **Прослушивание входящих запросов**: Coyote настроен прослушивать определенный порт (обычно 8080 для HTTP). Когда клиент (например, веб-браузер) отправляет запрос на этот порт, Coyote принимает этот запрос. 
 2. **Передача запросов на обработку**: После того как Coyote принял запрос, он передает его на обработку в Catalina. Catalina затем определит, к какому веб-приложению следует направить запрос на основании URL. 
 3. **Возвращение ответа клиенту**: После того как Catalina обработала запрос и сформировала HTTP-ответ, Coyote возвращает этот ответ обратно клиенту. Таким образом, Coyote играет центральную роль в обработке HTTP-запросов и ответов в Tomcat, выступая своего рода "посредником" между клиентом и Catalina, основным обработчиком веб-приложений в Tomcat.

## Пример

каждый раз, когда вы обрабатываете запрос или формируете ответ в сервлете, вы взаимодействуете с Coyote. Допустим, у нас есть следующий сервлет:

```java
@WebServlet(name = "HelloServlet", urlPatterns = {"/hello"}) public class HelloServlet extends HttpServlet { 
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException { 
	response.setContentType("text/html"); 
	response.setCharacterEncoding("UTF-8"); 
	
	PrintWriter writer = response.getWriter(); 
	writer.println("<!DOCTYPE html><html>"); 
	writer.println("<head><title>Привет, мир!</title></head>"); 
	writer.println("<body><h1>Привет, мир!</h1></body>"); 
	writer.println("</html>"); 
	} 
}
```
В этом коде вы обрабатываете входящий HTTP-запрос (это делает Coyote) и формируете HTTP-ответ, отправляя HTML-страницу обратно клиенту (это тоже делает Coyote). В этом смысле, весь код примера, который взаимодействует с `request` и `response`, работает через Coyote, но все детали реализации Coyote скрыты от вас как разработчика.