จะวางโค้ดก่อน อย่าเพิ่งทำอะไร

" ANLC Keys
TYPES : BEGIN OF ty_ackey,
          bukrs TYPE anlc-bukrs,
          anln1 TYPE anlc-anln1,
          anln2 TYPE anlc-anln2,
        END OF ty_ackey.

" ANLA Keys
TYPES : BEGIN OF ty_aakey,
          bukrs TYPE anla-bukrs,
          anln1 TYPE anla-anln1,
          anln2 TYPE anla-anln2,
        END OF ty_aakey.

" ----Each Table----
TYPES : BEGIN OF ty_anla,
          bukrs TYPE anla-bukrs, " PR
          anlkl TYPE anla-anlkl,
          anln1 TYPE anla-anln1, " PR
          anln2 TYPE anla-anln2, " PR
          txt50 TYPE anla-txt50,
          txa50 TYPE anla-txa50,
          ktogr TYPE anla-ktogr,
          sernr TYPE anla-sernr,
*          invnr TYPE anla-invnr, " Deleted
          menge TYPE anla-menge,
          meins TYPE anla-meins,
          aneqk TYPE anla-aneqk,
          aktiv TYPE anla-aktiv,
          zugdt TYPE anla-zugdt,
          liefe TYPE anla-liefe,
          aibn1 TYPE anla-aibn1,
          ord41 TYPE anla-ord41,
          ord42 TYPE anla-ord42,
          ord43 TYPE anla-ord43,
          ord44 TYPE anla-ord44,
          posnr TYPE anla-posnr,
        END OF ty_anla.

TYPES : BEGIN OF ty_anlb,
          bukrs TYPE anlb-bukrs, " PR
          anln1 TYPE anlb-anln1, " PR
          anln2 TYPE anlb-anln2, " PR
          afasl TYPE anlb-afasl,
          afabg TYPE anlb-afabg,
          schrw TYPE anlb-schrw,
          ndjar TYPE anlb-ndjar,
          ndper TYPE anlb-ndper,
        END OF ty_anlb.

TYPES : BEGIN OF ty_anlc,
          bukrs TYPE anlc-bukrs, " PR
          anln1 TYPE anlc-anln1, " PR
          anln2 TYPE anlc-anln2, " PR
          kansw TYPE anlc-kansw,
          answl TYPE anlc-answl,
          knafa TYPE anlc-knafa,
          nafag TYPE anlc-nafag,
        END OF ty_anlc.

TYPES : BEGIN OF ty_anlh,
          bukrs   TYPE anlh-bukrs, " PR
          anln1   TYPE anlh-anln1, " PR
          anlhtxt TYPE anlh-anlhtxt,
        END OF ty_anlh.

TYPES : BEGIN OF ty_anlz,
          bukrs       TYPE anlz-bukrs, " PR
          anln1       TYPE anlz-anln1, " PR
          anln2       TYPE anlz-anln2, " PR
          kostl       TYPE anlz-kostl,
          stort       TYPE anlz-stort,
          caufn       TYPE anlz-caufn,
          raumn       TYPE anlz-raumn,
          pernr       TYPE anlz-pernr,
          fistl       TYPE anlz-fistl,
          ps_psp_pnr2 TYPE anlz-ps_psp_pnr2,
        END OF ty_anlz.

"----Output Table----"
TYPES : BEGIN OF ty_output,
          "----ANLA----"
          bukrs       TYPE anla-bukrs,
          anlkl       TYPE anla-anlkl,
          anln1       TYPE anla-anln1,
          anln2       TYPE anla-anln2,
          txt50       TYPE anla-txt50,
          txa50       TYPE anla-txa50,
          "----ANLH----"
          anlhtxt     TYPE anlh-anlhtxt,
          "----ANLA----"
          ktogr       TYPE anla-ktogr,
          sernr       TYPE anla-sernr,
