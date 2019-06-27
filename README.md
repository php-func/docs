https://phpfunc-com.github.io/docs/

# [PhpFunc.com](https://docs.PhpFunc.com)
Documentation for Php Func Repositories

## Goals
The libraries are created for support fast development

## Cele projektu
Biblioteki pomocne przy szybkim budowaniu aplikacji mają pomóc w planowaniu i zarządzaniu architekturą.

Zamiast wykorzystywać jakiś framework do budowy prostego modułu, np do logowania.

## Funkcje parametru
https://pl.wikipedia.org/wiki/Parametr_(informatyka)

Parametrem jest określony, zadeklarowany i zdefiniowany w programie (kodzie źródłowym), element (identyfikator), umożliwiający przekazanie argumentu do podprogramu oraz wyniku z podprogramu do zadania wywołującego tenże podprogram (nadrzędnego).

Parametr może zostać zdefiniowany dla podprogramu lub programu. W tym drugim przypadku parametr służy do komunikacji danego programu (procesu) z systemem operacyjnym lub innym programem wywołującym.

Definiując podprogram programista posługuje się parametrem, czyli informacją (np. wartością), która nie jest znana w momencie definiowania podprogramu, a jedynie zadeklarowaną w jego nagłówku. Argument jest natomiast informacją (np. wartością), znaną, przekazaną z miejsca wywołania, którą posługuje się zdefiniowany wcześniej podprogram. 

## Parametr definition 

Wystarczy zbudować model danych wykorzystując Parametry:
+ generyczne: Imię, Nazwisko, E-mail
+ konfigurowalne: 
+ opcjonalne: option list


## Parametr ma takie cechy:

+ Identifier - identyfikator: np id w bazie mysql, id session
  + ID = string/integer/mix
  + Source = datamodel, którego dotyczy id
  
+ BelongCollection - przynaleźność: do konkretnego modelu danych, zbioru, np danych uzytkownika, wysyłającego, odbierającego wysyłkę, ten sam parametr może przynaleźeć do kilku zbiorów. Chodzi o walidację na poziomie przynaleźności, w przypadku, gdyby np w zbiorze krajów były jakieś ograniczenia
  
+ ParamFormat wymiany danych: np kod pocztowy, Zapis Wartości Waluty w różnych krajach ma różne formaty, lub zapis Imienia i Nazwiska razem, lub ulicy i numeru domu razem

    + from()
    + to()
    
  + ValidatorCollection: np. przy nazwisku pierwsza litera duża
  
  + ParamType: obliczany na podstawie walidatorów w odniesieniu do konkretnych potrzeb: sql, php, java, javascript object
      + export()
      + import()
      
  + dependency collection: w przypadku złożenia wielu typów na raz, jako zbiór Parametrów  
    


## Przykład kolekcji parametrów

  Generic Parameter

    + Name
    + Street
    + House number
    + Postcode
    + City
    + Country
    
  SenderAddress
  
    + Name
    + Street
    + House number
    + Postcode
    + City
    + Country

  ReceiverAddress
  
    + Name
    + Street
    + House number
    + Postcode
    + City
    + Country
    
## Przykład prostego parametru

    FirstName
    LastName

## Przykład złożonego parametru

    PersonName 
      FirstName + BetweenName + LastName



## Przykład prostego parametru

    + StreetParam extends Convert implements Param

    + HomeNumber
    + PostCode
    + City





## Convert Format
ta sama wartość może być pokazana jako dwa różne formaty

    $format = new ParamFormat()

    class ParamFormat extends Convert
  
      $value_in = 00.00; // default
      $type_in = ParamFormatType::PhpFloat
      
      $value_out = "0.000,00";
      $type_out = ParamFormatType::NumberFormat
      


    class Convert
      
      inToOut()
      outToIn()


## Identyfikator for Sql


    abstract class ParamSql extends Value
      
      $identifier = new ParamSqlIdentifier()            
      $value = '' // new ParamValue()
      $required = true;
          
    class ParamIdentifier
      id (row id)
      source (table name)
      name (column name)
  
  
    class ParamValue
      $value = new Value()
       

      
    class ValidatorCollection
      $collection = [
        ['empty',false]
        ['format', 'XX-XXX']
      ]
      

