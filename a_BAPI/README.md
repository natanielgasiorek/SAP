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
## Edycja dokumentu sprzedaży:

```
    DATA: ls_header_in   TYPE bapisdh1,
          ls_header_inx  TYPE bapisdh1x,
          lv_order       TYPE vbeln_va,
          lt_item        TYPE STANDARD TABLE OF bapisditm,
          lt_itemx       TYPE STANDARD TABLE OF bapisditmx,
          lt_return      TYPE bapiret2_t,
          lt_return_temp TYPE bapiret2_t.
```

```
            CALL FUNCTION 'BAPI_SALESORDER_CHANGE'
              EXPORTING
                salesdocument    = lv_order
                order_header_in  = ls_header_in
                order_header_inx = ls_header_inx
*               SIMULATION       =
*               BEHAVE_WHEN_ERROR           = ' '
*               INT_NUMBER_ASSIGNMENT       = ' '
*               LOGIC_SWITCH     =
*               NO_STATUS_BUF_INIT          = ' '
              TABLES
                return           = lt_return_temp
                order_item_in    = lt_item
                order_item_inx   = lt_itemx.

            READ TABLE lt_return_temp TRANSPORTING NO FIELDS WITH KEY type = 'E'.
            IF sy-subrc <> 0.
              CALL FUNCTION 'BAPI_TRANSACTION_COMMIT'
                EXPORTING
                  wait = abap_true
*       IMPORTING
*                 RETURN        =
                .
```
