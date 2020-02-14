-- Table: "500_detroit"
 
-- DROP TABLE "500_detroit";
 
CREATE TABLE "500_detroit"
(
  id serial NOT NULL,
  geom geometry(MultiPolygon,2898),
  objectid bigint,
  statefp10 character varying(80),
  countyfp10 character varying(80),
  tractce10 character varying(80),
  geoid10 character varying(80),
  name10 character varying(80),
  namelsad10 character varying(80),
  mtfcc10 character varying(80),
  funcstat10 character varying(80),
  aland10 bigint,
  awater10 character varying(80),
  intptlat10 character varying(80),
  intptlon10 character varying(80),
  city character varying(80),
  globalid character varying(80),
  sqmiles numeric,
  acres numeric,
  stateabbr character varying(254),
  placename character varying(254),
  placefips bigint,
  place_trac character varying(254),
  population character varying(254),
  access2_cr numeric,
  access2__1 character varying(254),
  arthritis_ numeric,
  arthriti_1 character varying(254),
  binge_crud numeric,
  binge_cr_1 character varying(254),
  bphigh_cru numeric,
  bphigh_c_1 character varying(254),
  bpmed_crud numeric,
  bpmed_cr_1 character varying(254),
  cancer_cru numeric,
  cancer_c_1 character varying(254),
  casthma_cr numeric,
  casthma__1 character varying(254),
  chd_crudep numeric,
  chd_crude9 character varying(254),
  checkup_cr numeric,
  checkup__1 character varying(254),
  cholscreen numeric,
  cholscre_1 character varying(254),
  colon_scre numeric,
  colon_sc_1 character varying(254),
  copd_crude numeric,
  copd_cru_1 character varying(254),
  corem_crud numeric,
  corem_cr_1 character varying(254),
  corew_crud numeric,
  corew_cr_1 character varying(254),
  csmoking_c numeric,
  csmoking_1 character varying(254),
  dental_cru numeric,
  dental_c_1 character varying(254),
  diabetes_c numeric,
  diabetes_1 character varying(254),
  highchol_c numeric,
  highchol_1 character varying(254),
  kidney_cru numeric,
  kidney_c_1 character varying(254),
  lpa_crudep numeric,
  lpa_crude9 character varying(254),
  mammouse_c numeric,
  mammouse_1 character varying(254),
  mhlth_crud numeric,
  mhlth_cr_1 character varying(254),
  obesity_cr numeric,
  obesity__1 character varying(254),
  paptest_cr numeric,
  paptest__1 character varying(254),
  phlth_crud numeric,
  phlth_cr_1 character varying(254),
  sleep_crud numeric,
  sleep_cr_1 character varying(254),
  stroke_cru numeric,
  stroke_c_1 character varying(254),
  teethlost_ numeric,
  teethlos_1 character varying(254),
  geolocatio character varying(254),
  CONSTRAINT "500_detroit_pkey" PRIMARY KEY (id)
)
WITH (
  OIDS=FALSE
);
ALTER TABLE "500_detroit"
  OWNER TO postgres;
 
-- Index: sidx_500_detroit_geom
 
-- DROP INDEX sidx_500_detroit_geom;
 
CREATE INDEX sidx_500_detroit_geom
  ON "500_detroit"
  USING gist
  (geom);
 
select
count_stores.*
, ct2.bphigh_cru as bp_prev
, ct2.diabetes_c as db_prev
, ct2.highchol_c as chol_prev
, ct2.obesity_cr as obes_prev  
 
from(
select
  trim (ct.geoid10) as tract_id
 , avg(store.total_score) as average_score
 , count(*) as count_stores
 
from "500_detroit" as ct
 join nems_2013 as store
 on ST_Intersects(ST_Transform(store.geom, 2898), ST_Buffer(ST_Centroid(ST_Transform(ct.geom, 2898)), 5280))
 
--where geoid_trac = '08031000402' -- if you want to test on one census tract, otherwise leave it out
 
group by ct.geoid10
) as count_stores
 
join "500_detroit" as ct2
on ct2.geoid10 = count_stores.tract_id
