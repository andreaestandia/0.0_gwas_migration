Generate two datasets, one with the migrants and another one with the nonmigrants

```bash
PATH_SCRIPT="~/sjoh4959/projects/0.0_island_rule/src/myscripts/"
PATH_GENOME="/data/Users/Andrea/silvereye/wgs_beagle/raw/"
PATH_LISTS="/data/Users/Andrea/silvereye/projects_data/0.0_migrants/data/lists/"
PATH_OUT="/data/Users/Andrea/silvereye/projects_data/0.0_migrants/data/beagle/"
declare -a migrant_list=()
migrant_list+=("migrants" "residents")
for list_type in "${migrant_list[@]}"
do
	python "${PATH_SCRIPT}subset_beagle.py" --beagle "${PATH_GENOME}wholegenome_pruned.beagle" --samples "${PATH_LISTS}list_${list_type}" --out "${PATH_OUT}whole_genome_pruned_${list_type}.beagle"
	done
```

Calculate SFS for each group

```
PATH_ANGSD="~/sjoh4959/projects/0.0_island_rule/src/others/angsd/"
PATH_REF_GENOME="/data/Users/Andrea/silvereye/ref_genome/"
PATH_INPUT="/data/Users/Andrea/silvereye/projects_data/0.0_migrants/data/beagle/"
PATH_OUT="/data/Users/Andrea/silvereye/projects_data/0.0_migrants/analysis/fst/"

"${PATH_ANGSD}misc/realSFS" -beagle "${PATH_INPUT}whole_genome_pruned_migrants.beagle" -anc "${PATH_REF_GENOME}Zlat_2_Tgut_pseudochromosomes.shortChromNames.fasta.gz" -doSaf 4 -fold 1 -out "${PATH_OUT}migrant"

angsd -beagle "${PATH_BAM}chatham.beagle" -doSaf 4  -anc "${PATH_REF_GENOME}Zlat_2_Tgut_pseudochromosomes.shortChromNames.fasta.gz" -fai "${PATH_REF}Zlat_2_Tgut_pseudochromosomes.shortChromNames.fasta.gz.fai" -out "${P
ATH_BAM}chatham"
```

