### Deklaracja ALV:

```
* Deklaracja ALV
CLASS lcl_view DEFINITION DEFERRED.
DATA: lo_alv TYPE REF TO lcl_view.
```

### Wywołanie obiektu ALV:

```
** przeniesienie danych do ALV
CREATE OBJECT lo_alv EXPORTING it_data = gt_alv.
lo_alv->display( ).
```
