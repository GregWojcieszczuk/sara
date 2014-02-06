sara
====

RHEL6.x/CentOS 6.x/OpenSUSE 13.1 (RPM, 64-bit only)

[Download latest version](https://github.com/GregWojcieszczuk/sara/blob/master/sara-1.0-12.el6.x86_64.rpm?raw=true)

[GPG KEY](https://github.com/GregWojcieszczuk/sara/raw/master/GREGW-GPG-KEY)

SARA - Linux SAR Analyzer

SARA is the tool that helps visualizing SAR (System Activity Reporter) logs.
This tool creates PDF/PNG report based on data contained in sa (binary) file.

[Sample PDF report generated on OpenSUSE 13.1](https://github.com/GregWojcieszczuk/sara/raw/master/sample-reports/linux-y2xn-sa05-REPORT.pdf)

[Sample PDF report generated on CentOS 6.5](https://github.com/GregWojcieszczuk/sara/raw/master/sample-reports/linux-y2xn-sa05-REPORT.pdf)

Notice that sara can be installed on any supported OS. 
It can graph/analyze sysstat performance data generated on any Linux distro that utilizes systat 9.x or higher.

Features:
  * Creating PDF report (multiple-page single doc)
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


Installation:

    On CentOS/RHEL 6.x

    yum install sara-1.0-12.el6.x86_64.rpm

    On OpenSUSE 13.1

    zypper install ./sara-1.0-12.el6.x86_64.rpm

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

    gzip /var/log/sa/sa$(date +%d -d '1 day ago')


Do not forget to make processSA executable:

    chmod 755 /var/log/sa/processSA


TODO LIST:

    * Verify if that program works correctly on: Fedora 19 (RHEL7), SLES, SLED
    * Build DEB package for Ubuntu (13.10, 12.0.4 LTS) and latest Debian

Report bugs to: saraproject '''at''' unixos.org