*          invnr       TYPE anla-invnr, " Deleted
          menge       TYPE anla-menge,
          meins       TYPE anla-meins,
          aneqk       TYPE anla-aneqk,
          aktiv       TYPE anla-aktiv,
          zugdt       TYPE anla-zugdt,
          "----ANLZ----"
          kostl       TYPE anlz-kostl,
          stort       TYPE anlz-stort,
          caufn       TYPE anlz-caufn,
          raumn       TYPE anlz-raumn,
          pernr       TYPE string,
          fistl       TYPE anlz-fistl,
          ps_psp_pnr2 TYPE anlz-ps_psp_pnr2,
          "----ANLA----"
          liefe       TYPE anla-liefe,
          aibn1       TYPE anla-aibn1,
          ord41       TYPE anla-ord41,
          ord42       TYPE anla-ord42,
          ord43       TYPE anla-ord43,
          ord44       TYPE anla-ord44,
          posnr       TYPE anla-posnr,
          "----ANLB----"
          afasl       TYPE anlb-afasl,
          afabg       TYPE anlb-afabg,
          schrw       TYPE anlb-schrw,
          ndjar       TYPE anlb-ndjar,
          ndper       TYPE anlb-ndper,
          "----ANLC----"
*          kansw       TYPE anlc-kansw,
*          answl       TYPE anlc-answl,
*          knafa       TYPE anlc-knafa,
*          nafag       TYPE anlc-nafag,
          kansw       TYPE string,
          answl       TYPE string,
          knafa       TYPE string,
          nafag       TYPE string,
        END OF ty_output.

*----------------------------------------------------------------------*
* INTERNAL TABLES
*----------------------------------------------------------------------*
INITIALIZATION.
*----------------------------------------------------------------------*
* DATA DECLARATION
*----------------------------------------------------------------------*
  DATA : gt_ackeys TYPE TABLE OF ty_ackey,
         gt_aakeys TYPE TABLE OF ty_aakey.

  DATA : gt_anla TYPE TABLE OF ty_anla,
         gt_anlb TYPE TABLE OF ty_anlb,
         gt_anlc TYPE TABLE OF ty_anlc,
         gt_anlh TYPE TABLE OF ty_anlh,
         gt_anlz TYPE TABLE OF ty_anlz.

  DATA : gt_output TYPE TABLE OF ty_output,
         gs_output TYPE ty_output.

  DATA: lt_fieldcat TYPE slis_t_fieldcat_alv,
        ls_fieldcat TYPE slis_fieldcat_alv.

  " Optional Excel Download Auto
  DATA: lv_download    TYPE string,
        lv_userprofile TYPE string,
        lv_fullpath    TYPE string.

  TABLES : anlc.
*----------------------------------------------------------------------*
* Selection Screen
*----------------------------------------------------------------------*
  SELECTION-SCREEN BEGIN OF BLOCK b1 WITH FRAME TITLE TEXT-001.
    " Company Code
*    PARAMETERS : p_bukrs TYPE anlc-bukrs.
    SELECT-OPTIONS : s_bukrs FOR anlc-bukrs.

    SELECTION-SCREEN SKIP 1.
    SELECTION-SCREEN COMMENT /1(50) TEXT-002.
    " Radio Button
    PARAMETERS: p_reg    RADIOBUTTON GROUP g1 DEFAULT 'X',
                p_unpost RADIOBUTTON GROUP g1.
  SELECTION-SCREEN END OF BLOCK b1.

  SELECTION-SCREEN BEGIN OF BLOCK b2 WITH FRAME TITLE TEXT-003.
    " Optional (Show Alv or Auto download Excel)
    PARAMETERS : p_alv  RADIOBUTTON GROUP g2,
                 p_auto RADIOBUTTON GROUP g2 DEFAULT 'X'.

*    SELECTION-SCREEN BEGIN OF BLOCK b3 WITH FRAME TITLE TEXT-004.
*      PARAMETERS: p_path TYPE string MODIF ID BLK.
*    SELECTION-SCREEN END OF BLOCK b3.

  SELECTION-SCREEN END OF BLOCK b2.

*----------------------------------------------------------------------*
* Validate Input
*----------------------------------------------------------------------*
AT SELECTION-SCREEN.

*  IF s_bukrs IS INITIAL.
*    MESSAGE 'Please Enter CoCd.' TYPE 'E'.
*  ENDIF.

*----------------------------------------------------------------------*
* START OF SELECTION
*----------------------------------------------------------------------*
START-OF-SELECTION.

  PERFORM validate_input.

  PERFORM get_userpath.

  PERFORM get_anlkey.

  IF p_reg = 'X'.

    PERFORM get_register. " ANLC

    PERFORM merge_data.

    debugon = 1.

  ELSEIF p_unpost = 'X'.
    PERFORM remove_samekey. " (ANLA U ANLC)!

    PERFORM get_unposted.

    PERFORM merge_data.

    debugon = 1.

  ENDIF.

  IF p_alv = 'X'.
    REFRESH lt_fieldcat.
    PERFORM build_fieldcat.
    PERFORM display_alv.
  ELSEIF p_auto = 'X'.
    PERFORM export_excel.
  ENDIF.

  FORM get_anlkey.

  " ----ANLC----"
  SELECT bukrs, anln1, anln2
    FROM anlc
    INTO TABLE @gt_ackeys
