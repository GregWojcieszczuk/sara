sara
====

SARA - Linux SAR Analyzer

SARA is the tool that helps visualizing SAR (System Activity Reporter) logs.
This tool creates PDF/PNG report based on data contained in sa (binary) file.

Features:
  * Creating PDF report (multiple-page single doc)
  * Creating report for specified period of time (within single day)
  * Creating PNG files covering individual data sections (e.g. disk activity, network activity, etc)
  * 100% non-interactive
  * Customizable
  * Supports all SAR 9.x tests
  * Compatible with sar 9.x and 10.x
  * Relies on:

     a) sar, http://sebastien.godard.pagesperso-orange.fr
     b) gnuplot, http://www.gnuplot.info
     c) imagemagick, http://www.imagemagick.org
     

  * Does not require sar, gnuplot and imagemagick to be installed (bundles all required packages/libs)


To get list of available options and usage syntax, run:

$ /opt/sara/sara


    EXAMPLES:
    
    /opt/sara/sara -s /var/log/sa/sa05 -t 00:00:00-02:09:58 -o /tmp/sartest

    /opt/sara/sara -s /var/log/sa/sa05 -o /tmp/sartest

TODO LIST:

    * Verify if that program works correctly on: Latest Fedora, SLES, SLED
    * Build DEB package for Ubuntu (13.10, 12.0.4 LTS) and latest Debian

Report bugs to: greg <at> unixos.org
