# Contributing

Thank you for helping improve the AMEDTEC ECGpro GP Customisation Tool.

## Reporting a problem

Before opening an issue:

1. Confirm AMEDTEC ECGpro is installed in a supported default path.
2. Confirm all repository files were extracted into the same folder.
3. Search existing issues for the same problem.
4. Remove all patient, clinic, credential, and organisation-sensitive data from
   logs, screenshots, and generated configuration files.

Include the following where safe:

- Windows version
- ECGpro version
- ECGpro installation path
- selected filter option
- exact error text
- steps required to reproduce the problem

Do not upload `PCSettingsCustom.cnf` without inspecting and sanitising it first.

## Proposing a change

1. Fork the repository and create a focused branch.
2. Keep changes small and explain their purpose.
3. Preserve compatibility with standard Windows batch processing unless the
   proposed change deliberately introduces a new requirement.
4. Test all four filter options and both supported ECGpro installation paths
   where possible.
5. Confirm that cancelling, blank clinic fields, and clinic-detail updates work
   as expected.
6. Update `README.md` when behaviour or requirements change.
7. Open a pull request describing the testing performed.

## Safety and privacy

Changes must not include real patient information, clinic credentials, licence
keys, private server details, or exported production configurations.

Configuration changes that could affect ECG capture, display, filtering,
analysis, printing, or clinical workflow must be clearly identified. They
should be validated with the software/equipment supplier and an appropriately
qualified clinical representative before production use.
