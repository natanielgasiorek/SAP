# SAP
### Wszystkie potrzebne kody do pracy.

### Jak zmienić nazwę systemowego elementu danych.

* Wchodzimy w transakcję CMOD
* Wybieramy zakładki tak jak na obrazku:

![f5233ad0-585b-49c6-8c54-4a848cc5ef4b](https://user-images.githubusercontent.com/91785152/204749013-9db20e4e-c8c4-4a52-8c49-1f25255eb387.jpg)

--------------------------------------------------------------

Przekazanie parametru select-options do modułu funkcyjnego!

DATA: gt_werks_opt TYPE RSELOPTION.

MOVE-CORRESPONDING so_werks[] TO gt_werks_opt.

![image](https://user-images.githubusercontent.com/91785152/196413115-73fcfaf3-132a-4c11-88c1-482532c18bc6.png)

---------------------------------------------------------------
#### Przykład sortowania: 

*SORT gt_price BY kscha.

#### Przykład zabrania pierwszej lini tabeli: 

*READ TABLE gt_price_temp INTO DATA(gs_price_temp) INDEX 1.

#### Przerzucanie danych do tabeli z warunkiem nie usówania takich samych:

*MOVE-CORRESPONDING gt_price_temp_1 TO  gt_price_temp KEEPING TARGET LINES.

#### Usuwanie zer wiodących podczas przypisania wartości.

*ls_xyz-matnr = |{ ls_mseg-matnr ALPHA = OUT }|.
	
#### Tworzenie concatenate podczas przypisywania wartości.
	
*ls_xyz-matdoc = lv_temp && ls_mseg-zeile.
