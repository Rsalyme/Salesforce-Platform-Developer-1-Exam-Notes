
These notes were originally by SANTOSH KUMAR SRIRAM from 
<https://withsalesforce.wordpress.com>

To make them more easily available to the wider developer community I've migrated the content to markdown so that we it can be shared on git.

 Salesforce AppExchange Overview Demo
 
<http://www.salesforce.com/platform/appexchange/appexchange-overview-demo.jsp?d=70130000000mC5D&internal=true>

   Salesforce Appexchange is the leading business app marketplace
    Customers can:
    
        install apps
        read reviews
        customize apps (unmanaged)
        Apps run on salesforce 1 platform - pre integrated - ugrades are automatic and hassle free
Working with Schema Builder

    Schema Builder provides a dynamic environment for viewing and modifying all the objects and relationships in your app.
Schema Builder is enabled by default and lets you add the following to your schema:

        a. Custom objects
        b. Lookup relationships
        c. Master-detail relationships
        d. All custom fields except: Geolocation
 Trailhead: Working with Schema Builder

    <https://developer.salesforce.com/trailhead/data_modeling/schema_builder>
  Primitive Data Types and Variables
    
    Apex Workbook

    <https://resources.docs.salesforce.com/sfdc/pdf/apex_workbook.pdf>

        //String 
        //Strings are set of characters and are enclosed in single quotes. 
        //They store text values such as a name or an address.
        
        String myVariable = 'Hey Look! I am a string!!';
        String myVariable = String.valueOf(Date.today());
        String myVariable = 'Hey Look ' + 'I am a concatenated String!';
        
        String x = 'I am a string';
        String y = 'I AM A STRING';
        System.debug (x == y); 
        //Result -> True 
        //"==" and "!=" are case insensitive comparisons

Have a basic understanding of all the string methods:

<https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_methods_system_string.htm>

• Boolean: Boolean values hold true or false values and you can use them to test whether a certain condition is true or false.

        The negation operator "!" is important &&(AND operator) and ||(OR operator)

Ternary conditional operation:

    If x, a Boolean, is true, then the result is y; otherwise it is z. 
    x ? y : z
• Time, Date and Datetime: 

Variables declared with any of these data types hold time, date, or time and date values combined.

The basics of any timestamp fields on the Salesforce sObjects:

            Date.newInstance()..
            Time.newInstance()..
            Datetime.newInstance()..
            System.today(), date.today()
            System.now(), Datetime.now()
            System.now().time(), Datetime.now().time()

Date methods:

<https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_methods_system_date.htm>

Datetime methods:

<https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_methods_system_datetime.htm>

Integer, Long, Double and Decimal: 

Variables declared with any of these data types hold numeric values.

Integer

    A 32-bit number that doesn’t include a decimal point. Integers have a minimum value of -2,147,483,648 and a maximum value of
2,147,483,647.

Long

    A 64-bit number that doesn’t include a decimal point. Longs have a minimum value of -263 and a maximum value of 263-1.
Double
    
    A 64-bit number that includes a decimal point. Doubles have a minimum value of -263 and a maximum value of 263-1.
Decimal
    
    A number that includes a decimal point. Decimal is an arbitrary precision number. Currency fields are automatically assigned the type Decimal.
    
Null variables: 
    
    Variables that don’t have a value.
    
    If you declare a variable and don't initialize it with a value, it will be null. In essence, null means the absence of a value. You can also assign null to any variable declared with a primitive type.

Enum:

    An enumeration of contant values.

Use enumerations (enums) to specify a set of constants. 
Define a new enumeration by using the enum keyword followed by the list of identifiers between curly braces. 
    
    public ENUM ExampleEnum{CONSTANT1,CONSTANT2}
        
Each value in the enumeration corresponds to an Integer value, starting from zero and incrementing
by one from left to right. 
Because each value corresponds to a constant, the identifiers are in upper case. For example, this example defines an enumeration called Season that contains the four seasons:


        public enum Season {WINTER, SPRING, SUMMER, FALL}

sObjects and the database

    Apex Workbook <https://resources.docs.salesforce.com/sfdc/pdf/apex_workbook.pdf>
    