*    WHERE bukrs = @p_bukrs
    WHERE bukrs IN @s_bukrs
    AND gjahr = 2026
    AND afabe = 1.

  " ----ANLA----"
  SELECT bukrs, anln1, anln2
    FROM anla
    INTO TABLE @gt_aakeys
*    WHERE bukrs = @p_bukrs.
    WHERE bukrs IN @s_bukrs.

  SORT gt_ackeys BY bukrs anln1 anln2.
  SORT gt_aakeys BY bukrs anln1 anln2.

  DELETE ADJACENT DUPLICATES FROM gt_ackeys COMPARING bukrs anln1 anln2.
  DELETE ADJACENT DUPLICATES FROM gt_aakeys COMPARING bukrs anln1 anln2.

ENDFORM.

FORM remove_samekey.
  LOOP AT gt_aakeys ASSIGNING FIELD-SYMBOL(<fs_aakey>).
    READ TABLE gt_ackeys ASSIGNING FIELD-SYMBOL(<fs_ackey>)
     WITH KEY bukrs = <fs_aakey>-bukrs
              anln1 = <fs_aakey>-anln1
              anln2 = <fs_aakey>-anln2.

    IF sy-subrc = 0.
      DELETE gt_aakeys USING KEY loop_key.
    ENDIF.

    " same key -> remove
  ENDLOOP.
ENDFORM.

" Get Register
FORM get_register.
  "---- ANLA ----"
  SELECT bukrs, anlkl, anln1, anln2, txt50, txa50, ktogr, sernr, menge,
         meins, aneqk, aktiv, zugdt, liefe, aibn1, ord41, ord42, ord43, ord44, posnr
    FROM anla
    INTO TABLE @gt_anla
    FOR ALL ENTRIES IN @gt_ackeys
    WHERE bukrs = @gt_ackeys-bukrs
    AND anln1 = @gt_ackeys-anln1
    AND anln2 = @gt_ackeys-anln2.

  SORT gt_anla BY bukrs anln1 anln2.

  "---- ANLB ----"
  SELECT bukrs, anln1, anln2,
         afasl, afabg, schrw, ndjar, ndper
    FROM anlb
    INTO TABLE @gt_anlb
    FOR ALL ENTRIES IN @gt_ackeys
    WHERE bukrs = @gt_ackeys-bukrs
    AND anln1 = @gt_ackeys-anln1
    AND anln2 = @gt_ackeys-anln2.

  "---- ANLC ----"
  SELECT bukrs, anln1, anln2, kansw, answl, knafa, nafag
    FROM anlc
    INTO TABLE @gt_anlc
    FOR ALL ENTRIES IN @gt_ackeys
    WHERE bukrs = @gt_ackeys-bukrs
    AND anln1 = @gt_ackeys-anln1
    AND anln2 = @gt_ackeys-anln2
    AND gjahr = 2026
    AND afabe = 1.

  SORT gt_anlc BY bukrs anln1 anln2.

  "---- ANLH ----"
  SELECT bukrs, anln1, anlhtxt
    FROM anlh
    INTO TABLE @gt_anlh
    FOR ALL ENTRIES IN @gt_ackeys
    WHERE bukrs = @gt_ackeys-bukrs
    AND anln1 = @gt_ackeys-anln1.

  SORT gt_anlh BY bukrs anln1.

  "---- ANLZ ----"
  SELECT bukrs, anln1, anln2, kostl, stort, caufn, raumn, pernr, fistl, ps_psp_pnr2
    FROM anlz
    INTO TABLE @gt_anlz
    FOR ALL ENTRIES IN @gt_ackeys
    WHERE bukrs = @gt_ackeys-bukrs
    AND anln1 = @gt_ackeys-anln1
    AND anln2 = @gt_ackeys-anln2
    AND bdatu = '99991231'.

  SORT gt_anlz BY bukrs anln1 anln2.

  debugon = 1.

ENDFORM.

