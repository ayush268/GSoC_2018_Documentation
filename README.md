# Documentation for work done (taskwise)

## First Task ->  CUPS general options

The CUPS backend tells the print dialog only about printer-specific user-settable options, not about general options implemented in CUPS or cups-filters and so being available for all print queues. These are options like N-up, reverse order, selected pages, As they are only common for CUPS and not necessarily available with other print technologies like Google Cloud Print, they should get reported to the print dialog by the CUPS backend.

### Steps 

- Went through the CUPS API documentation and programming manual but the only way to get cups printer options was to retrieve it using the function __cupsFindDestSupported__ with option_name __job-creation-attributes__.
- The info mentioned in above point can be found [here](https://www.cups.org/doc/cupspm.html#detailed-destination-information).

- Earlier the above function used to return the following options:

```
job-priority, ipp-attribute-fidelity, confidential, page-ranges, job-hold-until, print-quality, media, multiple-document-handling, finishings, copies, job-name, output-bin, print-color-mode, orientation-requested, printer-resolution, sides, media-col, number-up
```

-  I was having doubt that if there exists Isome other API function I can use to get few remaining attributes, so I opened up issue on the main CUPS repository, link to which is the following topic:

      [Question: Regarding cups API functions for cups standard/common options.](https://github.com/apple/cups/issues/5340)

- After discussion on this issue, the things were more clearer and I discussed the same with Till (my mentor).

- The final conclusion was that some of the options are to be PPD specific but the options which are not and were not being retrieved are added to the CUPS repo and thus they will be retrieved now by making the same call as mentioned in first point.

- Thus, there was no change required to be made to the dialog, all the options will be retrieved from cups via CUPS API using the existing function.

## Minor Changes

- Added "libtool" as dependency to cpdb-libs in README.

## Repositories

- [CUPS Backend](https://github.com/ayush268/cpdb-backend-cups)
- [GCP Backend](https://github.com/ayush268/cpdb-backend-gcp)
- [CPDB Library](https://github.com/ayush268/cpdb-libs)
