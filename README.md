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


Parametr ma takie cechy:
+ identyfikator: np id w bazie mysql, id session
+ przynaleźność: do konkretnego modelu danych, zbioru, np danych uzytkownika, wysyłającego, odbierającego wysyłkę, ten sam parametr może przynaleźeć do kilku zbiorów
+ format wymiany danych: np kod pocztowy, Zapis Wartości Waluty w różnych krajach ma różne formaty, lub zapis Imienia i Nazwiska razem, lub ulicy i numeru domu razem
  + validator
  + type
  + dependency: w przypadku złożenia wielu typów na raz, jako zbiór Parametrów
  + convert 
    + from()
    + to()


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
    

[Todo List](TODO.md)

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).
