# SAP
Wszystkie potrzebne kody do pracy.

Aby stworzyć transakcję dla opracowania wglądu należy:

- uruchomić transakcję SE93,
- wybrać nazwę dla nowej transakcji,
- wybrać opcję transakcja z parametrami (transakcja parametrów),
- dalej w polu transakcja wpisać SM30,
- zaznaczyć pominięcie ekranu początk.,
- zaznaczyć GUI-dziedziczenie właściwości,
- w parametrach podać VIEWNAME - wartość NAZWA WGLĄDU
		      UPDATE	- X
		      
![92f7bf09-3341-45c8-8d28-50a478a585e8](https://user-images.githubusercontent.com/91785152/198004684-a3dce76d-9377-49cf-a564-8c2e45915daa.jpg)
   
Edytowanie układu wglądu do tabeli:

- uruchomić transakcję SE11,
- w trybie zmiany odpalić tabelę,
- pomoce (generator opracowania tabeli),
- otoczenie
- modyfikacja,
- ekrany opracowania,
- wybierasz ekran (enter),
- układ

---------------------------------------------------------------
Przekazanie parametru select-options do modułu funkcyjnego!

DATA: gt_werks_opt TYPE RSELOPTION.

MOVE-CORRESPONDING so_werks[] TO gt_werks_opt.

![image](https://user-images.githubusercontent.com/91785152/196413115-73fcfaf3-132a-4c11-88c1-482532c18bc6.png)

---------------------------------------------------------------
-Przykład sortowania: 

*SORT gt_price BY kscha.

-Przykład zabrania pierwszej lini tabeli: 

*READ TABLE gt_price_temp INTO DATA(gs_price_temp) INDEX 1.

-Przerzucanie danych do tabeli z warunkiem nie usówania takich samych:

*MOVE-CORRESPONDING gt_price_temp_1 TO  gt_price_temp KEEPING TARGET LINES.