An sObject is any object that can be stored in the Force.com platform database. These are not objects in the sense of instances of Apex classes; rather, they are representations of data that has or will be persisted.
    
sObject is a holder of a salesforce record. It could be externally visible user object or internal referenced in Salesforce.com
    
sObject is a generic abstract type that corresponds to any persisted object type. The generic sObject can be cast into a specific sObject type, such as an account or the Invoice_Statement__c custom object.


SOQL and SOSL Queries


The same way database systems support a query language for data retrieval, the Force.com peristence layer also provides two query languages.

Salesforce Object Query Language (SOQL) is a query-only language. While similar to SQL in some ways, it's an object query language that uses relationships, not joins, for a more intuitive navigation of data. This is the main query language that is used for data retrieval of a single sOobject and its related sObjects. 

Salesforce Object Search Language (SOSL) is a simple language for searching across all multiple persisted objects simultaneously.

SOSL is similar to Apache Lucene.

You can write queries directly in Apex without much additional code since Apex is tightly integrated with the database.

    SOQL queries return a sObject or a list<sObject>
    
    SOSL queries always return a list<list<sObject>>
sObject Relationships and Dot Notation

        sObjectTypeName parentObject = objectA.RelationshipName; //traversing from child to parent
        DataType s = objectA.RelationshipName.FieldName; //traversing to a field on the parent from the child record
SOQL For Loops

        for(Integer i=0; i < listTemporary.size() ; i ++){
           System.debug( listTemporary[i] );
        }
List iterating for loops
        
        listTemporary = [Select Id From Account];
        for (sObject iterating_temp : listTemporary){
            your code here!!
        }
Inline SOQL for loops


    for(sObject iterating_temp : [SOQL query..]){
        your code here!!
    }
Apex Data Manipulation Language

         Insert 
         Update
         Delete
         UnDelete
         Upsert - Inserts/updates based on Salesforce Id or existing external ID prescribed

Database DML Methods

        Database.insert();
        Database.update();
        Database.upsert();
        Database.delete();
        Database.undelete();
When to Use DML Statements and Database DML Statements

Typically, you will want to use Database methods instead of DML statements if you want to allow partial success of a bulk DML operation by setting the opt_allOrNone argument to false. In this way, you avoid exceptions being thrown in your code and you can inspect the rejected records in the returned results to possibly retry the operation. 

Database methods also support exceptions if not setting the opt_allOrNone argument to false.
Use the DML statements if you want any error during bulk DML processing to be thrown as an Apex exception that immediately interrupts control flow and can be handled using try/catch blocks. This behavior is similar to the way exceptions are handled in most database procedure languages.
Force.com developer guide - https://resources.docs.salesforce.com/sfdc/pdf/salesforce_apex_language_reference.pdf

More Data types and variables

        list<> - ordered, non-unique collection of data
        set<> - unordered, unique collection of data
        map<key, value> - key, value pair collection of data. Keys have to be unique, values neednt be unique
        
Expressions and operators - https://developer.salesforce.com/docs/atlas.en-us.pages.meta/pages/pages_variables_operators.htm
Force.com developer guide - https://resources.docs.salesforce.com/sfdc/pdf/salesforce_apex_language_reference.pdf

Dynamic APEX

a. Understanding the APEX Describe information

2 methods:

        i) Token - using a lightweight, serializable reference to sObject or field validated at run time
        
        ii) describeSObjects - method from the schema class
        
        Both returns Schema.describeSObjectResult - non-serializable and validated at run time.
        Schema.DescribeSObjectResult dsr = Account.sObjectType.getDescribe();
        Schema.DescribeFieldResult dfr = Schema.sObjectType.Account.fields.Name;
        //Get the describe result from the token
        dfr = dfr.getSObjectField().getDescribe();
        Accessing All Field Describe Results for an sObject
        Map<String,Schema.SObjectField> fieldMap = Schema.SObjectType.Account.fields.getMap();

b. Dynamic SOQL

        List<sObject> sobjList = Database.query(string);


