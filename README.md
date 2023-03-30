# SAP
### Wszystkie potrzebne kody do pracy.

--------------------------------------------------------------
### Jak zmienić nazwę systemowego elementu danych.

* Wchodzimy w transakcję CMOD
* Wybieramy zakładki tak jak na obrazku:

![f5233ad0-585b-49c6-8c54-4a848cc5ef4b](https://user-images.githubusercontent.com/91785152/204749013-9db20e4e-c8c4-4a52-8c49-1f25255eb387.jpg)

* Wpisujemy nazwę elementu który chcemy zmienić. 

--------------------------------------------------------------
### Jak znaleźć tabelę (FIORI), w której dokonujemy zmian.

* Wchodzimy w transakcję ST05
* Wchodzimy w okienko Activate Trace with Filter
* Wypełniamy użytkownika i mandant

![image](https://user-images.githubusercontent.com/91785152/207831920-94bec0a1-4042-43c7-9725-d64f4f5af33a.png)
* Dokonujemy zmian w jakimś polu
* Klikamy w okienko Deactive Trace.
* Wchodzimy w okienko Display Trace

![image](https://user-images.githubusercontent.com/91785152/207832145-9ef28301-b4d1-45aa-a4ea-3fdee73229a4.png)

--------------------------------------------------------------
### Jak przenieść transport między mandantami:

* Wchodzimy w transakcję SCC1

![1498591a-2afa-4e38-a830-b4f0ccfb381b](https://user-images.githubusercontent.com/91785152/207814568-f7fe984b-d017-43a1-ba48-859a75202db2.jpg)
![9c4c553a-0950-417e-beb7-3432d9454eea](https://user-images.githubusercontent.com/91785152/207814929-089b337a-05d5-4292-844d-33a42035efb7.jpg)

--------------------------------------------------------------
### Odpowiednie pomoce wyszukiwania dla obszaru zbytu:

![image](https://user-images.githubusercontent.com/91785152/212666906-4ad36901-19ff-408d-93c9-7e7d306c5c54.png)

#### Przykład: Mennica - tr. ZSD_VAT_DATE

--------------------------------------------------------------
### Przekazanie parametru select-options do modułu funkcyjnego:

DATA: gt_werks_opt TYPE RSELOPTION.

MOVE-CORRESPONDING so_werks[] TO gt_werks_opt.

![image](https://user-images.githubusercontent.com/91785152/196413115-73fcfaf3-132a-4c11-88c1-482532c18bc6.png)

---------------------------------------------------------------
### Uruchomienie usługi mobilnej:

![36ba0fc3-30d0-48c1-b1e5-5e210d352861](https://user-images.githubusercontent.com/91785152/220081411-bf18c3c5-961b-49d6-989d-58301a432aa9.jpg)
![ba65babd-c6be-405a-adc6-3f8387f6d9f0](https://user-images.githubusercontent.com/91785152/220081423-1de80d5a-563d-4222-b388-69e91518a5ce.jpg)
![e408645b-1070-49ba-a162-b430ceecadda](https://user-images.githubusercontent.com/91785152/220081470-9da2e269-7adb-4d33-a695-3b994e464ad1.jpg)
![74bdbe3b-2dbd-4811-b44c-c761de9d7a4b](https://user-images.githubusercontent.com/91785152/220081488-2b163ce8-147c-4a3e-ad3a-186fd2e1868a.jpg)

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

#### Sprawdzanie czy stworzony obiekt jest pusty.

IF o_test IS NOT BOUND.

#### Przekonwertowanie daty i czasu, na konkretny typ czasu:

CONVERT TIME STAMP gs_header-date TIME ZONE 'CET' INTO DATE gv_date.

#### Usówanie rekordów które w konkretnym polu posiadają taką samą wartość:

DELETE ADJACENT DUPLICATES FROM lt_text_item COMPARING consignee_id .

#### Zmiana przecinka na kropkę w wartości liczbowej:

REPLACE FIRST OCCURRENCE OF ',' IN ls_intern1-value WITH '.'.

#### Zaokrąglenie liczb do miejsc po przecinku o sumie dwóch pól:

```
*       trzeba zaokrąglić wartość do liczby miesc po przecinku: STELLEN + NKSTELLOF
<lv_any_m_dec> = <ls_data_hlp>-stellen + <ls_data_hlp>-nkstellof.
<lv_any_m> = round( val = <ls_data_hlp>-mittelwert
                            dec = <lv_any_m_dec> ).
```
