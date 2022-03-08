Test Question . The table dividend consists of companies and their respective fiscal year of dividend
distribution. Some companies give dividend every year, but some companies do not. From
investment point of view, Those companies who have given dividend for at least 3 consecutive
years in the past are labelled as 'valuestocks'. Please write a query to find the 'valuestocks' i.e the
companies that have given dividend for at least 3 consecutive year in the past.
 
/*creation of table */
CREATE TABLE Data_dividend.sql (
company VARCHAR(12) NUT NULL,
fiscal_year INT NUT NULL,
) 

/* entry of test data*/
INSERT INTO Data_dividend.sql
 ('AHPC',20702071),
 ('AHPC',20712072),
 ('AHPC',20732074),
 ('AHPC',20762077),
 ('CZBIL',20692070),
 ('CZBIL',20702071),
 ('CZBIL',20712072),
 ('CZBIL',20732074),
 ('GBIME',20692070),
 ('GBIME',20702071),
 ('GBIME',20712072),
 ('GBIME',20732074);

 for quering the valued stocks 
 
WITH RECURSIVE pre1 AS (
  SELECT company, fiscal_year/10000::INT AS yr FROM dividend), pre2 AS (
  SELECT pre1.company, pre1.yr, 1 AS cs 
   FROM pre1
  UNION DISTINCT
  SELECT pre1.company, pre1.yr, pre2.cs + 1 
   FROM pre1
   JOIN pre2 
     ON pre1.company = pre2.company
    AND pre1.yr = pre2.yr + 1
)
SELECT JSONB_AGG(DISTINCT company) FROM pre2
WHERE cs >= 3;



 

