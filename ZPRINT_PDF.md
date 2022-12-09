```
FORM print.

  DATA: lt_makt TYPE zmakt_t.

  gv_fp_outputparams-nodialog = 'X'.
  "gv_fp_outputparams-preview = ' '.
  gv_fp_outputparams-device = 'PRINTER'.
  gv_fp_outputparams-copies = 1.
  gv_fp_outputparams-reqnew = 'X'.
  gv_fp_outputparams-reqimm = 'X'.
  gv_fp_outputparams-reqdel = 'X'.

  SELECT SINGLE padest FROM tsp03d
    INTO gv_fp_outputparams-dest
    WHERE name = gv_printer.

  MOVE-CORRESPONDING gt_print TO lt_makt.
***********************************************************************
*           PROGRAM DRUKUJCY ADOBE FORMS                              *
***********************************************************************
  CALL FUNCTION 'FP_JOB_OPEN'
    CHANGING
      ie_outputparams = gv_fp_outputparams
    EXCEPTIONS
      cancel          = 1
      usage_error     = 2
      system_error    = 3
      internal_error  = 4
      OTHERS          = 5.
  IF sy-subrc <> 0.
* Implement suitable error handling here
  ENDIF.
***********************************************************************
  CALL FUNCTION 'FP_FUNCTION_MODULE_NAME'
    EXPORTING
      i_name     = gv_formname
    IMPORTING
      e_funcname = gv_fm_names.
*     E_INTERFACE_TYPE           =
*     EV_FUNCNAME_INBOUND        =
***********************************************************************
*  lv_fp_formoutput-getpdf = 'X'.
  CALL FUNCTION gv_fm_names
    EXPORTING
      /1bcdwb/docparams  = gv_fp_docparams
      im_makt_t          = lt_makt
    IMPORTING
      /1bcdwb/formoutput = gv_fp_formoutput
    EXCEPTIONS
      usage_error        = 1
      system_error       = 2
      internal_error     = 3.
  IF sy-subrc <> 0.
  ENDIF.
***********************************************************************
  CALL FUNCTION 'FP_JOB_CLOSE'
*   IMPORTING
*     E_RESULT             =
    EXCEPTIONS
      usage_error    = 1
      system_error   = 2
      internal_error = 3
      OTHERS         = 4.
  IF sy-subrc <> 0.
* Implement suitable error handling here
  ENDIF.

ENDFORM.
```
