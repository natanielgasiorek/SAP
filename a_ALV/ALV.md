## ALV

```
CLASS lcl_view DEFINITION FINAL.

  PUBLIC SECTION.
    CONSTANTS mc_dynnr  TYPE sy-dynnr VALUE '0100'.

    DATA: mr_alv TYPE REF TO cl_gui_alv_grid.
    DATA: mr_cc  TYPE REF TO cl_gui_custom_container.
    DATA: mt_fcat TYPE lvc_t_fcat.

    DATA: mt_data TYPE tt_alv." <-- Wpisać typ tabeli z jakiej czerpie dane

    METHODS:
      constructor    IMPORTING it_data TYPE tt_alv, " <-- Wpisać typ tabeli z jakiej czerpie dane
      display,
      build_alv      IMPORTING iv_dynnr      TYPE sy-dynnr,
      run_scr_module IMPORTING iv_mod        TYPE char3,
      refresh_alv.
    METHODS:
      handle_toolbar      FOR EVENT toolbar OF cl_gui_alv_grid IMPORTING e_object e_interactive,
      handle_user_command FOR EVENT user_command OF cl_gui_alv_grid IMPORTING e_ucomm.

  PROTECTED SECTION.

  PRIVATE SECTION.

    METHODS:
      build_fcat IMPORTING it_data_structure TYPE ANY TABLE
                 EXPORTING et_fieldcat       TYPE lvc_t_fcat,
      set_layout EXPORTING es_layout TYPE lvc_s_layo,
      modify_fieldcatalog CHANGING ct_fieldcat TYPE lvc_t_fcat,
      run_pbo,
      run_pai    RETURNING VALUE(ev_ucomm) TYPE syucomm.

ENDCLASS.

CLASS lcl_view IMPLEMENTATION.

  METHOD constructor.
    mt_data[] = it_data[].
  ENDMETHOD.                    "constructor

  METHOD display.
    CALL SCREEN 0100.           "mc_dynnr.
  ENDMETHOD.

  METHOD run_scr_module.
    CASE iv_mod.
      WHEN 'PBO'.
        run_pbo( ).
      WHEN 'PAI'.
        run_pai( ).
    ENDCASE.
  ENDMETHOD.                    "run_scr_module

  METHOD run_pbo.
***********************************************************
* PBO
***********************************************************
    SET PF-STATUS 'STATUS_0100'.
    SET TITLEBAR 'TITLE_0100'.

    build_alv( mc_dynnr ).

  ENDMETHOD.                    "run_pbo

  METHOD run_pai.
***********************************************************
*  PAI - ev_ucomm: user command
**********************************************************

    CASE sy-ucomm.
      WHEN 'BACK' OR 'CANCEL'.
        LEAVE TO SCREEN 0.
      WHEN 'EXIT'.
        LEAVE PROGRAM.
      WHEN OTHERS.
        ev_ucomm = sy-ucomm.
    ENDCASE.

  ENDMETHOD.                    "run_pai

  METHOD build_alv.
***********************************************************
* Print ALV
***********************************************************
    DATA: "lt_fcat   TYPE lvc_t_fcat,
      ls_layo   TYPE lvc_s_layo,
      lv_title  TYPE lvc_title,
      ls_layout TYPE disvariant.
    DATA: ls_stable TYPE lvc_s_stbl.

    CLEAR ls_stable.

    FIELD-SYMBOLS: <lt_tab>  TYPE ANY TABLE.
    ASSIGN mt_data TO <lt_tab>.
    CHECK sy-subrc = 0.
    IF mr_cc IS NOT BOUND.

      CREATE OBJECT mr_cc
        EXPORTING
          container_name = 'CC_0100'
        EXCEPTIONS
          OTHERS         = 99.
      IF sy-subrc = 0.

        CREATE OBJECT mr_alv
          EXPORTING
            i_parent = mr_cc
*           i_appl_events = 'X'
          EXCEPTIONS
            OTHERS   = 99.
        IF sy-subrc = 0.

          SET HANDLER handle_toolbar      FOR mr_alv.
          SET HANDLER handle_user_command FOR mr_alv.
          REFRESH mt_fcat.
          build_fcat( EXPORTING it_data_structure = <lt_tab>
                      IMPORTING et_fieldcat = mt_fcat ).
          modify_fieldcatalog( CHANGING ct_fieldcat = mt_fcat ).
          "set_layout( IMPORTING es_layout = ls_layo ).
          ls_layout-report = sy-repid.

          CALL METHOD mr_alv->set_table_for_first_display
            EXPORTING
              is_variant      = ls_layout
              is_layout       = ls_layo
              i_save          = 'A'
            CHANGING
              it_outtab       = mt_data
              it_fieldcatalog = mt_fcat
            EXCEPTIONS
              OTHERS          = 99.

          CALL METHOD mr_alv->set_ready_for_input
            EXPORTING
              i_ready_for_input = 0.

        ENDIF.
      ENDIF.

      mr_alv->get_frontend_layout( IMPORTING es_layout = ls_layo ).
      set_layout( IMPORTING es_layout = ls_layo ).
      mr_alv->set_frontend_layout( ls_layo ).
      refresh_alv( ).
    ENDIF.
  ENDMETHOD.                    "build_alv
  METHOD build_fcat.
    CLEAR: et_fieldcat[].

    CALL FUNCTION 'LVC_FIELDCATALOG_MERGE'
      EXPORTING
        i_structure_name       = 'ZTM_CUSTOMER_ZONE_ALV_ST' " <-- Wpisać strukturę jaka będzie wyświetlana
        i_client_never_display = 'X'
      CHANGING
        ct_fieldcat            = et_fieldcat[].

  ENDMETHOD.                    "build_fcat

  METHOD set_layout.
*    es_layout-grid_title = TEXT-003.
    es_layout-cwidth_opt = 'X'.
    es_layout-col_opt = 'X'.
    es_layout-zebra = 'X'.
    es_layout-no_keyfix = 'X'.
    "es_layout-no_rowmark = 'X'.
    es_layout-sel_mode = 'A'.
*    es_layout-info_fname = 'ROWCOLOR'.
*     es_layout-ctab_fname = 'CELLCOLOR'.
  ENDMETHOD.                    "set_layout

  METHOD modify_fieldcatalog.
    FIELD-SYMBOLS: <lf_fcat> TYPE lvc_s_fcat,
                   <fs_temp> TYPE any,
                   <fs_text> TYPE any.

    DATA: lv_message(8),
          lv_index(10).

* modyfikacja ALV
    LOOP AT ct_fieldcat ASSIGNING <lf_fcat>.
*      <lf_fcat>-col_opt = 'X'.
      CASE <lf_fcat>-fieldname.
*        WHEN 'ORT01'.
*         <lf_fcat>-style = 4.    "Dodanie koloru do kolumny (jasny żółty)
*         <lf_fcat>-scrtext_s = 'Przyp.'. "Krótki tekst
*         <lf_fcat>-scrtext_l = 'Przypisanie'. "Długi tekst
        WHEN OTHERS.
      ENDCASE.
    ENDLOOP.

  ENDMETHOD.                    "modify_fieldcatalog

  METHOD refresh_alv.
    "mr_alv->refresh_table_display( ).
    DATA: ls_stable TYPE lvc_s_stbl.

    ls_stable-row = 'X'.
    ls_stable-col = 'X'.

    CALL METHOD mr_alv->refresh_table_display
      EXPORTING
        is_stable = ls_stable.
    cl_gui_cfw=>flush( ).
  ENDMETHOD.                    "refresh_alv

  METHOD handle_toolbar.

  ENDMETHOD.

  METHOD handle_user_command.

  ENDMETHOD.

ENDCLASS.
```
