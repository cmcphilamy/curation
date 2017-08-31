---
layout: default
---

# File Transfer Procedures

**Note: We are developing these instructions as a step in designing our secure EHR data storage facilities for PMI. All uploads, whether for testing purposes or for production, will be performed with @pmi-ops.org user accounts to ensure a consistent process.
You should not upload real participand data or even de-identified data at this stage.  Instead please use synthetic data.**

These instructions walk you through the steps to upload test files to the RDR Test Bucket. To summarize the process: you will

1. Describe your site configuration and share with the PMI Ops team
1. Ensure that the individual upload users each have @pmi-ops.org user accounts
1. Primary & Secondary Account Creation
1. Perform Test Upload

# 1. Information Gathering

1. Describe and share your site configuration with the PMI Ops team.
The below google sheet (https://docs.google.com/spreadsheets/d/1Slh4teXKBwtD_ZrTFEjUTVH3Jk5ii-tcSJxocZnAqdo/edit?usp=sharing) was compiled from the Data Sprint done by the DRC and the Excel file compiled by NIH.  Consider it a first draft.  Please review your information and make deletions and additions as needed.  

Specifically we are looking to identify the following key details about your organization's structure:

1. Which sites within your Awardee will be individually responsible for performing uploads (this may be only one site, if you'll be doing a single, coordinated upload for your entire Awardee or organization).
1. Two individual "individual upload users" for each site. These are the people who will be responsible for performing uploads at each site. One should be designated as primary, and the other should be designated secondary.  
1. Do the primary and secondary POC have a PMI Opps account?
1. What is the role of the contact? (Not sure if these should be described in a different way or at all.)
    1. Project Manager - Manages the pmi-opps accounts for the Awardee
    1. Technical Lead - Organizing the EHR data for the site or sites
    1. Data Steward - The individual(s) using the pmi-opps account to upload data

This information is being collected to make sure the pmi-opps accounts are correctly provisioned to work with the buckets.

# 2.  Ensure that all of your site upload users have @pmi-ops.org user accounts
To correctly provision your pmi-ops.org account, please send the following information to sysadmin@pmi-ops.org: 
    Email Subject Line: “New User Request: EHR Upload Bucket Access” 
    Rules of Behavior for Privileged Use – Note that the full doc needs to be scanned and returned, not just the signed page.
    https://docs.google.com/document/d/1E6bRJ4l7AclEkaFS4Tg2zt9u3WyFMOpu4-omMjhlTRM/edit?usp=sharing
    Attestation of completion of your institutional general security training
    Attestation of completing and reviewing the online google sheet https://docs.google.com/spreadsheets/d/1Slh4teXKBwtD_ZrTFEjUTVH3Jk5ii-tcSJxocZnAqdo/edit?usp=sharing.
The System Administrator will send directions on what the next steps are after account creation. General processing time for pmi-ops.org account creation is 1 day.

Individual access request will be sent for each user. 

# 3. Determine the uploaders group and the uploads bucket for each site
The DRC will create an EHR upload bucket for each user you identified in Step 1, after receiving information from the Site Coordinators on how their EHR uploads process is going to be structured (Step 1 Google Sheethttps://docs.google.com/spreadsheets/d/1Slh4teXKBwtD_ZrTFEjUTVH3Jk5ii-tcSJxocZnAqdo/edit?usp=sharing).   After the buckets have been created, the primary and secondary uploading users will be sent the links to these buckets.

# 4. Perform a test upload.
Note that the arguments in bold-italics below will be need to be replaced with names and paths pointing to your own local files.
Let's assume a few things:
    You are John Smith, and your PMI Ops user account is john.smith@pmi-ops.org
    You're performing an EHR data upload for Site "123" of Awardee "ABC". 
    Your site's uploads bucket is "all-of-us-ehr-uploads-test-awardee-abc-site-123"

Then you would perform a test upload. You have two options:
A) Command line upload (gsutil) 
gcloud auth login
This opens a browser window to authenticate to Google Cloud Platform. You should sign in using your individual upload user (e.g. john.smith@pmi-ops.org — of course you'd substitute your actual username here instead)
gsutil cp -r my-site-ehr-data-2017-05-20 gs://all-of-us-ehr-uploads-test-awardee-abc-site-123/
B) Browser upload (Google Cloud Console) 
Open a web browser and navigate to https://console.cloud.google.com/storage/browser/all-of-us-ehr-uploads-test-awardee-abc-site-123 (replacing the bolded portion with your bucket name).   Verify that you are using HTTPS

Credit distribution is dependent on the following upload rules:

Upload each OMOP table separately, do not combine them into one large file.
No .zip or other file compressions are accepted.
If you are uploading a folder of files make sure the folder name is unique from the files inside.
When uploading multiple HPOs make sure you are clearly labeling each HPO.   In the example below Pittsburg is uploading for two HPOs, each one is clearly labeled in the beginning of the file name.
    PITT_Monroe/omop_20170701/person.csv
    PITT_Monroe/omop_20170701/visit.csv
    PITT_Aiken/omop_20170701/person.csv
    PITT_Aiken/omop_20170701/visit.csv
Do not upload to the root.
If you upload the same file twice it will prompt you to replace or cancel.

This section will cover the file naming convention **undecided** as well as the method of transmission for the alpha data load. Each of the above tables will be exported to separate CSV file. The proposed naming convention will be:

    <hpo_id>_<table_name>_DataSprint_<data_sprint_number>.csv

The following abbreviations will be used for the HPO Names:

<table>
<thead>
<tr>
  <th>Healthcare Provider Organization</th>
  <th>Abbreviation</th>
</tr>
</thead>
<tbody>
{% for hpo in site.data.hpo %}
<tr>
  <td>{{ hpo.name }}</td>
  <td>{{ hpo.hpo_id }}</td>
</tr>
{% endfor %}
</tbody>
</table>

So a file name for the person table export from Columbia would like this: 

    NYC_Columbia_person_DataSprint_2.csv.
    
If the file is from a site within an HPO, like Cornell within the NYC HPO, the file name would look like this: 
    
    NYC_Cornell_person_DataSprint_2.csv.

# once uploaded and reporting tools successfully tested site may upload live EHR. Might need a live and alpha page because when uploading live data the naming and format may change.
