---
layout: extension
name: officedocs
title: MS Office and OpenOffice Resource Viewer
author: Ross Jones
homepage: https://github.com/jqnatividad/ckanext-officedocs
github_user: jqnatividad
github_repo: ckanext-officedocs
category: Extension
featured: 1
permalink: /extension/officedocs/
---


|--------------------|
| ckanext-officedocs |

This plugin provides the option of using the Microsoft Office viewer for previewing both MS Office and OpenOffice documents as an IResourceView

------------Supported formats ------------

This plugin will attempt to preview the following formats

> "DOC", "DOCX", "XLS", "XLSX", "PPT", "PPTX", "PPS", "ODT", "ODS", "ODP"

Installation
============

To install ckanext-officedocs:

1.  Clone this repository into the place where you normally install extensions, by default this will be /usr/lib/ckan/default/src/
2.  Activate your CKAN virtual environment, for example:

        . /usr/lib/ckan/default/bin/activate

3.  Install the ckanext-officedocs Python package into your virtual environment:

        cd ckanext-officedocs
        python setup.py install

4.  Add `officedocs_view` to the `ckan.plugins` setting in your CKAN config file (by default the config file is located at `/etc/ckan/default/production.ini`).
5.  Restart CKAN. For example if you've deployed CKAN with Apache on Ubuntu:

        sudo service apache2 reload



