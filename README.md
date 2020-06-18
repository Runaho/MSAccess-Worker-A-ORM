# Access-Worker-A-ORM
Micro-ORM For Access

## Install

## How It's Work
To put it simply, it is a system that reads all the properties in the class and converts them into an access query's.

You can easily pull the data, send and update it with the id, send the data by filling the class, save the database, and access the id of the recorded record.

What can be done ?
* List All Datas
* List the data with the top. (Class,5)
* Get first Data (Class,1).FirstOrDefault();
* Insert data via filling class.
* Update data via filling class with Identity

## Using
Generate Struct or Class of the Table or Query

``` csharp
/*
 * DisplayName : Access Column name
 * DataObjectField(true) : Is Identity
 * Must be Same Order Table
 * Must be similar types.
 * if you want to update you must define one DataObjectField
 * Table Name can be getted via class Display Name attribute. If you don't have a D.N.A. code will use class name. Sturct is working only struct name.
*/

public struct Users
{
  [DisplayName("ID"), DataObjectField(true)]
  public int id { get; set; }

  [DisplayName("Name")]
  public string Name { get; set; }

  [DisplayName("Surname")]
  public string Surname { get; set; }

  [DisplayName("Age")]
  public int PersonAge { get; set; }
}

// OR

[DisplayName("Users")]
public class MyUsers
{
  [DisplayName("ID"), DataObjectField(true)]
  public int id { get; set; }

  [DisplayName("Name")]
  public string Name { get; set; }

  [DisplayName("Surname")]
  public string Surname { get; set; }

  [DisplayName("Age")]
  public int PersonAge { get; set; }
}
 
 

//Set the path.
AccesWorker.DatabasePath = Server.MapPath("~/DB/test.mdb");

//AccesWorker.Provider = "Else Microsoft.JET.OLEDB.4.0";

```
###### Insert

``` csharp
        // Fill class without identity.
var newuser = new Users()
{
  Name = "Jhon",
  Surname = "Doe",
  PersonAge = 32
};

var InsertedID = AccesWorker.Insert(newuser);
``` 
###### Update

``` csharp
       // Fill Class with identity
var updateuser = new Users()
{
  id = InsertedID,
  Name = "New Jhon",
  Surname = "Doe",
  PersonAge = 33
};

AccesWorker.Update(updateuser);
```             
###### Select's

``` csharp
// Get All
  IEnumerable<Users> allDatas = AccesWorker.List(new Users()).Cast<Users>();

// Get 5
  IEnumerable<Users> top5 = AccesWorker.List(new Users(), 5).Cast<Users>();

// Get First
  Users getfirst = AccesWorker.List(new Users(), 1).Cast<Users>().FirstOrDefault();
``` 
