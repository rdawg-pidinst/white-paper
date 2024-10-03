Collecting the metadata
~~~~~~~~~~~~~~~~~~~~~~~

To create a DOI for an instrument, you need to collect all the
metadata that describe the instrument and that you want to include in
the DOI record.  Section :ref:`pidinst-metadata-schema` in the PIDINST
White Paper describes the metadata that you should consider.

The Persistent Identification of Instruments WG has developed a
PIDINST Metadata Schema.  But since you are going to create a DataCite
DOI, you will be constrained to use the `DataCite Metadata Schema`_.
With version 4.5 of that schema, DataCite has significantly improved
support for instruments and also provides a `Mapping of the
PIDINST Schema onto the DataCite Schema <DataCite PIDINST Mapping_>`_

Mapping of PIDINST metadata onto DataCite
-----------------------------------------

Based on the mapping provided by DataCite, we want to give in the
following additional hints and discuss how the metadata describing the
instrument can be best represented in the DataCite Schema:

`Identifier`
  The DOI that you are going to create.  Add as DataCite property
  `Identifier` with `identifierType=DOI`.

`LandingPage`
  The URL of the landing page that the PID resolves to.  The DataCite
  Schema does not have a property for this, but you'll register the
  URL along with the metadata when creating the DOI.

`Name`
  The name by which this instrument is known.  Add as DataCite property
  `Title`. The DataCite schema allows for multiple kinds of titles that are 
  distinguished by the `titleType` subproperty. A title without a specified
  type is assumed to be the main title. Many instruments are commonly refered 
  to with acronyms. Use "title (acronym)" to include the acronym in the main title.
  
`Owner`
  The organization or individual that manages the instrument.  Add as
  DataCite property `Contributor` with `contributorType=HostingInstitution`.  
  An identifier can be used to unambiguously identify the owner,
  typically a `ROR <https://ror.org>`, in the `nameIdentifier`
  subproperty of `Contributor <https://datacite-metadata-schema.readthedocs.io/en/4.5/properties/contributor/>`_.

`Manufacturer`
  The organization or individual that built the instrument.  Add as
  DataCite property `Creator`.  Consider also to add an identifier for
  the manufacturer in the `nameIdentifier` subproperty of `Creator <https://datacite-metadata-schema.readthedocs.io/en/4.5/properties/creator/>`_.

`Model`
  The name of the model or type of the instrument.  As of this
  writing, the DataCite Schema has no specific property for that.  The
  mapping provided by DataCite suggest to add it as a `Description`
  with `descriptionType=TechnicalInfo`, see note below.

  The DataCite property `Description` does not provide a way to
  include the `modelIdentifier`.  If the model has a PID and you want
  to include that, one option would be to additionally add a
  `RelatedIdentifier` with `relationType=References`.

`Description`
  A textual description of the device and its capabilities.  Add as
  DataCite property `Description` with `descriptionType=Abstract`. A description with
  `descriptionType=TechnicalInfo` can also be used to provide additional technical details 
  (see Model, InstrumentType, and MeasuredVariable).

`InstrumentType`
  A classification of the type of the instrument.  As of this writing,
  the DataCite Schema has no specific property for that.  The mapping
  provided by DataCite suggest to add it as a `Description` with
  `descriptionType=TechnicalInfo`, see note below.  An alternative
  might be to add it as keywords providing such a classification in
  the `Subject` property.  The latter might be particularly useful if
  the instrument type is using terms from a controlled vocabulary, as
  `Subject` allows to link those terms using the `subjectScheme`,
  `schemeURI`, and `valueURI` subproperties.

`MeasuredVariable`
  The variables or physical properties that the instrument measures or
  observes.  As of this writing, the DataCite Schema has no specific
  property for that.  The mapping provided by DataCite suggest to add
  it as a `Description` with `descriptionType=TechnicalInfo`, see note
  below.

`Date`
  Relevant events pertaining to this instrument instance.  Add as
  DataCite property `Date`.  Use `dateType=Available` to indicate the
  date that the instrument is or was in operation.  Use a single date
  if the instrument is still in operation, to indicate a start date.
  Use a date interval to indicate a start and an end date, if the
  instrument has already been decommissioned.

