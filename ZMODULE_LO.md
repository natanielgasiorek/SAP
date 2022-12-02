### Sprawdzenie czy dostawa jest przypisana do zlecenia transportowego głównego.

Link do pytania: https://answers.sap.com/questions/13771125/assigning-the-delivery-to-the-main-transport-order.html

```
DATA:
    lo_tms_docflow      TYPE REF TO cl_tms_docflow_data,
    lt_docflow_erp      TYPE tms_t_doc_flow_scr.

  CREATE OBJECT lo_tms_docflow
    EXPORTING
      iv_doc_type = '06' "outbound delivery
      iv_doc_nr   = <-- outbound delivery number here

  CALL METHOD lo_tms_docflow->get_data_for_display
    EXPORTING
      iv_display_type = if_tms_docflow_c=>view_erp
*     iv_doc_item     =
    IMPORTING
      et_docflow      = lt_docflow_erp
*     ev_internal_int =
    .

  READ TABLE lt_docflow_erp ASSIGNING FIELD-SYMBOL(<docflow_erp>) WITH KEY btd_category_code = 'TO'. "freight order<br>
```

Przykład: Grupa funkcyjna -> ZTM_RF, pakiet -> ZTM -> Zarys

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------