Note: Binding variables have to split from the query string. Dynamic SOQL will throw a - "variable does not exist" error
SOQL injection - To prevent SOQL injection, use the escapeSingleQuotes method. This method adds the escape character (\) to all single quotation marks in a string that is passed in from a user. The method ensures that all single quotation marks are treated as enclosing strings, instead of database commands.
c. Dynamic SOSL

        List<List<sObject>> myQuery=search.query(SOSL_search_string);
d. Dynamic DML

        Account a = Database.query( 'SELECT Id FROM account LIMIT 1' );
Can also be used with newSObject method


        SObject s = Database.query( 'SELECT Id FROM account LIMIT 1' )[0].getSObjectType().newSObject([SELECT Id FROM               Account LIMIT 1][0].Id);

Force.com developer guide <https://resources.docs.salesforce.com/sfdc/pdf/salesforce_apex_language_reference.pdf>

Custom labels

If you want to display error messages/visual force headers/validation rules in languages based on user's record, then custom label is your best friend.

        String errorMsg = System.Label.generic_error;

Accessing sObject Fields 

Covered in dynamic apex - Point # 7 - DescribeResult


DML vs Database methods

One difference between the two options is that by using the Database class method, you can specify whether or not to allow for partial record processing if errors are encountered. 

You can do so by passing an additional second Boolean parameter. If you specify false for this parameter and if a record fails, the remainder of DML operations can still succeed. Also, instead of exceptions, a result object array (or one result object if only one sObject was passed in) is returned containing the status of each operation and any errors encountered.
By default, this optional parameter is true, which means that if at least one sObject can’t be processed, all remaining sObjects won’t and an exception will be thrown for the record that causes a failure.

The following helps you decide when you want to use DML statements or Database class methods.

• Use DML statements if you want any error that occurs during bulk DML processing to be thrown as an Apex exception that immediately
interrupts control flow (by using try. . .catch blocks). This behavior is similar to the way exceptions are handled in most
database procedural languages.

Use Database class methods if you want to allow partial success of a bulk DML operation—if a record fails, the remainder of the DML operation can still succeed. Your application can then inspect the rejected records and possibly retry the operation. When using this form, you can write code that never throws DML exception errors. Instead, your code can use the appropriate results array to judge success or failure. Note that Database methods also include a syntax that supports thrown exceptions, similar to DML statements.
Most operations overlap between the two, except for a few.
    • The convertLead operation is only available as a Database class method, not as a DML statement.
    • The Database class also provides methods not available as DML statements, such as methods transaction control and         rollback, emptying the Recycle Bin, and methods related to SOQL queries.

Apex Data Manipulation Language

        Insert 
        Update
        Delete
        UnDelete
        Upsert - Inserts/updates based on Salesforce Id or existing external ID prescribed


        Database DML Methods
        Database.insert();
        Database.update();
        Database.upsert();
        Database.delete();
        Database.undelete();

9. Control Flow Statements

        Apex supports the following five types of procedural loops:
        • do {statement} while (Boolean_condition);
        • while (Boolean_condition) statement;
        • for (initialization; Boolean_exit_condition; increment) statement;
        • for (variable : array_or_set) statement;
        • for (variable : [inline_soql_query]) statement;
        All loops allow for loop control structures:
        • break; exits the entire loop
        • continue; skips to the next iteration of the loop
        
Triggers and Order of Execution

<https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_triggers_order_of_execution.htm>

Lightning Components Developer’s Guide (Basic level questions - read first 2 chapters)

<https://resources.docs.salesforce.com/sfdc/pdf/lightning.pdf>

Introducing Lightning Components

<https://developer.salesforce.com/trailhead/modules>
Just complete these trailheads and you are good for the exam!

Invoking Apex

<https://youtu.be/ScEyirckrD4?list=PLLEljoYbeYUWgVLyi4qKLzTU-NE6sqt4o>
This youtube will cover it all. 20 min video and this will do it

Testing APEX

Part 1

<https://youtu.be/mKtYud7wgRE?list=PLLEljoYbeYUWgVLyi4qKLzTU-NE6sqt4o>

Part 2 

<https://youtu.be/PTorr9UzlHk?list=PLLEljoYbeYUWgVLyi4qKLzTU-NE6sqt4o>

