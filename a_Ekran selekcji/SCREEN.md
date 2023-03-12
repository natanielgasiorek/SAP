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
