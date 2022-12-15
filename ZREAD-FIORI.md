### Helper znajdujący zmienione dane dla partnera biznesowego w SAP FIORI.

![image](https://user-images.githubusercontent.com/91785152/207812633-24d48cff-b0a4-4dc1-a60c-37bc929a85ab.png)

```
CALL METHOD /scmtms/cl_tor_helper_read=>get_tor_address_data
  EXPORTING
    it_root_key    = VALUE #( ( key = gs_header-db_key ) )
  IMPORTING
    et_doc_address = DATA(lt_doc_address).
```
