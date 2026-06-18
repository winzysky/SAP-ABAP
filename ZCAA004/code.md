DATA : debugon     TYPE i, " use for checkpoint debuging
       lv_selected TYPE char4. " use when export excel (customer or vendor)
DATA : lv_exprtstus TYPE string.
" customer general data sheet
TYPES : BEGIN OF cus_gendata,
          partner        TYPE but000-partner,
          bu_group       TYPE but000-bu_group,
          anred          TYPE kna1-anred,
          name_org1      TYPE but000-name_org1,
          name_org2      TYPE but000-name_org2,
          name_org3      TYPE but000-name_org3,
          bu_sort1       TYPE but000-bu_sort1,
          bu_sort2       TYPE but000-bu_sort2,
          city1          TYPE adrc-city1,
          city2          TYPE adrc-city2,
          post_code1     TYPE adrc-post_code1,
          street         TYPE adrc-street,
          house_num1     TYPE adrc-house_num1,
          str_suppl1     TYPE adrc-str_suppl1,
          str_suppl2     TYPE adrc-str_suppl2,
          str_suppl3     TYPE adrc-str_suppl3,
          country        TYPE adrc-country,
          langu          TYPE char5,
          xcpdk          TYPE kna1-xcpdk,
          vbund          TYPE kna1-vbund,
          taxtype        TYPE dfkkbptaxnum-taxtype,
          taxnum         TYPE dfkkbptaxnum-taxnum,
          j_1tpbupl      TYPE fitha_pbupl_d-j_1tpbupl,
          default_branch TYPE fitha_pbupl_d-default_branch,
          description    TYPE fitha_pbupl_d_t-description,

        END OF cus_gendata.

" customer address sheet
TYPES : BEGIN OF cus_address,
          partner    TYPE but000-partner,
          nation     TYPE adrc-nation,
          name_org1  TYPE but000-name_org1,
          name_org2  TYPE but000-name_org2,
          name_org3  TYPE but000-name_org3,
          city1      TYPE adrc-city1,
          city2      TYPE adrc-city2,
          post_code1 TYPE adrc-post_code1,
          street     TYPE adrc-street,
          house_num1 TYPE adrc-house_num1,
          str_suppl1 TYPE adrc-str_suppl1,
          str_suppl2 TYPE adrc-str_suppl2,
          str_suppl3 TYPE adrc-str_suppl3,
          country    TYPE adrc-country,
          langu      TYPE char5,
        END OF cus_address.

" customer phone sheet
TYPES : BEGIN OF cus_phone,
          partner    TYPE but000-partner,
          name_org1  TYPE but000-name_org1,
          consnumber TYPE adr2-consnumber,
          country    TYPE adr2-country,
          flgdefault TYPE adr2-flgdefault,
          home_flag  TYPE adr2-home_flag,
          tel_number TYPE adr2-tel_number,
          tel_extens TYPE adr2-tel_extens,
          telnr_long TYPE adr2-telnr_long,
          telnr_call TYPE adr2-telnr_call,
          dft_receiv TYPE adr2-dft_receiv,
          r3_user    TYPE adr2-r3_user,
        END OF cus_phone.

" customer fax sheet
TYPES : BEGIN OF cus_fax,
          partner    TYPE but000-partner,
          name_org1  TYPE but000-name_org1,
          consnumber TYPE adr3-consnumber,
          country    TYPE adr3-country,
          flgdefault TYPE adr3-flgdefault,
          home_flag  TYPE adr3-home_flag,
          fax_number TYPE adr3-fax_number,
          fax_extens TYPE adr3-fax_extens,
          faxnr_long TYPE adr3-faxnr_long,
          faxnr_call TYPE adr3-faxnr_call,
        END OF cus_fax.

" customer email sheet
TYPES : BEGIN OF cus_email,
          partner    TYPE but000-partner,
          name_org1  TYPE but000-name_org1,
          consnumber TYPE adr6-consnumber,
          flgdefault TYPE adr6-flgdefault,
          home_flag  TYPE adr6-home_flag,
          smtp_addr  TYPE adr6-smtp_addr,
        END OF cus_email.

" customer company ORIGINAL data sheet
TYPES : BEGIN OF cus_comdata,
          partner   TYPE but000-partner,
          name_org1 TYPE but000-name_org1,
          bukrs     TYPE knb1-bukrs,
          zuawa     TYPE knb1-zuawa,
          akont     TYPE knb1-akont,
          txt50     TYPE skat-txt50,
          zterm     TYPE knb1-zterm,
          xzver     TYPE knb1-xzver,
          altkn     TYPE knb1-altkn,
          witht     TYPE knbw-witht,
          qsrec     TYPE knbw-qsrec,
          wt_agent  TYPE knbw-wt_agent,
        END OF cus_comdata.

" customer company EXPORT data sheet
TYPES : BEGIN OF cus_e_comdata,
          partner   TYPE but000-partner,
          name_org1 TYPE but000-name_org1,
          bukrs     TYPE knb1-bukrs,
          zuawa     TYPE knb1-zuawa,
          akont     TYPE knb1-akont,
          txt50     TYPE skat-txt50,
          zterm     TYPE knb1-zterm,
          xzver     TYPE knb1-xzver,
          altkn     TYPE knb1-altkn,
          n1        TYPE char1,
          n2        TYPE char1,
          p1        TYPE char1,
          r1        TYPE char1,
          r2        TYPE char1,
          qsrec     TYPE knbw-qsrec,
          wt_agent  TYPE knbw-wt_agent,
        END OF cus_e_comdata.

" customer sales data sheet
TYPES : BEGIN OF cus_saledata,
          partner   TYPE but000-partner,
          name_org1 TYPE but000-name_org1,
          vkorg     TYPE knvv-vkorg,
          vtweg     TYPE knvv-vtweg,
          spart     TYPE knvv-spart,
          versg     TYPE knvv-versg,
          kalks     TYPE knvv-kalks,
          waers     TYPE knvv-waers,
          ktgrd     TYPE knvv-ktgrd,
          zterm     TYPE knvv-zterm,
          vwerk     TYPE knvv-vwerk,
          kvgr1     TYPE knvv-kvgr1,
          kurst     TYPE knvv-kurst,
          aland     TYPE knvi-aland,
          tatyp     TYPE knvi-tatyp,
          taxkd     TYPE knvi-taxkd,
        END OF cus_saledata.

