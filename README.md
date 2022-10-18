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
