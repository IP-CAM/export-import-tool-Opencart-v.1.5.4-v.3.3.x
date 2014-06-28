Export/Import Tool for OpenCart 1.5.6.x
=======================================

The Import/Export Tool allows the admin user to do a bulk export
of all the categories, products, and product options to an Excel spreadsheet file.
The spreadsheet file can be edited offline and then be re-imported to the OpenCart database.


Requirements and Limitations
============================

1)	This module only supports one front end language.

2)	Memory requirements can be quite high.

	For example, for a store that has 13,500 products and 300 categories:

		XLS File Size: 9 to 10MB
		Memory Usage Export: up to 13MB
		Memory Usage Import: up to 355MB

	Which works fine with the following PHP settings:

		memory_limit 512M
		post_max_size 16M 
		upload_max_filesize 16M

	Not every shared web hosting account supports such a high process memory usage.
	Therefore, if you use a basic shared web hosting account, no more than than a few thousands
	products can be supported. Use a more dedicated web hosting account if a higher number of
	products are to be supported for the Export/Import module.

	The high memory usage of the Import is due to the fact that the underlying PHPExcelReader parses 
	the whole file into RAM memory first before being able to access the spreadsheet cells.


Installation
============


Step 1) 
Upload the folders 'admin' and 'system' and their files 
from the 'upload' directory to your remote OpenCart main directory.

Step 2)
The following OpenCart core files need to be changed:

	admin/controller/common/header.php
	admin/language/english/common/header.php
	admin/view/template/common/header.tpl

There are 3 ways to do that:

a) If the Override Engine is already pre-installed:
   (see http://www.opencart.com/index.php?route=extension/extension/info&extension_id=8588)
   Simply upload the folder 'override' with its sub-folders and files
   to your remote OpenCart main directory.

b) Else, if you have VQmod pre-installed:
   (see http://code.google.com/p/vqmod/)
   Simply upload the folder 'vqmod' with its sub-folders and files 
   to your remote OpenCart main directory.

c) Neither the Override Engine nor VQmod is pre-installed:
   You have to manually edit the header files, as follows:

	In file admin/controller/common/header.php find:
	$this->data['text_backup'] = $this->language->get('text_backup');
	Add the following after the found line:
	$this->data['text_export'] = $this->language->get('text_export');

	In file admin/controller/common/header.php find:
	$this->data['backup'] = $this->url->link('tool/backup', 'token=' . $this->session->data['token'], 'SSL');
	Add the following after the found line:
	$this->data['export'] = $this->url->link('tool/export', 'token=' . $this->session->data['token'], 'SSL');

	In file admin/language/english/common/header.php find:
	$_['text_backup'] = 'Backup / Restore';
	Add the folling after the found line:
	$_['text_export'] = 'Export / Import';

	In file admin/view/template/common/header.tpl find:
	<li><a href="<?php echo $backup; ?>"><?php echo $text_backup; ?></a></li>
	Add the following after the found line:
	<li><a href="<?php echo $export; ?>"><?php echo $text_export; ?></a></li>

Step 3) 
Before using this newly installed Export/Import feature for the first time, you must set the 
access rights for top administrator as follows:

In the admin interface, choose 

	System > Users > User Group

From there, select 'Top Administrator', then click on the 'Edit' link to the right. 
This will open up an edit window with multichoice dropdown lists for 'Access' and 'Modify' rights. 
In both of them, you'll see a new entry for 'tool/export' which you can select by clicking
on their check boxes.




Further help and customized versions
====================================

This tool has been successfully tested for a standard OpenCart 1.5.6.x.
Don't use other Opencart versions with this module.

If you need a customized version of the Export/Import Tool,
let us know and we can create one for a charge.

You can contact us at <http://www.mhccorp.com>

	Juergen Neuhoff - MHCCORP.COM
	http://www.mhccorp.com