" vendor general data sheet
TYPES : BEGIN OF ven_gendata,
          partner        TYPE but000-partner,
          bu_group       TYPE but000-bu_group,
          anred          TYPE lfa1-anred,
          name_org1      TYPE but000-name_org1,
          name_org2      TYPE but000-name_org2,
          name_org3      TYPE but000-name_org3,
          bu_sort1       TYPE but000-bu_sort1,
          bu_sort2       TYPE but000-bu_sort2,
          city1          TYPE adrc-city1,
          city2          TYPE adrc-city2,
          post_code1     TYPE adrc-post_code1,
          street         TYPE adrc-street,
          house_num1     TYPE adrc-house_num1,
          str_suppl1     TYPE adrc-str_suppl1,
          str_suppl2     TYPE adrc-str_suppl2,
          str_suppl3     TYPE adrc-str_suppl3,
          country        TYPE adrc-country,
          langu          TYPE char5,
          xcpdk          TYPE lfa1-xcpdk,
          vbund          TYPE lfa1-vbund,
          xzemp          TYPE lfa1-xzemp,
          dtaws          TYPE lfa1-dtaws,
          stkzn          TYPE lfa1-stkzn,
          taxtype        TYPE dfkkbptaxnum-taxtype,
          taxnum         TYPE dfkkbptaxnum-taxnum,
          banks          TYPE but0bk-banks,
          bankl          TYPE but0bk-bankl,
          bankn          TYPE but0bk-bankn,
          koinh          TYPE but0bk-koinh,
          accname        TYPE but0bk-accname,
          j_1tpbupl      TYPE fitha_pbupl_k-j_1tpbupl,
          default_branch TYPE fitha_pbupl_k-default_branch,
          description    TYPE fitha_pbupl_k_t-description,
        END OF ven_gendata.

" vendor general data sheet
TYPES : BEGIN OF ven_address,
          partner    TYPE but000-partner,
          nation     TYPE adrc-nation,
          name_org1  TYPE but000-name_org1,
          name_org2  TYPE but000-name_org2,
          bu_sort1   TYPE but000-bu_sort1,
          bu_sort2   TYPE but000-bu_sort2,
          city1      TYPE adrc-city1,
          city2      TYPE adrc-city2,
          post_code1 TYPE adrc-post_code1,
          street     TYPE adrc-street,
          house_num1 TYPE adrc-house_num1,
          str_suppl1 TYPE adrc-str_suppl1,
          str_suppl2 TYPE adrc-str_suppl2,
          str_suppl3 TYPE adrc-str_suppl3,
          country    TYPE adrc-country,
          langu      TYPE char5,
        END OF ven_address.

TYPES : BEGIN OF ven_purc,
          lifnr     TYPE lfa1-lifnr,
          name_org1 TYPE but000-name_org1,
          ekorg     TYPE lfm1-ekorg,
          waers     TYPE lfm1-waers,
          verkf     TYPE lfm1-verkf,
          telf1     TYPE lfm1-telf1,
          minbw     TYPE lfm1-minbw,
          zterm     TYPE lfb1-zterm,
          inco1     TYPE lfm1-inco1,
          inco2     TYPE lfm1-inco2,
          webre     TYPE lfm1-webre,
          inco2_l   TYPE lfm1-inco2_l,
        END OF ven_purc.

" vendor company ORIGINAL data sheet
TYPES : BEGIN OF ven_comdata,
          lifnr     TYPE lfa1-lifnr,
          name1     TYPE lfa1-name1,
          bukrs     TYPE lfb1-bukrs,
          pernr     TYPE lfb1-pernr,
          zuawa     TYPE lfb1-zuawa,
          hbkid     TYPE lfb1-hbkid,
          fdgrv     TYPE lfb1-fdgrv,
          zterm     TYPE lfb1-zterm,
          zwels     TYPE lfb1-zwels,
          akont     TYPE lfb1-akont,
          txt50     TYPE skat-txt50,
          uzawe     TYPE lfb1-uzawe,
          busab     TYPE lfb1-busab,
*          hbkid TYPE lfb1-hbkid,
          altkn     TYPE lfb1-altkn,
          witht      TYPE lfbw-witht,
          qsrec      TYPE lfbw-qsrec,
          wt_subjct  TYPE lfbw-wt_subjct,
        END OF ven_comdata.

" vendor company EXPORT data sheet
TYPES : BEGIN OF ven_e_comdata,
          lifnr     TYPE lfa1-lifnr,
          name1     TYPE lfa1-name1,
          bukrs     TYPE lfb1-bukrs,
          pernr     TYPE lfb1-pernr,
          zuawa     TYPE lfb1-zuawa,
          hbkid     TYPE lfb1-hbkid,
          fdgrv     TYPE lfb1-fdgrv,
          zterm     TYPE lfb1-zterm,
          zwels     TYPE lfb1-zwels,
          akont     TYPE lfb1-akont,
          txt50     TYPE skat-txt50,
          uzawe     TYPE lfb1-uzawe,
          busab     TYPE lfb1-busab,
*          hbkid TYPE lfb1-hbkid,
          altkn     TYPE lfb1-altkn,
          d1        TYPE char1,
          i1        TYPE char1,
          i2        TYPE char1,
          p1        TYPE char1,
          p2        TYPE char1,
          p3        TYPE char1,
          qsrec      TYPE lfbw-qsrec,
          wt_subjct  TYPE lfbw-wt_subjct,
        END OF ven_e_comdata.

" vendor phone sheet
TYPES : BEGIN OF ven_phone,
          partner    TYPE but000-partner,
          name_org1  TYPE but000-name_org1,
          consnumber TYPE adr2-consnumber,
          country    TYPE adr2-country,
          flgdefault TYPE adr2-flgdefault,
          home_flag  TYPE adr2-home_flag,
          tel_number TYPE adr2-tel_number,
          tel_extens TYPE adr2-tel_extens,
          telnr_long TYPE adr2-telnr_long,
          telnr_call TYPE adr2-telnr_call,
          dft_receiv TYPE adr2-dft_receiv,
          r3_user    TYPE adr2-r3_user,
        END OF ven_phone.

TYPES : BEGIN OF ven_email,
          partner     TYPE but000-partner,
          name_org1   TYPE but000-name_org1,
          j_1tpbupl   TYPE fitha_pbupl_k-j_1tpbupl,
          description TYPE fitha_pbupl_k_t-description,
          consnumber  TYPE adr6-consnumber,
          flgdefault  TYPE adr6-flgdefault,
          home_flag   TYPE adr6-home_flag,
          smtp_addr   TYPE adr6-smtp_addr,
        END OF ven_email.

