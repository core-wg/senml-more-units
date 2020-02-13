---
stand_alone: true
ipr: trust200902
docname: draft-ietf-core-senml-more-units-latest
keyword: Internet-Draft
cat: std
pi:
  toc: 'yes'
  tocompact: 'yes'
  tocdepth: '3'
  tocindent: 'yes'
  symrefs: 'yes'
  sortrefs: 'yes'
  comments: 'yes'
  inline: 'yes'
  strict: 'no'
  compact: 'yes'
  subcompact: 'no'
title: Additional Units for SenML
abbrev: Additional Units for SenML
date: 2020-02-13
author:
-
  ins: C. Bormann
  name: Carsten Bormann
  org: Universitaet Bremen TZI
  street: Postfach 330440
  city: Bremen
  code: D-28359
  country: Germany
  phone: +49-421-218-63921
  email: cabo@tzi.org

normative:
  RFC8428: senml
  RFC8126: ianacons
  IANA.senml:
  IEC-80000-6:
    title: >
      Quantities and units –
      Part 6: Electromagnetism
    seriesinfo:
      IEC: 80000-6
      Edition: 1.0
    date: 2008-03-01
  IEC-80000-13:
    title: >
      Quantities and units –
      Part 13: Information science and technology
    seriesinfo:
      IEC: 80000-13
      Edition: 1.0
    date: 2008-03-01
  IEEE-1459:
    title: >
      IEEE Standard Definitions for the Measurement of Electric Power
      Quantities Under Sinusoidal, Nonsinusoidal, Balanced, or
      Unbalanced Conditions
    seriesinfo:
      IEEE Std: 1459-2010
    date: 2010-03-19
informative:
  I-D.bormann-core-senml-versions: versions
  RS:
    title: "Standard-compliant usage of quantities, units and equations"
    author:
      org: Rohde&Schwarz
    seriesinfo:
      version: 04.00
    date: 2016-11
    target:  https://karriere.rohde-schwarz.de/fileadmin/user_upload/Standard-compliant_usage_of_quantities_units_and_equations_bro_en_5214-5061-62_v0400_96dpi.pdf
  BIPM:
    title: The International System of Units (SI), 9th edition
    date: 2019
    target: https://www.bipm.org/utils/common/pdf/si-brochure/SI-Brochure-9-EN.pdf
    author:
      org: Bureau International des Poids es Mesures



--- abstract

The Sensor Measurement Lists (SenML) media type supports the
indication of units for a quantity represented.
This short document registers a number of additional unit names in the
IANA registry for Units in SenML.
It also defines a registry for secondary units that cannot be in SenML's
main registry as they are derived by linear transformation from units
already in that registry.

--- middle


# Introduction {#intro}


The Sensor Measurement Lists (SenML, {{-senml}}) media type supports the
indication of a unit, using the SenML field "u", for the quantity
given as a data value in a SenML record.   For this purpose, SenML
defines an IANA registry of defined Unit names and their meanings; in
the present document, we call the Unit names registered there "primary
Unit names".

This short document registers a number of additional units in the IANA
registry for Units in SenML that appear to be
necessary for further adopting SenML in other Standards Development
Organizations (SDOs).

The document also defines a registry for secondary Unit names that
cannot be in SenML's main registry as they are derived by linear
transformation from units already in that registry.

{::boilerplate bcp14}

# New Units

IANA is requested to assign new units in the "SenML Units"
subregistry of the SenML registry {{IANA.senml}} (as defined in {{RFC8428}}):

