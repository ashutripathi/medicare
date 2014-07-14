medicare
========

Question:

In Java, how can you declare a variable non-serializable? When it is required?

Answer:
A variable can be made non-serializable by declaring it as transient by using 'transient'  keyword. By default all variables are persistent. 
Variables can be marked 'transient' when you want to avoid persisting them, you don't have the necessity to maintain their state.

----------------------------------------------

Question:
In Java, what are the differences between Shallow copy and Deep copy?

Answer:
In Java, shallow copy is a bit-wise copy of an object. A new object is created that has an exact copy of the values in the original object. If any of the fields of the object are references to other objects, just the reference addresses are copied i.e., only the memory address is copied. The default implementation of clone() method in Java performs a shallow copy.

A deep copy copies all fields, and makes copies of dynamically allocated memory pointed to by the fields. A deep copy occurs when an object is copied along with the objects to which it refers.

----------------------------------------------

Question:
In Java, what is the difference between Stack and Queue?

Answer:
In Java, Stack is a collection of objects that works in LIFO (Last in First out) mechanism while Queue is FIFO (First in First out). 
This means that the object that is inserted first is removed last in a stack while an object that is inserted first is removed first in a queue.

----------------------------------------------

Question:
What is Dependency Injection?

Answer:
   Software components (Client), are often a part of a set of collaborating components which depend upon other components (Services) to successfully complete a business function. The client object need to know which service objects to communicate with, where to locate them and how to communicate with them.

      Dependency Injection is based on the principle of ‘Inversion of Control’. The idea is to avoid direct dependency between collaborating objects by not creating objects using ‘new’ operator. Dependency injection is a way of structuring code such that clients do not locate or instantiate services as part of usual logic. Rather the  dependencies are provided in a configuration file / through annotations and an external component (in case of spring framework the IoC container) is responsible for hooking up the objects. 

      One of the biggest advantages of dependency injection is that it reduces coupling between objects thereby making testing a lot easier. Independent clients are easier to unit test in isolation using stub or mock objects.

----------------------------------------------

Question:
What are the different types of dependency injection supported in Spring?

Answer:
Spring framework supports two types of Dependency Injection
•	Constructor Injection - Dependencies are provided by constructor parameters
•	Setter Injection - Dependencies are assigned through setter methods (Java Beans properties) after object instantiation using a no argument constructor

----------------------------------------------

Question:
In Spring, what is the difference between BeanFactory and ApplicationContext?

Answer:
A BeanFactory is a factory class that holds bean definitions and then instantiates the beans whenever asked for by clients. It also creates dependencies between collaborating objects as they are instantiated. BeanFactory also enforces the life cycle of a bean, making calls to various initialization and destruction methods.

ApplicationContext is a more advanced container for beans. It provides all the BeanFactory functions like loading bean definitions, wiring beans together, and providing beans upon request. It also provides the following additional functions: 

•	A means for resolving text messages, including support for internationalization.
•	A generic way to load file resources.
•	Events to beans that are registered as listeners.

ApplicationContext is the preferred way to access beans in Spring.

--------------------------------------------

Question:
What is the typical Bean life cycle in Spring BeanFactory Container ?

Answer:
Bean life cycle in Spring BeanFactory Container is as follows:

a)	The spring container finds the bean’s definition (from the XML file) and instantiates the bean. 
b)	The bean is populated with all the properties as specified in the bean definition. If a property is reference to another bean, then the other bean will be created and populated, and reference injected into the bean.
c)	If the bean implements the BeanNameAware interface, the factory calls setBeanName() passing the bean’s ID. 
d)	If the bean implements the BeanFactoryAware interface, the factory calls setBeanFactory(), passing an instance of Bean Factory. 
e)	If there are any BeanPostProcessors associated with the bean, their post- ProcessBeforeInitialization() methods will be called for pre initialization. 
f)	If an init-method is specified for the bean, it will be called.
g)	If there are any BeanPostProcessors associated with the bean, their  postProcessAfterInitialization() methods will be called. 

--------------------------------------------

Question:
In Spring, what do you mean by Auto Wiring?
Answer:
Auto wiring is a capability by which Spring container is able to establish relationships between collaborating beans without the need to provide explicit wiring instructions through <constructor-arg> and <property> elements on bean definition (XML) files. 

This helps in reducing the amount of XML configurations. The auto wiring functionality has five modes:
•	no - This is the default setting which means no auto wiring. Explicit bean reference should be provided through the XML file. 
•	byName - Auto wiring by property name. When this option is used, the container attempts to look for a bean that has the same name as the property of the auto wired bean. 
•	byType - Auto wiring by property type. The container attempts to match all properties of the auto wired bean with beans whose types are compatible to the properties. 
•	constructor - This is similar to byType but applies to constructor. The container attempts to match up a constructor of the auto wired bean with beans whose types are assignable to the constructor arguments
•	autodetect - The container attempts to apply 'Auto wiring by Constructor' first if it fails, it applies 'Auto wiring byType'.