" vendor fax sheet
TYPES : BEGIN OF ven_fax,
          partner    TYPE but000-partner,
          name_org1  TYPE but000-name_org1,
          consnumber TYPE adr3-consnumber,
          country    TYPE adr3-country,
          flgdefault TYPE adr3-flgdefault,
          home_flag  TYPE adr3-home_flag,
          fax_number TYPE adr3-fax_number,
          fax_extens TYPE adr3-fax_extens,
          faxnr_long TYPE adr3-faxnr_long,
          faxnr_call TYPE adr3-faxnr_call,
        END OF ven_fax.

*----------------------------------------------------------------------*
* INTERNAL TABLES
*---------------------------------------------------------

" Define Internal Tables seperate each sheet
DATA : gt_cust_gendata  TYPE TABLE OF cus_gendata,
       gt_cust_address  TYPE TABLE OF cus_address,
       gs_cust_address  TYPE cus_address,
       gt_cust_comdata  TYPE TABLE OF cus_comdata,
       gt_cust_saledata TYPE TABLE OF cus_saledata,
       gt_cust_phone    TYPE TABLE OF cus_phone,
       gt_cust_fax      TYPE TABLE OF cus_fax,
       gt_cust_email    TYPE TABLE OF cus_email.

" Define Internal Tables for get export sheet customer
DATA : et_cust_comdata TYPE TABLE OF cus_e_comdata,
       es_cust_comdata TYPE cus_e_comdata.

FIELD-SYMBOLS: <fs_e_comdata> TYPE cus_e_comdata.

DATA : gt_ven_gendata TYPE TABLE OF ven_gendata,
       gt_ven_address TYPE TABLE OF ven_address,
       gt_ven_purc    TYPE TABLE OF ven_purc,
       gt_ven_comdata TYPE TABLE OF ven_comdata,
       gt_ven_phone   TYPE TABLE OF ven_phone,
       gt_ven_fax     TYPE TABLE OF ven_fax,
       gt_ven_email   TYPE TABLE OF ven_email.

" Define Internal Tables for get export sheet customer
DATA : et_ven_comdata TYPE TABLE OF ven_e_comdata,
       es_ven_comdata TYPE ven_e_comdata.

FIELD-SYMBOLS: <fs_ve_comdata> TYPE ven_e_comdata.

*----------------------------------------------------------------------*
* Selection Screen
*----------------------------------------------------------------------*
TABLES : t001, but000.
SELECTION-SCREEN BEGIN OF BLOCK b1 WITH FRAME TITLE TEXT-001.
  PARAMETERS:
    p_cust RADIOBUTTON GROUP g1 DEFAULT 'X',
    p_vend RADIOBUTTON GROUP g1.

  SELECT-OPTIONS:
  s_bukrs FOR t001-bukrs,
  s_bp    FOR but000-partner.

  SELECTION-SCREEN SKIP 1.
  PARAMETERS:
  p_file TYPE string.

SELECTION-SCREEN END OF BLOCK b1.

AT SELECTION-SCREEN ON VALUE-REQUEST FOR p_file.

  DATA:
    lv_filename TYPE string,
    lv_path     TYPE string,
    lv_fullpath TYPE string,
    lv_action   TYPE i.

  cl_gui_frontend_services=>file_save_dialog(
    EXPORTING
      window_title      = 'Save Excel File'
      default_extension = 'xlsx'
      default_file_name = |select_Master.xlsx|
    CHANGING
      filename          = lv_filename
      path              = lv_path
      fullpath          = lv_fullpath
      user_action       = lv_action
    EXCEPTIONS
      OTHERS            = 1 ).

  IF sy-subrc = 0
     AND lv_action = cl_gui_frontend_services=>action_ok.

    p_file = lv_fullpath.

  ENDIF.

*----------------------------------------------------------------------*
*
*----------------------------------------------------------------------*



*----------------------------------------------------------------------*
* START-OF-SELECTION
*----------------------------------------------------------------------*

START-OF-SELECTION.

  PERFORM validate_input.

  IF p_cust = 'X'.
    lv_selected = 'cust'.
    p_file = |CUSTOMER_MASTER_{ sy-uzeit }.xlsx|.

    PERFORM get_cust_gendata.
    PERFORM change_langu_format CHANGING gt_cust_gendata.

    PERFORM get_cust_address.
    PERFORM change_langu_format CHANGING gt_cust_address.

    PERFORM get_cust_comdata.
    PERFORM get_e_cust_comdata.

    PERFORM get_cust_saledata.
    PERFORM get_cust_phone.
    PERFORM get_cust_email.
    PERFORM get_cust_fax.

    debugon = 1.
  ELSE.
    lv_selected = 'vend'.
    p_file = |VENDOR_MASTER_{ sy-uzeit }.xlsx|.

    PERFORM get_ven_gendata.
    PERFORM change_langu_format CHANGING gt_ven_gendata.

    PERFORM get_ven_address.
    PERFORM change_langu_format CHANGING gt_ven_address.

    PERFORM get_ven_purc.

    PERFORM get_ven_comdata.
    PERFORM get_e_ven_comdata.

    PERFORM get_ven_phone.
    PERFORM get_ven_email.
    PERFORM get_ven_fax.
    debugon = 1.
  ENDIF.

