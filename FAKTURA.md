### Poradnik, jak pobrać tekst z nagłówka faktury do programu:

Tekst z nagłówka faktury znajdziemy w transakcji VF03.

Skok do -> Nagłówek -> Szczegóły nagłówka = T. nagłówka

Aby pobrać dany tekst potrzebujemy jego ID i nazwę obiektu.

![4b62fbe2-2b9d-4a19-9dbf-c7ed704ba075](https://user-images.githubusercontent.com/91785152/204576883-ff914dd7-de71-435b-8238-9618ad97f71e.jpg)

![image](https://user-images.githubusercontent.com/91785152/204576960-7910d28f-0041-472f-bc5a-f875c5f491cb.png)

Aby użyć tego tekstu używamy MF:

DATA: lt_line  TYPE TABLE OF tline.

CALL FUNCTION 'READ_TEXT'
    EXPORTING
      client                  = sy-mandt
      id                      = '0001'
      language                = sy-langu
      name                    = lv_vbeln
      object                  = 'VBRK'
*     ARCHIVE_HANDLE          = 0
*     LOCAL_CAT               = ' '
*       IMPORTING
*     HEADER                  =
*     OLD_LINE_COUNTER        =
    TABLES
      lines                   = lt_line
    EXCEPTIONS
      id                      = 1
      language                = 2
      name                    = 3
      not_found               = 4
      object                  = 5
      reference_check         = 6
      wrong_access_to_archive = 7
      OTHERS                  = 8.
  IF sy-subrc <> 0.
    MESSAGE ID sy-msgid TYPE sy-msgty NUMBER sy-msgno
    WITH sy-msgv1 sy-msgv2 sy-msgv3 sy-msgv4.
  ENDIF.
  
  Przykład: ZXVVFU02 - Mennica.
  
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------
