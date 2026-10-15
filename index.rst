.. Test Project documentation master file, created by
   sphinx-quickstart on Thu Nov  7 17:42:26 2024.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

FMI layered standard ls-sign
============================

.. Add your content using ``reStructuredText`` syntax. See the `reStructuredText <https://www.sphinx-doc.org/en/master/usage/restructuredtext/index.html>`_ documentation for details.

Based on the `FMI 2.0.2 standard <https://fmi-standard.org>`_ [FMI]_, this layered standard defines a way to sign FMUs cryptographically.
That way, the users of FMUs can create trust in the simulation models implemented and their authenticity.


Copyright © 2024 Christian Wolf.

This document is licensed under the Attribution-ShareAlike 4.0 International license.
The code is released under the 2-Clause BSD License.
The licenses text can be found in the LICENSE.txt file that accompanies this distribution.


.. toctree::
   :maxdepth: 2
   :caption: Contents:

   content/introduction.rst
   content/manifest.rst
   content/concepts.rst
   content/individual-files.rst
   content/crypto.rst
   content/importer.rst
   content/appendix.rst


.. rubric:: References

.. [Coreutils] GNU Coreutils, https://www.gnu.org/software/coreutils/

.. [FMI] FMI 2.0.2 standard, https://fmi-standard.org

.. [IEC9594] ISO/IEC 9594-8, Part 8: The Directory: Public-key and attribute certificate frameworks, Edition 9, 2020, https://www.iso.org/cms/render/live/en/sites/isoorg/contents/data/standard/08/03/80325.html

.. [PGP] PGARFINKEL, Simson. PGP: pretty good privacy. " O'Reilly Media, Inc.", 1995.

.. [RFC4648] RFC4648, The Base16, Base32, and Base64 Data Encodings, https://datatracker.ietf.org/doc/html/rfc4648

.. [RFC5754] RFC5754,  Using SHA2 Algorithms with Cryptographic Message Syntax, https://datatracker.ietf.org/doc/html/rfc5754

.. [RFC8017] RFC8017, PKCS #1: RSA Cryptography Specifications Version 2.2, https://datatracker.ietf.org/doc/html/rfc8017

.. [RFC9580] RFC9580, OpenPGP, https://datatracker.ietf.org/doc/html/rfc9580

.. [SemVer] Semantic versioning, https://semver.org/spec/v2.0.0.html