--------------------------------------------

Question:
What are the Bean scopes in Spring Framework ?

Answer:
The Spring Framework supports five scopes which allow us to control the scope of the bean. 

a)	singleton - This is the default scope and allows a single instance per Spring IoC container.
b)	prototype - Allows a bean to be instantiated any number of times. A distinct instance is provided to everyone who has wiring for this bean.
c)	request -  Scopes a single bean definition to the lifecycle of a single HTTP request; that is each and every HTTP request will have its own instance of a bean created off the back of a single bean definition. This scope is only valid in the context of a web-aware Spring ApplicationContext.
d)	session -  Scopes a single bean definition to the lifecycle of a HTTP Session. This scope is only valid in the context of a web-aware Spring ApplicationContext.
e)	global session - Scopes a single bean definition to the lifecycle of a global HTTP Session. Typically only valid when used in a portlet context. Only valid in the context of a web-aware Spring ApplicationContext.

--------------------------------------------

Question:
How will you configure Spring without using XML?

Answer:
Spring provides an alternate means to configure beans through use of Java Annotations. Some of the common annotations and their usage is below:

@Configuration - The class having this annotation can be used by Spring container as a source of bean definitions
@Bean - The method having this annotation returns an object that will be treated as a bean by spring container
@Import - Allows loading of bean definitions from another configuration class.
@Scope - Used along with @Bean annotation to configure scope for the bean

-------------------------------------------

Question:
In Spring, what are bean post processors? Can we associate multiple bean post processors with a bean?

Answer:
      In Spring framework, the BeanPostProcessor interface defines a number of callback methods that an application developer can implement in order to provide their own  instantiation logic, dependency-resolution logic etc. These methods are invoked by the Spring container after it has finished with bean instantiation, configuring and initialization. 

      Multiple BeanPostProcessor can be configured for a bean. The order of their execution can be controlled through "order" property.

-------------------------------------------

Question:
In Spring, how to implement inheritance in bean definition?

Answer:
A Spring bean can inherit from another Spring bean through parent attribute on the child bean. The child bean will inherit all configuration information like constructor arguments, property values and container specific information. The inheritance concept is very similar to Java inheritance whereby the child can override some values and add some more if needed. However Spring does not enforce Java inheritance for the classes that are configured as parent child through spring configurations.

-------------------------------------------

Question:
In Spring, what are lazily instantiated beans?

Answer:
The default behavior of Spring Container is to instantiate all singleton beans at startup. Lazy Initialization is a mechanism through which the Spring container can be instructed to instantiate the bean only when it gets a first client request. Lazy initialization is achieved by providing lazy-init property to true on the bean. 

Lazy Initialization does not guarantee that a bean will not be instantiated at startup. A bean with lazy-init property set to true can still be instantiated at startup if it is referenced by a non-lazy-init singleton bean. In such case Spring container has to create the instance for dependency injection.

-------------------------------------------

Question:
Explain the concept of inner beans in Spring?

Answer:
Spring inner beans are beans that are defined within the scope of another bean. The concept is very similar to Java inner classes. Inner beans are supported both by constructor injection as well as setter injection. 

Inner beans are typically used when a bean is being referenced by only one bean. An important point to note is that scope, id and name tags for inner beans are always ignored by the Spring container. Inner beans are always anonymous and they are always scoped as prototype.

-------------------------------------------

Question:
In Spring, explain the significance of init-method and destroy-method attributes on a bean?

Answer:
The init-method and destroy-method can be used to provide custom code that will be invoked by the Spring container. The init-method is invoked immediately after the bean is initialized and the destroy-method is invoked  before the bean is removed from the container.

-------------------------------------------

Question:
Explain transaction management in Spring framework.

Answer:
Spring supports programmatic as well as declarative transaction management. The main benefits of using Spring transaction management are:
a)	Provides a consistent programming model across different transaction APIs like JTA, JDBC, JPA, Hibernate etc.
b)	Provides a simpler API for programmatic transaction management than JTA
c)	Integrates very well with Spring's various data access abstractions

-------------------------------------------

Question:
Explain the similarities and differences between Spring Declarative transactions and EJB CMT(Container Managed Transactions).

Answer:
The basic functions of both these transaction framework is the same. Both of them allow transaction to be applied at a method level and setRollbackOnly to be called within the transaction context to rollback. However Spring framework is far more versatile due to following reasons:

