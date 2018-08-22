The below instructions are for Linux servers only, using the 'patch' command.

# Instructions

* the following is quite technical, if you are not sure what you are doing, or not confident to execute the below, please wait until Perfex CRM maybe integrates this code in the next version.

* make a backup of your code & database first! (you can never be safe enough)

* copy / download the patch file to the root / base directory of Perfex CRM

* in the root / base directory of your Perfex CRM execute the following

```
patch -p1 < perfexcrm_ngc201-identitypdf.patch
```

You should see

```
patching file application/composer.json
patching file application/controllers/admin/Settings.php
patching file application/helpers/pdf_helper.php
patching file application/helpers/upload_helper.php
patching file application/language/english/english_lang.php
patching file application/libraries/Pdf.php
patching file application/views/admin/settings/includes/pdf.php
```

* go to application/vendor, and execute

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

* Log in to the admin, and go to Setup > Settings, on the bottom of the page you have a new option to upload the Corporate Identity PDF.

* upload your PDF

* try to view an invoice, quote, etc. It will normally use the newly uploaded Corporate Identity.

* it is possible that your invoice, estimate, etc. templates will overlap with your imported corporate identity. You will probably need to change the template a bit.

This is just an initial version, please let me know if there are issues.
