-- create working
 
drop table dufb_access_work
create table dufb_access_work as (select * from dfm."dufb_Det2mi_12_13");
 
-- edit geom
SELECT (ST_Dump(geom)).geom AS pt_geom
  FROM dfm.gardens13;
 
SELECT (ST_Dump(geom)).geom AS pt_geom
  FROM dufb_access_work;
 
 
alter table dufb_access_work add column geom geometry(Point, 4326)
update dufb_access_work set geom=st_setsrid(ST_MakePoint(longitude, latitude), 4326);
 
-- select counts
drop table dufb_access_021518
create table dufb_access_021518 as(
 
select zip_9,
(select count(*) from dfm.gardens13 as g
  where st_dwithin(d.pt_geom, g.pt_geom, 5280))
  as gardens,
(select count(*) from dfm.snap13 as s
  where st_dwithin(d.pt_geom, s.geom, 5280))
  as snap,
(select count(*) from dfm.stores13 as st
  where st_dwithin(d.pt_geom, st.geom, 5280))
  as stores,
(select count(*) from dfm.markets12_13 as m
  where st_dwithin(d.pt_geom, m.geom, 5280))
  as markets
 
from dufb_access_work as d
);
