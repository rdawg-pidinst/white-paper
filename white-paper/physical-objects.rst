Linking physical objects
========================

Accessing digital representations directly from the physical device is critically important, as it allows users to quickly identify devices, streamline tracking and inventory management, and efficiently contextualize data.

The most trivial method to link physical objects with their
digital representation would be to permanently label an instrument by
writing or engraving its PID onto it or its container. Because space for labels is limited on smaller devices, modern QR tags or barcodes may be more convenient as they offer the possibility to encode any identifying information in a machine-readable way. The `Sensor Management System <SMS_>`_ initiative, developed as part of the DataHub Earth, generates a unique QR code for each registered instrument PID. As part of an integrated ecosystem of key services supporting the European Ocean Observing System (EOOS), the Horizon Europe-funded `AMRIT`_ project is currently developing mobile applications to scan these QR codes applied to sensor platforms in the field. We recommend to use QR codes to embed a PID’s actionable URIs (:numref:`fig-objects-qr`). Some QR code generators now allow users to integrate images like organisation logos or embed extra information (such as serial number or name). Additionally, some QR code providers offer tracking when a label is scanned, helping to monitor device locations more effectively.

If engraving or applying QR codes is not possible, instruments can still be linked to their digital representations by including key identifying metadata in PID records. For example, a combination of the manufacturer name and serial number - often found on physical devices - can serve as a unique identifier. Other metadata such as an owner name or inventory number may also be helpful.

While PIDINST schema metadata does not provide explicit fields for
serial numbers or inventory numbers, it currently offers a generic way
to capture any kind of identifier which can be used for this purpose.
*AlternateIdentifier* can be used to record any identifier string and
*alternateIdentifierType* to specify an identifier type
(:numref:`snip-objects-serial`). PIDINST schema recommends the use of
the terms *serialNumber* and *inventoryNumber.*

.. figure:: /images/image4.png
    :name: fig-objects-qr
    :alt: QR code

    An example of a webpage QR code that includes an organisation logo
    and re-directs the scanner to the PID URL
    (http://hdl.handle.net/21.T11998/0000-001A-3905-F).

.. code-block:: XML
    :name: snip-objects-serial
    :caption: An instrument serial number expressed in XML

      <AlternateIdentifiers>
         <AlternateIdentifier alternateIdentifierType="serialNumber">7351-349l-mn24-019f</AlternateIdentifier>
      </AlternateIdentifiers>

.. _SMS: https://zenodo.org/records/15111317
.. _AMRIT: https://www.amritproject.eu/