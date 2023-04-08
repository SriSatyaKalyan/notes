# Springboot



***Spring Container*** acts as the Object Factory and its primary functions are:
* Create and manage objects(**Inversion Control**)
* Inject object dependencies(**Dependency Injection**)

We can confiure Spring Container using three ways 
* XML Configuration File (legacy)
* Java Annotations (modern)
* Java Source Code (modern)

**Inversion of Control** The approach of outsourcing the construction and management of objects

**Dependency Injection** The client delegates to another object the responsibility of providing its dependencies. There are two different Injection types.
* Constructor Injection
    * Use this when you have required dependencies
    * Generally recommended by spring.io development team as first choice 
* Setter Injection
    * Use this when you have optional dependencies
    * If dependency is not provided, your app can provide reasonable default logic

 ***Spring Autowiring*** is used for dependency injection. Spring will look for a class that 
* matches by type: class or interface

`@Autowired` annotation tells Spring to inject a dependency. If you have only one constructor, then the annotation on the constructor is optional.

Spring will inject it automatically. Hence it is autowired.

Spring will scan for `@Component`. This annotation marks the class a Spring Bean, which is just a regular Java class that is managed by Spring. Also, @Component makes the bean available for dependency injection.




###Related links
* https://start.spring.io/






