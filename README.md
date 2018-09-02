Reactive Couchbase with Webflux and Spring Boot Sample - WIP
---

This is a basic sample of Reactive Couchbase with Webflux and Spring Boot, I used the following technologies:
* Spring Boot 2.0.4.RELEASE
* Spring Data Couchbase 3.0.9.RELEASE
* Spring Webflux 5.0.8.RELEASE
* Couchbase Database 5.5.0
* Apache Maven 3.3.9

How to run?

I only implemented the `find` method to access to the database, all CRUD methods have yet to be implemented,
therefore to reproduce this sample you have to create a document manually in the database.

I use docker, if you want to use it, you can copy and paste the following command in your terminal:

```
docker run -d --name db -p 8091-8094:8091-8094 -p 11210:11210 couchbase
```

or else just open the couchbase ui in your browser and login with your credentials:

```
http://localhost:8091/ui/index.html
```

* Create a new bucket called `sample`
* Open the `sample` bucket documents and create a new one, copy and paste this snippet of code in json
```
{
  "id": "1",
  "name": "Juan",
  "lastName": "Calvopina",
  "addresses": [
    {
      "code": "A1",
      "mainStreet": "AAA",
      "secondStreet": "BBB",
      "phone": "11111"
    }
  ],
  "classType": "com.jcalvopinam.model.Person"
}
```
This code snippet has the same mapping used in the model `com.jcalvopinam.model.Person.java`
* Create a new user on `Security` tab called `sample` with password `password` and give it full access
* Clone the project and open it in your IDE
* Download dependencies with maven: `mvn clean install` at the end you should see `[INFO] BUILD SUCCESS`
* Run the main class: `SampleCouchbaseRxApplication.java`
* Open a new tab in your browser and use the following endpoint:

```
http://localhost:8080/people/1/addresses
```

* Finally you should get something like this:

```
[
   {
      "id":"1",
      "addresses":[
         {
            "mainStreet":"AAA",
            "secondStreet":"BBB",
            "phone":"11111"
         }
      ]
   }
]
```

_P.D. This is still process, I will continue to implementing the missing methods to have the full sample of CRUD _