*----------------------------------------------------------------------*
* Export to excel
*----------------------------------------------------------------------*
  PERFORM export_excel USING lv_selected.

  DATA : lvl_sheet1 TYPE i,
         lvl_sheet2 TYPE i,
         lvl_sheet3 TYPE i,
         lvl_sheet4 TYPE i.

  IF lv_selected = 'cust'.
    lvl_sheet1 = lines( gt_cust_gendata ).
    lvl_sheet2 = lines( gt_cust_address ).
    lvl_sheet3 = lines( gt_cust_comdata ).
    lvl_sheet4 = lines( gt_cust_saledata ).
  ELSE.
    lvl_sheet1 = lines( gt_ven_gendata ).
    lvl_sheet2 = lines( gt_ven_address ).
    lvl_sheet3 = lines( gt_ven_purc ).
    lvl_sheet4 = lines( gt_ven_comdata ).
  ENDIF.

  SKIP.

  FORMAT COLOR COL_HEADING INTENSIFIED ON.
  WRITE : 'Customer Master Export Summary'.
  FORMAT RESET.

  ULINE.

  IF lv_selected = 'cust'.
    WRITE : 'SELECT : CUSTOMER'.
  ELSE.
    WRITE : 'SELECT : VENDOR'.
  ENDIF.

  IF s_bukrs IS NOT INITIAL.
    WRITE : /, 'Company Code : ', s_bukrs.
  ENDIF.

  IF s_bp IS NOT INITIAL.
    WRITE : /, 'Partner : ', s_bp.
  ENDIF.

  WRITE : /, |File Name : { p_file }|.
  SKIP.

  FORMAT COLOR COL_HEADING.
  WRITE: / 'Sheet Name',
           35 'Records'.
  FORMAT RESET.

  ULINE.

  IF lv_selected = 'cust'.
    WRITE: / 'General Data',
           32 lvl_sheet1.

    WRITE: / 'Address Data',
           32 lvl_sheet2.

    WRITE: / 'Company Data',
           32 lvl_sheet3.

    WRITE: / 'Sales Data',
           32 lvl_sheet4.
  ELSE.
    WRITE: / 'General Data',
           32 lvl_sheet1.

    WRITE: / 'Address Data',
           32 lvl_sheet2.

    WRITE: / 'Purchasing Data',
           32 lvl_sheet3.

    WRITE: / 'Company Data',
           32 lvl_sheet4.
  ENDIF.

  ULINE.

  FORMAT COLOR COL_HEADING INTENSIFIED ON.
  WRITE: / 'Actions'.
  SKIP.
  FORMAT RESET.

  FORMAT HOTSPOT ON.
  FORMAT COLOR COL_NORMAL.

  WRITE: / '[ Open Exported Excel ]'.

  FORMAT RESET.
  FORMAT HOTSPOT OFF.

  SKIP.

  IF lv_exprtstus IS NOT INITIAL.
    FORMAT COLOR COL_POSITIVE INTENSIFIED ON.
    WRITE: / 'Export Status : Success'.
  ELSE.
    FORMAT COLOR COL_NEGATIVE INTENSIFIED ON.
    WRITE: / 'Export Status : Fail'.
  ENDIF.
  FORMAT RESET.

  *----------------------------------------------------------------------*
* Click to open
*----------------------------------------------------------------------*
AT LINE-SELECTION.

  IF p_file IS NOT INITIAL.

    cl_gui_frontend_services=>execute(
      EXPORTING
        document = p_file
      EXCEPTIONS
        OTHERS   = 1 ).
  ENDIF.

*----------------------------------------------------------------------*
* FORMS (get internal table)
*----------------------------------------------------------------------*
FORM get_cust_gendata.
*  SELECT DISTINCT
*    b~partner, b~bu_group, b~name_org1, b~name_org2, b~name_org3, b~name_org4, k~anred, b~bu_sort1,b~bu_sort2, k~vbund,
*    a~street, a~house_num1, a~city2, a~post_code1, a~city1, a~country, a~str_suppl1, a~str_suppl2, a~str_suppl3,
*    k~stkzn, d~taxtype, d~taxnum, f~j_1tpbupl, f~default_branch, a~langu, ft~description
*
*    FROM but000 AS b
*    INNER JOIN kna1 AS k
*    ON b~partner = k~kunnr
*    INNER JOIN adrc AS a
*    ON k~adrnr = a~addrnumber
*    INNER JOIN knb1 AS comp
*    ON k~kunnr = comp~kunnr
*    INNER JOIN dfkkbptaxnum AS d
*    ON k~kunnr = d~partner
*    INNER JOIN fitha_pbupl_d_t AS ft
*    ON k~kunnr = ft~kunnr
*    INNER JOIN fitha_pbupl_d AS f
*    ON k~kunnr = f~kunnr
*
*    WHERE b~partner IN @s_bp
*    AND comp~bukrs IN @s_bukrs
*    AND a~nation <> 'I'
*
*  INTO TABLE @gt_cust_gendata.

  SELECT DISTINCT
       b~partner,
       b~bu_group,
       k~anred,
       b~name_org1,
       b~name_org2,
       b~name_org3,
       b~bu_sort1,
       b~bu_sort2,
       a~city1,
       a~city2,
       a~post_code1,
       a~street,
       a~house_num1,
       a~str_suppl1,
       a~str_suppl2,
       a~str_suppl3,
       a~country,
       a~langu,
       k~xcpdk,
       k~vbund,
       d~taxtype,
       d~taxnum,
       f~j_1tpbupl,
       f~default_branch,
       ft~description

    FROM but000 AS b
    INNER JOIN kna1 AS k
        ON b~partner = k~kunnr
    INNER JOIN adrc AS a
        ON k~adrnr = a~addrnumber
    INNER JOIN knb1 AS comp
        ON k~kunnr = comp~kunnr
    INNER JOIN dfkkbptaxnum AS d
        ON k~kunnr = d~partner

    " แก้จุดที่ 1: JOIN ตารางหลักของสาขา และกรองเอาเฉพาะสาขาที่แมตช์กัน

    INNER JOIN fitha_pbupl_d AS f ON k~kunnr = f~kunnr

    " แก้จุดที่ 2: JOIN ตาราง Text ต้องระบุด้วยว่าเอาสาขาไหน และภาษาอะไร ไม่ครั้นมันจะเบิ้ลสาขาอื่นมาด้วย
    LEFT JOIN fitha_pbupl_d_t AS ft ON f~kunnr = ft~kunnr
                                   AND f~j_1tpbupl = ft~j_1tpbupl
                                   AND ft~spras = @sy-langu
    WHERE b~partner IN @s_bp
      AND comp~bukrs IN @s_bukrs
      AND a~nation <> 'I'

  INTO TABLE @gt_cust_gendata.

ENDFORM.

*FORM change_clang_gendata.
*  LOOP AT gt_cust_gendata ASSIGNING FIELD-SYMBOL(<ls_data>).
*    CASE <ls_data>-langu.
*    WHEN '2' OR 'T'. " บางที SAP เก็บ T สำหรับไทย
*      <ls_data>-langu = 'TH'.
*    WHEN 'E' OR '1'.
*      <ls_data>-langu = 'ENG'.
*    WHEN OTHERS.
*      <ls_data>-langu = 'NULL'.
*  ENDCASE.
*  ENDLOOP.
*ENDFORM.