a)	Spring declarative transactions can be applied to any class whereas EJB CMT can be applied only on EJBs
b)	EJB CMT can only work with JTA whereas Spring can work with JDBC, JPA, Hibernate etc.
c)	Spring framework allows declarative rollback rules whereas this can only be done programmatically in EJB CMT. 

However, Spring framework does not support propagation of transactions across remote calls. This can be achieved only through EJB CMT.

-------------------------------------------

Question:
In Spring, how do you ensure that all properties are set on a particular bean?

Answer:
The Spring container also has the ability to check for the existence of unresolved dependencies of a bean deployed into the container. These are properties of the bean, which do not have actual values set for them in the bean definition, or alternately provided automatically by the autowiring feature. Spring container provides a dependency checking mechanism for a bean which can be specified through dependency-check attribute of a bean when using XML-based configuration. 

Various dependency checking modes supported and their behavior is provided below:
•	none - This is the default mode and implies that dependency check will not be performed.
•	simple - Dependency Check is performed for primitive types and collections
•	object - Dependency Check is performed for objects
•	all - Dependency Check is done for all objects, primitive types and collections

For annotation based configuration, this can be achieved using @Required annotation in in the org.springframework.beans.factory.annotation package.

------------------------------------------

Question:
What are the benefits of Hibernate over JDBC?

Answer:
Hibernate is a simple, flexible and powerful ORM framework to map Java classes to database tables. Hibernate itself takes care of this mapping using XML files so developer does not need to write code for this. 

Benefits of Hibernate are:
1.	Supports POJO based persistence
2.	Is database Independent
3.	Supports powerful query language Hibernate Query Language (HQL) which is database independent. This is expressed in a familiar SQL like syntax and includes full support for polymorphic queries. Hibernate also supports native SQL statements. 
4.	Supports Inheritance, Association and Relationships
5.	Provides powerful Hibernate Cache which helps in increasing the application performance
6.	Provides improved Performance and maintainability

------------------------------------------

Question:
In Hibernate, what is SessionFactory? Is it thread-safe?

Answer:
SessionFactory in Hibernate is a factory object used to create a session instance. It is part of org.hibernate package. It is a multithreaded object and hence it is thread-safe. Many threads can access it concurrently.

SessionFactory can be created through the hibernate configuration file (hibernate.cfg.xml) which determines the hibernate mapping file (.hbm) to be loaded.  These files contain the properties required for configuring the database and the tables. 

SessionFactory can be created as follows:
Configuration cfg=new Configuration();   
cfg=cfg.configure();
// When you invoke the configure() method, the framework looks for hibernate.cfg.xml and  for hibernate mapping file (.hbm file).

SessionFactory sc=cfg.buildSessionFactory();
// When you invoke the buildSessionFactory() method on the configuration object, the SessionFactory object is created. 

-------------------------------------------

Question:
What is the role of Session object in Hibernate?  Is it thread-safe?

Answer:
Session object represents a unit of work in Hibernate that represents conversation between application and database. It is used to maintain connection with database. Session object is referred to as persistence manager  since it is responsible for storing and retrieving object to and from database. 

Session object is single threaded and hence it is not thread-safe. It can't be shared between multiple threads.

Session object is created with the SessionFactory object:

SessionFactory sessionFactory = new Configuration().configure().buildSessionFactory();
Session session = sessionFactory.openSession();

-------------------------------------------

Question:
What is the difference between Hibernate get() and load() methods?

Answer:
Hibernate session's get() method is used to retrieve an object from the database using a unique Id. The method returns null if the object is not found in the database. If the object is not available in cache, but exists on database, it may involve several data access calls to database returning a completely initialized object. 

Hibernate session's load() method is also used to retrieve an object from the database using a unique Id. However this method throws an exception if the object is not available in the database. If the object is not available in cache, but exists on database, load() method can return proxy in place providing lazy initialization which results in better performance.

-------------------------------------------

Question:
In Hibernate, when to use get() method and load() method?

Answer:
The load() method may return a proxy instead of a real persistent instance. A proxy is a placeholder that triggers the loading of the real object when it’s accessed for the first time; On the other hand, get() never returns a proxy. 

Choosing between get() and load() is easy: If you’re certain the persistent object exists, and nonexistence would be considered exceptional, load() is a good option. If you aren’t certain there is a persistent instance with the given identifier, use get() and test the return value to see if it’s null. Using load() has a further implication: The application may retrieve a valid reference (a proxy) to a persistent instance without hitting the database to retrieve its persistent state. So load() might not throw an exception when it doesn’t find the persistent object in the cache or database; the exception would be thrown later, when the proxy is accessed. 

-------------------------------------------

Question:
What are the different levels of caching supported in Hibernate?
Answer:
Hibernate supports two main levels of cache:

