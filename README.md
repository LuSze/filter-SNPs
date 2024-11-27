# filter-SNPs
Search, fetch and filter out SNPs from NCBI's dbSNP with certain criteria (only get IDs of SNPs that are T>C, pathogenic and preceded by a T)

The code in this project uses the python implementation of the edirect (Entrez Direct) functions that can interface with the NCBI's interconnected databases (pubmed, dbSNP, genes, etc.). Biopython makes the bash commands described below (most important are `esearch` and `efetch`) available in python.

- GitHub: https://github.com/ncbi/dbsnp
- Tutorial Website: https://www.ncbi.nlm.nih.gov/books/NBK179288/ (very exhaustive document)

## Environment

The environment was created with `conda create -n "dnsnp" python=3.8` and activated with `conda activate dnsnp`. Necessary packages should be downloaded once the jupyter notebook is ran. 

## Notes

To filter out the SNPs:

- the script searches for all SNP IDs that match the query `Y[Allele] AND pathogenic[Clinical significance]` where `Y` is the IUPAC coding for C or T (meaning that we can have either C>T or T>C at that position)
- only those entries that have a T>C variant are kept. This is obtained by looking at the SPDI entry. The deletion:insertion should match `"T:C"`
- if this condition holds, the script fetches the left flank of this SNP and checks if it is a `"T"`.

If all these conditions are satisfied, the entry ends up in the filtered list.

## Jupyter Notebooks

`T_to_C_filter.ipynb` is the notebook that searches, fetches and filters the SNPs for our criteria.

`webscraper` takes the manually pasted list of links that `T_to_C_filter` produces and requests the website html and extracts the disease name from it.

`get_all_T_to_C_mutations.ipynb` is copied from https://github.com/ncbi/dbsnp and only minimally adjusted