# Concatenate Raw MEG/EEG Files

[![Run on Brainlife.io](https://img.shields.io/badge/Brainlife-bl.app.756-blue.svg)](https://doi.org/10.25663/brainlife.app.756)

## Description

Concatenates multiple MNE raw data files (`.fif` format) into a single unified raw data file using `mne.concatenate_raws()`. This app is useful for combining data from multiple recording sessions, runs, or files into a single dataset for unified downstream processing. Before concatenation, channel order and the order of channels marked as bad are normalized across the input files so that `mne.concatenate_raws()` does not reject files that differ only in ordering.

The app generates:
- A single concatenated raw `.fif` file
- An HTML report with a summary of the input files and the concatenated data
- A `product.json` summary of the concatenated data

## Inputs

- **`raw`** (`neuro/meeg/mne/raw`, multiple): list of continuous MNE raw data files to concatenate. Files must share the same set of channels and the same set of bad channels (order may differ and is normalized automatically).

## Outputs

- **`out_dir/raw.fif`**: concatenated raw data file in MNE format
- **`out_report/report.html`**: QC report containing a summary of the input files and channel details of the concatenated data
- **`product.json`**: metadata summary of the concatenated data

## Configuration Parameters

This app reads no configuration parameters beyond its input file list (see Inputs above).

## Usage

### Running on Brainlife.io

1. Go to the [Brainlife.io](https://brainlife.io) platform and start a new process.
2. Select this app ("Concatenate Raw MEG/EEG Files") and choose two or more `neuro/meeg/mne/raw` datasets as the `raw` input.
3. Submit the process; the concatenated raw file and QC report will appear in your project outputs.

### Local Testing

```bash
git clone <this-repo>
cd concat
./main
```

`config.json` must contain a `raw` key with a list of paths to the input `.fif` files, e.g.:

```json
{
    "raw": [
        "in_dir/raw1.fif",
        "in_dir/raw2.fif"
    ]
}
```

## Technical Details

- **Execution**: Python with MNE-Python and the shared `brainlife_utils` library
- **Data format**: MNE `.fif` format (compatible with all downstream Brainlife.io apps)
- **Concatenation**: uses `mne.concatenate_raws()` after normalizing channel order and bad-channel order across inputs
- **Preloading**: all files are preloaded into memory before concatenation
- **Report generation**: automatic HTML report with per-file summary table and channel information

## Authors

- [Kamilya Salibayeva](https://github.com/KSalibay) (Indiana University)
- [Maximilien Chaumon](https://github.com/dnacombo), Paris Brain Institute

## Citations

We kindly ask that you cite the following articles when publishing papers and code using this app:

- Hayashi, S., Caron, B.A., Heinsfeld, A.S. et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. Nat Methods 21, 809–813 (2024). https://doi.org/10.1038/s41592-024-02237-2
- Gramfort, A. et al. MEG and EEG data analysis with MNE-Python. Front. Neurosci. 7, 267 (2013). https://doi.org/10.3389/fnins.2013.00267

## Funding Acknowledgement

brainlife.io is publicly funded and for the sustainability of the project we kindly ask that you acknowledge the following funding sources:

[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-1636893](https://img.shields.io/badge/NSF_BCS-1636893-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-ACI-1916518](https://img.shields.io/badge/NSF_ACI-1916518-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1916518)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://grantome.com/grant/NIH/R01-EB029272-01)
[![NIH-NIBIB-R01EB030896](https://img.shields.io/badge/NIH_NIBIB-R01EB030896-green.svg)](https://grantome.com/grant/NIH/R01-EB030896-01)

## License

Copyright (c) 2026 MEEG Brainlife team. Licensed under AGPL-3.0, see [license.txt](license.txt).
