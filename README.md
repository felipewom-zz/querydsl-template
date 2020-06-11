##Simple Kotlin with Querydsl template

**Gradle integration**

 Add the following dependencies to your Maven project :

```
compile "com.mysema.querydsl:querydsl-jpa:3.6.3"
kapt "com.mysema.querydsl:querydsl-apt:3.6.3:jpa" // Magic happens here  
compile "org.hibernate:hibernate-entitymanager:4.3.5.Final"
```

The JPAAnnotationProcessor finds domain types annotated with the javax.persistence.Entity annotation and generates query types for them.

If you use Hibernate annotations in your domain types you should use the APT processor com.querydsl.apt.hibernate.HibernateAnnotationProcessor instead.

Run clean install and you will get your Query types generated into target/generated-sources/java.

If you use Eclipse, run mvn eclipse:eclipse to update your Eclipse project to include target/generated-sources/java as a source folder.

Now you are able to construct JPQL query instances and instances of the query domain model.     

**Querying**

Querying with Querydsl JPA is as simple as this :

```JAVA
QCustomer customer = QCustomer.customer;
JPAQuery<?> query = new JPAQuery<Void>(entityManager);
Customer bob = query.select(customer)
  .from(customer)
  .where(customer.firstName.eq("Bob"))
  .fetchOne();
```