" Get Unposted Asset
FORM get_unposted.

  "---- ANLA ----"
  SELECT bukrs, anlkl, anln1, anln2, txt50, txa50, ktogr, sernr, menge,
         meins, aneqk, aktiv, zugdt, liefe, aibn1, ord41, ord42, ord43, ord44, posnr
    FROM anla
    INTO TABLE @gt_anla
    FOR ALL ENTRIES IN @gt_aakeys
    WHERE bukrs = @gt_aakeys-bukrs
    AND anln1 = @gt_aakeys-anln1
    AND anln2 = @gt_aakeys-anln2.

  SORT gt_anla BY bukrs anln1 anln2.

  "---- ANLB ----"
  SELECT bukrs, anln1, anln2,
         afasl, afabg, schrw, ndjar, ndper
    FROM anlb
    INTO TABLE @gt_anlb
    FOR ALL ENTRIES IN @gt_aakeys
    WHERE bukrs = @gt_aakeys-bukrs
    AND anln1 = @gt_aakeys-anln1
    AND anln2 = @gt_aakeys-anln2
    AND afabe = 1.

  SORT gt_anlb BY bukrs anln1 anln2.

  "---- ANLC ----" Must have no data
  SELECT bukrs, anln1, anln2, kansw, answl, knafa, nafag
    FROM anlc
    INTO TABLE @gt_anlc
    FOR ALL ENTRIES IN @gt_aakeys
    WHERE bukrs = @gt_aakeys-bukrs
    AND anln1 = @gt_aakeys-anln1
    AND anln2 = @gt_aakeys-anln2
    AND gjahr = 2026
    AND afabe = 1.

  "---- ANLH ----"
  SELECT bukrs, anln1, anlhtxt
    FROM anlh
    INTO TABLE @gt_anlh
    FOR ALL ENTRIES IN @gt_aakeys
    WHERE bukrs = @gt_aakeys-bukrs
    AND anln1 = @gt_aakeys-anln1.

  SORT gt_anlh BY bukrs anln1.

  "---- ANLZ ----"
  SELECT bukrs, anln1, anln2, kostl, stort, caufn, raumn, pernr, fistl, ps_psp_pnr2
    FROM anlz
    INTO TABLE @gt_anlz
    FOR ALL ENTRIES IN @gt_aakeys
    WHERE bukrs = @gt_aakeys-bukrs
    AND anln1 = @gt_aakeys-anln1
    AND anln2 = @gt_aakeys-anln2
    AND bdatu = '99991231'.

  SORT gt_anlz BY bukrs anln1 anln2.

ENDFORM.

