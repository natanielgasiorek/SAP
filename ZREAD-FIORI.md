
```
CALL METHOD /scmtms/cl_tor_helper_read=>get_tor_address_data
  EXPORTING
    it_root_key    = VALUE #( ( key = gs_header-db_key ) )
  IMPORTING
    et_doc_address = DATA(lt_doc_address).
```
