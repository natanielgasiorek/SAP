### Pętle:

#### Pętla grupowana - działa na zasadzie pogrupowania według klucza a następnie w kolejnej pętli idzie po wszystkich rekordach spełniających tą instrukcję.

```
LOOP AT lt_offers_pos INTO ls_offers_pos GROUP BY ls_offers_pos-vbeln ASCENDING.

lv_order = |{ ls_offers_pos-vbeln ALPHA = IN }|.

CLEAR: lt_item[], lt_itemx[].

LOOP AT GROUP ls_offers_pos INTO DATA(ls_pos).

APPEND INITIAL LINE TO lt_item ASSIGNING FIELD-SYMBOL(<item_pos>).
APPEND INITIAL LINE TO lt_itemx ASSIGNING FIELD-SYMBOL(<itemx_pos>).
<item_pos>-itm_number = ls_pos-posnr.
<itemx_pos>-itm_number = ls_pos-posnr.
<item_pos>-ship_type = lv_vsart.
<itemx_pos>-ship_type = abap_true.
<itemx_pos>-updateflag = 'U'.

ENDLOOP.
```
