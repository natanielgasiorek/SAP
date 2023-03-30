### Autoryzacja wyświetlania wrażliwych danych dla STATUSU posiadającego 9 możliwości.

![image](https://user-images.githubusercontent.com/91785152/228840912-83b7ca04-251c-408d-8f22-3886f3726fca.png)
![image](https://user-images.githubusercontent.com/91785152/228841020-f5938be2-ae88-4904-a052-cfe51324def0.png)

#### KOD:
```
  TYPES: BEGIN OF ty_int,
           order_id TYPE zsi_order_id,
         END OF ty_int,
         tt_int TYPE STANDARD TABLE OF ty_int.
  DATA: lt_int TYPE tt_int,
        ls_int TYPE ty_int.
```
```
  DO 9 TIMES.
    CLEAR ls_auth-auth.
    ls_auth-order_status = ls_auth-order_status + 1.
    AUTHORITY-CHECK OBJECT 'ZSI_STATUS'
         ID 'ZSTATUS_AC' FIELD ls_auth-order_status
         ID 'ACTVT' FIELD '03'.
    IF sy-subrc = 0.
      ls_auth-auth = 'X'.
    ENDIF.
    APPEND ls_auth TO lt_auth.
ENDDO.
```
```
      CLEAR: g_t_display_new-zzpesel,
      g_t_display_new-zzobywatelstwo,
      g_t_display_new-zznumerdok,
      g_t_display_new-zzdataur,
      g_t_display_new-zztypdok.
      READ TABLE lt_auth INTO ls_auth WITH TABLE KEY order_status = lt_shop_h-order_status.
      IF ls_auth-auth = 'X'.
        g_t_display_new-zzpesel          = lt_shop_h-zzpesel.
        g_t_display_new-zzobywatelstwo   = lt_shop_h-zzobywatelstwo.
        g_t_display_new-zznumerdok       = lt_shop_h-zznumerdok.
        g_t_display_new-zzdataur         = lt_shop_h-zzdataur.
        g_t_display_new-zztypdok         = lt_shop_h-zztypdok.
      ENDIF.
```

#### Przykład ZSI_PRCOC -> ZSD_INT_PROC_NEW_F03_ZI : MENNICA
