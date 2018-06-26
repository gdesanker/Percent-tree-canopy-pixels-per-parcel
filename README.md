# Percent-tree-canopy-pixels-per-parcel

-- scenario 1: parcels with >75% canopy cover, loose 35% of existing canopy
-- sum all pixels from lc to find total number of pixels per parcel

--create table results_scratch.scen_one as
SELECT tid, geom_2263, bbl, borough, sdlbl, "lc_2010_parcel_17x1x1_Correct_histo_1", ("lc_2010_parcel_17x1x1_Correct_histo_0" + "lc_2010_parcel_17x1x1_Correct_histo_1" + "lc_2010_parcel_17x1x1_Correct_histo_2" + "lc_2010_parcel_17x1x1_Correct_histo_3" + "lc_2010_parcel_17x1x1_Correct_histo_4" + "lc_2010_parcel_17x1x1_Correct_histo_5" + "lc_2010_parcel_17x1x1_Correct_histo_6" + "lc_2010_parcel_17x1x1_Correct_histo_7") as total_pixels
FROM results_scratch.snad_parcels_lc_gkd;

--calculate percent of canopy cover in each parcel
-- make sure canopy cover pixels and total pixels are case as numeric
select  bbl, "lc_2010_parcel_17x1x1_Correct_histo_1" as treepix, total_pixels, ("lc_2010_parcel_17x1x1_Correct_histo_1"::numeric/total_pixels::numeric) as prop_canopy
from results_scratch.scen_one
group by bbl, "lc_2010_parcel_17x1x1_Correct_histo_1", total_pixels