FORM get_cust_address.
  SELECT DISTINCT
    b~partner, a~nation, b~name_org1, b~name_org2, b~name_org3, a~city1, a~city2,
    a~post_code1, a~street, a~house_num1, a~str_suppl1, a~str_suppl2, a~str_suppl3, a~country, a~langu

  FROM but000 AS b INNER JOIN kna1 AS k
  ON b~partner = k~kunnr
  INNER JOIN adrc AS a
  ON k~adrnr = a~addrnumber
  " get company code
  INNER JOIN knb1 AS comp
  ON k~kunnr = comp~kunnr

  WHERE b~partner IN @s_bp
  AND comp~bukrs IN @s_bukrs
  AND a~nation = 'I'

  INTO TABLE @gt_cust_address.

ENDFORM.

FORM get_cust_comdata.
  SELECT DISTINCT
    b~partner, b~name_org1, k~bukrs, k~zuawa, k~akont, s~txt50, k~zterm,
 k~xzver, k~altkn, kw~witht, kw~qsrec, kw~wt_agent

  FROM but000 AS b INNER JOIN knb1 AS k
  ON b~partner = k~kunnr
  INNER JOIN knbw AS kw
  ON b~partner = kw~kunnr
  INNER JOIN skat AS s
  ON k~akont = s~saknr

  WHERE b~partner IN @s_bp
  AND k~bukrs IN @s_bukrs

  INTO TABLE @gt_cust_comdata.
ENDFORM.


FORM get_e_cust_comdata.
  LOOP AT gt_cust_comdata ASSIGNING FIELD-SYMBOL(<fs_or_comdata>).

    " 1. Cut Thai Letters (ผ่านการตรวจสอบของคุณ เรียบร้อยดีครับ)
    FIND REGEX '[ก-๏]' IN <fs_or_comdata>-txt50.
    IF sy-subrc = 0.
      CONTINUE. " เจอภาษาไทยข้ามไปเลย ไม่ทำต่อ
    ENDIF.

    " 2. เช็คว่ามี Partner + Bukrs (บริษัท) นี้อยู่ในตารางส่งออกแล้วหรือยัง?
    READ TABLE et_cust_comdata ASSIGNING <fs_e_comdata>
      WITH KEY partner = <fs_or_comdata>-partner
               bukrs   = <fs_or_comdata>-bukrs.

    IF sy-subrc <> 0.
      " ---------------------------------------------------------
      " กรณีที่ 1: ยังไม่มีข้อมูลคู่นี้ในตารางใหม่ -> สร้างบรรทัดใหม่
      " ---------------------------------------------------------
      CLEAR es_cust_comdata.

      " ย้ายข้อมูลฟิลด์ที่ชื่อเหมือนกันจากตารางเดิมมาตารางใหม่ (Safe & Clean)
      MOVE-CORRESPONDING <fs_or_comdata> TO es_cust_comdata.

      " เช็คค่าจากฟิลด์ witht เพื่อติ๊กฟิลด์เป้าหมาย (สมมติว่าเป็น 'X' หรือคงค่าเดิมไว้)
      CASE <fs_or_comdata>-witht.
        WHEN 'N1'. es_cust_comdata-n1 = 'X'.
        WHEN 'N2'. es_cust_comdata-n2 = 'X'.
        WHEN 'P1'. es_cust_comdata-p1 = 'X'.
        WHEN 'R1'. es_cust_comdata-r1 = 'X'.
        WHEN 'R2'. es_cust_comdata-r2 = 'X'.
      ENDCASE.

      APPEND es_cust_comdata TO et_cust_comdata.

    ELSE.
      " ---------------------------------------------------------
      " กรณีที่ 2: มีข้อมูล Partner + Bukrs นี้อยู่แล้ว -> อัปเดตฟิลด์เพิ่มเข้าไป
      " ---------------------------------------------------------
      CASE <fs_or_comdata>-witht.
        WHEN 'N1'. <fs_e_comdata>-n1 = 'X'.
        WHEN 'N2'. <fs_e_comdata>-n2 = 'X'.
        WHEN 'P1'. <fs_e_comdata>-p1 = 'X'.
        WHEN 'R1'. <fs_e_comdata>-r1 = 'X'.
        WHEN 'R2'. <fs_e_comdata>-r2 = 'X'.
      ENDCASE.

    ENDIF.

  ENDLOOP.
ENDFORM.

FORM get_cust_saledata.
  SELECT DISTINCT
       b~partner, b~name_org1, kv~vkorg, kv~vtweg, kv~spart, kv~versg, kv~kalks,
    kv~waers, kv~ktgrd, kv~zterm, kv~vwerk, kv~kvgr1, kv~kurst, ki~aland,
    ki~tatyp, ki~taxkd
  FROM but000 AS b INNER JOIN knvv AS kv
  ON b~partner = kv~kunnr
  INNER JOIN knvi AS ki
  ON b~partner = ki~kunnr
  INNER JOIN knb1 AS k1
  ON b~partner = k1~kunnr

  WHERE b~partner IN @s_bp
  AND k1~bukrs IN @s_bukrs

  INTO TABLE @gt_cust_saledata.
ENDFORM.

FORM get_cust_phone.
  SELECT DISTINCT
       b~partner, b~name_org1, a2~consnumber, a2~country, a2~flgdefault, a2~home_flag,
       a2~tel_number, a2~tel_extens, a2~telnr_long, a2~telnr_call, a2~dft_receiv, a2~r3_user

  FROM but000 AS b
  INNER JOIN KNb1 AS k1
  ON b~partner = k1~kunnr
  INNER JOIN kna1 AS k
  ON b~partner = k~kunnr
  INNER JOIN adr2 AS a2
  ON k~adrnr = a2~addrnumber

  WHERE b~partner IN @s_bp
  AND k1~bukrs IN @s_bukrs

  INTO TABLE @gt_cust_phone.
ENDFORM.

FORM get_cust_email.
  SELECT DISTINCT
       b~partner, b~name_org1, a6~consnumber, a6~flgdefault, a6~home_flag, a6~smtp_addr

  FROM but000 AS b
  INNER JOIN KNb1 AS k1
  ON b~partner = k1~kunnr
  INNER JOIN kna1 AS k
  ON b~partner = k~kunnr
  INNER JOIN adr6 AS a6
  ON k~adrnr = a6~addrnumber

  WHERE b~partner IN @s_bp
  AND k1~bukrs IN @s_bukrs

  INTO TABLE @gt_cust_email.

ENDFORM.