| Symbol | Description                                    | Type  | Reference |
|--------+------------------------------------------------+-------+-----------|
| B      | Byte (information content)                     | float | RFCthis   |
| VA     | volt-ampere (Apparent Power)                   | float | RFCthis   |
| VAs    | volt-ampere second (Apparent Energy)           | float | RFCthis   |
| var    | volt-ampere reactive (Reactive Power)          | float | RFCthis   |
| vars   | volt-ampere reactive second (Reactive Energy)  | float | RFCthis   |
| J/m    | joule per meter (Energy per distance)          | float | RFCthis   |
| kg/m3  | kilogram per cubic meter (mass concentration)  | float | RFCthis   |
| deg    | degree (angle)*                                | float | RFCthis   |
{: #new-unit-tbl title="New units registered for SenML"}

# Rationale

SenML {{-senml}} takes the position that unscaled SI units should
always be used.  However, SenML makes one exception: The degree
Celsius (as Cel) is allowed as an alternative to the K (Kelvin).

This document takes the position that the same should apply to
a small number of alternative units in wide use:

* The Byte.  {{IEC-80000-13}} defines both the bit (item 13-9.b) and
  the byte (item 13-9.c, also
  called octet) as alternative names for the coherent unit one for the
  purpose of giving storage capacity and related quantities.  While
  the name octet is associated with the symbol o, this is in wide use
  only in French-speaking countries.  Globally more wide-spread is the
  symbol B for byte, even though B is already taken in SI for bel.
  {{-senml}} therefore registers dB as the SenML unit for logarithmic relative
  power, leaving B free for the usage proposed here.  While this is
  potentially confusing, the situation is widely understood in
  engineering circles and is unlikely to cause actual problems.
* The Volt-Ampere. {{IEC-80000-6}}} item 6-57.a defines the VA (volt
  ampere) as a unit for apparent power; items 6-59.a, 6-60.a and
  6-61.a also use the unit for complex, reactive, and non-active
  power.
* The Volt-Ampere-reactive.  {{IEC-80000-6}} item 6-60.b defines the
  var (volt ampere reactive) as an alternative (and fully equivalent)
  unit to VA specifically for reactive power (with the primary unit
  VA).  It is not presently known to this author how the upcoming
  revision of IEC 80000-6 will update this, but it has became clear
  that there is strong interest in using this unit
  specifically for the imaginary content of complex power, reactive
  power {{IEEE-1459}}.

The unit "degrees" is in wide use in practice for plane angles (as
in heading, bearing, etc.).  It is marked with an asterisk because the
preferred coherent SI unit is radian ("rad").

The Joule per meter is not a traditional electromagnetic unit.  It and
its scaled derivatives (in particular Wh/km) are used to describe the
energy expended for achieving motion over a given distance, e.g., as an
equivalent for electrical cars of the inverse of "mileage".


# New Registry

IANA is requested to create a "secondary units"
subregistry in the SenML registry {{IANA.senml}} defined in
{{RFC8428}}.

The registry has six columns:

* secondary unit: a newly registered name allocated within the same
  namespace as SenML units
* description: short description (usually just expansion of abbreviation)
* SenML unit: an existing SenML unit from the SenML units registry
* scale, offset: two rational numbers, expressed in decimal
  (optionally, with a decimal exponent given) or as a
  fraction divided by a "/" character.
* Reference: where does the entry come from.

Quantities expressed in the secondary unit can be converted into the
SenML unit by first multiplying their value with the scale number and
then adding the offset, yielding the value in the given SenML unit.

The initial content of the secondary units registry is provided in {{secondary-unit-tbl}}:

| secondary unit | description                | SenML unit |     scale | off set | refer- ence |
| ms             | millisecond                | s          |    1/1000 |       0 | RFCthis     |
| min            | minute                     | s          |        60 |       0 | RFCthis     |
| h              | hour                       | s          |      3600 |       0 | RFCthis     |
| kW             | kilowatt                   | W          |      1000 |       0 | RFCthis     |
| kVA            | kilovolt-ampere            | VA         |      1000 |       0 | RFCthis     |
| kvar           | kilovar                    | var        |      1000 |       0 | RFCthis     |
| Ah             | ampere-hour                | C          |      3600 |       0 | RFCthis     |
| Wh             | watt-hour                  | J          |      3600 |       0 | RFCthis     |
| kWh            | kilowatt-hour              | J          |   3600000 |       0 | RFCthis     |
| varh           | var-hour                   | vars       |      3600 |       0 | RFCthis     |
| kvarh          | kilovar-hour               | vars       |   3600000 |       0 | RFCthis     |
| kVAh           | kilovolt-ampere-hour       | VAs        |   3600000 |       0 | RFCthis     |
| Wh/km          | watt-hour per kilometer    | J/m        |       3.6 |       0 | RFCthis     |
| KiB            | kibibyte                   | B          |      1024 |       0 | RFCthis     |
| GB             | gigabyte                   | B          |       1e9 |       0 | RFCthis     |
| Mbit/s         | megabit per second         | bit/s      |   1000000 |       0 | RFCthis     |
| MB/s           | megabyte per second        | bit/s      |   8000000 |       0 | RFCthis     |
| mV             | millivolt                  | V          |    1/1000 |       0 | RFCthis     |
| mA             | milliampere                | A          |    1/1000 |       0 | RFCthis     |
| dBm            | decibel (milliwatt)        | dBW        |         1 |     -30 | RFCthis     |
| ug/m3          | microgram per cubic meter  | kg/m3      |      1e-9 |       0 | RFCthis     |
| mm/h           | millimeter per hour        | m/s        | 1/3600000 |       0 | RFCthis     |
| m/h            | meter per hour             | m/s        |    1/3600 |       0 | RFCthis     |
| ppm            | parts per million          | /          |      1e-6 |       0 | RFCthis     |
| /100           | percent (Note 1)           | /          |     1/100 |       0 | RFCthis     |
| /1000          | permille                   | /          |    1/1000 |       0 | RFCthis     |
| hPa            | hectopascal                | Pa         |       100 |       0 | RFCthis     |
| mm             | millimeter                 | m          |    1/1000 |       0 | RFCthis     |
| cm             | centimeter                 | m          |     1/100 |       0 | RFCthis     |
| km             | kilometer                  | km         |      1000 |       0 | RFCthis     |
| km/h           | kilometer per hour         | m/s        |     1/3.6 |       0 | RFCthis     |
{: #secondary-unit-tbl title="Secondary units registered for SenML"
cols="9l l 6l 9r r l"}

