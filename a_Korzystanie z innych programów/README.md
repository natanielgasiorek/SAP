## Pobranie danych z raportu ALV używając innego programu:

```
**********************************************************
* Odpalenie programu rfitemap (fbl1n) i pobranie danych z ALV oraz wybranie z niego dostawców

    cl_salv_bs_runtime_info=>set(
       EXPORTING
         display  = abap_false
         metadata = abap_false
         data     = abap_true
      ).     
      
    SUBMIT rfitemap
    WITH  kd_bukrs-low = pa_bukrs
    WITH kd_lifnr IN so_lifnr
    AND RETURN
    EXPORTING LIST TO MEMORY.    
    
    TRY.
        " get data from SALV model
        cl_salv_bs_runtime_info=>get_data_ref(
              IMPORTING
                r_data = lo_data
        ).
      CATCH cx_salv_bs_sc_runtime_info.
    ENDTRY.
    
    ASSIGN lo_data->* TO FIELD-SYMBOL(<data>).
    CHECK <data> IS ASSIGNED.
    MOVE-CORRESPONDING <data> TO gt_lifnr.     
    
" Jeżeli nie wywołasz tej metody z tymi parametrami to nie odpali się nasz raport
    cl_salv_bs_runtime_info=>set(
       EXPORTING
         display  = abap_true
         metadata = abap_true
         data     = abap_true
      ).ma menu kontekstowe
```
----------------------------------------------------------------------------------------------------------------