FORM merge_data.
  " Unposted Asset
  IF p_unpost = 'X'.
    LOOP AT gt_anla ASSIGNING FIELD-SYMBOL(<fs_anla>).
      MOVE-CORRESPONDING <fs_anla> TO gs_output.

      " APPEND ANLH
      READ TABLE gt_anlh ASSIGNING FIELD-SYMBOL(<fs_anlh>)
        WITH KEY bukrs = <fs_anla>-bukrs
                 anln1 = <fs_anla>-anln1.
      IF sy-subrc = 0.
        MOVE-CORRESPONDING <fs_anlh> TO gs_output.
      ENDIF.

      " APPEND ANLZ
      READ TABLE gt_anlz ASSIGNING FIELD-SYMBOL(<fs_anlz>)
        WITH KEY bukrs = <fs_anla>-bukrs
                 anln1 = <fs_anla>-anln1
                 anln2 = <fs_anla>-anln2.
      IF sy-subrc = 0.
        MOVE-CORRESPONDING <fs_anlz> TO gs_output.
      ENDIF.

      " APPEND ANLB
      READ TABLE gt_anlb ASSIGNING FIELD-SYMBOL(<fs_anlb>)
        WITH KEY bukrs = <fs_anla>-bukrs
                 anln1 = <fs_anla>-anln1
                 anln2 = <fs_anla>-anln2.
      IF sy-subrc = 0.
        MOVE-CORRESPONDING <fs_anlb> TO gs_output.
      ENDIF.

      " APPEND ANLC
      READ TABLE gt_anlc ASSIGNING FIELD-SYMBOL(<fs_anlc>)
        WITH KEY bukrs = <fs_anla>-bukrs
                 anln1 = <fs_anla>-anln1
                 anln2 = <fs_anla>-anln2.
      IF sy-subrc = 0.
        MOVE-CORRESPONDING <fs_anlc> TO gs_output.
      ENDIF.

      PERFORM changeformat CHANGING gs_output.
      PERFORM set_decimal CHANGING gs_output.

      APPEND gs_output TO gt_output.

    ENDLOOP.

  ELSEIF p_reg = 'X'.
    LOOP AT gt_anlc ASSIGNING FIELD-SYMBOL(<fs_anlcc>).
      MOVE-CORRESPONDING <fs_anlcc> TO gs_output.

      " APPEND ANLA
      READ TABLE gt_anla ASSIGNING FIELD-SYMBOL(<fs_anlaa>)
        WITH KEY bukrs = <fs_anlcc>-bukrs
                 anln1 = <fs_anlcc>-anln1
                 anln2 = <fs_anlcc>-anln2.
      IF sy-subrc = 0.
        MOVE-CORRESPONDING <fs_anlaa> TO gs_output.
      ENDIF.

      " APPEND ANLB
      READ TABLE gt_anlb ASSIGNING FIELD-SYMBOL(<fs_anlbb>)
        WITH KEY bukrs = <fs_anlcc>-bukrs
                 anln1 = <fs_anlcc>-anln1
                 anln2 = <fs_anlcc>-anln2.
      IF sy-subrc = 0.
        MOVE-CORRESPONDING <fs_anlbb> TO gs_output.
      ENDIF.

      " APPEND ANLH
      READ TABLE gt_anlh ASSIGNING FIELD-SYMBOL(<fs_anlhh>)
        WITH KEY bukrs = <fs_anlcc>-bukrs
                 anln1 = <fs_anlcc>-anln1.
      IF sy-subrc = 0.
        MOVE-CORRESPONDING <fs_anlhh> TO gs_output.
      ENDIF.

      " APPEND ANLZ
      READ TABLE gt_anlz ASSIGNING FIELD-SYMBOL(<fs_anlzz>)
        WITH KEY bukrs = <fs_anlcc>-bukrs
                 anln1 = <fs_anlcc>-anln1
                 anln2 = <fs_anlcc>-anln2.
      IF sy-subrc = 0.
        MOVE-CORRESPONDING <fs_anlzz> TO gs_output.
      ENDIF.

      PERFORM changeformat CHANGING gs_output.
      PERFORM set_decimal CHANGING gs_output.

      APPEND gs_output TO gt_output.
    ENDLOOP.
  ENDIF.

  debugon = 1.
ENDFORM.

FORM set_decimal CHANGING cs_output TYPE ty_output.
  " AH
  IF cs_output-kansw CA '-'.
    SHIFT cs_output-kansw UP TO '-' CIRCULAR. " ==== Rotate Value ===="
  ENDIF.
  " AI
  IF cs_output-answl CA '-'.
    SHIFT cs_output-answl UP TO '-' CIRCULAR. " ==== Rotate Value ===="
  ENDIF.
  " AJ
  IF cs_output-knafa CA '-'.
    SHIFT cs_output-knafa UP TO '-' CIRCULAR. " ==== Rotate Value ===="
  ENDIF.
  " AK
  IF cs_output-nafag CA '-'.
    SHIFT cs_output-nafag UP TO '-' CIRCULAR. " ==== Rotate Value ===="
  ENDIF.

ENDFORM.

FORM changeformat CHANGING cs_output TYPE ty_output.
  DATA : lv_pernr TYPE string.
  "==== Cut 0 Infront ===="
  CALL FUNCTION 'CONVERSION_EXIT_ALPHA_OUTPUT'
    EXPORTING
      input  = cs_output-pernr
    IMPORTING
      output = lv_pernr.

  cs_output-pernr = lv_pernr.

  debugon = 1.
ENDFORM.

FORM validate_input.
  IF s_bukrs[] IS INITIAL.
    MESSAGE s001(00) WITH 'Please Enter CoCd' DISPLAY LIKE 'E'.
    LEAVE LIST-PROCESSING.
  ENDIF.
ENDFORM.

FORM set_pf_status USING rt_extab TYPE slis_t_extab.
  SET PF-STATUS 'ZALV_STATUS'.
ENDFORM.