FORM get_cust_fax.
  SELECT DISTINCT
       b~partner, b~name_org1, a3~consnumber, a3~country, a3~flgdefault, a3~home_flag,
       a3~fax_number, a3~fax_extens, a3~faxnr_long, a3~faxnr_call

  FROM but000 AS b
  INNER JOIN knb1 AS k1
  ON b~partner = k1~kunnr
  INNER JOIN kna1 AS k
  ON b~partner = k~kunnr
  INNER JOIN adr3 AS a3
  ON k~adrnr = a3~addrnumber

  WHERE b~partner IN @s_bp
  AND k1~bukrs IN @s_bukrs

  INTO TABLE @gt_cust_fax.
ENDFORM.

FORM get_ven_gendata.
*  SELECT DISTINCT  b~partner, b~bu_group, l~anred, b~name_org1, b~name_org2, b~bu_sort1, b~bu_sort2,
*         a~city1, a~city2, a~post_code1, a~street, a~house_num1, a~str_suppl1, a~str_suppl2,
*         a~country, l~vbund, l~dtaws, l~xzemp, l~stkzn, a~langu, d~taxnum, bk~banks, bk~bankl,
*         bk~bankn, bk~koinh, bk~accname, fk~j_1tpbupl, fk~default_branch, ft~description
*
*  FROM but000 AS b INNER JOIN lfa1 AS l
*  ON b~partner = l~lifnr
*  INNER JOIN adrc AS a
*  ON l~adrnr = a~addrnumber
*  INNER JOIN dfkkbptaxnum AS d
*  ON b~partner = d~partner
*  INNER JOIN but0bk AS bk
*  ON b~partner = bk~partner
*  INNER JOIN fitha_pbupl_k AS fk
*  ON b~partner = fk~lifnr
*  INNER JOIN fitha_pbupl_k_t AS ft
*  ON b~partner = ft~lifnr
*  INNER JOIN lfb1 AS lb
*  ON b~partner = lb~lifnr
*
*  WHERE b~partner IN @s_bp
*  AND lb~bukrs IN @s_bukrs
*
*  INTO TABLE @gt_ven_gendata.

  SELECT DISTINCT
    b~partner,
       b~bu_group, l~anred, b~name_org1, b~name_org2, b~name_org3, b~bu_sort1, b~bu_sort2, a~city1, a~city2,
       a~post_code1, a~street, a~house_num1, a~str_suppl1, a~str_suppl2, a~str_suppl3, a~country,
       a~langu, l~xcpdk, l~vbund, l~xzemp, l~dtaws, l~stkzn, d~taxtype, d~taxnum,
       bk~banks, bk~bankl, bk~bankn, bk~koinh, bk~accname, fk~j_1tpbupl, fk~default_branch, ft~description
    FROM but000 AS b
    INNER JOIN lfa1 AS l ON b~partner = l~lifnr
    INNER JOIN adrc AS a ON l~adrnr = a~addrnumber
    INNER JOIN lfb1 AS lb ON b~partner = lb~lifnr

    " ใช้ LEFT JOIN สำหรับตารางที่ไม่บังคับว่าต้องมีข้อมูลเสมอไป
    LEFT JOIN dfkkbptaxnum AS d ON b~partner = d~partner
    LEFT JOIN but0bk AS bk ON b~partner = bk~partner

    " ตารางสาขา Vendor
    INNER JOIN fitha_pbupl_k AS fk ON b~partner = fk~lifnr

    " แก้ไขจุดสำคัญ: เชื่อม Text ด้วย รหัสสาขา + ภาษา
    LEFT JOIN fitha_pbupl_k_t AS ft ON fk~lifnr     = ft~lifnr
                                   AND fk~j_1tpbupl = ft~j_1tpbupl
                                   AND ft~spras     = @sy-langu

    WHERE b~partner IN @s_bp
      AND lb~bukrs IN @s_bukrs
     AND a~nation <> 'I'
    INTO TABLE @gt_ven_gendata.
ENDFORM.

FORM get_ven_address.
  SELECT DISTINCT
       b~partner, a~nation, b~name_org1, b~name_org2, b~bu_sort1, b~bu_sort2, a~city1, a~city2,
       a~post_code1, a~street, a~house_num1, a~str_suppl1, a~str_suppl2, a~str_suppl3, a~country, a~langu

  FROM but000 AS b INNER JOIN lfa1 AS l
  ON b~partner = l~lifnr
  INNER JOIN adrc AS a
  ON l~adrnr = a~addrnumber
  INNER JOIN lfb1 AS lb
  ON b~partner = lb~lifnr

  WHERE b~partner IN @s_bp
  AND lb~bukrs IN @s_bukrs
  AND a~nation = 'I'
  INTO TABLE @gt_ven_address.
ENDFORM.

FORM get_ven_purc.
*  SELECT DISTINCT b~partner, b~name_org1, lm~ekorg, lm~waers, lm~verkf, lm~telf1,
*         lb~zterm, lm~inco1, lm~inco2, lm~webre
*
*  FROM but000 AS b INNER JOIN lfm1 AS lm
*  ON b~partner = lm~lifnr
*  INNER JOIN lfb1 AS lb
*  ON b~partner = lb~lifnr
*
*  WHERE b~partner IN @s_bp
*  AND lb~bukrs IN @s_bukrs
*
*  INTO TABLE @gt_ven_purc.

  SELECT DISTINCT
       l~lifnr,
       b~name_org1,
       lm~ekorg,
       lm~waers,
       lm~verkf,
       lm~telf1,
       lm~minbw,
       lb~zterm,
       lm~inco1,
       lm~inco2,
       lm~webre,
       lm~inco2_l
  FROM but000 AS b
  INNER JOIN lfa1 AS l
    ON b~partner = l~lifnr
  INNER JOIN lfm1 AS lm
    ON l~lifnr = lm~lifnr
  INNER JOIN lfb1 AS lb
    ON l~lifnr = lb~lifnr
  WHERE b~partner IN @s_bp
    AND lb~bukrs   IN @s_bukrs
  INTO TABLE @gt_ven_purc.
ENDFORM.

FORM get_ven_comdata.
  SELECT DISTINCT
       la~lifnr,
       la~name1,
       l1~bukrs,
       l1~pernr,
       l1~zuawa,
       l1~hbkid,
       l1~fdgrv,
       l1~zterm,
       l1~zwels,
       l1~akont,
       s~txt50,
       l1~uzawe,
       l1~busab,
       l1~altkn,
       lw~witht,
       lw~qsrec,
       lw~wt_subjct

