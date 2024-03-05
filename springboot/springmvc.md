https://www.baeldung.com/spring-mvc-annotations

 @RequestMapping marks request handler methods inside @Controller classes; it can be configured using:

path, or its aliases, name, and value: which URL the method is mapped to
method: compatible HTTP methods
params: filters requests based on presence, absence, or value of HTTP parameters
headers: filters requests based on presence, absence, or value of HTTP headers
consumes: which media types the method can consume in the HTTP request body
produces: which media types the method can produce in the HTTP response body

Let’s move on to @RequestBody – which maps the body of the HTTP request to an object

@PathVariable
This annotation indicates that a method argument is bound to a URI template variable. We can specify the URI template with the @RequestMapping annotation and bind a method argument to one of the template parts with @PathVariable.

We can achieve this with the name or its alias, the value argument

We use @RequestParam for accessing HTTP request parameters


@PathVariable and @RequestParam are both annotations used in Spring MVC to extract data from incoming HTTP requests, but they are used in different contexts and for different purposes.

Here are the key differences between @PathVariable and @RequestParam:

Purpose:

@PathVariable: Used to extract values from the URI template of the request URL. It allows you to capture variable parts of the URL path.
@RequestParam: Used to extract query parameters from the request URL. It allows you to access key-value pairs sent in the query string of the URL.
Usage:

@PathVariable: Applied to method parameters in controller methods to bind them to a URI template variable. The variable parts of the URL are specified within curly braces {} in the request mapping.
@RequestParam: Applied to method parameters in controller methods to bind them to query parameters sent in the request URL. Query parameters are specified as key-value pairs after the ? in the URL.
Syntax:

@PathVariable: Syntax involves specifying the name of the variable part in the URI template within curly braces {} and providing a matching parameter name in the method signature.
@RequestParam: Syntax involves specifying the name of the query parameter as the value of the annotation, which is then matched to a method parameter with the same name.
Example:

java
Copy code

	// Using @PathVariable
	@GetMapping("/users/{id}")
	public User getUserById(@PathVariable Long id) {
	    // Implementation to fetch user by ID
	}

	// Using @RequestParam
	@GetMapping("/users")
	public List<User> getUsersByRole(@RequestParam String role) {
	    // Implementation to fetch users by role
	}


In the first example, id is extracted from the URL path /users/{id} using @PathVariable. In the second example, the query parameter role is extracted from the request URL using @RequestParam.

/users?role=role

Optional vs. Required:

@PathVariable: By default, path variables are required. If the variable is not present in the URL, Spring will throw a MissingPathVariableException. You can make path variables optional by specifying a default value or using the @PathVariable(required = false) attribute.
@RequestParam: Query parameters are optional by default. If the parameter is not present in the URL, the corresponding method parameter will be set to null. You can specify a default value using the defaultValue attribute of @RequestParam.
In summary, @PathVariable is used to extract values from the URI path, while @RequestParam is used to extract values from the query string of the URL. They serve different purposes and are applied in different scenarios based on how the data is passed in the HTTP request.



To access a URL using request parameters in a Spring MVC controller, you can use the @RequestParam annotation to extract the parameters from the request URL. Here's an example of how to do this:

java
Copy code

	import org.springframework.stereotype.Controller;
	import org.springframework.web.bind.annotation.GetMapping;
	import org.springframework.web.bind.annotation.RequestParam;
	import org.springframework.web.bind.annotation.ResponseBody;

	@Controller
	public class MyController {

	    @GetMapping("/greet")
	    @ResponseBody
	    public String greet(@RequestParam String name) {
	        return "Hello, " + name + "!";
	    }
	}
	In this example:

We define a controller class MyController annotated with @Controller.
We define a handler method greet() annotated with @GetMapping("/greet"). This method handles GET requests to the /greet endpoint.
The name parameter is extracted from the request URL using @RequestParam. This annotation binds the value of the name query parameter to the name method parameter.
Inside the method, we return a greeting message using the value of the name parameter.
Now, if you make a GET request to /greet?name=John, Spring will extract the value of the name parameter from the request URL and pass it to the greet() method. The method will then return the response "Hello, John!".

Here's how you can access this endpoint using request parameters:

bash
Copy code
     GET /greet?name=John
And the response will be:

Copy code
	Hello, John!

You can add more @RequestParam annotations to extract additional parameters from the request URL as needed.
