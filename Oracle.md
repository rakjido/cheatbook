

# Oracle

INSERT INTO <TABLE B>
SELECT * FROM <TABLE A>

```sql

insert into NCR_DMI_OPT_RISK_POSN(
             TDATE
            ,POSN_ID
            ,POSN_SEQ
            ,OPT_RISK_AGGR_UNIT_CD
            ,OPT_RISK_AGGR_UNIT_NM
            ,CNTY_CD
            ,OPT_RGT_TY_CD
            ,UASSET_CD
            ,UASSET_TY_CD
            ,UASSET_NM
            ,UASSET_PRICE
            ,ISS_UASSET_PRICE
            ,STRIKE
            ,CONTRSZ
            ,ISS_DT
            ,MAT_DT
            ,IR_TBAND_CD
            ,DELTA
            ,GAMMA
            ,VEGA
            ,VOL
            ,DELTA_POSN
            ,GAMMA_POSN
            ,VEGA_POSN
            ,CUR_CD
            ,BASE_ER
            ,KRW_CONV_DELTA_POSN
            ,KRW_CONV_GAMMA_POSN
            ,KRW_CONV_VEGA_POSN
            ,SENS_DATA_SRC_CD
            ,VOL_DATA_SRC_CD
            ,DOTM_YN
            ,CRE_ID
    )
    select
            posn.TDATE
           ,posn.POSN_ID
           ,1 as POSN_SEQ
           ,NVL(
                 CASE WHEN prod.STKIND_CD = 'KOSPI200' THEN 'KOSPI' END
           ,'NA') as OPT_RISK_AGGR_UNIT_CD
           ,prod.STKIND_CD as OPT_RISK_AGGR_UNIT_NM
           ,PROD.STK_MKT_CD as CNTY_CD
           ,prod.OPT_RGT_TY_CD
           ,nvl(prod.UASSET_CD,'MD')
           ,'11' AS UASSET_TY_CD
           ,prod.UASSET_NM
           ,nvl(prod.UASSET_PRICE,999123)
           ,nvl(prod.ISS_UASSET_PRICE,999123)
           ,nvl(prod.STRIKE , 999123)
           ,prod.CONV_RT as CONTRSZ
           ,prod.ISS_DT
           ,prod.MAT_DT
           ,CASE
                  WHEN TO_NUMBER(TO_DATE(prod.MAT_DT,'yyyymmdd')- TO_DATE(#{TDATE},'yyyymmdd'))/365 = 0 THEN '01'
                  ELSE (SELECT NVL(IR_TBAND_CD,0) FROM NCR_DMI_IR_TBAND_RISK_WGT WHERE  TO_NUMBER(TO_DATE(prod.MAT_DT,'yyyymmdd')- TO_DATE(#{TDATE},'yyyymmdd'))/365 <= END_MAT2
                         AND TO_NUMBER(TO_DATE(prod.MAT_DT,'yyyymmdd')-TO_DATE(#{TDATE},'yyyymmdd'))/365 > BEG_MAT2)
            END AS IR_TBAND_CD
           , sens.DELTA as DELTA
           , sens.GAMMA as  GAMMA
           , sens.VEGA  as  VEGA
           , sens.VOL AS VOL
           , sens.DELTA * prod.UASSET_PRICE * posn.QTY AS DELTA_POSN
           , 0.5  * sens.GAMMA  *( power( (UASSET_PRICE * 0.08)  ,2 ) ) * posn.QTY  AS GAMMA_POSN
           , sens.VEGA * sens.VOL * posn.QTY * 0.25 AS VEGA_POSN
           , prod.CUR_CD
           , 1 as BASE_ER
           , sens.DELTA*prod.UASSET_PRICE*posn.QTY AS KRW_CONV_DELTA_POSN
           , 0.5  * sens.GAMMA  *( power( (UASSET_PRICE * 0.08)  ,2 ) ) * posn.QTY  AS KRW_CONV_GAMMA_POSN
           , sens.VEGA * sens.VOL * posn.QTY * 0.25 AS KRW_VEGA_POSN
           , nvl(sens.SENS_DATA_SRC_CD,'MD')  AS  SENS_DATA_SRC_CD
           , nvl(sens.VOL_DATA_SRC_CD,'MD') AS VOL_DATA_SRC_CD
           , CASE WHEN prod.OPT_RGT_TY_CD='C' AND posn.QTY <0 THEN
                        CASE WHEN ( SELECT LQ_RECOG_YN FROM NCR_DMI_IND WHERE IND_CD=prod.STKIND_CD)='Y' AND  SUBSTR(prod.UASSET_CD,1,1)='A' THEN
                                         CASE WHEN prod.STRIKE > prod.ISS_UASSET_PRICE * (1+0.08+0.08) THEN 'Y'
                                                 ELSE 'N'
                                         END
                                  WHEN ( SELECT LQ_RECOG_YN FROM NCR_DMI_IND WHERE IND_CD=prod.STKIND_CD)='N' AND  SUBSTR(prod.UASSET_CD,1,1)='A' THEN
                                         CASE WHEN prod.STRIKE > prod.ISS_UASSET_PRICE * (1+0.12+0.08) THEN 'Y'
                                                 ELSE 'N'
                                         END
                                  WHEN ( SELECT LQ_RECOG_YN FROM NCR_DMI_IND WHERE IND_CD=prod.STKIND_CD)='Y' AND  SUBSTR(prod.UASSET_CD,1,1)<>'A' THEN
                                         CASE WHEN prod.STRIKE > prod.ISS_UASSET_PRICE * (1+0.04+0.08) THEN 'Y'
                                                 ELSE 'N'
                                         END
                                  ELSE
                                         CASE WHEN prod.STRIKE > prod.ISS_UASSET_PRICE * (1+0.12+0.08) THEN 'Y'
                                                 ELSE 'N'
                                         END
                         END
                     WHEN prod.OPT_RGT_TY_CD='P' AND posn.QTY <0 THEN
                        CASE WHEN ( SELECT LQ_RECOG_YN FROM NCR_DMI_IND WHERE IND_CD=prod.STKIND_CD)='Y' AND  SUBSTR(prod.UASSET_CD,1,1)='A' THEN
                                        CASE WHEN prod.STRIKE < prod.ISS_UASSET_PRICE * (1-0.08-0.08) THEN 'Y'
                                                 ELSE 'N'
                                         END
                                  WHEN ( SELECT LQ_RECOG_YN FROM NCR_DMI_IND WHERE IND_CD=prod.STKIND_CD)='N' AND  SUBSTR(prod.UASSET_CD,1,1)='A' THEN
                                         CASE WHEN prod.STRIKE < prod.ISS_UASSET_PRICE * (1-0.12-0.08) THEN 'Y'
                                                 ELSE 'N'
                                         END
                                  WHEN ( SELECT LQ_RECOG_YN FROM NCR_DMI_IND WHERE IND_CD=prod.STKIND_CD)='Y' AND  SUBSTR(prod.UASSET_CD,1,1)<>'A' THEN
                                         CASE WHEN prod.STRIKE < prod.ISS_UASSET_PRICE * (1-0.04-0.08) THEN 'Y'
                                                 ELSE 'N'
                                         END
                                  ELSE
                                         CASE WHEN prod.STRIKE < prod.ISS_UASSET_PRICE * (1-0.12-0.08) THEN 'Y'
                                                 ELSE 'N'
                                         END
                         END
             END as DOTM_YN
           , '504c' as CRE_ID
     from NCR_IF_POSN posn
            , NCR_IF_PROD_ELW prod
            , NCR_DMI_STK_MKT mkt
            , ( SELECT
                     TDATE , PROD_CD , DELTA ,  GAMMA , VEGA  , VOL , SENS_DATA_SRC_CD , VOL_DATA_SRC_CD
                 FROM (
                         SELECT
                                 a.TDATE , a.PROD_Cd , a.UASSET_CD , a.DELTA , a.GAMMA , a.VEGA , b.VOL , a.DATA_SRC_CD AS SENS_DATA_SRC_CD , b.DATA_SRC_CD AS VOL_DATA_SRC_CD  ,  ROW_number() over(   partition by  a.PROD_CD, a.UASSET_CD order by decode(a.DATA_SRC_CD,'01',1,'92',2,3)) as rn
                         FROM
                                 NCR_IF_SENS a , NCR_IF_VOL b
                         WHERE
                                 a.TDATE = b.TDATe AND a.prod_cd = b.prod_cd AND a.uasset_cd = b.uasset_cd AND a.data_src_cd = b.data_src_cd
               ) WHERE rn =1 AND TDATE = #{TDATE} ) sens
      where
             posn.TDATE = prod.TDATE
      and    posn.PROD_CD = prod.PROD_CD
      and    posn.TDATE = sens.TDATE(+)
      and    posn.PROD_CD = sens.PROD_CD(+)
      and    prod.stk_mkt_cd = mkt.stk_mkt_cd(+)
      and    posn.prod_cls_lrg_cd not in ('06','07','08','09','10','11','12','13','14')
      and    posn.TDATE = #{TDATE}
```


