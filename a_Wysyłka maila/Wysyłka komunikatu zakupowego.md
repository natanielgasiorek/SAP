## Miejsca gdzie dokonujemy zmian w programie drukującym !

![image](https://github.com/natanielgasiorek/SAP/assets/91785152/2fe82ca3-3e13-496f-8527-f71fc7685af1)

![image](https://github.com/natanielgasiorek/SAP/assets/91785152/d7619b0c-47ce-4359-ba43-484868f7cba3)

![image](https://github.com/natanielgasiorek/SAP/assets/91785152/bdfecd89-695b-4bf8-8b69-6cf3d289b685)

![image](https://github.com/natanielgasiorek/SAP/assets/91785152/7ee1e320-7847-48ea-81ee-a32ca72602cb)

![image](https://github.com/natanielgasiorek/SAP/assets/91785152/7686cd10-0ba8-46d5-a27d-ce1c51806bc7)

![image](https://github.com/natanielgasiorek/SAP/assets/91785152/2607f62b-4896-4709-9f26-3f4f6617604f)

## Kod znajdujący się w mofule funkcyjnym:

```
FUNCTION zmm_send_email_sapscript.
*"----------------------------------------------------------------------
*"*"Lokalny interfejs:
*"  IMPORTING
*"     REFERENCE(IV_ADRNR) TYPE  ADRNR
*"     REFERENCE(IV_TCODE) TYPE  CSTRATEGY
*"     REFERENCE(IV_TITLE) TYPE  TDTITLE
*"     REFERENCE(IV_ORDER_NUMBER) TYPE  NA_OBJKEY
*"  TABLES
*"      IT_OTF_DATA STRUCTURE  ITCOO
*"----------------------------------------------------------------------
***********************************************************************
*           DATA DECLARATION                                          *
***********************************************************************
  DATA: lt_pdf_tab TYPE STANDARD TABLE OF tline,
        lt_otf     TYPE STANDARD TABLE OF itcoo.

  DATA: lt_line TYPE STANDARD TABLE OF tline,
        ls_line LIKE LINE OF lt_line,
        lt_text TYPE soli_tab,
        ls_text LIKE LINE OF lt_text.

  DATA: lv_bin_filesize      TYPE so_obj_len,
        lv_bin_filesize_temp TYPE so_obj_len,
        lv_bin_xstr          TYPE xstring,
        lt_binary_content    TYPE solix_tab,
        lv_subject           TYPE so_obj_des,
        lv_title             TYPE so_obj_des,
        lv_sent_to_all       TYPE os_boolean,
        lv_email             TYPE ad_smtpadr,
        ls_comm_values       TYPE   szadr_comm_values.

  DATA: lo_bcs     TYPE REF TO cl_bcs,
        lo_doc_bcs TYPE REF TO cl_document_bcs,
        lo_recep   TYPE REF TO if_recipient_bcs,
        lo_cx_bcx  TYPE REF TO cx_bcs.
***********************************************************************
*           PROCESS                                                   *
***********************************************************************
  CALL FUNCTION 'ADDR_GET_NEXT_COMM_TYPE'
    EXPORTING
      strategy           = iv_tcode
      address_number     = iv_adrnr
    IMPORTING
      comm_values        = ls_comm_values
    EXCEPTIONS
      address_not_exist  = 1
      person_not_exist   = 2
      no_comm_type_found = 3
      internal_error     = 4
      parameter_error    = 5
      OTHERS             = 6.

  lt_otf[] = it_otf_data[].

  IF ls_comm_values-adsmtp-smtp_addr IS NOT INITIAL.

    CALL FUNCTION 'CONVERT_OTF'
      EXPORTING
        format                = 'PDF'
      IMPORTING
        bin_filesize          = lv_bin_filesize
        bin_file              = lv_bin_xstr
      TABLES
        otf                   = lt_otf[]
        lines                 = lt_pdf_tab[]
      EXCEPTIONS
        err_max_linewidth     = 1
        err_format            = 2
        err_conv_not_possible = 3
        OTHERS                = 4.
    IF sy-subrc = 0.

      CALL FUNCTION 'SCMS_XSTRING_TO_BINARY'
        EXPORTING
          buffer     = lv_bin_xstr
        TABLES
          binary_tab = lt_binary_content.
      IF sy-subrc = 0.
        TRY.
            lo_bcs = cl_bcs=>create_persistent( ).

            lv_subject = iv_title.

            CALL FUNCTION 'READ_TEXT'
              EXPORTING
                client   = sy-mandt
                id       = 'ST'
                language = 'L'
                name     = 'ZEMAIL_PURCHASE_MESSAGES'
                object   = 'TEXT'
*               ARCHIVE_HANDLE                = 0
*               LOCAL_CAT                     = ' '
*         IMPORTING
*               HEADER   =
*               OLD_LINE_COUNTER              =
              TABLES
                lines    = lt_line
*         EXCEPTIONS
*               ID       = 1
*               LANGUAGE = 2
*               NAME     = 3
*               NOT_FOUND                     = 4
*               OBJECT   = 5
*               REFERENCE_CHECK               = 6
*               WRONG_ACCESS_TO_ARCHIVE       = 7
*               OTHERS   = 8
              .
            IF sy-subrc = 0.

              LOOP AT lt_line INTO ls_line.
                ls_text-line = ls_line-tdline.
                APPEND ls_text TO lt_text.
              ENDLOOP.

            ENDIF.

            CONCATENATE 'Order number:' iv_order_number INTO lv_title SEPARATED BY space.

            lo_doc_bcs = cl_document_bcs=>create_document(
                    i_type    = 'RAW'
                    i_text    = lt_text[]        "Opcjonalna treść wiadomości
                    i_length  = '12'
                    i_subject = lv_title )."lv_subject ).     "Subject of the Email

            CONCATENATE lv_title '.pdf' INTO lv_title.

            CALL METHOD lo_doc_bcs->add_attachment
              EXPORTING
                i_attachment_type    = 'PDF'
                i_attachment_size    = lv_bin_filesize
                i_attachment_subject = lv_title "lv_subject
                i_att_content_hex    = lt_binary_content.

            CALL METHOD lo_bcs->set_document( lo_doc_bcs ).

            lv_email = ls_comm_values-adsmtp-smtp_addr.

            lo_recep = cl_cam_address_bcs=>create_internet_address( lv_email ).

            CALL METHOD lo_bcs->add_recipient
              EXPORTING
                i_recipient = lo_recep
                i_express   = 'X'.

            CALL METHOD lo_bcs->set_send_immediately
              EXPORTING
                i_send_immediately = 'X'.

            CALL METHOD lo_bcs->send(
              EXPORTING
                i_with_error_screen = 'X'
              RECEIVING
                result              = lv_sent_to_all ).
            IF lv_sent_to_all IS NOT INITIAL.

              COMMIT WORK.

            ENDIF.

          CATCH cx_bcs INTO lo_cx_bcx.

        ENDTRY.

      ENDIF.

    ENDIF.

  ENDIF.
ENDFUNCTION.
```

![image](https://github.com/natanielgasiorek/SAP/assets/91785152/9d7790f1-b53a-4c9b-9f95-11e5947c46ea)
![image](https://github.com/natanielgasiorek/SAP/assets/91785152/07527837-925b-4420-bd7a-90a0af6fdf65)

### Prace wykonane dla Jutrzenki.