## Identyfikator for Sql


    abstract class Param extends SqlValue
      
      $identifier = new ParamSqlIdentifier()            
      $value = '' // new ParamValue()
      $required = true;
          
    class ParamIdentifier
      id (row id)
      source (table name)
      name (column name)
      type (varchar)
  

    class ParamSqlType
        static Varchar
        static Text
        static Integer
        static Blob
      
    

## Identyfikator for RESTAPI


    abstract class Param extends JsonValue
      
      $identifier = new ParamJsonIdentifier()            
      $value = '' // new ParamValue()
      $required = true;
      
      create()
      read()
      update()
      delete()
      
      validate()
      
          
    class ParamJsonIdentifier 
      id (request id)
      source: Source:RestApi
      path: "/users/"
      name: first_name
      type: Json::String
  
    class ParamJsonType
      static String
      static Integer
      static Bollean
    
    class JsonValue extends CRUDValue implements CreateValue, ReadValue, UpdateValue, DeleteValue
      create()
      read()
      update()
      delete()
        $validator = new ValidatorCollection() // import for REST Validation
      
     CreateValue
      $value
      $validator

     ReadValue
      $value
      $validator

     UpdateValue
      $value
      $validator

     DeleteValue
      $value
      $validator

      
    class ValidatorCollection
      $collection = [
        ['empty',false]
        ['format', 'XX-XXX']
      ]
      
## ParamCollection      

    $UserInfo = new ParamCollection([
      ParamIdentifier,
      ParamJsonIdentifier
      ParamSqlIdentifier
    ])


    $UserInfo->each()->read()->toString(); // pokazuje wszystkie dane jako łańcuch
    $UserInfo->each()->read()->toFormatString(', '); // pokazuje wszystkie dane jako odseparowane przecinkiem wyrazy
    
    
    $UserInfo->each()->update() // aktualizuje wszystkie zmienne, działania na każdym atrybucie
    
    
    $UserInfo->each()->delete() // usuwa wszystkie zmiennem, działania na każdym atrybucie


    $UserInfo->first()->delete() // usuwa pierwsza zmienna
    
    $UserInfo->current()->delete() // usuwa aktualna zmienna
    
    $UserInfo->find('ParamIdentifier')->delete() // usuwa wybraną zmienna
    
    $UserInfo->find('ParamIdentifier')->update('22') // aktualizuje wybraną zmienna
    
    
## Wymiana danych pomiędzy ParamSqlCollection i ParamJsonCollection

    $UserSqlInfo = new ParamSqlCollection([
      ParamIdentifier,
      ParamJsonIdentifier
      ParamSqlIdentifier
    ])  
    
    
    $UserJsonInfo = new ParamJsonCollection([
      ParamIdentifier,
      ParamJsonIdentifier
      ParamSqlIdentifier
    ])  
    
    
### jedna komenda robi wymiane danych pomiedzy RESTAPI a bazą danych MySQL

    $UserJsonInfo->all()->update(
      $UserSqlInfo->all()->read()
    );
    
    
    
    //new Fill(UserSqlInfo)
  
## Identyfikator dla widoku Formularza, Tabeli

    ParamView
      $param = new Param();
      $title = new ParamTitle();
      $format = new ParamFormat();


    class ParamTitle extends Word
      $language_iso = 'PL' // localisation
      $word = ''
      $shortcut = ''
      $description = ''    
      

## Parametr z Identyfikatorem

   

## Identyfikator for RESTAPI


    abstract class Param
      
      $id (request id)
      $source: Source:RestApi /Sql /Html
      $path: "/users/" /xpath
      $name: first_name
      $label: "First Name"
      $description: "First Name of User, Requeired"
      $type: Json::String      
      $required = true; // if optional param in collection
      $validator_collection = new ValidatorCollection() 
      $value = '';
      
      
      create()
      read()
      update()
      delete()
      
      validate()
      
          
    
    class ValidatorCollection
      $collection = [
        ['empty',false]
        ['format', 'XX-XXX']
      ]
      

## Przykład złożonego parametru

  GermanyAddressParam extends ParamFormat implements ParamCollection
    
    Collection
      Street
      HomeNumber
      PostCode
      City

  
  interface ParamFormat

      fromString()
      toString()

  
[Todo List](TODO.md)

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).
