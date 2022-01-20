In this repository I provide the taxonomy information of different mOTUs version, ready to be loaded into R.

## mOTUs 3.0

To load the taxonomy of the mOTUs for the database version 3.0.0 and 3.0.1 you can use:
```R
load(url("https://github.com/AlessioMilanese/motus_taxonomy/blob/master/data/motus_taxonomy_3.0.1.Rdata?raw=true"))
```

## mOTUs 2.6

To load the taxonomy of the mOTUs for the database version 2.6.0 and 2.6.1 you can use:
```R
load(url("https://github.com/AlessioMilanese/motus_taxonomy/blob/master/data/motus_taxonomy_2.6.1.Rdata?raw=true"))
```

## mOTUs 2.5

To load the taxonomy of the mOTUs for the database version 2.5.0 and 2.5.1 you can use:
```R
load(url("https://github.com/AlessioMilanese/motus_taxonomy/blob/master/data/motus_taxonomy_2.5.1.Rdata?raw=true"))
```

## Useful functions

Additionally I provide two functions that can be loaded with:
```R
load(url("https://github.com/AlessioMilanese/motus_taxonomy/blob/master/data/motus_functions.Rdata?raw=true"))
```
There are two functions:

#### `extract_motus_id`
Which given the name of a profiled mOTUs, it extract the mOTUs ID. Example input: `"Abiotrophia defectiva [ref_mOTU_v25_04788]"` and output: `"ref_mOTU_v25_04788"`

#### `motus_summarise_higher_level`
Which given a taxonomic profile table, it can summarise the profile at higher taxonomic level. The input are:
- `profile`, the mOTUs taxonomic profile. expect to have rownames as mOTUs and colnames as samples
- `taxonomy`, the mOTUs taxonomy. as downloaded from any of the command listed before
- `level`, the taxonomic level to which you want to change the taxonomic profile
- `convert_NA`, convert NAs to -1. For example "NA Clostria unknown genus" and "NA Firmicutes unknown genus" would both be added to `unassigned`. By default this is set to `True`.

Example command:
```R
# we load the functions
load(url("https://github.com/AlessioMilanese/motus_taxonomy/blob/master/data/motus_functions.Rdata?raw=true"))
# we load a table of samples: 2,010 samples profiled with mOTUs 2.5.1
load(url("https://github.com/AlessioMilanese/motus_taxonomy/blob/master/data/example_healthy_human_gut.Rdata?raw=true"))
# we load the taxonomy information for mOTUs 2.5
load(url("https://github.com/AlessioMilanese/motus_taxonomy/blob/master/data/motus_taxonomy_2.5.1.Rdata?raw=true"))

# we convert the taxonomic table from species level to genus:
genus_table = motus_summarise_higher_level(PROFILES,motus2.5_taxonomy,"Genus")
```

#### How to load a mOTUs table into R

Let's say you run:
```
motus merge -i sample1.motus,sample2.motus -o ~/Desktop/merged.motus
```
on the terminal and obtain a motus table in `~/Desktop/merged.motus` which look like:
```
head ~/Desktop/merged.motus
  # motus version 2.5.1 | merge 2.5.1 | info merged profiles: # git tag version 2.5.1 |  motus version 2.5.1 | map_tax 2.5.1 | gene database: nr2.5.1 | calc_mgc 2.5.1 -y insert.scaled_counts -l 75 | calc_motu 2.5.1 -k mOTU -C no_CAMI -g 3 | taxonomy: ref_mOTU_2.5.1 meta_mOTU_2.5.1 
  # call: python motus merge -i sample1.motus,sample2.motus -o ~/Desktop/merged.motus
  #consensus_taxonomy	sample1	sample2
  Leptospira alexanderi [ref_mOTU_v25_00001]	0.0000000000	0.0000000000
  Leptospira weilii [ref_mOTU_v25_00002]	0.0000000000	0.0000000000
  Chryseobacterium sp. [ref_mOTU_v25_00004]	0.0000000000	0.0000000000
  Chryseobacterium gallinarum [ref_mOTU_v25_00005]	0.0000000000	0.0000000000
  Chryseobacterium indologenes [ref_mOTU_v25_00006]	0.0000000000	0.0000000000
  Chryseobacterium artocarpi/ureilyticum [ref_mOTU_v25_00007]	0.0000000000	0.0000000000
  Chryseobacterium jejuense [ref_mOTU_v25_00008]	0.0000000000	0.0000000000
```

In R, you can load it with:
```
merged_motus = read.csv("~/Desktop/merged.motus",header = T, sep = "\t", row.names = 1, skip = 2, check.names = F)
```