*  FROM lfb1 AS l1 INNER JOIN lfbw AS lw
*  ON l1~lifnr = lw~lifnr
*  AND l1~bukrs = lw~bukrs
*  INNER JOIN lfa1 AS la
*  ON l1~lifnr = la~lifnr
*
*  WHERE l1~lifnr IN @s_bp
*  AND l1~bukrs IN @s_bukrs

  FROM lfb1 AS l1
  INNER JOIN lfbw AS lw
    ON l1~lifnr = lw~lifnr
   AND l1~bukrs = lw~bukrs
  INNER JOIN lfa1 AS la
    ON l1~lifnr = la~lifnr
  LEFT JOIN skat AS s
    ON l1~akont = s~saknr
  WHERE l1~lifnr IN @s_bp
    AND l1~bukrs IN @s_bukrs

  INTO TABLE @gt_ven_comdata.
ENDFORM.

FORM get_e_ven_comdata.
  LOOP AT gt_ven_comdata ASSIGNING FIELD-SYMBOL(<fs_vor_comdata>).

    " 1. Cut Thai Letters (ผ่านการตรวจสอบของคุณ เรียบร้อยดีครับ)
*    FIND REGEX '[ก-๏]' IN <fs_vor_comdata>-txt50.
*    IF sy-subrc = 0.
*      CONTINUE. " เจอภาษาไทยข้ามไปเลย ไม่ทำต่อ
*    ENDIF.

    " 2. เช็คว่ามี lifnr + Bukrs (บริษัท) นี้อยู่ในตารางส่งออกแล้วหรือยัง?
    READ TABLE et_ven_comdata ASSIGNING <fs_ve_comdata>
      WITH KEY lifnr = <fs_vor_comdata>-lifnr
               bukrs   = <fs_vor_comdata>-bukrs.

    IF sy-subrc <> 0.
      " ---------------------------------------------------------
      " กรณีที่ 1: ยังไม่มีข้อมูลคู่นี้ในตารางใหม่ -> สร้างบรรทัดใหม่
      " ---------------------------------------------------------
      CLEAR es_ven_comdata.

      " ย้ายข้อมูลฟิลด์ที่ชื่อเหมือนกันจากตารางเดิมมาตารางใหม่ (Safe & Clean)
      MOVE-CORRESPONDING <fs_vor_comdata> TO es_ven_comdata.

      " เช็คค่าจากฟิลด์ witht เพื่อติ๊กฟิลด์เป้าหมาย (สมมติว่าเป็น 'X' หรือคงค่าเดิมไว้)
      CASE <fs_vor_comdata>-witht.
        WHEN 'D1'. es_ven_comdata-d1 = 'X'.
        WHEN 'I1'. es_ven_comdata-i1 = 'X'.
        WHEN 'I2'. es_ven_comdata-i2 = 'X'.
        WHEN 'P1'. es_ven_comdata-p1 = 'X'.
        WHEN 'P2'. es_ven_comdata-p2 = 'X'.
        WHEN 'P3'. es_ven_comdata-p3 = 'X'.
      ENDCASE.

      APPEND es_ven_comdata TO et_ven_comdata.

    ELSE.
      " ---------------------------------------------------------
      " กรณีที่ 2: มีข้อมูล Partner + Bukrs นี้อยู่แล้ว -> อัปเดตฟิลด์เพิ่มเข้าไป
      " ---------------------------------------------------------
      CASE <fs_vor_comdata>-witht.
        WHEN 'D1'. <fs_ve_comdata>-d1 = 'X'.
        WHEN 'I1'. <fs_ve_comdata>-i1 = 'X'.
        WHEN 'I2'. <fs_ve_comdata>-i2 = 'X'.
        WHEN 'P1'. <fs_ve_comdata>-p1 = 'X'.
        WHEN 'P2'. <fs_ve_comdata>-p2 = 'X'.
        WHEN 'P3'. <fs_ve_comdata>-p3 = 'X'.
      ENDCASE.

    ENDIF.

  ENDLOOP.
ENDFORM.

FORM get_ven_phone.
  SELECT DISTINCT
       b~partner, b~name_org1, a2~consnumber, a2~country, a2~flgdefault, a2~home_flag,
       a2~tel_number, a2~tel_extens, a2~telnr_long, a2~telnr_call, a2~dft_receiv, a2~r3_user

  FROM but000 AS b
  INNER JOIN lfb1 AS lb
  ON b~partner = lb~lifnr
  INNER JOIN lfa1 AS la
  ON b~partner = la~lifnr
  INNER JOIN adr2 AS a2
  ON la~adrnr = a2~addrnumber

  WHERE b~partner IN @s_bp
  AND lb~bukrs IN @s_bukrs

  INTO TABLE @gt_ven_phone.

ENDFORM.

FORM get_ven_email.
  SELECT DISTINCT
       b~partner, b~name_org1, fk~j_1tpbupl, ft~description, a6~consnumber, a6~flgdefault,
       a6~home_flag, a6~smtp_addr

  FROM but000 AS b
  INNER JOIN lfb1 AS lb
  ON b~partner = lb~lifnr
  INNER JOIN lfa1 AS la
  ON b~partner = la~lifnr
  INNER JOIN adr6 AS a6
  ON la~adrnr = a6~addrnumber

  INNER JOIN FITHA_PBUPL_K AS fk
  ON lb~lifnr = fk~lifnr
  LEFT JOIN FITHA_PBUPL_K_T AS ft
  ON lb~lifnr = ft~lifnr
  AND fk~j_1tpbupl = ft~j_1tpbupl

  WHERE b~partner IN @s_bp
  AND lb~bukrs IN @s_bukrs

  INTO TABLE @gt_ven_email.
ENDFORM.

FORM get_ven_fax.
  SELECT DISTINCT
       b~partner, b~name_org1, a3~consnumber, a3~country, a3~flgdefault, a3~home_flag,
       a3~fax_number, a3~fax_extens, a3~faxnr_long, a3~faxnr_call

  FROM but000 AS b
  INNER JOIN lfb1 AS lb
  ON b~partner = lb~lifnr
  INNER JOIN lfa1 AS la
  ON b~partner = la~lifnr
  INNER JOIN adr3 AS a3
  ON la~adrnr = a3~addrnumber

  WHERE b~partner IN @s_bp
  AND lb~bukrs IN @s_bukrs

  INTO TABLE @gt_ven_fax.
