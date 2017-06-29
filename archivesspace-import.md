

# IMPORT GUIDE

## Start ArchivesSpace

To start the Demo version of AS we need to execute manually the program directory. To run it just execute on the computer terminal one of those scripts. ArchivesSpace will start in foreground model, so you must keep open the terminal window (if you close it the program shuts down). Java 1.6 (or newer) is required.

 
|On Windows|On Linux and OSX|
|----|----|
| `cd /path/to/archivesspace`<br/>`./archivesspace.sh`|`cd \path\to\archivesspace`<br/>`archivesspace.bat`|


You can drag and drop the AS folder from the Applications to the Terminal, instead of write the path to the program. The path will automatically appear.

![Drag and Drop Image](https://github.com/marcolock/archivesspace-importguide/blob/master/images/1%20Drag%20and%20Drop.png)

It will take a while to run completely the program, and once it’s ready you can access the system by one of these URL links on your internet browser:

* http://localhost:8089/ -- the backend
* http://localhost:8080/ -- the staff interface
* http://localhost:8081/ -- the public interface
* http://localhost:8082/ -- the OAI-PMH server
* http://localhost:8090/ -- the Solr admin console

A detailed description is on the GitHub page of [ArchivesSpace](https://github.com/archivesspace/archivesspace/README.md).
  
  

## How to import on ArchivesSpace

To import Data in ArchivesSpace run the program on the Terminal and open the staff interface with the URL. After logging in go to `Create` and choose `Background Jobs`.

![Create button image](https://github.com/marcolock/archivesspace-importguide/blob/master/images/2%20Create%20button.png)

Select `Data Import` and then the kind of file you want to import: you can choose between EAD2002 (the only one format that allows to import `Resources`, the AS level for a Collection), EAC, CSV and Xml with the UniMarc Standards. To import finding aids and archival paper collections choose the EAD. 

![Background Jobs Image](https://github.com/marcolock/archivesspace-importguide/blob/master/images/4%20Import%20Type.png)

The Import/Export Mapping for the EAD2002 is the guide tool to understand how EAD elements are formatted to be imported in AS and which are the corresponding objects and properties on AS data fields. 



## How to prepare the EAD for the import

The EAD is a text document written with the Xml markup language, and describe in a standard and machine-readable form a finding aid for an archival collection, with all the elements recommended by international standards as the Dublin Core and the ISOs. To write a valid EAD for the import we need to convert our collection spreadsheets. There are two different steps to convert the Excel spreadsheet in a valid EAD: the first one using the Spreadsheet Template  `EADtoAS.xlsx`  refers to the records of series and subseries; the second one in the EAD encoded text  `EADtoAS.txt`  is to give a structure to the data and insert the collection’s information of your finding aid.
A helpful online tool is [Xml-Validator]( http://xmlvalidation.com/), that check the validity of you EAD, underling the syntax errors in the text. Check your EADs before the import to avoid import errors.      



### From the Collection to the Template Spreadsheet

To convert an Excel Spreadsheet in an Xml EAD (Encoding Archival Description) finding aid we can use the Excel Template written and posted by the Harvard University Blog, and upload by the Carnegie Hall Archives to fit with our needs. 

The template is an Excel Spreadsheet with denominated and fixed header for each columns. Populate the columns with the data from your spreadsheet, being attentive to choose the right column/element to ingest them. Copy and paste the normalized columns of your spreadsheet and autofill the new spreadsheet, but do not use formatting character (as tabs, returns and bullets) or symbols and accented letters (as &, <, and > because they can interfere with the encoding). The first row below the headers indicates the EAD note, to have an overview how the records are converted.

![Template headers Image](https://github.com/marcolock/archivesspace-importguide/blob/master/images/5%20Template%20Headers.PNG)

The values inserted will be shown in the public interface of AS, exception for the Creator and the Agents that need to be published manually from the staff interface.

Mandatory fields to fill and to not leave blank are:
* `Level`: Key one of the following values, to indicate the position of each record in the collection hierarchy “class, collection, file, fonds, item, otherlevel, recordgrp, series, sub-fonds, sub-grp, sub-series".
* `Date`: Key one, two or all the type of date cells,
  * `Date expression` for a free text, 
  * `Second Date` (event) if you need to specify performance dates,
  * `Date begin/Date end`, to express the inclusive years (“yyyy” format): they always have to be different but in couple, and they need `Date expression`. 
* `Title`: Type in the header of the record. It will be the title of your AS component.
* `Unique ID`: Key the Identification code of the document.
* `File type (label)`: if you want to insert the container information, be sure that the label for the `File #` be filled. The template have already pre-filled the columns with “Folders” but check for all the length of the spreadsheet.

The entire EAD record is provided, for each row, by a single formula in the column EAD encoding. The `CONCATENATE` function is written to merge the fields we have populated and to translate them in the markup language Xml. To change or upload the function and to insert more fields, you need to re-write the function’s fragile syntax. Be careful, once you open the cell do not click on other cells because it could change the function, but use `Enter` to get out.

![Concatenate Image](https://github.com/marcolock/archivesspace-importguide/blob/master/images/6%20Concatenate%20function.png)

Now you can copy the EAD encoding cells for each record you want to import and paste them into another application. Do the copy/paste of the `EAD encoding` only with Microsoft Office 13 – Excel [Import with other programs could causes import errors].


### Create and edit the EAD

To create the EAD Xml use the pre-form example here called [`EADtoAS.txt`](https://github.com/marcolock/archivesspace-importguide/blob/master/EAD%20to%20AS.txt), originally written by Kate Bowers and posted on the [Harvard University Blog](https://blogs.harvard.edu/archivaldescription/2017/01/26/spreadsheet_to_ead_to_as/), and then modified by Marco Lo Cascio for Carnegie Hall Archives. The Xml is a markup language based on standard elements and attributes, able to describe a finding aid in a machine readable structure. To open, edit and modify an EAD Xml you can use a simple text editor (.txt) as the Notepad on Windows or specific encoding program as AtoM or Oxygen.



	<?xml version="1.0" encoding="UTF-8"?>
	<ead xmlns="urn:isbn:1-931666-22-9" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	    xsi:schemaLocation="urn:isbn:1-931666-22-9 http://www.loc.gov/ead/ead.xsd">;
	    
	    <eadheader>
	        <eadid> CHA-CollectionID_EAD </eadid>
	        <filedesc>
	            <titlestmt>
	                <titleproper> CollectionName finding aids, by YourName</titleproper>
	            </titlestmt>
	        </filedesc>
	    </eadheader>
	    
	    <archdesc level="collection">
	    
 	       <did>
	            <unitid> CHA-CollectionID </unitid>
  	          <langmaterial><language> English, and other?</language></langmaterial>
  	          <origination><persname> Creator of the collection </persname></origination>
  	          <unittitle> Title of the Collection </unittitle>
  	          <unitdate normal="1900/2000"> 1900-2000 </unitdate>
  	          <physdesc><extent> Number / Container  </extent></physdesc>
 	       </did>
	       
 	    <dsc>
		[Paste here the records from the spreadsheet]
           </dsc>
	   
   	 </archdesc>
	</ead>



Here’s a list of the principal elements and how to fill it out:

* `<eadheader>` = EAD Identifier: A required sub-element that designates a unique code for the EAD finding aid document. Type in the node “Collection ID, underscore EAD (CollectionID_EAD)” to standardize the titles.
* `<eadid>` = EAD Identifier: A required sub-element of <eadheader> that designates a unique code for a particular EAD finding aid document.
* `<titleproper>` = Title Proper of the Finding Aid: The name of the finding aid or finding aid series. Key the whole title of the collection, and the name of the creator of the finding aids. More information about the process can be add on AS.* `<archdesc>` = Archival Description: A wrapper element for the bulk of an EAD document instance, which describes the content, context, and extent of a body of archival materials.
* `<untid>` = ID of the unit: Any alpha-numeric text string that serves as a unique reference point or control number for the described material. 
* `<langmaterial>` =  Language of the material: Type in the languages of the materials. This is a free text, so you can put more than one language.
* `<origination><creator>` = Information about the individual or organization responsible for the creation, accumulation, or assembly of the described materials. As the other Agents Links it won’t be shown in the public interface.
* `<unittitle>` = Title of the unit: This will be the title of the collection.
* `<unitdate>` = Date of the unit: Type in the inclusive dates inside the quotes and the year (or the same inclusive dates) in the brackets.
* `<physdesc>` = Physical description: A wrapper element for bundling information about the appearance or construction of the described materials. Key a number and the kind of containers


The records copied in the EAD encoding column of the Template, must be paste in the second part of the of the provided EAD form, where you read: `“Paste here your records from the spreadsheet”` , inside the `<dsc></dsc>` element. 



![Copy and Paste Image](https://github.com/marcolock/archivesspace-importguide/blob/master/images/7%20Copy%20and%20Paste%20elements.png)


This spreadsheet does not generate the hierarchical relationships in the EAD. It is expected that users will insert components as needed into the EAD. To structure your data and put  item level records  inside a  series level record  you have to paste them inside the `<c>` series element: the right position is the <did> element just before the closing node couple </did></c>.


![Insert elements Image](https://github.com/marcolock/archivesspace-importguide/blob/master/images/8%20Insert%20elements%20in%20series.png)


To add more information about the collection you can encode it in the EAD or use the ArchivesSpace interface. If you want to do it on the EAD you can key in your texts in the following form, and then copy and paste them in the EAD in the `<archdesc>` node after the <did> and just before the `<dsc>`. You can add more elements or cut off the one you don’t need. To format and lay out the texts, use ArchivesSpace avoiding the risks of import errors. 



	  <did> </did>
	       <abstract> Abstract </abstract>
	       <bioghist> History or Biography </bioghist>
	       <scopecontent> Scope and Content </scopecontent>
	       <custodhist> Provenance </custidhist>
	       <arrangement> Arrangement </arrangement>
	       <odd><head> Note label </head><p> Note body </p></odd>
	       <acessrestrict> Restrictions </acessrestrict>

	    <dsc>
	  [Paste here your records from the spreadsheet]
	    </dsc>




## Start the import and solve the errors

Once the EAD is ready, go on ArchivesSpace in the Background Jobs section, and upload the file. To start the import process click on the button `Queue work` and your import will start as soon the program have finish to run the previous job. The black “Log” window executes the import procedures and it will show the final message with the results of the import.


![Img 9](https://github.com/marcolock/archivesspace-importguide/blob/master/images/9%20Import%20page%20sml.png)


If the import goes fine refresh the page and search for the new collection browsing the Resources (in the staff interface) or the Collections (in the public interface). If some errors occurred, the Log explain why the process interrupted and where to find the error. Mistake in the writing of the EAD could be in both of the preparatory moments (the copy/paste of the records from the collection spreadsheet to the Import Spreadsheet, and the writing of the EAD). 


![Img 10](https://github.com/marcolock/archivesspace-importguide/blob/master/images/10%20Import%20error.png)


Check the spreadsheet and be sure every mandatory field is filled and there aren’t not acceptable characters. Then you may have to check the syntax of the EAD. Here some useful tips: 
* Check the EAD with the online [XML-Validate](http://xmlvalidation.com/)
* Search in your Xml editor how many `<c>` nodes are and compare with the number of `</c>` tags. They have to be at the same amount, or you have to add/delete one or more of them to have a clear syntax. Same procedure for the other relevant elements as the `<did></did>` and the `<unitdate></untdate>`.
* Check the orthography of the EAD and delete characters as the ampersand “&”, the angle brackets “<” and “>” and the quotation marks “ inside the attributes. To insert these not permitted characters you can type:

   * `&lt`; to represent "<";
   * `&gt`; to represent ">";
   * `&amp`; to represent "&";
   * `&apos`; to represent "  **'**  ";
   * `&quot`; to represent '  **"**  '.
   
* Check the “collection description” encoded in EAD to eliminate every formatting characters. 
* Check in the spreadsheet the dates format; sometimes Excel automatically change dates to numbers (and vice-versa) invalidating the EAD. Be sure to copy and paste the columns with the right values. A helpful trick is to copy the records and paste them in a blank NotePad, then copy again and paste on the Template Spreadsheet, formatting the dates column for “text”. 
* To import big collection the best way it’s to split it in series and subseries, and try the import of singles and coherent groups of records and then merge them in a one collective EAD.



## Other systems of import

There are seven different ways to import data in AS. The kind of data you want to import in (Resources, Accessions, Digital object) determinates the kind of format you have to prepare and use as importer. To import Archival Collections (called “Resources” in AS) you can use the EAD or the MARCXml. Here some basic acknowledgment about the import:

* The MARCXml permits also the import of “Resources”, “Accessions” and “Digital Objects”.  It’s an XML schema, released by the Library of Congress, based on the international UNIMARC standards and it is thought to manage bibliographic information in a simple way.
* The CVS it’s a language to store data in a plain text format as simple comma-separated values. It could import “Accessions” and “Digital Objects” in ArchivesSpace. Populate with your data records this Excel Template, following the provided mapping. To create “Digital Objects” with insider subseries, just pay attention to type in the cells digital_object_is_a_component TRUE or FALSE and digital_object_component_id with the ID of the parent object. To transform the Spreadsheet in a CSV file just use the export function of Excel and select CSV as the desired language.

 The migration tools and the import mappings are accessible on the [website](http://archivesspace.org/application/data-import-and-export-maps/). 


## Resources

A lot of resources could be found in internet about the data import on ArchivesSpace. Here some good manuals, articles and online instruments that could be helpful. 

* [ArchivesSpace Manual by the YALE University AS Team](https://docs.google.com/document/d/1DI_7YNZy-RcjQ9hpMMbxJEkHFpYndzmDoG3ylOc38BY/edit#heading=h.1n1mu2y)

* [Migration tools and Data Mapping from AS website](http://archivesspace.org/using-archivesspace/migration-tools-and-data-mapping/)

* [Article about importing errors by the Bentley Historical Library, University of Michigan](http://archival-integration.blogspot.com/2015/04/legacy-ead-import-into-archivesspace.html)

* [Article about data import published on the Harvard University blog](https://dash.harvard.edu/handle/1/30356833)

* [A website about EAD, with vocabulary of elements and attribute, by the Library of Congress](http://loc.gov/ead/index.html)

* [Online tool to check and validate the EAD](http://xmlvalidation.com/)





