*---------------------------------------------------------------------*
* Mockup ALV Example
*
* Purpose :
* - Create sample data manually using PERFORM
* - Display data in ALV Grid
* - Show icon based on gender value
* - Apply ALV layout enhancements
*   > Zebra pattern
*   > Row color by condition
*   > Report header information
*   > adjust a little bit fieldcat
*   > Add Double Click and Hotspot Click
*   > Bench Code For Filter (Copy Table From lt_mockup)
*   > Filter Data (Male, Female)
*---------------------------------------------------------------------*
*---------------------------------------------------------------------*

*---------------------------------------------------------------------*
* Structure for mockup data
*---------------------------------------------------------------------*
TYPES : BEGIN OF ty_data,
          id          TYPE n,
          name        TYPE char15,
          gender      TYPE char1,
          gender_icon TYPE icon_d,
          line_color  TYPE char4,
        END OF ty_data.

*---------------------------------------------------------------------*
* Internal table for sample data
*---------------------------------------------------------------------*
DATA : lt_mockup TYPE TABLE OF ty_data,
       ls_mockup TYPE ty_data.

DATA : lt_mockup_all TYPE TABLE OF ty_data.

*---------------------------------------------------------------------*
* ALV field catalog
*---------------------------------------------------------------------*
DATA : gt_fieldcat TYPE slis_t_fieldcat_alv,
       gs_fieldcat TYPE slis_fieldcat_alv.

*---------------------------------------------------------------------*
* ALV layout settings
*---------------------------------------------------------------------*
DATA gs_layout TYPE slis_layout_alv.
PERFORM build_layout.

*---------------------------------------------------------------------*
* Build ALV columns
*---------------------------------------------------------------------*
PERFORM build_fieldcat.

*---------------------------------------------------------------------*
* Generate mockup data
*---------------------------------------------------------------------*
DATA : index TYPE n.

PERFORM addtotable USING 'John'  'M'.
PERFORM addtotable USING 'Mary'  'F'.
PERFORM addtotable USING 'Peter' 'M'.


*---------------------------------------------------------------------*
* Bench Code For Filter With UserCommand
*---------------------------------------------------------------------*
lt_mockup_all = lt_mockup.

*---------------------------------------------------------------------*
* Display result in ALV
*---------------------------------------------------------------------*
PERFORM display_alv.

*---------------------------------------------------------------------*
* Add data into internal table
* Assign icon based on gender value
*---------------------------------------------------------------------*
FORM addtotable USING p_name p_gender.

  index = index + 1.

  ls_mockup-id = index.
  ls_mockup-name = p_name.
  ls_mockup-gender = p_gender.

  CASE ls_mockup-gender.
    WHEN 'M'.
      ls_mockup-gender_icon = icon_led_green.
      ls_mockup-line_color = 'C510'.

    WHEN 'F'.
      ls_mockup-gender_icon = icon_led_red.
      ls_mockup-line_color = 'C610'.
  ENDCASE.

  APPEND ls_mockup TO lt_mockup.

ENDFORM.

*---------------------------------------------------------------------*
* Handle ALV user interactions
* - Triggered by double click or hotspot click
*---------------------------------------------------------------------*

FORM user_command USING r_ucomm      LIKE sy-ucomm
                         rs_selfield TYPE slis_selfield.

  CASE r_ucomm.

    WHEN '&IC1'. " double click / hotspot click

      READ TABLE lt_mockup INTO ls_mockup
           INDEX rs_selfield-tabindex.

      IF sy-subrc = 0.

        MESSAGE |Selected : { ls_mockup-name }|
          TYPE 'I'.

      ENDIF.

*------------------------------------------------------------------*
* Show male records only
*------------------------------------------------------------------*
    WHEN 'MALE'.
      lt_mockup = lt_mockup_all.
      DELETE lt_mockup WHERE gender <> 'M'.

      rs_selfield-refresh = 'X'.

*------------------------------------------------------------------*
* Show female records only
*------------------------------------------------------------------*
    WHEN 'FEMALE'.
      lt_mockup = lt_mockup_all.
      DELETE lt_mockup WHERE gender <> 'F'.

      rs_selfield-refresh = 'X'.

    WHEN 'RESET'.

      lt_mockup = lt_mockup_all.

      rs_selfield-refresh = 'X'.

  ENDCASE.

ENDFORM.

*---------------------------------------------------------------------*
* ALV layout settings
*---------------------------------------------------------------------*
FORM build_layout.
  gs_layout-zebra = 'X'.
  "gs_layout-colwidth_optimize = 'X'.
  gs_layout-info_fieldname = 'LINE_COLOR'.

ENDFORM.

*---------------------------------------------------------------------*
* Configure ALV column properties
*---------------------------------------------------------------------*
FORM build_fieldcat.

  CLEAR gs_fieldcat.
  gs_fieldcat-fieldname = 'ID'.
  gs_fieldcat-seltext_m = 'ID'.
  gs_fieldcat-col_pos   = 1.
  APPEND gs_fieldcat TO gt_fieldcat.

  CLEAR gs_fieldcat.
  gs_fieldcat-fieldname = 'NAME'.
  gs_fieldcat-seltext_m = 'Name'.
  gs_fieldcat-col_pos   = 2.
  gs_fieldcat-just = 'C'.   "Center
  gs_fieldcat-hotspot = 'X'.
  APPEND gs_fieldcat TO gt_fieldcat.

  CLEAR gs_fieldcat.
  gs_fieldcat-fieldname = 'GENDER_ICON'.
  gs_fieldcat-seltext_m = 'Gender'.
*  gs_fieldcat-no_out = 'X'. " Hide Column
*  gs_fieldcat-tooltip = 'Gender status'.
  gs_fieldcat-col_pos   = 3.

* Mark field as icon type for ALV rendering
  gs_fieldcat-icon = 'X'.

  APPEND gs_fieldcat TO gt_fieldcat.

ENDFORM.

*---------------------------------------------------------------------*
* Set custom ALV toolbar
*---------------------------------------------------------------------*
FORM set_pf_status USING rt_extab TYPE slis_t_extab.

  SET PF-STATUS 'ZALV_STATUS'.

ENDFORM.

*---------------------------------------------------------------------*
* Build ALV report header
* - Display title and record count
*---------------------------------------------------------------------*
FORM top_of_page.

  DATA: lt_header TYPE slis_t_listheader,
        ls_header TYPE slis_listheader.

  ls_header-typ = 'H'.
  ls_header-info = 'ALV Mockup Demo'.
  APPEND ls_header TO lt_header.

  ls_header-typ = 'S'.
  ls_header-key = 'Total Records:'.
  ls_header-info = lines( lt_mockup ).
  APPEND ls_header TO lt_header.

  CALL FUNCTION 'REUSE_ALV_COMMENTARY_WRITE'
    EXPORTING
      it_list_commentary = lt_header.

ENDFORM.

*---------------------------------------------------------------------*
* Display internal table in ALV Grid
*---------------------------------------------------------------------*
FORM display_alv.

  CALL FUNCTION 'REUSE_ALV_GRID_DISPLAY'
    EXPORTING
      i_callback_program       = sy-repid
      i_callback_user_command  = 'USER_COMMAND'
      i_callback_pf_status_set = 'SET_PF_STATUS'
      i_callback_top_of_page   = 'TOP_OF_PAGE'
      is_layout                = gs_layout
      it_fieldcat              = gt_fieldcat
    TABLES
      t_outtab                 = lt_mockup
    EXCEPTIONS
      program_error            = 1
      OTHERS                   = 2.

ENDFORM.
