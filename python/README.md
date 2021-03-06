**EADrenamer.py** - Python script to batch rename EAD exports based on value of <eadid> element.

**EADrenamer_published_only.py** - Python script to batch rename EAD exports based on value of <eadid> element.  The script will only process EADs where eadheader/@findaidstatus="published".  Files are renamed and moved to the specified source directory

**asEADexport_public.py** - Python script to batch export all EADs from a specified repository where finding_aid_status=published and save those EADs to a specified location using the <eadid> value as the filename. Can configure export parameters (include DAOs, unpublished, etc.). Usernames, passwords, and repository URLs have been removed. Adapted from: https://gist.github.com/helrond/1ef5b5bd47b47bd52f02

**asEADexport_eadid_input.py** - Python script to batch export EADs based on eadid input. Prompts for a list of eadid values separated with commas (e.g. eadid1,eadid2,eadid3). Will export EADs for all eadids provided if marked "published" in ASpace. Script requires a config file (local_settings.cfg) in the same directory that contains the backend URL, username, password.

Example of local_settings.cfg:
```
[ArchivesSpace]
baseURL:http://aspace-backend-url.lib.duke.edu
repository:1
user:admin
password:adminpassword
```

**asEADpublish_and_export_eadid_input.py** - Python script (similar to above) that exports EADs based on eadid input. Prompts for list of eadid values separated with commas. Checks to see if a resource's finding aid status is 'published'.  If so, it exports the EAD to a spficied location, if not, it sets the finding aid status to "published" AND publishes the resource and all components.  Then, it exports the modified EAD.  See comments in script for more details.

**asUpdateDAOs.py** - ONLY WORKS WITH ARCHIVESSPACE v.1.5+. A python script used to update Digital Object identifiers and file version URIs in ASpace based on an input CSV with refIDs for the the linked Archival Object.  Input is a five column CSV (without column headers) that includes: #[old file version use statement],[old file version URI],[new file version URI],[ASpace ref_id],[ark identifier in DDR (e.g. ark:/87924/r34j0b091)].

**duke_create_ao_and_do.py** - ONLY WORKS WITH ARCHIVESSPACE v.1.5+. Starting with an input CSV, this script will use the ArchivesSpace API to batch create archival object records in ASpace as children of a specified archival object parent (e.g. a series/subseries/file). The script will then create digital object records from the same input CSV and link them as instances of the newly created archival objects. Finally, the script will output a CSV containing all of the info in the input CSV plus the refIDs and URIs for the created archival objects and the URIs for the created digital objects. 

**duke_update_archival_object.py** - Python script that reads CSV file containing ArchivesSpace archival object ref_IDs, digital object identifiers, URLs, and file_version_use_statements and batch creates digital object records and links them as instances to existing archival object records based on the archival object's refID value. Script also outputs a CSV file including all the info in the input CSV and the URIs of the created digital objects and updated archival object records.  The script prompts for the ASpace backend URL, login credentials, location of input and output CSV, and whether or not the created digital objects should be published.
This script is adapted from: https://github.com/djpillen/bentley_scripts/blob/master/update_archival_object.py

**duke_update_archival_object_args.py** - Python script that reads TSV file produces from aspace_dig_guide_creator.xsl script and batch loads digital object records in ArchivesSpace and links them as instances to existing archival object component records based on the archival object's refID value. In other words, it functions similarly to duke_update_archival_object.py. It differs in that it accepts arguments for the input TSV file and output CSV file, as well as arguments for the Aspace User ID and password. It also will read file version use statements from the input TSV. It still must be modified to map the correct column position of the Digital Object IDs, URIs, and File Version Use Statements. This script was adapated from duke_update_archival_object.py which was itself adapted from: https://github.com/djpillen/bentley_scripts/blob/master/update_archival_object.py

**duke_as_replace_notes.py** - Python script that reads CSV, finds notes, and replaces existing note text with new text provided in CSV. Primarily used to clean up accessrestrict notes. Script slightly modified from script provided by Alicia Detelich (Yale Manuscripts and Archives)

**duke_as_replace_notes_restrictions.py** - Python script that reads CSV, finds restriction notes, and replaces note text while supplying a local access restriction type and a restriction end date from the input CSV.

**duke_update_archival_object_containers.py** - Python script that batch updates archival objects with new top containers. Input is a CSV with three columns: Archival Object URI, old top container URI, and new top container URI.

**as_change_ao_level.py** - Python script that takes 2-column input CSV (AO ID, desired_level) and updates level of description values in ASpace accordingly, writing log to output CSV.