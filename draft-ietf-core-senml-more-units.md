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
  compact: 'no'
  subcompact: 'no'
title: Additional Units for SenML
abbrev: Additional Units for SenML
date: 2019-09-02
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
  RS:
    title: "Standard-compliant usage of quantities, units and equations"
    author:
      org: Rohde&Schwarz
    seriesinfo:
      version: 04.00
    date: 2016-11
    target:  https://karriere.rohde-schwarz.de/fileadmin/user_upload/Standard-compliant_usage_of_quantities_units_and_equations_bro_en_5214-5061-62_v0400_96dpi.pdf



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
defines an IANA registry of defined Unit names and their meanings.

This short document registers a number of additional units in the IANA
registry for Units in SenML that appear to be
necessary for further adopting SenML in other Standards Development
Organizations (SDOs).

{::boilerplate bcp14}

# New Units

IANA is requested to assign new units in the "SenML Units"
subregistry of the SenML registry {{IANA.senml}} (as defined in {{RFC8428}}):

| Symbol | Description                                    | Type  | Reference |
|--------+------------------------------------------------+-------+-----------|
| B      | Byte (information content)                     | float | RFCthis   |
| VA     | volt-ampere (Apparent Power)                   | float | RFCthis   |
| var    | volt-ampere reactive (Reactive Power)          | float | RFCthis   |
| vars   | volt-ampere reactive seconds (Reactive Energy) | float | RFCthis   |
| J/m    | joule per meter (Energy per distance)          | float | RFCthis   |
| kg/m3  | kilograms per cubic meter (mass concentration) | float | RFCthis   |
| deg    | degrees (angle)*                               | float | RFCthis   |
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
  since that there is strong interest in using this unit
  specifically for the imaginary content of complex power, reactive
  power {{IEEE-1459}}.

The unit "degrees" is unit in wide use in practice for plane angle (as
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

The registry has four columns:

* secondary unit: a newly registered name allocated within the same
  namespace as SenML units
* SenML unit: an existing SenML unit from the SenML units registry
* scale, offset: two rational numbers, expressed in decimal
  (optionally, with a decimal exponent given) or as a
  fraction divided by a "/" character.

Quantities expressed in the secondary unit can be converted into the
SenML unit by first multiplying their value with the scale number and
then adding the offset, yielding the value in the given SenML unit.

The initial content of the secondary units registry is:

| secondary unit | SenML unit |     scale | offset | Reference |
| ms             | s          |    1/1000 |      0 | RFCthis   |
| min            | s          |        60 |      0 | RFCthis   |
| h              | s          |      3600 |      0 | RFCthis   |
| kW             | W          |      1000 |      0 | RFCthis   |
| kVA            | VA         |      1000 |      0 | RFCthis   |
| kvar           | var        |      1000 |      0 | RFCthis   |
| Ah             | C          |      3600 |      0 | RFCthis   |
| Wh             | J          |      3600 |      0 | RFCthis   |
| kWh            | J          |   3600000 |      0 | RFCthis   |
| kvar           | var        |      1000 |      0 | RFCthis   |
| varh           | vars       |      3600 |      0 | RFCthis   |
| Wh/km          | J/m        |       3.6 |      0 | RFCthis   |
| KiB            | B          |      1024 |      0 | RFCthis   |
| mV             | V          |    1/1000 |      0 | RFCthis   |
| mA             | A          |    1/1000 |      0 | RFCthis   |
| dBm            | dBW        |         1 |    -30 | RFCthis   |
| ug/m3          | kg/m3      |      1e-9 |      0 | RFCthis   |
| mm/h           | m/s        | 1/3600000 |      0 | RFCthis   |
| ppm            | /          |      1e-6 |      0 | RFCthis   |
| hPa            | Pa         |       100 |      0 | RFCthis   |
| mm             | m          |    1/1000 |      0 | RFCthis   |


Example: the value of a quantity given as 100 ms is first multiplied
by 1/1000, yielding the number 0.1, and then the offset 0 is added,
yielding the number 0.1 again, leading to a quantity of 0.1 s.
The value of a quantity given as 10 dBm is first multiplied by 1,
yielding the number 10, and then the offset -30 is added, yielding the
number -20, leading to a quantity of -20 dBW.

New entries can be added to the registration by Expert Review as
defined in {{RFC8126}}.  Experts should exercise their own good
judgment, with the same guidelines as used for SenML units (Section
12.1 of {{RFC8428}}), but without applying the rules 4 and 5.
Guidelines to the difference between units (which can go into the
registry) and quantities are widely available, see for instance {{RS}}.

SenML packs MAY, but SHOULD NOT use secondary units in place of SenML
units, where the exception of the "SHOULD NOT" lies in the context of
specific existing data models that are based on these secondary units.

\[So does this spec update RFC 8428?]

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

--- back
