## Otwarte pozycje na koncie dostawcy:

```
      CALL FUNCTION 'BAPI_AP_ACC_GETOPENITEMS'
        EXPORTING
          companycode = pa_bukrs
          vendor      = ls_lifnr-konto
          keydate     = pa_datum
*         NOTEDITEMS  = ' '
*     IMPORTING
*         RETURN      =
        TABLES
          lineitems   = gt_bapi_temp.
```

#### Przykład Veolia - Program ZPS_INVEST_ZOBOWIAZANIA.
-------------------------------------------------------------------------------------
