# README #

### Latest updates ###

* _11/07/2019_: Now compatable with the latest version of sen2cor (2.8.0). Note that command line scripts have also moved to a new location (.../sen2mosaic/cli).
* Now compatable with Python 3. It should remain possible to run these scripts with Python 2, but this will no longer be supported.
* Multiple near-identical mask outputs have been replaced with a single 'SLC' file.

### What is this repository for? ###

Building cloud-free mosaics of Sentinel-2 data for land cover mapping is difficult, with existing tools still under-development and frequently confusing.

This is a set of tools to aid in the production of large-scale cloud-free seasonal mosaic products from Sentinel-2 data. The goal is to streamline this processing chain with a set of straightforward command line tools.

This repository contains four command-line based scripts to perform the following tasks:

* Downloading Sentinel-2 data from the [Copernicus Open Access Hub](https://scihub.copernicus.eu/) for a particular tile, specifying date ranges and degrees of cloud cover. This is based on the [Sentinelsat](https://github.com/sentinelsat/sentinelsat) utility.
* Executing the [sen2cor](http://step.esa.int/main/third-party-plugins-2/sen2cor/) tool to perform atmospheric correction, and performing simple improvements to its cloud mask.
* Building a mosaic of cloud-free GeoTIFF files that are suitable for image classification.


### How do I get set up? ###

These tools are written in Python for use in Linux. You will need to have first successfully installed:

* [sentinelhub](https://github.com/sinergise/sentinelhub): A library for searching and downloading Sentinel-2 products.
* [sen2cor](http://step.esa.int/main/third-party-plugins-2/sen2cor/): Atmospheric correction and cloud masking for Sentinel-2.

The tool sen2cor is both built around the [Anaconda](https://www.anaconda.com/download/) distribution of Python. The modules used in these scripts are all available in Anaconda Python.

### How does it work? ###

Full documentation is hosted at: [http://sen2mosaic.readthedocs.io/](http://sen2mosaic.readthedocs.io/).

### Who do I talk to? ###

Written and maintained by Samuel Bowers ([sam.bowers@ed.ac.uk](mailto:sam.bowers@ed.ac.uk)).
