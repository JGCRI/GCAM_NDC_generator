This file set was made to create GCAM NDC constraint files. This document details the steps to create these files.
The data was compiled by Matt Binsted in the Fall of 2016 and the R script and file structure was made by Jonathan Huster in the Summer of 2019

NOTE: The file set is complete as is. These steps should be followed if 
	1. GDP pathways change
	2. Emissions pathways change
	3. NDC paths based off of a new baseline scenario are desired

STEPS:
1. Run a baseline scenario. This is to establish emissions and GDP pathways.

2. Open the modelinterface and run the [PATH]/NDC_generator/input/queries/batch_query_NDC.xml query on the results.
	a. Save the result as "NDC_QUERY.csv" in the same directory

3. Open [PATH]/NDC_generator/generate_NDC.R and ensure the working directory is set to [PATH]/NDC_generator/. 
	a. This can be checked with getwd() and set with setwd([PATH]/NDC_generator).

4. To generate the output constraints source generate_NDC.R. The output will either  and and you can either
	a. Generate .csv versions of the constraints and linking file and use a model interface to convert to xmls (headers file included in output/)
		i. Uncomment the sections of generate_NDC.R with "write_const_csv" and "write_header_csv"
		ii. Source the script and the csvs will be added to the output/ directory
		iii. Open the GCAM ModelInterface and read the desired scenario constraint with the header file in the output directory.
		iv.  NOTE: the files may have quotation issues from being read through the MI
			A. Open [PATH]/NDC_generator/scripts/clean_xml.R.
			B. call the clean_xml (or clean_xml_dir) function on the xmls you would like to use 
			
	b. Add the headers into a version of the gcamdata system (one time) to automatically generate the xmls 
		i. Download (or open) a full version of GCAM
		ii. Add the headers in Header_ndc.txt to input\gcamdata\inst\extdata\mi_headers\ModelInterface_headers.txt
		iii. Add the headers in header_generate_package_data.txt to input\gcamdata\data-raw\generate_package_data.R
		iv. Source generate_package_data.R (with working directory set to the location of generate_package_data.R)
		v. Load this version of the gcamdata library then source "generate_NDC.R" with the working directory set to 
		    the location of generate_NDC.R and the xmls will be in the output/ directory

