## Aktywacja tabeli po dokonanych zmianach:

* Wchodzimy w transakcję se14

![tabela1](https://user-images.githubusercontent.com/91785152/224951430-ac96fc80-a7f7-4850-b760-d90ba76cdcab.png)

![Tabela](https://user-images.githubusercontent.com/91785152/224951455-62e6b16c-2122-4e1f-8672-ed47e205de48.png)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Instrukcja, jak dodać autoryzację wglądu dla tabeli konfiguracyjnej:

* Wchodzimy w transakcję se54
* Wpisujemy nazwę tabeli/wglądu
* Zaznaczamy tak jak na obrazku i wchodzimy w tworzenie/zmiana

![b6abc302-03cf-42f9-bcca-3f812e29da56](https://user-images.githubusercontent.com/91785152/204552477-25fcf053-bc05-41ba-a3e7-9c1f105337df.jpg)

* Tworzymy nową grupę uprawnień
* Dodajemy ją do generatora opracowania tabeli

Przykład Mennica - ZMM_ETYKIETY

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Instrukcja jak stworzyć transakcje dla drzewa klastrowego:

![image](https://github.com/natanielgasiorek/SAP/assets/91785152/7be76ada-1549-47f6-a504-0b100b1824e6)

## Instrukcja jak stworzyć wgląd do tabeli konfiguracyjnej:

Aby stworzyć transakcję dla opracowania wglądu należy:

- uruchomić transakcję SE93,
- wybrać nazwę dla nowej transakcji,
- wybrać opcję transakcja z parametrami (transakcja parametrów),
- dalej w polu transakcja wpisać SM30,
- zaznaczyć pominięcie ekranu początk.,
- zaznaczyć GUI-dziedziczenie właściwości,
- w parametrach podać VIEWNAME - wartość NAZWA WGLĄDU
		      UPDATE	- X
		      
Tworzymy generator opracowania tabeli:

![92f7bf09-3341-45c8-8d28-50a478a585e8](https://user-images.githubusercontent.com/91785152/198004684-a3dce76d-9377-49cf-a564-8c2e45915daa.jpg)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Instrukcja jak edytować wygląd tabeli konfiguracyjnej:

Edytowanie układu wglądu do tabeli:

- uruchomić transakcję SE11,
- w trybie zmiany odpalić tabelę,
- pomoce (generator opracowania tabeli),
- otoczenie
- modyfikacja,
- ekrany opracowania,
- wybierasz ekran (enter),
- układ

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Usuwanie danych z tabeli se16n:

-wchodzimy w debager

-parametry ( gd-edit = X, gd-sapedit = X)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Usuwanie duplikatów w pomocy wyszukiwania:

![image](https://user-images.githubusercontent.com/91785152/205066443-0507f392-41af-4f48-aa8f-938e20ae76fe.png)

Nazwa exitu = /DSD/DX_SH_EXIT_DUPLICATES

Przyklad: ZMM_LABELS - ZPRINTER_F4 - Mennica

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Jak zrobić tabelę słownikową z przypisanym opisem:

![image](https://github.com/natanielgasiorek/SAP/assets/91785152/ec395543-e14c-4262-9afe-5062d40566f7)

![image](https://github.com/natanielgasiorek/SAP/assets/91785152/dbdbd757-43a8-4f86-9918-1109fcc7f332)

![image](https://github.com/natanielgasiorek/SAP/assets/91785152/1a0777f2-621c-4479-8fc0-d7b0c49da840)

![image](https://github.com/natanielgasiorek/SAP/assets/91785152/d6f37fa5-790d-437a-8213-ebc472af11c8)

![image](https://github.com/natanielgasiorek/SAP/assets/91785152/d798a8b1-009c-4fdb-83ba-7a68d1183bf5)
