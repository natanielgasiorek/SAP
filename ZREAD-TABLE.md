### Instrukcja, jak dodać autoryzację wglądu dla tabeli konfiguracyjnej:

* Wchodzimy w transakcję se54
* Wpisujemy nazwę tabeli/wglądu
* Zaznaczamy tak jak na obrazku i wchodzimy w tworzenie/zmiana

![b6abc302-03cf-42f9-bcca-3f812e29da56](https://user-images.githubusercontent.com/91785152/204552477-25fcf053-bc05-41ba-a3e7-9c1f105337df.jpg)

* Tworzymy nową grupę uprawnień
* Dodajemy ją do generatora opracowania tabeli

Przykład Mennica - ZMM_ETYKIETY

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Instrukcja jak stworzyć wgląd do tabeli konfiguracyjnej:

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

### Instrukcja jak edytować wygląd tabeli konfiguracyjnej:

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

### Usuwanie danych z tabeli se16n:

-wchodzimy w debager

-parametry ( gd_edit = X, gd_sapedit = X)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Usuwanie duplikatów w pomocy wyszukiwania:

![image](https://user-images.githubusercontent.com/91785152/205066443-0507f392-41af-4f48-aa8f-938e20ae76fe.png)

Nazwa exitu = /DSD/DX_SH_EXIT_DUPLICATES

Przyklad: ZMM_LABELS - ZPRINTER_F4 - Mennica

