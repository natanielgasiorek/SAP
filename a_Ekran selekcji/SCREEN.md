----------------------------------------------------------------------------------------------------------------
## Przykładowe tworzenie ekranu selekcji:

```
/Ekran selekcji - wprowadzanie wielu parametrów.
DATA: s_kschl TYPE a904-kschl,
      s_prdha TYPE mara-prdha.

SELECTION-SCREEN BEGIN OF BLOCK a01 WITH FRAME TITLE TEXT-001.
  SELECTION-SCREEN SKIP 1. <- Jeżeli chcemy pominąć jedną linijkę.
  SELECT-OPTIONS: so_kschl FOR s_kschl OBLIGATORY <- Jeżeli pole ma być obowiązkowe.
  SELECT-OPTIONS: so_prdha FOR s_prdha.
SELECTION-SCREEN END OF BLOCK a01.

/Ekran selekcji - wprowadzenie jednego parametru.
SELECTION-SCREEN BEGIN OF BLOCK a01 WITH FRAME TITLE TEXT-001.
  PARAMETERS: pa_datum TYPE sy-datum OBLIGATORY.
SELECTION-SCREEN END OF BLOCK a01.

/Ekran selekcji - przyciski.
SELECTION-SCREEN BEGIN OF BLOCK a02 WITH FRAME TITLE TEXT-002.
  SELECTION-SCREEN   PUSHBUTTON 2(34) TEXT-b03 USER-COMMAND but01.
  SELECTION-SCREEN   PUSHBUTTON 40(34) TEXT-b04 USER-COMMAND but02.
SELECTION-SCREEN END OF BLOCK a02.
```

----------------------------------------------------------------------------------------------------------------
## Ekran selekcji z ikonami:

![image](https://user-images.githubusercontent.com/91785152/224555418-49a41519-b601-4882-b906-2d7aaa76764c.png)

### Kod:

```
***********************************************************************
*           SCREEN                                                    *
***********************************************************************
SELECTION-SCREEN BEGIN OF BLOCK a01 WITH FRAME TITLE TEXT-001.
  SELECT-OPTIONS: so_kunnr FOR s_kunnr.
  SELECT-OPTIONS: so_locno FOR s_locno.
  SELECT-OPTIONS: so_post  FOR s_post.
  SELECT-OPTIONS: so_zone  FOR s_zone.

  SELECTION-SCREEN SKIP 1.

  SELECTION-SCREEN BEGIN OF LINE.
    SELECTION-SCREEN COMMENT 1(31)  text_001.
    PARAMETERS: cha1 AS CHECKBOX DEFAULT 'X'.
    SELECTION-SCREEN COMMENT 35(8)  text_002.
    PARAMETERS: cha2 AS CHECKBOX DEFAULT 'X'.
    SELECTION-SCREEN COMMENT 46(8)  text_003.
    PARAMETERS: cha3 AS CHECKBOX DEFAULT 'X'.
    SELECTION-SCREEN COMMENT 57(4)  text_004.
  SELECTION-SCREEN END OF LINE.

SELECTION-SCREEN END OF BLOCK a01.

***********************************************************************
*           INITIALIZATION                                                 *
***********************************************************************
INITIALIZATION.
  text_001 = 'Status:'.
  text_002 = '@08@'.
  text_003 = '@09@'.
  text_004 = '@0A@'.
```
----------------------------------------------------------------------------------------------------------------
## Ekran selekcji z dezaktywacją pól:

![image](https://user-images.githubusercontent.com/91785152/225346801-91f131b5-43de-495c-a2a0-eb19711e195d.png)
![image](https://user-images.githubusercontent.com/91785152/225346892-c9f76943-f05a-479e-b816-5583fe39e333.png)

### Kod:

```
***********************************************************************
*           SCREEN                                                    *
***********************************************************************
SELECTION-SCREEN BEGIN OF BLOCK a01 WITH FRAME TITLE TEXT-001.
  PARAMETERS: pa_bukrs TYPE acdoca-rbukrs OBLIGATORY.
  PARAMETERS: pa_datum TYPE datum OBLIGATORY DEFAULT sy-datum.
  SELECT-OPTIONS: so_lifnr FOR s_lifnr.
  SELECTION-SCREEN SKIP 1.
  PARAMETERS: ra_alv  RADIOBUTTON GROUP rad1 USER-COMMAND but01, " <- To jest ważne do zaznaczenia
              ra_save RADIOBUTTON GROUP rad1.
  SELECTION-SCREEN SKIP 1.
  PARAMETERS: ch_fak  AS CHECKBOX DEFAULT 'X',
              ch_dost AS CHECKBOX.
SELECTION-SCREEN END OF BLOCK a01.
***********************************************************************
*           INITIALIZATION                                            *
***********************************************************************
INITIALIZATION. 

AT SELECTION-SCREEN.
* Edycja ekranu selekcji gdy wybierze się zapis do bazy danych
  IF sy-ucomm = 'BUT01'.
    LOOP AT SCREEN.
      IF ra_save IS NOT INITIAL.
        ch_fak = 'X'.
        ch_dost = 'X'.
        pa_datum = sy-datum.
        CLEAR: so_lifnr[].         IF screen-name CS 'SO_LIFNR'
          OR screen-name CS 'CH_FAK'
          OR screen-name CS 'CH_DOST'
          OR screen-name CS 'PA_DATUM'.
          screen-input = 0.
          MODIFY SCREEN.
        ENDIF.
      ENDIF.
    ENDLOOP.
  ENDIF. 
  
  AT SELECTION-SCREEN OUTPUT.
  LOOP AT SCREEN.
    IF ra_save IS NOT INITIAL.
      ch_fak = 'X'.
      ch_dost = 'X'.
      pa_datum = sy-datum.
      CLEAR: so_lifnr[].
      IF screen-name CS 'SO_LIFNR'
      OR screen-name CS 'CH_FAK'
      OR screen-name CS 'CH_DOST'
      OR screen-name CS 'PA_DATUM'.
        screen-input = 0.
        MODIFY SCREEN.
      ENDIF.
    ENDIF.
  ENDLOOP.
**********************************************************
```
----------------------------------------------------------------------------------------------------------------

## Wstawienie radiobuttonów z większą nazwą niż standard:

![image](https://user-images.githubusercontent.com/91785152/228186003-80dad2e3-ab3a-44f3-a495-80b363e903c7.png)

### Kod:

```
************************************************
* Modyfikacja, 27.03.2023
* Jarosław G.
* Modyfikacja raportu wyników kontroli
************************************************
SELECTION-SCREEN SKIP 1.
SELECTION-SCREEN BEGIN OF BLOCK typ WITH FRAME TITLE text-s03.
SELECTION-SCREEN BEGIN OF LINE.
PARAMETERS: ra_old  RADIOBUTTON GROUP rad1.
SELECTION-SCREEN COMMENT (40) text-011.
SELECTION-SCREEN END OF LINE.

SELECTION-SCREEN BEGIN OF LINE.
  PARAMETERS: ra_new  RADIOBUTTON GROUP rad1.
SELECTION-SCREEN COMMENT (40) text-012.
SELECTION-SCREEN END OF LINE.
SELECTION-SCREEN END OF BLOCK typ.
************************************************
* Koniec modyfikacji
************************************************
```