FORM build_fieldcat.
  "=====================================================================*
  " ANLA A-F
  "=====================================================================*
  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'BUKRS'.
  ls_fieldcat-ref_tabname = 'ANLA'.
  ls_fieldcat-seltext_m   = 'Company Code'.
  ls_fieldcat-col_pos     = 1.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'ANLKL'.
  ls_fieldcat-ref_tabname = 'ANLA'.
  ls_fieldcat-seltext_m   = 'Asset Class'.
  ls_fieldcat-col_pos     = 2.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'ANLN1'.
  ls_fieldcat-ref_tabname = 'ANLA'.
  ls_fieldcat-seltext_m   = 'Main Asset'.
  ls_fieldcat-col_pos     = 3.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'ANLN2'.
  ls_fieldcat-ref_tabname = 'ANLA'.
  ls_fieldcat-seltext_m   = 'Asset Subno.'.
  ls_fieldcat-col_pos     = 4.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'TXT50'.
  ls_fieldcat-ref_tabname = 'ANLA'.
  ls_fieldcat-seltext_m   = 'Asset Description'.
  ls_fieldcat-col_pos     = 5.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'TXA50'.
  ls_fieldcat-ref_tabname = 'ANLA'.
  ls_fieldcat-seltext_m   = 'Additional Descr.'.
  ls_fieldcat-col_pos     = 6.
  APPEND ls_fieldcat TO lt_fieldcat.

  "=====================================================================*
  " ANLH -G
  "=====================================================================*

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'ANLHTXT'.
  ls_fieldcat-ref_tabname = 'ANLH'.
  ls_fieldcat-seltext_m   = 'Asset Main No. text'.
  ls_fieldcat-col_pos     = 7.
  APPEND ls_fieldcat TO lt_fieldcat.

  "=====================================================================*
  " ANLA H-N
  "=====================================================================*

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'KTOGR'.
  ls_fieldcat-ref_tabname = 'ANLA'.
  ls_fieldcat-seltext_m   = 'Account Determ.'.
  ls_fieldcat-col_pos     = 8.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'SERNR'.
  ls_fieldcat-ref_tabname = 'ANLA'.
  ls_fieldcat-seltext_m   = 'Serial Number'.
  ls_fieldcat-col_pos     = 9.
  APPEND ls_fieldcat TO lt_fieldcat.

