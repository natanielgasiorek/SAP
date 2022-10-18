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
-Przykład sortowania: 
*SORT gt_price BY kscha.

-Przykład zabrania pierwszej lini tabeli: 
*READ TABLE gt_price_temp INTO DATA(gs_price_temp) INDEX 1.

-Przeżucanie danych do tabeli z warunkiem nie usówania takich samych:
*MOVE-CORRESPONDING gt_price_temp_1 TO  gt_price_temp KEEPING TARGET LINES.
