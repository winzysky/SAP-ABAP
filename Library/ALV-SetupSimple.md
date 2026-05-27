REPORT ZABAPTRANINGTP.

*---------------------------------------------------------------------*
* Mockup ALV Example
* Purpose :
* - Create sample data manually using PERFORM
* - Display data in ALV Grid
* - Show icon in ALV based on gender value
*---------------------------------------------------------------------*

*---------------------------------------------------------------------*
* Structure for mockup data
*---------------------------------------------------------------------*
TYPES : BEGIN OF ty_data,
          id            TYPE n,
          name          TYPE char15,
          gender        TYPE char1,
          gender_icon   TYPE icon_d,
        END OF ty_data.

*---------------------------------------------------------------------*
* Internal table for sample data
*---------------------------------------------------------------------*
DATA : lt_mockup TYPE TABLE OF ty_data,
       ls_mockup TYPE ty_data.

*---------------------------------------------------------------------*
* ALV field catalog
*---------------------------------------------------------------------*
DATA : gt_fieldcat TYPE slis_t_fieldcat_alv,
       gs_fieldcat TYPE slis_fieldcat_alv.

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
      ls_mockup-gender_icon = ICON_LED_GREEN.

    WHEN 'F'.
      ls_mockup-gender_icon = ICON_LED_RED.
  ENDCASE.

  APPEND ls_mockup TO lt_mockup.

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
  APPEND gs_fieldcat TO gt_fieldcat.

  CLEAR gs_fieldcat.
  gs_fieldcat-fieldname = 'GENDER_ICON'.
  gs_fieldcat-seltext_m = 'Gender'.
  gs_fieldcat-col_pos   = 3.

* Mark field as icon type for ALV rendering
  gs_fieldcat-icon = 'X'.

  APPEND gs_fieldcat TO gt_fieldcat.

ENDFORM.

*---------------------------------------------------------------------*
* Display internal table in ALV Grid
*---------------------------------------------------------------------*
FORM display_alv.

  CALL FUNCTION 'REUSE_ALV_GRID_DISPLAY'
    EXPORTING
      i_callback_program = sy-repid
      it_fieldcat        = gt_fieldcat
    TABLES
      t_outtab           = lt_mockup
    EXCEPTIONS
      program_error      = 1
      OTHERS             = 2.

ENDFORM.
