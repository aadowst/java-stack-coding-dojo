*Creating the Application*
File > New > Spring Starter Project
change name(lower case)
Make sure Type = Maven; Java Version = 8; and Packaging = War
package and group fields = reverse domain (com.aadowst.projectname)
Add Description
Next
Select "Spring Boot DevTools" and "Spring Web"
Finish

*Running the Application*
Right click on application (i.e. projectname) > Run As > Spring Boot App
visit localhost:8080 to look for whitelabel error (this is good)

*Setting up Controller(s)*
Right click on the main package (in src/main/java folder) > New > Package
add ".controllers" to the name and click finish (this will put the controllers package inside the main package)
Right click on the .controllers package and create a new class. Name the class 'xcontroller' where x is something meaningful

<!-- *Setting up RestController*
in xcontroller.java add @RestController above the public class ... method.
Ctrl+shift+O will auto-import what is needed -->

*Setting up Controller*
in xcontroller.java add @Controller above the public class ... method.
Ctrl+shift+O will auto-import what is needed

*Setting up RequestMapping*
within the class, type "@RequestMapping('route')" and then set up a function below:
public String index(){
    return "string"
}

<!-- _Sample Code for using RestController_
```java
package com.aadowst.helloworld.controllers;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@Controller
public class HomeController {
	@RequestMapping("/")
	public String index() {
		return "hello there";
	}
}
``` -->

_Sample Code using Controller_
```java
package com.aadowst.PACKAGENAME.controllers;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class HomeController {

	@RequestMapping("/")
	public String index() {
		return "index.jsp";
	}
}
```

*Run project*
Save and run

<!-- *Settin up Path Variables*
in the RequestMapping, you can include variables in the route
the variables are then passed in to the method as paramenters
The variables can also be in the return string

_Sample Code_
```java
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
@RestController
public class HomeController {
    @RequestMapping("/m/{track}/{module}/{lesson}")
    public String showLesson(@PathVariable("track") String track, @PathVariable("module") String module, @PathVariable("lesson") String lesson){
    	return "Track: " + track + ", Module: " + module + ", Lesson: " + lesson;
    }
} -->
```

*Add Dependencies*

Install the dependency below into pom.xml:
```java
    	<dependency>
                <groupId>org.apache.tomcat.embed</groupId>
                <artifactId>tomcat-embed-jasper</artifactId>
        </dependency>
		<dependency>
                <groupId>javax.servlet</groupId>
                <artifactId>jstl</artifactId>
        </dependency>
```
*Set up WEB-INF*
in src > main > webapp, add WEB-INF folder
right click on the WEB-INF folder, add New > Other. Search for JSP and select "JSP File"
name it (e.g. index.jsp)
check src/main/resources > templates > application.properties
if needed, add: spring.mvc.view.prefix=/WEB-INF/


*Import JSTL into your template in any .jsp file where it is needed*
```java
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<!-- New line below to use the JSP Standard Tag Library -->
<%@ taglib prefix = "c" uri = "http://java.sun.com/jsp/jstl/core"%>
```

*Import Model class in Controller*
as a parameter in the method add (Model model)
now attributes of the model can be passed to the jsp file and rendered on the page.

_Sample Controller Code_
```java
package com.aadowst.PACKAGE;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;
@Controller
public class HomeController {
	@RequestMapping("/")
	public String index(Model model) {
		model.addAttribute("firstname", "Adrian");
		model.addAttribute("lastname", "Dowst");
		return "index.jsp";
	}
}
```

_Sample JSP Code_
```java
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib prefix = "c" uri = "http://java.sun.com/jsp/jstl/core"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
<h1>Two plus two is: </h1>
<h2><c:out value="${2+2}"/></h2>
<h2>My name is <c:out value="${firstname}"/> <c:out value="${lastname}"/></h2>
</body>
</html>
```