ENDFORM.

*----------------------------------------------------------------------*
* Convert Language
*----------------------------------------------------------------------*

FORM change_langu_format CHANGING ct_data TYPE STANDARD TABLE.

  FIELD-SYMBOLS <ls_data> TYPE any.
  LOOP AT ct_data ASSIGNING <ls_data>.

    ASSIGN COMPONENT 'LANGU' OF STRUCTURE <ls_data> TO FIELD-SYMBOL(<lv_langu>).
    IF sy-subrc = 0.
      CASE <lv_langu>.
        WHEN '2' OR 'T'.
          <lv_langu> = 'TH'.
        WHEN 'E' OR '1'.
          <lv_langu> = 'ENG'.
        WHEN OTHERS.
          <lv_langu> = 'NULL'.
      ENDCASE.
    ENDIF.
  ENDLOOP.

ENDFORM.

*----------------------------------------------------------------------*
* Config Excel
*----------------------------------------------------------------------*

FORM export_excel USING pv_selected TYPE char4.
  DATA : lo_excel TYPE REF TO zcl_excel.
  CREATE OBJECT lo_excel.

  DATA lo_sheet TYPE REF TO zcl_excel_worksheet.

  CASE pv_selected.
    WHEN 'cust'.
      lo_sheet = lo_excel->get_active_worksheet( ).
      lo_sheet->set_title( 'General data' ).
      lo_sheet->bind_table( ip_table = gt_cust_gendata ).
      lo_sheet->set_cell( ip_column = 'R'
                    ip_row    = 1
                    ip_value  = 'Language' ).

      lo_sheet = lo_excel->add_new_worksheet( ).
      lo_sheet->set_title( 'International Address Version' ).
      lo_sheet->bind_table( ip_table = gt_cust_address ).
      lo_sheet->set_cell( ip_column = 'O'
                    ip_row    = 1
                    ip_value  = 'Language' ).

*      lo_sheet = lo_excel->add_new_worksheet( ).
*      lo_sheet->set_title( 'Company Data' ).
*      lo_sheet->bind_table( ip_table = gt_cust_comdata ).

      lo_sheet = lo_excel->add_new_worksheet( ).
      lo_sheet->set_title( 'Company Data' ).
      lo_sheet->bind_table( ip_table = et_cust_comdata ).

      lo_sheet = lo_excel->add_new_worksheet( ).
      lo_sheet->set_title( 'Sales Data' ).
      lo_sheet->bind_table( ip_table = gt_cust_saledata ).

      lo_sheet = lo_excel->add_new_worksheet( ).
      lo_sheet->set_title( 'Phone' ).
      lo_sheet->bind_table( ip_table = gt_cust_phone ).

      lo_sheet = lo_excel->add_new_worksheet( ).
      lo_sheet->set_title( 'Email' ).
      lo_sheet->bind_table( ip_table = gt_cust_email ).

      lo_sheet = lo_excel->add_new_worksheet( ).
      lo_sheet->set_title( 'Fax' ).
      lo_sheet->bind_table( ip_table = gt_cust_fax ).

    WHEN 'vend'.
      lo_sheet = lo_excel->get_active_worksheet( ).
      lo_sheet->set_title( 'General data' ).
      lo_sheet->bind_table( ip_table = gt_ven_gendata ).
      lo_sheet->set_cell( ip_column = 'R'
                     ip_row   = 1
                     ip_value = 'Language' ).

      lo_sheet = lo_excel->add_new_worksheet( ).
      lo_sheet->set_title( 'International Address Version' ).
      lo_sheet->bind_table( ip_table = gt_ven_address ).
      lo_sheet->set_cell( ip_column = 'P'
                    ip_row    = 1
                    ip_value  = 'Language' ).

      lo_sheet = lo_excel->add_new_worksheet( ).
      lo_sheet->set_title( 'Purchasing data' ).
      lo_sheet->bind_table( ip_table = gt_ven_purc ).

*      lo_sheet = lo_excel->add_new_worksheet( ).
*      lo_sheet->set_title( 'Old Company data' ).
*      lo_sheet->bind_table( ip_table = gt_ven_comdata ).

      lo_sheet = lo_excel->add_new_worksheet( ).
      lo_sheet->set_title( 'Company data' ).
      lo_sheet->bind_table( ip_table = et_ven_comdata ).

      lo_sheet = lo_excel->add_new_worksheet( ).
      lo_sheet->set_title( 'Phone' ).
      lo_sheet->bind_table( ip_table = gt_ven_phone ).

      lo_sheet = lo_excel->add_new_worksheet( ).
      lo_sheet->set_title( 'Email' ).
      lo_sheet->bind_table( ip_table = gt_ven_email ).

      lo_sheet = lo_excel->add_new_worksheet( ).
      lo_sheet->set_title( 'Fax' ).
      lo_sheet->bind_table( ip_table = gt_ven_fax ).
    WHEN OTHERS.
      MESSAGE 'pv_selected undectected' TYPE 'E'.
  ENDCASE.

  DATA:
    lo_writer  TYPE REF TO zif_excel_writer,
    lv_xstring TYPE xstring,
    lt_binary  TYPE solix_tab,
    ls_binary  TYPE solix.

  CREATE OBJECT lo_writer
    TYPE zcl_excel_writer_2007.

  lv_xstring = lo_writer->write_file( lo_excel ).

  CALL FUNCTION 'SCMS_XSTRING_TO_BINARY'
    EXPORTING
      buffer     = lv_xstring
    TABLES
      binary_tab = lt_binary.

  cl_gui_frontend_services=>gui_download(
  EXPORTING
    filename     = p_file
    filetype     = 'BIN'
    bin_filesize = xstrlen( lv_xstring )
  CHANGING
    data_tab     = lt_binary
  EXCEPTIONS
    OTHERS       = 1 ).

  IF sy-subrc = 0.
    MESSAGE 'Excel file downloaded successfully' TYPE 'S'.
    lv_exprtstus = 'success'.
*    cl_gui_frontend_services=>execute(
*      EXPORTING
*        document = p_file
*    ).

  ELSE.
    MESSAGE s001(00) WITH 'Error downloading Excel file' DISPLAY LIKE 'E'.
    LEAVE LIST-PROCESSING.
  ENDIF.
ENDFORM.

FORM validate_input.
  IF p_file IS INITIAL.
    MESSAGE 'Please specify file path' TYPE 'E'.
  ENDIF.
ENDFORM.
