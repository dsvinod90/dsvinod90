---
title: Spring 
layout: default
filename: spring 
--- 
[back](/dsvinod90/tech)

<h2 style="text-align: center;"> Spring Basics </h2>
<br><br>

## MVC Architecture
![](https://i.imgur.com/agATsyr.png)

## MVC - Non-REST setup
- Use the annotation `@Controller` to identify the class as Controller.
- The annotation `@RequestMapping("/test")` is used to give a top level namespace to this controller. All requests with url `/test/..` will be served by this controller
### Accessing Request params in the Controller
Here are two code samples that show various ways of accessing the request params in with `@Controller`
1. Using `HttpServletRequest`
```java
public String letsShoutDude(HttpServletRequest request, Model model) {
    String theName = request.getParameter("studentName");
    theName = theName.toUpperCase();
    String result = "Yo! " + theName;
    model.addAttribute("message", result);
    return "helloworld";
}
```
2. Using `@RequestParam`
```java
public String processFormVersion3(@RequestParam("studentName") String theName, Model model) {
    theName = theName.toUpperCase();
    String result = "Hey my friend from V3! " + theName;
    model.addAttribute("message", result);
    return "helloworld";
}
```
### Accessing ModelAttributes in the Controller
If a jsp page uses `modelAttribute` for its form input, then the receiving controller to which the action is addressed can access the form's inputs as the corresponding Model's attributes. The code sample below shows how to access the model atttributes.
```java
public String processForm(@ModelAttribute("student") Student theStudent) {
    // log input data
    System.out.println("theStudent: " +
            theStudent.getFirstName() + " " + theStudent.getLastName() + "\n" +
            "\tCountry: " + theStudent.getCountry() + "\n" +
            "\tFavorite Programming Language: " + theStudent.getFavoriteLanguage() + "\n" +
            "\t Operating Systems: " + theStudent.getOperatingSystems()
            );
    return "student-confirmation";
}
```
### Displaying model's attributes in a JSP page
Let's assume we have a class called `Student` and we want to display all the attributes of this class' object on a JSP page.

Here's how the Controller action would look like:
```java
public String showForm(Model theModel) {
    // create student object
    Student theStudent = new Student();

    // add student object to the model
    theModel.addAttribute("student", theStudent);
    theModel.addAttribute("countries", moreCountryOptions);
    return "student-form";
}
```

The corresponding view page will have the following:
```java
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>Student Confirmation</title>
	</head>
	<body>
		<a href="showForm"> Back to student form </a>
		<br><br>
		The student is confirmed: ${student.firstName} ${student.lastName}
		<br><br>
		Country: ${student.country}
		<br><br>
		Favorite Language: ${student.favoriteLanguage}
		<br><br>
		Operating Systems:
			<ul>
				<c:forEach var="temp" items="${student.operatingSystems}">
					<li> ${temp} </li>
				</c:forEach>
			</ul>
	</body>
</html>
```
## [Spring MVC Form Tags](https://docs.spring.io/spring-framework/docs/5.0.2.RELEASE/spring-framework-reference/web.html#mvc-view-jsp-tags)
In the JSP view page include the following to use form tags.
```java
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form" %>
```
Code sample for a form:
```java
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form" %>

<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>Student Registration Form</title>
	</head>
	<body>
		<a href="/spring-mvc-demo/"> Back to main menu </a>
		<br><br>
		<form:form action="processForm" modelAttribute="student">
			First Name: <form:input path="firstName"/>
			<br><br>
			Last Name: <form:input path="lastName"/>
			<br><br>
			Country:
				<form:select path="country">
					<form:options items="${countries}" />
					<form:options items="${student.countryOptions}" />
					<form:option value="Indonesia" label="Indonesia" />
					<form:option value="Sri Lanka" label="Sri Lanka" />
					<form:option value="Poland" label="Poland" />
					<form:option value="Iceland" label="Iceland" />
				</form:select>
			<br><br>
			Favorite Language:
				<form:radiobutton path="favoriteLanguage" value="Java" /> Java
				<form:radiobutton path="favoriteLanguage" value="Ruby" /> Ruby
				<form:radiobutton path="favoriteLanguage" value="Python" /> Python
				<form:radiobutton path="favoriteLanguage" value="Javascript" /> JavaScript
				<form:radiobuttons path="favoriteLanguage" items="${student.favoriteLanguageOptions}" />
			<br><br>
			Operating Systems:
				Linux <form:checkbox path="operatingSystems" value="Linux" />
				Mac OS <form:checkbox path="operatingSystems" value="Mac OS" />
				Windows <form:checkbox path="operatingSystems" value="Windows" />
			<br><br>
			<input type="submit" value="Submit" />
		</form:form>
	</body>
</html>
```
- Here `action` corresponds to the controller method that will be called on submission of the form.
- `modelAttribute` binds the object to the model. In this case, `student` is the model attribute; meaning that the form's input fields correspond to an instance of the `Student` class. When the form is submitted, the setter methods of those fields are called and the value used to fill the input fields is set as the values of the those attributes.
- `path` is the name of the field attribute for that instance of Class. For example, all the path values mentioned in the code sample are the `Student` class' attributes.


## Important Links:
* [Bean Validation](https://beanvalidation.org/) - For performing form validations on view pages.
* [Hibernate](https://hibernate.org/) - It started off as ORM but has moved to other functionalities such as Validator etc.

