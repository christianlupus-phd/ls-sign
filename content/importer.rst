Obligations of the importer
###########################

.. _check-hashes:

Checking of the hash values by the importer
===========================================

The importer must check the hashes of each file found in the extracted zipped file.
To do so, the importer must decode the base64-encoded string.
For each file, the importer must guess the underlying hashing algorithm based on the length of the hashes in the raw string.

Any discrepancies between hash stored in the ``individual-hashes`` and the hashes of the actual files in the FMU is considered an **integrity check failure** and must be reported to the user.
The simulation process must not be started if the integrity check of the files fails, such that the import process is aborted before any binary code from the FMU under test is executed..
The user must get at least a warning or a notification about the integrity check failure.

If there are additional files in the FMU present which are not part of the hash list, the integrity check must be considered as failed.

Similarly, files not present in the FMU but existing in the hash mapping list should be reported to the user.
The exact discrepancy between the files must be reported to the user and there should be an option to abort the execution in this case as well before executing any binary content of the FMU.

The importer must calculate the total hash based on the provided individual file hashes as described in :ref:`total-hash`.
It must check the calculated total hash against the provided total hash string.
If the total hash as claimed in the FMU's ``hash`` attribute of the ``total-hash`` XML tag does not match the calculated hash from the ``individual-hashes`` tag, the importer must issue an error message to the user and consider the integrity check as failed.

The importer may offer the option to the administrator to override integrity check failures and proceed with the import process at their own risk.
In that case, the importer must clearly inform the administrator about the potential risks and obtain explicit approval before the checks are disarmed.
In any case, the user must be informed about a potential integrity check failure before proceeding with the import process.
The user must then be able to decide if the FMU should be imported despite the integrity check failure.
*This ensures that the user is aware of the integrity check status and can make an informed decision before any binary code from the FMU is executed.*
Only if the user consents to proceed, the FMU may be imported and binary code executed.

.. note::
    *The checking of the hashes is not cryptographically secure.
    If an attacker intentionally tampers with an FMU, the hashes can be modified as well and will not report the changes.
    To protect against this, a cryptographic signature is needed (see* :ref:`signatures` *).*


Checking of the cryptographic signatures by the importer
========================================================

If one of the signatures can be verified, the FMU should be considered valid.

.. warning:: One or all for validity? SHOULD / MUST?


Tasks of the importer with x509 chains
--------------------------------------

.. warning:: How to handle shortened certificate chains?

    If the certificate chain contains more certificates (another root CA), should this be accepted or rejected?

In order to check the cryptographic signature, the importer must first load the certificate chain as provided in the ``x509-chain`` XML tag specified.
Each certificate must be checked individually for validity, this is

- Certificate has not expired (``notAfter``)
- Certificate is already active (``notBefore``)
- Certificate is signed by a trusted certificate (parent certificate in the chain or in registered root CAs)
- Certificate subject must comply with parent's name constraints
- For intermediate certificates: Certificate name constraints must not soften name constraints imposed by parent certificate
- Additional checks may be added by the importer

Once, trust in a leaf certificate has been established, the certificate's public key can be extracted.
The importer must decode the base64-encoded signature and use the private key to verify the signature of the total hash.
In order to report an FMU as signed and thus secure, the importer must also check all hashes as described in the section :ref:`Checking of the hashes <check-hashes>`.

.. note::

    This layered standard intentionally does not specify what certificates should be considered as root certificates or as trusted.
    It is up to the importer to provide the user a way to specify which FMUs to trust and which are not to be trusted.

    For example, the user might only trust these FMUs that have a certain name constraint fulfilled.
    Then, there could be a whitelist of companies that are allowed to send in certificates.
    Then, the certificates' ``O`` (organization) subject must match one of these whitelist entries to be accepted.

    The actual policy of the certificate generation however should not be part of the layered standard for FMI.
    Instead, the exact policy should be published and enforced as a parallel publication depending on the needs at hand.

.. warning:: Open points

    - Trust anchor? Bisher nur Vertrauen in *ein Zertifikat*, wer kann das erstellen? Darf er das?
    - Certification policy und name constraints?
    - Welchen Firmen/CAs traue ich?
