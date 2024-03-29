# Perfex CRM patches

[Perfex CRM](https://www.perfexcrm.com) is a self-hosted CRM application written in PHP. This repository provides a set of unofficial patches to add specific functionality to Perfex CRM.

## Patches

* Identity PDF: add a 'corporate identity' PDF as background to most PDF documents. This eliminates the need to implement the look and feel of your existing documents in to Perfex CRM.

## Prerequisites

The below instructions are for Linux servers only, using the 'patch' command.

* the following is quite technical, if you are not sure what you are doing, or not confident to execute the below, please wait until Perfex CRM maybe integrates this code in the next version.

* **make a backup of your code & database first!** (you can never be safe enough)

## Instructions

### Installation

Copy / download the patch file to the root / base directory of Perfex CRM.

In the root / base directory of your Perfex CRM execute the following

```
patch -p1 < <patch filename>
```

You should see something similar as below, depending on the patch you have selected, this can be different,

```
patching file application/composer.json
patching file application/controllers/admin/Settings.php
patching file application/helpers/pdf_helper.php
patching file application/helpers/upload_helper.php
patching file application/language/english/english_lang.php
patching file application/libraries/Pdf.php
patching file application/views/admin/settings/includes/pdf.php
```

* change to application/vendor, and execute

```
composer.phar require setasign/fpdi-fpdf
```

This will install the PDF library required to ‘import’ a PDF document in to other PDF documents.

You will probably have to install / download composer.phar (https://getcomposer.org)

* go to your Perfex CRM database, and execute the following sql command

```
insert into tbloptions values (”, ‘identity_pdf’, ”, 0);
```

This prepares the option in your database. We did not want to add code to the automatic database upgrade / migrations system, since this would increase the version number, causing problems when a new Perfex CRM version is released.

### Configuration

* Log in to the admin, and go to Setup > Settings, on the bottom of the page you have a new option to upload the Corporate Identity PDF.

* upload your PDF

* try to view an invoice, quote, etc. It will normally use the newly uploaded Corporate Identity.

* it is possible that your invoice, estimate, etc. templates will overlap with your imported corporate identity. You will probably need to change the template a bit.


## Bugs & Features

If you find a bug, please use the Github Issue system for this repository to submit the details of your bug report.

If you would like to have a new feature implemented, use the Github Issue system to submit your feature request.


## Legal

This is an unofficial patch to Perfex CRM, built by/for the Perfex CRM community. The app is provided "as is", without warranty of any kind.