*  CLEAR ls_fieldcat.
*  ls_fieldcat-fieldname   = 'INVNR'.
*  ls_fieldcat-ref_tabname = 'ANLA'.
*  ls_fieldcat-seltext_m   = 'Inventory Number'.
*  ls_fieldcat-col_pos     = 10.
*  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'MENGE'.
  ls_fieldcat-ref_tabname = 'ANLA'.
  ls_fieldcat-seltext_m   = 'Quantity'.
  ls_fieldcat-col_pos     = 11.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'MEINS'.
  ls_fieldcat-ref_tabname = 'ANLA'.
  ls_fieldcat-seltext_m   = 'Base Unit'.
  ls_fieldcat-col_pos     = 12.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'ANEQK'.
  ls_fieldcat-ref_tabname = 'ANLA'.
  ls_fieldcat-seltext_m   = 'Historical Management'.
  ls_fieldcat-col_pos     = 13.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'AKTIV'.
  ls_fieldcat-ref_tabname = 'ANLA'.
  ls_fieldcat-seltext_m   = 'Capitalized Date'.
  ls_fieldcat-col_pos     = 14.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'ZUGDT'.
  ls_fieldcat-ref_tabname = 'ANLA'.
  ls_fieldcat-seltext_m   = 'First Posting'.
  ls_fieldcat-col_pos     = 15.
  APPEND ls_fieldcat TO lt_fieldcat.

  "=====================================================================*
  " ANLZ O-U
  "=====================================================================*
  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'KOSTL'.
  ls_fieldcat-ref_tabname = 'ANLZ'.
  ls_fieldcat-seltext_m   = 'Cost Center'.
  ls_fieldcat-col_pos     = 16.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'STORT'.
  ls_fieldcat-ref_tabname = 'ANLZ'.
  ls_fieldcat-seltext_m   = 'Asset Location'.
  ls_fieldcat-col_pos     = 17.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'CAUFN'.
  ls_fieldcat-ref_tabname = 'ANLZ'.
  ls_fieldcat-seltext_m   = 'Internal Order'.
  ls_fieldcat-col_pos     = 18.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'RAUMN'.
  ls_fieldcat-ref_tabname = 'ANLZ'.
  ls_fieldcat-seltext_m   = 'Room'.
  ls_fieldcat-col_pos     = 19.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'PERNR'.
  ls_fieldcat-ref_tabname = 'ANLZ'.
  ls_fieldcat-seltext_m   = 'Personnel No.'.
  ls_fieldcat-col_pos     = 20.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'FISTL'.
  ls_fieldcat-ref_tabname = 'ANLZ'.
  ls_fieldcat-seltext_m   = 'Funds Center'.
  ls_fieldcat-col_pos     = 21.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'PS_PSP_PNR2'.
  ls_fieldcat-ref_tabname = 'ANLZ'.
  ls_fieldcat-seltext_m   = 'WBS Element(Costs)'.
  ls_fieldcat-col_pos     = 22.
  APPEND ls_fieldcat TO lt_fieldcat.

  "=====================================================================*
  " ANLA V-AB
  "=====================================================================*
  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'LIEFE'.
  ls_fieldcat-ref_tabname = 'ANLA'.
  ls_fieldcat-seltext_m   = 'Asset Suplier'.
  ls_fieldcat-col_pos     = 23.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'AIBN1'.
  ls_fieldcat-ref_tabname = 'ANLA'.
  ls_fieldcat-seltext_m   = 'Original Asset'.
  ls_fieldcat-col_pos     = 24.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'ORD41'.
  ls_fieldcat-ref_tabname = 'ANLA'.
  ls_fieldcat-seltext_m   = 'Leasing Flag'.
  ls_fieldcat-col_pos     = 25.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'ORD42'.
  ls_fieldcat-ref_tabname = 'ANLA'.
  ls_fieldcat-seltext_m   = 'Furniture/Machine Grp'.
  ls_fieldcat-col_pos     = 26.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'ORD43'.
  ls_fieldcat-ref_tabname = 'ANLA'.
  ls_fieldcat-seltext_m   = 'Asset Status'.
  ls_fieldcat-col_pos     = 27.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'ORD44'.
  ls_fieldcat-ref_tabname = 'ANLA'.
  ls_fieldcat-seltext_m   = 'WBS Checking'.
  ls_fieldcat-col_pos     = 28.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'POSNR'.
  ls_fieldcat-ref_tabname = 'ANLA'.
  ls_fieldcat-seltext_m   = 'WBS Element'.
  ls_fieldcat-col_pos     = 29.
  APPEND ls_fieldcat TO lt_fieldcat.

  "=====================================================================*
  " ANLB AC-AG
  "=====================================================================*
  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'AFASL'.
  ls_fieldcat-ref_tabname = 'ANLB'.
  ls_fieldcat-seltext_m   = 'Depreciation Key'.
  ls_fieldcat-col_pos     = 30.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'AFABG'.
  ls_fieldcat-ref_tabname = 'ANLB'.
  ls_fieldcat-seltext_m   = 'Depr. Start Date'.
  ls_fieldcat-col_pos     = 31.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'SCHRW'.
  ls_fieldcat-ref_tabname = 'ANLB'.
  ls_fieldcat-seltext_m   = 'Scrap Value'.
  ls_fieldcat-col_pos     = 32.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'NDJAR'.
  ls_fieldcat-ref_tabname = 'ANLB'.
  ls_fieldcat-seltext_m   = 'Useful Life (Yrs)'.
  ls_fieldcat-col_pos     = 33.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'NDPER'.
  ls_fieldcat-ref_tabname = 'ANLB'.
  ls_fieldcat-seltext_m   = 'Useful Life (Prds)'.
  ls_fieldcat-col_pos     = 34.
  APPEND ls_fieldcat TO lt_fieldcat.

  "=====================================================================*
  " ANLC AH-AK
  "=====================================================================*
  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'KANSW'.
  ls_fieldcat-ref_tabname = 'ANLC'.
  ls_fieldcat-seltext_m   = 'Cum.Acquis. Value'.
  ls_fieldcat-col_pos     = 35.
*  ls_fieldcat-do_sum      = 'X'. " เพิ่มให้สามารถหาผลรวม (Sum) ท้ายคอลัมน์ได้
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'ANSWL'.
  ls_fieldcat-ref_tabname = 'ANLC'.
  ls_fieldcat-seltext_m   = 'Asset Transactions'.
  ls_fieldcat-col_pos     = 36.
*  ls_fieldcat-do_sum      = 'X'.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'KNAFA'.
  ls_fieldcat-ref_tabname = 'ANLC'.
  ls_fieldcat-seltext_m   = 'Accum. Ord. Depr.'.
  ls_fieldcat-col_pos     = 37.
*  ls_fieldcat-do_sum      = 'X'.
  APPEND ls_fieldcat TO lt_fieldcat.

  CLEAR ls_fieldcat.
  ls_fieldcat-fieldname   = 'NAFAG'.
  ls_fieldcat-ref_tabname = 'ANLC'.
  ls_fieldcat-seltext_m   = 'Ord. Depr. Year'.
  ls_fieldcat-col_pos     = 38.
