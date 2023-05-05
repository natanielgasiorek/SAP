## Szybka ALV z zebrą gdzie wsadzamy tylko tabelę.

```
  DATA gr_table TYPE REF TO cl_salv_table.
  DATA: gr_functions TYPE REF TO cl_salv_functions.
  DATA: gr_display   TYPE REF TO cl_salv_display_settings.

  cl_salv_table=>factory(
  IMPORTING
  r_salv_table = gr_table
  CHANGING
  t_table = gt_data_all ).

  gr_functions = gr_table->get_functions( ).
  gr_functions->set_all( abap_true ).

  gr_display = gr_table->get_display_settings( ).
  gr_display->set_striped_pattern( cl_salv_display_settings=>true ).

  gr_table->display( ).
```
