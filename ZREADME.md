# SAP
 ### Wszystkie potrzebne kody do pracy.

Usuwanie danych z tabeli se16n:

-wchodzimy w debager
-parametry ( gd_edit = X, gd_sapedit = X)

---------------------------------------------------------------
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
