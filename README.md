# EDB Docs Archive: PDF-formatted documentation for older product versions

This repository exists to store, serve and provide a framework for updating PDF files used to document versions of EDB products that are not currently maintained on https://github.com/EnterpriseDB/docs

## Working with this repository

_The instructions here are intended for the use of EDB documentation writers and maintainers who need to update or correct the documentation versions contained in this repository._

### Git LFS

This repository uses Git LFS to minimize local storage requirements. Before pulling or working with the files here via Git, you'll need to install the Git LFS extension. Instructions here: https://github.com/git-lfs/git-lfs/wiki/Installation

**Don't forget to run `git lfs install`** to tell Git about the extension after you've installed it!

### Branch structure

All updates should be pushed to the `develop` branch in this repository. At this point, they will be available for download via [the docs staging server](https://edb-docs-staging.netlify.app/docs/). After verifying that the updated files are available, merge changes into the `main` branch, and they will immediately become available via https://www.enterprisedb.com/docs

### Source files for PDFs

You need to have access to the product repo from which you want to pull the RST source files.

| Product        | Version  | Source format | Repo          | branch        |
| -------------- | -------- | ------------- | ------------- | ------------- |
| EPAS           | 9.6      | DOCX          | edb-documents | PPAS_96       |
|                | 10       | DOCX          | edb-documents | EPAS_10       |
| PEM            | 7.10     | RST           | pem           | REL-7_10      |
|                | 7.11     | RST           | pem           | REL-7_11      |
|                | 7.12     | RST           | pem           | REL-7_12      |
|                | 7.13     | RST           | pem           | REL-7_13      |
|                | 7.14     | RST           | pem           | REL-7_14      |
|                | 7.15     | RST           | pem           | REL-7_15      |
| EFM            | 3.9      | RST           | efm           | V3_9_STABLE   |
|                | 3.8      | RST           | efm           | V3_8_STABLE   |
|                | 3.7      | RST           | efm           | V3_7_STABLE   |
| JDBC Connector | 42.2.8.1 | RST           | edb-jdbc      | DOCS_42.2.8.1 |
|                | 42.2.9.1 | RST           | edb-jdbc      | DOCS_42.2.9.1 |
| .NET Connector | 4.1.5.1  | RST           | edb-dotnet    | DOCS_4.1.5.1  |
|                | 4.1.3.1  | RST           | edb-dotnet    | DOCS_4.1.3.1  |
|                | 4.0.10.1 | RST           | edb-dotnet    | DOCS_4.0.10.1 |
|                | 4.0.6.1  | RST           | edb-dotnet    | DOCS_4.0.6.1  |

### Setting up the environment for updating the RST files

We use Sphinx and Latexpdf packages to generate the PDFs from source RST files. The optimum environment that works for all our requirements is:

**Ubuntu**: 18.04

**Python**: Version 3.4 or above

**Sphinx**: Version 3.0 or above

1. Setup a fresh Ubuntu 18.4 VM on your system and then install Sphinx on it: [http://www.sphinx-doc.org/en/master/usage/installation.html](http://www.sphinx-doc.org/en/master/usage/installation.html).
1. After Sphinx installation, create a base folder for all your RST project directories and run the following command from that directory:

   `Sphinx-quickstart`

   Provide inputs when prompted. This command generates a complete documentation directory and sample Makefile to be used with sphinx-build. Reference

1. Use the following command to install make command:

   `sudo apt install make`

1. Use the following commands to install the required packages for Latexpdf:

   1. `sudo apt-get install latexmk`
   1. `sudo apt-get install texlive-formats-extra`

1. Use the following command to generate a PDF from sample files:

   `make -f Makefile latexpdf`

1. Verify that the PDF gets created in the folder that is displayed on the console.

   If you get the permission error, use the following command:

   `chmod -R 777 *`

### Updating the source files

You can use any editor to modify the RST files (most of the doc team members use [Atom](https://www.ubuntu18.com/install-atom-on-ubuntu-18/)).

After confirming that PDF generation works on your system:

1. Copy the RST files that you need to update from the applicable repo to a folder inside the base directory that you created before running the `sphinx-quickstart` command.

1. Make updates to the RST files.

1. Regenerate the PDF using the command:

   `make -f Makefile latexpdf`

1. Push the updated RST source files back to the repo and branch from which you had pulled it.

1. Push the PDF to the develop branch of docs-archive.

1. Sanity-check the output on the docs staging site (https://edb-docs-staging.netlify.app/).

1. Merge changes from the develop branch of docs-archive to the main branch, at which point they will be live on the production docs site.