*  ls_fieldcat-do_sum      = 'X'.
  APPEND ls_fieldcat TO lt_fieldcat.
ENDFORM.

FORM display_alv.

  "---- POSNR No Convext ----"
  READ TABLE lt_fieldcat ASSIGNING FIELD-SYMBOL(<fs_fcat>)
    WITH KEY fieldname = 'POSNR'.
  IF sy-subrc = 0.
    <fs_fcat>-no_convext = 'X'.
  ENDIF.

  CALL FUNCTION 'REUSE_ALV_GRID_DISPLAY'
    EXPORTING
      i_callback_program       = sy-repid
      i_callback_pf_status_set = 'SET_PF_STATUS'
      i_callback_user_command  = 'USER_COMMAND'
      it_fieldcat              = lt_fieldcat
    TABLES
      t_outtab                 = gt_output
    EXCEPTIONS
      program_error            = 1
      OTHERS                   = 2.

  IF sy-subrc <> 0.
    MESSAGE 'Error Loading ALV' TYPE 'E'.
  ENDIF.
ENDFORM.

FORM get_userpath.
  CALL METHOD cl_gui_frontend_services=>registry_get_value
    EXPORTING
      root      = cl_gui_frontend_services=>hkey_current_user
      key       = 'Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders'
      value     = '{374DE290-123F-4565-9164-39C4925E467B}'
    IMPORTING
      reg_value = lv_download.

  IF sy-subrc = 0.

    IF lv_download CS '%USERPROFILE%'.

      CALL METHOD cl_gui_frontend_services=>environment_get_variable
        EXPORTING
          variable = 'USERPROFILE'
        CHANGING
          value    = lv_userprofile.

      REPLACE '%USERPROFILE%' IN lv_download
        WITH lv_userprofile.

    ENDIF.

    " Arrange Path
    CONCATENATE lv_download '\Extract_Asset_' sy-uzeit '.xlsx' INTO lv_fullpath.

  ENDIF.
ENDFORM.

FORM export_excel.
  DATA : lo_excel TYPE REF TO zcl_excel.
  CREATE OBJECT lo_excel.

  DATA lo_sheet TYPE REF TO zcl_excel_worksheet.

  lo_sheet = lo_excel->get_active_worksheet( ).
  lo_sheet->set_title( 'Extract Asset' ).
  lo_sheet->bind_table( ip_table = gt_output ).
  "==== Rename Manual ===="
  lo_sheet->set_cell(
    ip_row = 1
    ip_column = 'S'
    ip_value = 'Personnel No.'
  ).

  lo_sheet->set_cell(
    ip_row = 1
    ip_column = 'AH'
    ip_value = 'Cum.Acquis. Value'
  ).
  lo_sheet->set_cell(
    ip_row = 1
    ip_column = 'AI'
    ip_value = 'Asset Transactions'
  ).
  lo_sheet->set_cell(
    ip_row = 1
    ip_column = 'AJ'
    ip_value = 'Accum. Ord. Depr.'
  ).
  lo_sheet->set_cell(
    ip_row = 1
    ip_column = 'AK'
    ip_value = 'Ord. Depr. Year'
  ).

  DATA:
    lo_writer  TYPE REF TO zif_excel_writer,
    lv_xstring TYPE xstring,
    lt_binary  TYPE solix_tab,
    ls_binary  TYPE solix.

  CREATE OBJECT lo_writer
    TYPE zcl_excel_writer_2007.

  lv_xstring = lo_writer->write_file( lo_excel ).

  CALL FUNCTION 'SCMS_XSTRING_TO_BINARY'
    EXPORTING
      buffer     = lv_xstring
    TABLES
      binary_tab = lt_binary.

  cl_gui_frontend_services=>gui_download(
  EXPORTING
    filename     = lv_fullpath
    filetype     = 'BIN'
    bin_filesize = xstrlen( lv_xstring )
  CHANGING
    data_tab     = lt_binary
  EXCEPTIONS
    OTHERS       = 1 ).

  IF sy-subrc = 0.
    MESSAGE 'Excel file downloaded successfully' TYPE 'S'.
    cl_gui_frontend_services=>execute(
      EXPORTING
        document = lv_fullpath
    ).

  ELSE.
    MESSAGE s001(00) WITH 'Error downloading Excel file' DISPLAY LIKE 'E'.
    LEAVE LIST-PROCESSING.
  ENDIF.
ENDFORM.
