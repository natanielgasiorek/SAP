### Dodanie guzika zapisu do ALV:

```
------------------------------------------------
  handle_toolbar      FOR EVENT toolbar OF cl_gui_alv_grid IMPORTING e_object e_interactive,
------------------------------------------------
  SET HANDLER handle_toolbar      FOR mr_alv.
------------------------------------------------
  METHOD handle_toolbar.

    DATA: gs_toolbar TYPE stb_button.

    CLEAR gs_toolbar.
    MOVE 3 TO gs_toolbar-butn_type.
    APPEND gs_toolbar TO e_object->mt_toolbar.

    CLEAR gs_toolbar.
    MOVE 'SAVE_DATA' TO gs_toolbar-function.
    MOVE icon_system_save TO gs_toolbar-icon.
    MOVE TEXT-011 TO gs_toolbar-quickinfo.
    MOVE 0 TO gs_toolbar-butn_type.
    MOVE space TO gs_toolbar-disabled.
    APPEND gs_toolbar TO e_object->mt_toolbar.

  ENDMETHOD.
  ------------------------------------------------
```
  
 ### Obsłużenie guzika zapisu w ALV:
```
  ------------------------------------------------
    handle_user_command FOR EVENT user_command OF cl_gui_alv_grid IMPORTING e_ucomm,
  ------------------------------------------------
    SET HANDLER handle_user_command FOR mr_alv.
  ------------------------------------------------
    METHOD handle_user_command.

    CASE e_ucomm.
      WHEN 'SAVE_DATA'.
      WHEN OTHERS.
    ENDCASE.

  ENDMETHOD.
  ------------------------------------------------
```
