# wf-scripts
A list of scripts for handling various outputs from wf-workflows

---------------------------------------------

transcript_unify_annotation.pl
This is a short script to merge information contained the output directories from wf-transcriptomes:
https://github.com/epi2me-labs/wf-transcriptomes

This is a personal script in no way associated with Oxford Nanopore or the wf-transcriptomes workflow and
may not be appropriate for all versions of the workflow. 

While every effort is made to ensure this script is bug free, this should not be assumed to be true and 
users should confirm or validate the results of this script themselves before. 

Usage:

	perl $0 --tsv <str_merged.tracking tsv file> --gtf <str_merged.annotated.gtf> --output <new output TSV file> [--help]

	where:

		tsv:    This is the str_merge TSV file for each of the isoform classes. e.g. str_merged.tracking.u.tsv
		gtf:    This is the GTF formatted annotation file for the isforms
		output: The file to write the results to
		help:   Prints out this helpful message

	Notes on inputs:
		TSV: 	Example row (5 comma separated columns): TCONS_id,query_locus_id,ref_gene_id,class,details
				details column is | separated containing 7 columns: internalID:qry_gene_id|qry_id|num_exons|FPKM|TPM|cov|len
		GTF:	Only features of the type transcript (3rd column) will be retained. Exon features are excluded
		OUTPUT:	Example output row: 

	Notes on behaviour:
		Any transcript in the TSV which is not found in the GTF will not be output
		If a transcript identifiers in the TSV file are assumed unique. If an identifier is found twice, you will get an error
		The number of columns in the TSV file is assumed fixed. If there are not 5 comma separated columns, outputs may be incorrect
		The fifth column in each TSV row is assumed to contain 7 pipe (|) separated columns. If there are not 7 pipe separated columns, outputs may be incorrect
		Header row in the first line is assumed (and the first row is always skipped)

		Any transcript in the GTF which is not found in the TSV will be skipped
		If a unique transcript ID is found more than once for a transcript feature, you will get an error (and have a problematic GTF)
		No header is present in the GTF generated by the wf-transcriptomes workflow, and this is assumed for your input

---------------------------------------------

