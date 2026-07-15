# AMEDTEC ECGpro GP Customisation Tool

A small Windows batch utility for applying common general-practice settings to
AMEDTEC ECGpro installations.

The tool builds an ECGpro configuration file, optionally adds clinic details,
lets the operator choose the power and EMG muscle filter settings, and imports
the result into ECGpro.

> [!IMPORTANT]
> This is an independent community tool. It is not developed, endorsed, or
> supported by AMEDTEC Medizintechnik Aue GmbH. It does not interpret ECGs and
> does not replace the AMEDTEC instructions for use, clinical judgement, local
> governance, or advice from your equipment/software supplier.

## Features

- Detects AMEDTEC ECGpro in the standard 32-bit or 64-bit installation path.
- Waits for ECGpro to be closed before importing settings.
- Optionally sets or clears:
  - clinic name
  - clinic address
  - clinic phone number
  - clinic fax number
- Offers four power-filter and EMG muscle-filter combinations.
- Generates `PCSettingsCustom.cnf` and imports it using ECGpro's
  `-importsettings` option.
- Requires no additional runtime or third-party modules.

## Requirements

- Windows 10 or Windows 11
- AMEDTEC ECGpro already installed in one of these default locations:
  - `C:\Program Files (x86)\AMEDTEC ECGpro\s05Main.exe`
  - `C:\Program Files\AMEDTEC ECGpro\s05Main.exe`
- The ECGpro SQL Server instance must be running.
- Permission to change ECGpro settings on the workstation.

Custom ECGpro installation paths are not currently detected.

## Before you begin

1. Back up or export the current ECGpro configuration using your organisation's
   normal procedure.
2. Confirm the required settings with your clinical lead, ECG supplier, or
   support provider.
3. Test the change on a non-production workstation where possible.
4. Download and extract the complete repository. Do not run `Install.bat`
   directly from inside a ZIP file.

The configuration templates contain more than just the two filter choices.
Importing them may replace existing ECGpro settings. Review and test the result
before wider deployment.

## Installation and use

1. Open the repository's [Releases](../../releases) page, download the latest
   source ZIP, and extract it to a local folder.
2. Make sure all `.txt` files remain in the same folder as `Install.bat`.
3. Close AMEDTEC ECGpro.
4. Right-click `Install.bat` and select **Run as administrator** if required by
   your environment.
5. Choose whether to update the clinic details.
6. If entering clinic details, review the displayed values before continuing.
7. Select a filter option:

   | Option | Power filter | EMG muscle filter |
   | --- | --- | --- |
   | 1 | On | On at 40 Hz |
   | 2 | Off | On |
   | 3 | On | Off |
   | 4 | Off | Off |

8. Allow ECGpro to import the generated configuration.
9. Open ECGpro and verify the clinic details, filters, recording layout, and
   other relevant settings before conducting a clinical recording.

The script identifies option 3 as the ECGpro default and recommends option 1.
Enabling the muscle filter can alter the displayed ECG trace; the appropriate
choice must be determined under your local clinical policy.

## Clinic-detail prompts

For each clinic field:

- Enter a value to replace the current value.
- Leave the entry blank and choose **Yes** to clear the existing value.
- Leave the entry blank and choose **No** to keep the existing value.

Avoid XML-reserved characters such as `&`, `<`, and `>` in clinic details. The
current batch script does not escape those characters before creating the
configuration file.

## Files

| File | Purpose |
| --- | --- |
| `Install.bat` | Interactive settings builder and ECGpro importer |
| `1stSegment.txt` | Beginning of the ECGpro configuration template |
| `3rdSegment.txt` | Common ECGpro settings |
| `5thSegment.txt` | End of the ECGpro configuration template |
| `mainstrue_muscletrue.txt` | Power on, muscle filter on template |
| `mainsfalse_muscletrue.txt` | Power off, muscle filter on template |
| `mainstrue_musclefalse.txt` | Power on, muscle filter off template |
| `mainsfalse_musclefalse.txt` | Power off, muscle filter off template |

`2ndSegment.txt`, `4thSegment.txt`, and `PCSettingsCustom.cnf` are generated
during execution and should not be committed.

## Troubleshooting

### ECGpro is reported as not installed

The tool only checks the two default installation paths listed above. Confirm
where `s05Main.exe` is installed. A custom path requires a script change.

### The tool waits for ECGpro to close

Save any work and close all ECGpro windows. If the message remains, use Task
Manager to confirm that `s05Main.exe` is no longer running.

### Settings do not import

- Confirm the ECGpro SQL Server instance is running.
- Confirm all repository files were extracted into one folder.
- Run the tool with the permissions required by your organisation.
- Check that endpoint security has not blocked the batch file or generated
  `.cnf` file.
- Restore the previous configuration if validation fails.

### Clinic details cause an import error

Retry without `&`, `<`, or `>` in the entered values. If those characters are
required, update the generated XML with correctly escaped values before import.

## Safety and compliance

This utility may help standardise an ECGpro workstation for an Australian
general-practice environment, but using it does not establish compliance with
RACGP standards, AGPAL accreditation requirements, legislation, manufacturer
requirements, or local clinical policy.

The operator and organisation remain responsible for validating the imported
configuration, maintaining backups, change control, patient safety, privacy,
and regulatory compliance.

## Contributing

Bug reports and improvements are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md)
before opening an issue or pull request.

For sensitive security reports, follow [SECURITY.md](SECURITY.md).

## Licence

No open-source licence has currently been specified. Until a licence is added,
copyright remains with the repository owner and normal copyright restrictions
apply.

AMEDTEC and ECGpro are trademarks or registered trademarks of their respective
owner. Their use here is solely to identify compatibility.
