---
layout: default
---

# Introduction

This site provides necessary information to test your pmi-opps account then loak EHR data for your HPO.  Your participation as a HPO will provide critical EHR information needed to drive the All of Us Research Program and its research. Provided here is an overview of the data request:

 1. Overview
 1. [Data Model](data_model.md)
 1. [File Transfer Procedures](file_transfer_procedures.md)

# EHR Alpha Upload Steps & Goals

1. Gather information needed to correctly provision pmi-opps accounts across your HPO.
1. DRC creates buckets using collected information.
1. HPO is notified of bucket creation
1. HPO loads a test csv to verify the pmi-opps account and bucket works
1. HPOs are notified of successful test load and told to begin uploading Prod EHR data immediately
1. Reacquaint with the changes to the OHDSI vocabulary. Based on the previous data sprint, an abridged version of the OMOP vocabulary was created. This alpha upload adds a location table to the coded data in OMOP required fields.

# Timeline

* DRC gathers information needed to correctly provision pmi-opps accounts across the HPO.
* The DRC will create buckets using collected information.
* HPO is notified of bucket creation
* HPO loads a test csv to verify the pmi-opps account and bucket works.  
 * Test data can be from previous sprint or any synthetic data.
* Data will follow the same format and structure as the sprint and is not changing.
* HPOs are notified of successful test load and told to begin uploading Prod EHR data when ready 
* Minimum Quarterly schedule
* Following the file format in documentation. 

# De-Identification

For this alpha load this will remain the same as the sprint, all dates will be de-identified and patient ids will be converted to a random number. All date fields will preserve the year, but set the month and day to Jan 1. For example, if an encounter occurs on March 12, 1985, the date will be de-identified to Jan 1, 1985. Also, all patients **greater than 80 years** of age should be removed from the submission.

[Proceed to Data Model >>](data_model.md)