UPDATE CASE

```sql
UPDATE NCR_DMI_CNTRP_CRGRD d SET CR_RISK_WGT = (
SELECT
              CASE WHEN a.CNTRP_TY_CD IN ('01','02','03','04','05','06') THEN (SELECT RISK_WGT FROM NCR_DMI_CR_RISK_WGT WHERE CNTRP_TY_CD = a.CNTRP_TY_CD)
                      WHEN a.CNTRP_TY_CD IN ('15') THEN (SELECT RISK_WGT FROM NCR_DMI_CR_RISK_WGT WHERE CNTRP_TY_CD = a.CNTRP_TY_CD)
                      WHEN a.CNTRP_TY_CD NOT IN ('01','02','03','04','05','06','15') THEN (
                             SELECT RISK_WGT
                             FROM (SELECT  wgt.CNTRP_TY_CD,
                                   (SELECT CRGRD_SEQ FROM NCR_DMI_CRGRD_MAP   WHERE CRGRD_CD=wgt.END_CRGRD_CD) as END_CRGRD_SEQ,
                                   (SELECT CRGRD_SEQ FROM NCR_DMI_CRGRD_MAP  WHERE CRGRD_CD=wgt.BEG_CRGRD_CD) as BEG_CRGRD_SEQ,
                                   wgt.RISK_WGT
                                  FROM NCR_DMI_CR_RISK_WGT wgt
                               ) cvwgt
                               WHERE CNTRP_TY_CD=a.CNTRP_TY_CD
                               AND NVL(c.CRGRD_SEQ,30) BETWEEN END_CRGRD_SEQ AND BEG_CRGRD_SEQ
                         )          
              END as CR_RISK_WGT
FROM NCR_DMI_CNTRP a, (SELECT * FROM NCR_DMI_CNTRP_CRGRD WHERE CAI_CD='00' AND TDATE= #{TDATE}) b, NCR_DMI_CRGRD_MAP c
WHERE a.CNTRP_ID=b.CNTRP_ID(+)
AND b.ISSUER_CRGRD_CD=c.CRGRD_CD (+) AND a.CNTRP_ID = d.CNTRP_ID) WHERE TDATE = #{TDATE} AND CAI_CD = '00'
```


MERGE CASE QUERY

```sql
MERGE INTO NCR_DMI_CNTRP a
USING NCR_IF_M_CNTRP b
ON(a.CNTRP_ID = b.CNTRP_ID)
WHEN MATCHED THEN
        UPDATE SET a.CNTRP_NM = b.CNTRP_NM
                         , A.CNTRP_TY_CD = b.CNTRP_TY_CD
                         , A.CORPNO = b.CORPNO
                         , A.BIZNO = B.BIZNO
                         , A.JMNO = B.JMNO  
                         , A.CNTY_CD = B.CNTY_CD
                         , A.STD_INDY_CLS_CD = NULL
                         , A.AFFPRSN_TY_CD = B.AFFPRSN_TY_CD
                         , A.CRE_ID = '401a'
                         , A.CRE_DTIME = SYSDATE
WHEN NOT MATCHED THEN
        INSERT VALUES(b.CNTRP_ID , b.CNTRP_NM , b.CNTRP_TY_CD , b.CORPNO , b.BIZNO , b.JMNO , b.CNTY_CD  ,NULL ,NULL, b.AFFPRSN_TY_CD , '401a2', SYSDATE  , NULL,NULL)
```        