`RelatedIdentifier`
  This can be used to establish links to related resources with identifiers.  The
  DataCite Schema has a property with the same name, having very
  similar subproperties and semantics as the PIDINST Schema.

  The type of the relation is described using the relationType property. The DataCite schema has 
  a list of valid `relation types <https://datacite-metadata-schema.readthedocs.io/en/4.5/appendices/appendix-1/relationType/>`_.
  
  Several relation types can be used to connect to more detailed instrument metadata:
  * `IsDescribedBy <https://datacite-metadata-schema.readthedocs.io/en/4.5/appendices/appendix-1/relationType/#isdescribedby>_`
  can be used to link to a more detailed description of the instrument. 
  * `HasMetadata <https://datacite-metadata-schema.readthedocs.io/en/4.5/appendices/appendix-1/relationType/#hasmetadata>` can be used to
  link to metadata records that describe the instrument in more detail. 
  * `HasVersion <https://datacite-metadata-schema.readthedocs.io/en/4.5/appendices/appendix-1/relationType/#hasversion>`_,
  `IsVersionOf <https://datacite-metadata-schema.readthedocs.io/en/4.5/appendices/appendix-1/relationType/#isversionof>`_,  
  `IsNewVersionOf <https://datacite-metadata-schema.readthedocs.io/en/4.5/appendices/appendix-1/relationType/#isnewversionof>`_, 
  and `IsPreviousVersionOf <https://datacite-metadata-schema.readthedocs.io/en/4.5/appendices/appendix-1/relationType/#ispreviousversionof>`_ can be used to link to
  other versions of the instrument.
  * `HasPart <https://datacite-metadata-schema.readthedocs.io/en/4.5/appendices/appendix-1/relationType/#haspart>`_ and `IsPartOf <https://datacite-metadata-schema.readthedocs.io/en/4.5/appendices/appendix-1/relationType/#ispartof>`_ can be used to define parts of instruments or instruments with parts.

  Version 4.5 of the DataCite schema added the relation type `Collects<https://datacite-metadata-schema.readthedocs.io/en/4.5/appendices/appendix-1/relationType/#collects>`_
  for describing the relation between an instrument and a dataset, i.e. instrument A collects dataset B. The complimentary relationship
  (dataset B is collected by instrument A) can be described using the relation type `IsCollectedBy<https://datacite-metadata-schema.readthedocs.io/en/4.5/appendices/appendix-1/relationType/#iscollectedby>`_.


`AlternateIdentifier`
  To be used if this instrument is also registered elsewhere.  Add as
  DataCite property `AlternateIdentifier`.  Use
  `alternateIdentifierType=SerialNumber` for a serial number
  attributed by the manufacturer.  Use
  `alternateIdentifierType=InventoryNumber` for an inventory number
  used by the owner.

  Note that as opposed to the PIDINST schema,
  `alternateIdentifierType` is free text in the DataCite schema.
  Thus, when adding an alternate identifier that is not a serial
  number or an inventory number, you are not forced to use
  `alternateIdentifierType=Other`, but may set the appropriate type in
  `alternateIdentifierType` right away.

Note on Description in the DataCite Schema
------------------------------------------

The mapping of PIDINST metadata onto DataCite suggest that `Model`,
`InstrumentType`, and `MeasuredVariable` should be added as a
`Description` with `descriptionType=TechnicalInfo`.  The value of
`Description` is free text.  There is no structured way to include
subproperties such as `modelIdentifier` here.

Note that `Description` is multivalued, so you may add as many
instances as needed, even using the same `descriptionType`.  We
suggest to use separate `Description` instances for `Model`,
`InstrumentType` and `MeasuredVariable` respectively.

Additional properties in the DataCite Schema
--------------------------------------------

There are a few more properties in the DataCite Schema that have no
counterpart in the PIDINST Schema and that either need to be set
because they are mandatory in DataCite or that are worth considering.
Of course, any other DataCite property not mentioned here may be
considered as well, if it makes sense for a particular use case.

`Publisher`
  “The name of the entity that holds, archives, publishes, prints,
  distributes, releases, issues, or produces the resource” (quote from
  the definition in the DataCite Schema).  It's not quite clear what
  that would mean in the case of an instrument and it seem to be a
  little redundant with what would be the `Owner` in the PIDINST
  Schema.  But it is mandatory in the DataCite Schema, so it needs to
  be set.  We recommend to set it to the entity that created the DOI
  and is responsible for maintaining the DOI metadata.

  In Version 4.5 of the schema several sub-properties were added to `publisher<https://datacite-metadata-schema.readthedocs.io/en/4.5/properties/publisher/#id1>`_:
  *  publisherIdentifier: An identifier for the publisher. Use a ROR ID if available.
  *  publisherIdentifierScheme: The scheme for the publisher identifier (e.g. ROR).
  *  schemeURI: The URI of the identifier scheme (e.g. https://ror.org).

`PublicationYear`
  Mandatory in the DataCite Schema.  We suggest to set it to the year
  of issuing the DOI.

`ResourceTypeGeneral`and `ResourceType` 
  DataCite DOIs are for many different types of objects, so there is a
  need to indicate the type.  ResourceTypeGeneral is a mandatory element in the DataCite
  Schema selected from a `shared vocabulary <https://datacite-metadata-schema.readthedocs.io/en/4.5/appendices/appendix-1/resourceTypeGeneral/>`_.
  Set `resourceTypeGeneral=Instrument` for DataCite instrument metadata records.

  ResourceType is a free text field that can be used to provide a more specific resource type.

`FundingReference`
  This optional element can be used to acknowledge external funding that supported the purchase or the
  creation of the instrument. See `funder metadata <https://datacite-metadata-schema.readthedocs.io/en/4.5/properties/fundingreference/>`_ for details.

.. _DataCite Metadata Schema: https://datacite-metadata-schema.readthedocs.io/en/4.5/introduction/

.. _DataCite PIDINST Mapping:
   https://datacite-metadata-schema.readthedocs.io/en/latest/mappings/pidinst/
