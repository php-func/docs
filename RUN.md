## Parametr z Identyfikatorem 

    class Param implements ParamValue
      
      $id (request, row, form id)
      
      $source: Source:RestApi /Sql /Html
      $path: "/users/" /xpath
      
      $name: first_name
      $type: Json::String
      
      $label: "First Name"
      $description: "First Name of User, Requeired"
           
      $required = true; // if optional param in collection
      $validator_collection = new ValidatorCollection() 
      
      $value = '';
      
      setValue();
      getValue();
      
      
    
    class ValidatorCollection
      $collection = [
        ['empty',false]
        ['format', 'XX-XXX']
      ]
      
      validate()
      
      


## Parametr z Identyfikatorem w 3 uzyciach
stworzenie kolejnych objektów klasy Param, różne parametry dla różnych implementacji:

### Definition of Collection process for param in source
$username_sql = new Def(Source, ProcessCollection, Param)
$password_sql = new Def(Source, ProcessCollection, Param)

### Use it one by one
$username_sql->Insert()
$password_sql->Insert()

### Use all of it
new DefCollection(
  $username_sql,
  $password_sql
)->Insert()

Source:

+ Sql
+ RestApi
+ ViewHtml


      class Source
        $id (request, row, form id)      
        $source: Source:RestApi /Sql /Html
        $path: "/users/" /xpath
        $required: false
    

Process:

+ Create
+ Read
+ Update
+ Delete
   

      class Process
        $value
        $validator_collection = new ValidatorCollection() 


      class ProcessCollection

Param:    

+ Username
+ Password
      

      class Param
        $name: first_name
        $type: Json::String      
        $label: "First Name"
        $description: "First Name of User, Required"            
        $value = '';

        setValue();
        getValue();
     
## Inny sposób uzycia, proces odseparowany

    $username_sql = new Def(Source, Param)
    $password_sql = new Def(Source, Param)

lub 

    new DefSourceCollection(Source, [
      Param1,
      Param2
    ])

### Use it one by one

    DefProcess( $username_sql, ProcessInsert )
    DefProcess( $password_sql, ProcessInsert )

### Use all of it

    new DefProcessCollection([
      $username_sql,
      $password_sql
    ],
    [
      ProcessInsert
    ]);
    

## Struktura



      class ParamFormat
        $name: postcode        
        $label: "kod Pocztowy"
        $description: "Format XX-XXX"        
        $collection = new ParamCollection([
            Param( Attr(XX, Int, dwie cyfry) , $validator(2 cyfry)),
            Param( Attr(-,string, znak rozdizeilajacy),
            Param( Attr(XXX, integer, 3 cyfry, $validator(3 cyfry))  
          ])
          
        get()
        set()
       
      
      class ParamString
        $name: postcode        
        $label: "kod Pocztowy"
        $description: "Format XX-XXX"
        $value = ''; //string
          
        get()
        set()
        
        
      class Def
        $name: postcode        
        $label: "kod Pocztowy"
        $description: "Format XX-XXX"            
        $value = '';
        $type=;
        $validator = ;
        
        
      class Source
        $id (request, row, form id)      
        $source: Source:RestApi /Sql /Html
        $path: "/users/" /xpath
        
        $required: false
        $type: Json::String      
        $format: XX-XXX


      class Process implements Run
        $param
        $source        
        $name="Create"
        $validator_collection = new ValidatorCollection() 
        
        function Run()
        

## Struktura: Variable, Param, Source, Process

    Entity: name, value      
        Param: label, description, VariableCollection, ValidationCollection

            Source:                             
              $id (request, row, form id)      
              $source: Source:RestApi /Sql /Html
              $path: "/users/" /xpath
              $required: false
              $Type:  php::int, sql::varchar, json::string  
              $format: XX-XXX

               
               Def
                $Source
                $Param: GenericParam::postcode
                $ProcessCollection: sql::insert

              Process
                $Source: SqlAdress::Postcode
                $Param: GenericParam::postcode
                $Process: sql::insert
                
  
      class VariableCollection
        $collection = [
            DwieCyfry,
            Rodzielnik,
            TrzyCyfry  
          ];
          
## Przykład złożonego parametru

Param example

    class GermanyAddressParam extends ParamFormat implements ParamCollection
    
        EntityCollection
          Street
          HomeNumber
          PostCode
          City

  
  interface ParamFormat

      fromString()
      toString()

  
[Todo List](TODO.md)

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).
