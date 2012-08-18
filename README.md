XMLTV Lineup Generator for the UK and Ireland
=============================================

A tool to generate XMLTV lineups for the majority of TV platforms in the UK
and Republic of Ireland.


Introduction
------------

Each lineup generated by this utility should contain all channels available
on a given TV platform. A platform is a specific TV service like Freesat or
Virgin TV in the UK.

Lineups are generated by merging a variety of information. Currently
the following daa sources are employed:

- TV service provider websites (e.g. Virgin, Sky) for EPG/channel details
- Wikipedia for EPG numbering, and channel availability
- Transmitted DVB stream information for service/network identifiers and
  service names extracted via the w\_scan or dvbscan tools
- Data I maintain for the [XMLTV Project](http://www.xmltv.org) including
  regional availability, XMLTV IDs and icons for supported channels
- Channel index file from the Radio Times XMLTV service
- Significant configuration information for each supported platform is
  also stored within the tool

Lineups are generated using the XMLTV Lineups Schema from the XMLTV Project to
ensure that documents are not only well-formed but also valid lineup documents.


Prerequisites
-------------

In addition to a current installation or local build of XMLTV (0.5.63 at time
of writing), this tool requires the following Perl modules to be installed for
XML parsing and generation:

- XML::Compile::Schema

If the tool should fail to run due to other missing dependencies, please
install them via your favourite package manager or from CPAN.


Usage
-----

To generate an XML document listing all supported platforms:

    ./lineup-generator --list-platforms

Each supported platform has an *id* which is used as an identifier in the
following commands.

To generate an XML document containing the full lineup for a particular
platform (e.g. 'freeview'):

    ./lineup-generator --generate-lineup --platform freeview

To output a multi-line list of icon URLs for all channels on a given platform
(e.g. 'freesat'):

    ./lineup-generator --list-icons --platform freesat

To view usage information:

    ./lineup-generator --help


Supported TV platforms
----------------------

Separate high definition and standard definition lineups are generated to
cater for users with or without HDTV capability. Lineups for the
following TV platforms are currently supported:

- Freesat
- Freesat HD
- Freesat From Sky
- Freeview
- Freeview HD
- Saorview
- Sky
- Sky HD
- UPC Ireland
- UPC Ireland HD
- Virgin
- Virgin HD


Pre-generated lineups
---------------------

Regularly generated lineups for all supported platforms are available in my
[xmltv-lineups-uk](https://github.com/knowledgejunkie/xmltv-lineups-uk)
repository on GitHub.


Filtering lineups
-----------------

Channels are associated with regional/national availability and subscrition
package details to allow filtering of a generated lineup to contain only
those channels available in a particular location with a specific subscription.
It is therefore quite likely to see several channels in a lineup occupying the
same EPG slot even though only one should be available in a given location.

Note that the tv\_grab\_uk\_rt listings grabber from the XMLTV Project filters
lineups automatically during configuration and listings retrieval based on a
user's configured location, TV platforms and subscription package selection.


Lineup details
--------------

The following details may be provided for a lineup:

- type (generally DVB or STB)
- display name
- availability (by country, region or postcode where necessary)
- details of lineup generation (date, generator, lineup id)


Channel details
---------------

The following details may be provided for each channel that is part of a
lineup:

- EPG preset
- EPG section
- Package (i.e. a subscription package or FTA)
- Availability (by country, region or postcode)
- Type (TV or radio)
- XMLTV ID (where supported)
- Name and short name
- Channel icon
- HDTV status
- Aspect ratio
- Whether channel is advert free

Additionally, channels broadcast via DVB-T (Freeview) and DVB-S (Freesat) may
include the following information broadcast in the digital signal:

- ONID (original network ID)
- SID (service ID)
- LCN (logical channel number)
- Transmitted service name
- Encryption status


xmltv-lineups.xsd
-----------------

The XML Schema document supplied is that used by the XMLTV Project. All
lineups are generated against this schema.


Robustness
----------

This tool employs significant pattern and string matching when merging data
from multiple sources, and thus is prone to breakage if channel names or other
key matching data are not consistent across sources. However, this tool has been
used successfully for several months, and the author works to ensure sources
maintain consistency over time.

If you notice any channels that have been renamed/added/deleted on a service
which are not reflected in a lineup, please inform the developer.


Author information
------------------

I contribute to the XMLTV and [MythTV](http://mythtv.org) projects and am
working on various ways to make channel configuration in these project easier,
especially for users in the UK and Republic of Ireland.

Feel free to follow me on
[GitHub](https://github.com/knowledgejunkie)
and
[Twitter](http://twitter.com/nickmorrott).


License
-------

Copyright (c) Nick Morrott. Licensed under the
[GNU GPL v2 or later](http://www.gnu.org/licenses/gpl.html).
