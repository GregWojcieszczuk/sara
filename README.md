sara
====

Only 64-bit builds

[RHEL6/CentOS6 download](https://github.com/GregWojcieszczuk/sara/raw/master/rpms/rhel6/sara-1.0-13.el6.x86_64.rpm)

[OpenSUSE 13.1 download](https://github.com/GregWojcieszczuk/sara/raw/master/rpms/opensuse13.1/sara-1.0-13.el6.x86_64.rpm)

[Fedora 20 download](https://github.com/GregWojcieszczuk/sara/raw/master/rpms/f20/sara-1.0-13.x86_64.rpm)


[GPG KEY](https://github.com/GregWojcieszczuk/sara/raw/master/GREGW-GPG-KEY)

**SARA - Linux SAR Analyzer**

SARA is the tool that helps visualizing SAR (System Activity Reporter) logs.
This tool creates PDF/PNG report based on data contained in sa (binary) file.

[Sample report 1](https://github.com/GregWojcieszczuk/sara/raw/master/sample-reports/srv3.unixos.org-sa26-REPORT.pdf)

[Sample report 2](https://github.com/GregWojcieszczuk/sara/raw/master/sample-reports/linux-y2xn-sa10-REPORT.pdf)

[Sample report 3](https://github.com/GregWojcieszczuk/sara/raw/master/sample-reports/buildhost1.linuxlab.local-sadc-9.0.6-data.dat-REPORT.pdf)

[Sample report 4](https://github.com/GregWojcieszczuk/sara/raw/master/sample-reports/buildhost1.linuxlab.local-sa10-REPORT.pdf)

Notice that sara can be installed on any supported OS. 
It can graph/analyze sysstat performance data generated on any Linux distro that utilizes systat 9.x or higher.

**Features**
  * Creating PDF report (multiple-page single doc); with bookmarks for each section
  * Creating report for specified period of time (within single day)
  * Creating PNG files covering individual data sections (e.g. disk activity, network activity, etc)
  * 100% non-interactive
  * Customizable
  * Supports all SAR 9.0.x tests
  * Compatible with sar 9.0.x, 10.0.x 10.2.x data files (sa1/sadc); only stable sysstat revisions
  * Relies on:

     a) sysstat, http://sebastien.godard.pagesperso-orange.fr

     b) gnuplot, http://www.gnuplot.info

     c) imagemagick, http://www.imagemagick.org
     
  * Does not require sar, gnuplot and imagemagick to be installed

**Known issues**
   **Adobe PDF reader (windows version only) doesn't display colors. All graphs are in grayscale.**

   **All other PDF readers (like Foxit PDF reader), evince, chrome built-in PDF reader, etc don't exhibit this problem.**


**Installation**

    On CentOS 6.x/RHEL 6.x

    yum install sara-1.0-13.el6.x86_64.rpm

    On Fedora 20

    yum install sara-1.0-13.x86_64.rpm

    On OpenSUSE 13.1

    zypper install sara-1.0-13.el6.x86_64.rpm

To get list of available options and usage syntax, run:

    /opt/sara/sara
    SYNTAX:

    /opt/sara/sara [options]

    Options:
    -s <path>
         Specify path to binary SA file (mandatory)

    -o <path>
         Specify path to output directory (mandatory)

    -t HH:MM:SS-HH:MM:SS
         Define time range for report (optional). 
         If not defined, display report for all available data in SA file.
   
    -c <path>
         Path to config file (optional). Default location: /opt/sara/etc/reports.pref

    -r ipdf|pdf|png
        Specify type of output report.
        Default: pdf

        ipdf - generate individual (for every sar test) pdf files in directory defined with "-o" option
        pdf  - generate single pdf file with all data
        png  - generate individual PNG files for every sar test

    -h|-?
         Display this help

    EXAMPLES:
    
    /opt/sara/sara -s /var/log/sa/sa06 -t 00:00:00-12:28:03 -o /tmp/sartest

    /opt/sara/sara -s /var/log/sa/sa06 -o /tmp/sartest



To get very granular sar performance data from your system you can modify default crontab job:

     */1 * * * * root /usr/lib64/sa/sa1 -S XALL 5 12

If you plan to use that tool, you can probably comment out this line:

     #53 23 * * * root /usr/lib64/sa/sa2 -A

Sysstat data with 5 sec sampling interval may create ~350-400MiB sa files (/var/log/sa).

In order to avoid storing lots of very large files, you can add the following crontab job:

     42 00 * * * root /var/log/sa/processSA

Content of processSA script

    #!/bin/bash

    dirprefix="/var/log/sa"
    Oldsafile="$dirprefix/sa$(date +%d -d '1 day ago')"
    Newsafile="$dirprefix/sa-$(date +%Y-%m-%d -d '1 day ago')"
    mv $Oldsafile $Newsafile
    gzip "$Newsafile"



Do not forget to make processSA executable:

    chmod 755 /var/log/sa/processSA


**TODO LIST**

    * Verify if that program works correctly on: RHEL7 beta, SLES, SLED
    * Build DEB package for Ubuntu (13.10, 12.0.4 LTS) and latest Debian

Report bugs to: saraproject '''at''' unixos.org
