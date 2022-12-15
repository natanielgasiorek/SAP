#### BAPI do pobierania danych 'Partnera biznesowego'"

```
CALL FUNCTION 'BAPI_BUPA_ADDRESS_GETDETAIL'
  EXPORTING
    businesspartner = gs_header-party_id
  IMPORTING
    addressdata     = ls_adres
  TABLES
    bapiadtel       = lt_bapiadtel.
 ```
 
 ------------------------------------------------------------------------------------------------------------------------------------------------------------------------
