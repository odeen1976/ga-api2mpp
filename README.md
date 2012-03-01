Introduction
============

These scripts were developed as part of an un-confrence session at the Analytics Camp held in
Chapel Hill, NC on February 25, 2012, described on this page as [http://wiki.analyticscamp.org/nc2011proposals](http://wiki.analyticscamp.org/nc2011proposals).

The scripts demonstrate how to pull data from the Google Analytics API to generate an RSS feed
of a website or blog's most popular pages, as well as creating a CSV file for further processing.

During the presentation, the RSS feed was incorporated into a WordPress blog by using the
build-in RSS widget.

Non-programmer analytics geeks also appreciated having their data in a spreadsheet so they could
do their magic.

Bear in mind, the data these tools collect are only as good as your Google Analytics implementation.

The presentation is available at Slideshare at: http://bitly.com/gaapi2mpp?git

## Installation ##
This example code was provided in both Python and Perl.

* The Python example script is stand-alone and does NOT need the Perl example script nor its dependencies.
* The Perl example script is stand-alone and does NOT need the Python example script nor its dependencies.

Below are the installation instructions for each respectively:

### Python ###

The Python script requires the following libraries:

* [python-googleanalytics](https://github.com/clintecker/python-googleanalytics)
* [PyRSS2Gen](http://www.dalkescientific.com/Python/PyRSS2Gen.html)

You should be able to type in the following after checking-out the source:

Theoretically you should be able to type the following after checking out the source:

`sudo python setup.py install`

You can also just install using `easy_install` like so:

`sudo easy_install python-googleanalytics`
`sudo easy_install PyRSS2Gen`


### Perl ###

The Python script requires the following CPAN libraries:

* [Net::Google::Analytics](http://search.cpan.org/dist/Net-Google-Analytics/)
* [Net::Google::AuthSub](http://search.cpan.org/~simonw/Net-Google-AuthSub-0.5/lib/Net/Google/AuthSub.pm)
* [XML::FeedPP](http://search.cpan.org/~kawasaki/XML-FeedPP-0.43/lib/XML/FeedPP.pm)

Installation is pretty straight forward:

`perl -MCPAN -e shell install Net::Google::Analytics Net::Google::AuthSub XML::FeedPP`

NOTE: 
You may encounter an error installing Net:Google::AuthSub in the form of a file 
permission error generated by ExtUtil::MakeMaker with regards to man page paths.

You'll want to see this page: 

* http://search.cpan.org/~leont/Module-Build-0.40/lib/Module/Build.pm
	
It explains how you can modify your ~/.cpan/CPAN/MyConfig.pm to modify makepl_arg arg.

Here's what mine looked like:

  `'makepl_arg' => q[PREFIX=~/perlmods INSTALLMAN1DIR=~/perlmods/share/man/man1 INSTALLSITEMAN1DIR=~/perlmods/share/man/man1 INSTALLMAN3DIR=~/perlmods/share/man/man3 INSTALLS
ITEMAN3DIR=~/perlmods/share/man/man3],`

On a personal note, Dreamhost doesn't seem to currently want to incorporate this directive from the MyConfig.pm file.


## Operation ##

Regardless of whether you're using the Perl or Python example scripts, you'll want to familiarize 
yourself with the arguments available on the Googl API 
[Dimensions & Metrics Reference](http://code.google.com/apis/analytics/docs/gdata/dimsmets/dimsmets.html) page.

Also note that regardless of whether you run the Python or Perl example script, you'll need
to have access to a Google Analytics account, and have obtained a profile id 
(note, this is NOT the same thing as the ua-key).

The general syntax for both scritps is:
[script name] [gmail/username] [password] [ga profile id]

As discussed in the demonstration, the script is made so it can run regularly using crontab. 
The online '[visual crontab utility](http://www.corntab.com/pages/crontab-gui)' may provide assistance to 
thos individuals who can't always remember the cron syntax.

### Ruby ###

Below is the command-line syntax for running the Python example script:
<pre>
python ga-api2mpp.py username\@gmail.com password 1234567
</pre>

The script generates the follwing files:
* mpp-py.rss - a python generated RSS 2.0 compliant file of the top 20 most popular pages
* mpp-py.csv - a python generated tab-delimited file of all pages pulled from Google Analytics

### Perl ###

Below is the command-line syntax for running the Perl example script:
<pre>
perl ga-api2mpp.pl username\@gmail.com password 1234567
</pre>

The script generates the follwing files:

* mpp-pl.rss - a perl generated RSS 2.0 compliant file of the top 20 most popular pages
* mpp-pl.csv - a perl generated tab-delimited file of all pages pulled from Google Analytics


### Environments ###

Once the required libraries/modules are installed, I was able to run both script on the following platforms:

* Mac OS X 10.7
* Ubuntu 11.00
* CentOS 5
* Windows 7

Of course, your mileage may vary!