Note 1: This registration does not use the obvious name "%" because
this name has been taken in {{-senml}} already, where it is a NOT
RECOMMENDED synonym for "/" (unity) for legacy reasons.  Note that the
presence of both "%" and "/100" with different meanings is likely to
create confusion, so the present document adds some weight to the
recommendation against using the counterintuitive unit name "%".

Example: the value of a quantity given as 100 ms is first multiplied
by 1/1000, yielding the number 0.1, and then the offset 0 is added,
yielding the number 0.1 again, leading to a quantity of 0.1 s.
The value of a quantity given as 10 dBm is first multiplied by 1,
yielding the number 10, and then the offset -30 is added, yielding the
number -20, leading to a quantity of -20 dBW.

New entries can be added to the registration by Expert Review as
defined in {{RFC8126}}.  Experts should exercise their own good
judgment, with the same guidelines as used for SenML units (Section
12.1 of {{RFC8428}}), but without applying the rules 4, 5, and 8.
Note that rule 7 limits the use of what could be understood as
prefixes on their own, not the use of prefixes inside secondary unit
names.
Guidelines to the difference between units (which can go into the
registry) and quantities are widely available, see for instance {{RS}}
and {{BIPM}}.

<!-- benefits of using the first one: can compare right away, no -->
<!-- normalization step; but normalization is not that hard either -->
As of SenML version 10 {{RFC8428}}, SenML packs are limited to
using primary units in "u" fields.
The use of primary units enables direct comparison of measurements
from different sources.  Also, it facilitates implementations that
trigger on the presence of a quantity in a certain unit, without the
need to track any additional secondary units that may be registered
for this quantity.

Where the benefits of directly using a secondary unit in a SenML pack
outweigh the above considerations,
the use of secondary units in "u" fields MAY be enabled by indicating a new SenML
version that specifically allows this and/or by using a field with a label name that ends with the "_"
character ("must-understand" field) that specifically allows this.
The definition of these versions and fields is outside the scope of
the present specification; one such definition is provided in {{-versions}}.

# Operational Considerations

The secondary unit registry is expected to grow at a faster pace than
the registry of primary unit names.  It also is amenable to automatic
interpretation, by making use of the scale and offset columns.

Implementers may be tempted to equip each instance of their systems
with code to download new versions of the registry from IANA
frequently, in order to be able to make use of newly defined secondary
unit names.  This can create high load at IANA and a potential single
point of failure.  Instead of pulling the registry in each individual
instance of the code, the software update mechanism (or a similar,
less frequently triggered mechanism) SHOULD be used to disseminate
updated units registries obtained from IANA towards the instances via
common repositories.

# Security Considerations {#seccons}

The security considerations of {{-senml}} apply.
The introduction of new measurement units poses no additional security
considerations except from a possible potential for additional
confusion about the proper unit to use.

# IANA Considerations {#iana}

See {{new-units}} and {{new-registry}}.

# Acknowledgements {#acks}
{: numbered="no"}

Ari Keranen pointed out the need for additional units in SenML.
Comments provided by him as well as by Thomas Fossati, Joaquin Prado,
and Jaime Jimenez helped improve the document.

--- back

<!--  LocalWords:  SenML's SDOs subregistry RFCthis unscaled
 -->
<!--  LocalWords:  namespace counterintuitive Implementers
 -->