1.	First-level Cache -  This is the default cache associated with the Session object. Hibernate uses this cache on a per-transaction basis.  Mainly it reduces the number of SQL queries it needs to generate within a given transaction. Instead of updating after every modification in the transaction, it updates only at the end of the transaction.

2.	Second-level Cache -  This cache is associated with the SessionFactory object. To reduce database traffic, second level cache keeps loaded objects with the SessionFactory between transactions. These objects are not bound to a single user, available at the application level. Since the objects are available at the cache, each time a query returns an object, one or more database transactions can be avoided. 

There is one more cache - Query level Cache is supported and this is more for caching query results which can be used along with second level cache for improved performance.

-------------------------------------------

Question:
What is the difference between transient, persistent and detached object in Hibernate?

Answer:
An object is hibernate can exist in one of the three states of the life cycle - transient, persistent and detached. 
When an object is instantiated, it is not associated with a session and it is not persisted directly in the database and it is said to be in transient state. When an object is associated with a session or when the transient object is made persistent, the object has a representation in the database and an identifier value and is said to be in persistent state. When the session object is closed, the association is lost with the persistence manager and the object is said to be in detached state. 
......
Student student = new Student();
student.setStudentId(1234);
student.setStudentName("Nitin");
// student object is in a transient state

Long id = (Long) session.save(student); 
// session is an object of Hibernate Session
// student object is now in persistent state
....
session.close();
// student is now in detached state

------------------------------------------

Question:
What is the difference between Hibernate merge() and update() methods?

Answer:
The update() method is used to save the object when the session object does not contain a persistent instance with the same identifier.  The method will throw an exception if there is already a persistence instance associated with the session. The merge() method is used to merge the modifications without considering about the state of the session. It will just update without considering the session state.

This is explained in the code snippet below:
// In the first session
Student student = (Student) firstSession.load(Student.class, 1001);
student.setStudentGrade("A+");
.........
session.close();
// student is detached 
Student studentTwo =  (Student) secondSession.load(Student.class, 1001);
studentTwo.setStudentGrade("B");
..........
secondSession.update(student);  
// Update here will it will throw an exception like org.hibernate.NonUniqueObjectException
secondSession.merge(student); 
// Merge will simply update without concern about the session

Use update() if you are certain that the session does not contain an already persistent instance with the same identifier. Use merge() if you want to merge your modifications at any time without consideration of the state of the session. 

-----------------------------------------

Question:
What is Criteria API in Hibernate?
Answer:
Criteria is a simplified API for retrieving entities by composing Criterion objects.  This is a very convenient approach for functionality like "search" where there is a variable number of conditions to be placed upon the result set. Complex Hibernate queries can be generated on-the-fly using Criteria API.

A Criteria object is created using the createCriteria() method in the Hibernate session object :
    Criteria criteria = session.createCriteria(Student.class);
    criteria.setMaxResults(10);
    List students = criteria.list();

Once created, Criterion instances are usually obtained via the factory methods on Restrictions.
List students = session.createCriteria(Student.class)
   .add(Restrictions.like("studentName", "James%"))
   .list();

-----------------------------------------

Question:
What is the difference between sorted and ordered collection in Hibernate?

Answer:
A sorted collection is sorting a collection by utilizing the sorting methods provided by the Java collections. The sorting is done in the memory of JVM that is running hibernate after the data being read from database using Java comparator. This is efficient way to sort when collection is small. 

An ordered collection is sorting a collection by specifying order-by clause or using OrderBy annotation when retrieval. This is more efficient when the collection is very large. With ordered collection you are saving process time allowing RDBMS sorting data in a fast-way, rather than ordering data in Java once received. Furthermore order-by clause or OrderBy annotation does not force you to use SortedSet or SortedMap collection. You can use any collection like HashMap, HashSet, or even a Bag, because hibernate will use internally a LinkedHashMap, LinkedHashSet or ArrayList respectively.

-----------------------------------------

Question:
What are the inheritance strategies supported in Hibernate?

Answer:
Three basic inheritance mapping strategies supported in Hibernate are:
1.	Table per class hierarchy strategy: A single table hosts all the instances of a class hierarchy. This table would include columns for all properties of all classes in the hierarchy. A discriminator is used as a key to uniquely identify the base type of the class hierarchy. This mapping strategy is preferred because of its performance and simplicity.
2.	Table per concrete class strategy: One table per concrete class and subclass is present and each table persist the properties of the class and its superclasses. The main problem with this strategy is that it doesn’t support polymorphic associations very well.
3.	Table per subclass strategy: One table per class and every subclass is present including abstract classes. Unlike the strategy that uses a table per concrete class, the table here contains columns only for each non-inherited property (each property declared by the subclass itself) along with a primary key that is also a foreign key of the superclass table. Even though this mapping strategy is deceptively simple, the performance may be problem for complex class hierarchies.

