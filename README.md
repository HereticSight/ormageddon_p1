# ORMageddon

## Project Description
A java based ORM for connecting to and from an SQL database without the need for SQL or connection management. 

## Technologies Used

* PostgreSQL - version 42.2.12  
* Java - version 8.0  
* Apache commons - version 2.1  

## Features

List of features ready and TODOs for future development  
* Easy to use and straightforward user API.  
* No need for SQL, HQL, or any databse specific language.  
* Straightforward and simple Annotations for ease of use. 

To-do list: [`for future iterations`]
* Mapping of foreign keys to their respective objects.    
* Implement of aggregate functions.    
* Implement retrieval of objects from the cache via findBy methods. So far only findAll is retrieved from the cache.
* etc...

## Getting Started  
Currently project must be included as local dependency. to do so:
```shell
  git clone https://github.com/HereticSight/ormageddon_p1.git
  cd ormageddon_p1
  mvn install
```
Next, place the following inside your project pom.xml file:
```XML
  <dependency>
    <groupId>com.ormageddon</groupId>
    <artifactId>ormageddon_p1</artifactId>
    <version>1.0-SNAPSHOT</version>
  </dependency>

```
Next, place a copy of 
https://github.com/HereticSight/ormageddon_p1/blob/main/src/main/resources/dataTypes.csv
within the src/main/resources folder.

Finally, inside your project structure you need a application.properties file. 
 (typically located src/main/resources/)
 ``` 
  url=path/to/database
  username=username/of/database
  password=password/of/database
  packageName=package/name/containing/annotated/models(eg: com.ormageddon.models)

  ```
  
## Usage  
  ### Annotating classes
  All classes which represent objects in database must be annotated.
   - #### @Entity(name = "table_name")
      - Indicates that this class is associated with table 'table_name'. If a name is not specified, the ORM will autogenerate a name based on the class name.
   - #### @Column(name = "column_name", notNull=false, unique=false)
      - Indicates that the Annotated field is a column in the table with the name 'column_name'. The flags for notNull and unique default to false. If a name is not specified, the ORM will autogenerate a name based on the field name.
   - #### @JoinColumn(name = "column_name", references={Class of object})  
      - Indicates that the anotated field is a column in the table with the name 'column_name'. If a name is not specified, the ORM will autogenerate a name based on the field name. The references property is the Class of the foreign key object (e.g. User.class) and must be specified.
   - #### @Id(name = "column_name") 
      - Indicates that the annotated field is the primary key for the table. If a name is not specified, this will default to "id". In addition, the indicated field will automatically be set as the primary key with an autoincremented value.

  ### User API  
  
  - #### `public HashMap<Class<?>, HashSet<Object>> getCache()`  
     - returns the cache as a HashMap.  
  - #### `public boolean addClass(final Class<?> clazz)`  
     - Adds a class to the ORM. This is the method to use to declare a Class is an object inside of the database. By default, the ORM will add all of your annotated classes to the database.
  - #### `public boolean UpdateObjectInDB(final Object obj,final String update_columns)`  
     - Updates the given object in the databse. Update columns is a comma seperated list of all columns in the object which need to be updated.
  - #### `public boolean removeObjectFromDB(final Object obj)`  
     - Removes the given object from the database.  
  - #### `public boolean addObjectToDB(final Object obj)`  
     - Adds the given object to the database.  
  - #### `public Optional<List<Object>> getListObjectFromDB(final Class <?> clazz, final String columns, final String conditions)`    
  - #### `public Optional<List<Object>> getListObjectFromDB(final Class<?> clazz)`  
     - Gets a list of all objects in the database which match the included search criteria  
        - columns - comma seperated list of columns to search by.  
        - conditions - coma seperated list the values the columns should match to. 
  - #### `public void disableAutoCommit()`  
     - AutoCommit is enabled by default. Use this to disable AutoCommits on the database, and begin a transaction.
  - #### `public void RollbackTransaction()`  
     - Rollback to previous begin statement.
  - #### `public void createSavePoint(final String name)`  
     - Set a savepoint with the given name.  
  - #### `public void rollBackToSavePoint(final String name)`  
     - Rollback to previous savePoint with given name.
  - #### `public void releaseSavepoint(final String name)`
     - Release the savepoint with the given name.  
  - #### `public void commitTransaction()`  
     - Commit the transaction block.
  - #### `public void addAllFromDBToCache(final Class<?> clazz)`  
     - Adds all objects currently in the databse of the given class type to the cache.  



## License

This project uses the following license: [GNU Public License 3.0](https://www.gnu.org/licenses/gpl-3.0.en.html).
