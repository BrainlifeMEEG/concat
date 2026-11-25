<h1 align="center">Concatenate raws</h1>

<p align="center">
  Concatenate multiple MNE.Raw instances into single .Raw
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/brainlife.app.756"><img src="https://img.shields.io/badge/Brainlife-brainlife.app.756-blue.svg" alt="Run on brainlife.io"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-see_LICENSE-lightgrey.svg" alt="License"></a>
</p>

## At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Concatenate multiple MNE.Raw instances into single .Raw**

Joins several MNE raw files end to end with mne.concatenate_raws(), for example multiple runs or sessions, and writes one raw.fif with a QC report. Inputs must share the same channels and bad channels (order is normalised automatically). It reads no configuration parameters.

| | |
|---|---|
| **Inputs** | `neuro/meeg/mne/raw` |
| **Outputs** | `neuro/meeg/mne/raw` · `report/html` |
| **Container** | `brainlifemeeg/mne:1.12.1` |
| **Resources** | 32 GB memory · 0.42 h walltime |
| **Run it** | [doi.org/10.25663/brainlife.app.756](https://doi.org/10.25663/brainlife.app.756) |

#### Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `raw` | `neuro/meeg/mne/raw` | yes | Continuous MNE raw files to concatenate. All files must share the same set of channels and the same bad channels. |

#### Outputs

| Output | Datatype | Description |
|---|---|---|
| `out_dir` | `neuro/meeg/mne/raw` | Concatenated raw data (raw.fif). |
| `out_report` | `report/html` | HTML report of concatenate process |

<!-- brainlife-app:end -->

## Running the App

### On brainlife.io

Open the App at [doi.org/10.25663/brainlife.app.756](https://doi.org/10.25663/brainlife.app.756), choose `neuro/meeg/mne/raw` from your project and press **Execute**. The results are saved to your project as `neuro/meeg/mne/raw`, `report/html`.

### Locally

You need [Singularity/Apptainer](https://apptainer.org/) (the App runs in `brainlifemeeg/mne:1.12.1`), [`jq`](https://jqlang.github.io/jq/).

1. Clone this repository.
2. Create `config.json` with the paths to your inputs and the parameters:

   ```json
   {
       "raw": "/path/to/raw/raw"
   }
   ```

3. Run `./main`.

## Configuration Parameters

This app reads no configuration parameters beyond its input file list (see Inputs above).

## Local Testing

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

## Citing

If you use this App, please cite it, the software it builds on and brainlife.io:

- Concatenate raws. brainlife.io App. [doi:10.25663/brainlife.app.756](https://doi.org/10.25663/brainlife.app.756)
- Gramfort, A. et al. MEG and EEG data analysis with MNE-Python. Front. Neurosci. 7, 267 (2013). https://doi.org/10.3389/fnins.2013.00267
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## Authors

- [Kamilya Salibayeva](https://github.com/KSalibay) (Indiana University)
- [Maximilien Chaumon](https://github.com/dnacombo), Paris Brain Institute

## Funding

[![Wellcome-226486/Z/22/Z](https://img.shields.io/badge/Wellcome-226486%2FZ%2F22%2FZ-purple.svg)](https://wellcome.org/)
[![NIH-NINDS-U24NS140384](https://img.shields.io/badge/NIH_NINDS-U24NS140384-green.svg)](https://reporter.nih.gov/project-details/11261037)
[![NIH-NINDS-UM1NS132207](https://img.shields.io/badge/NIH_NINDS-UM1NS132207-green.svg)](https://reporter.nih.gov/project-details/11411328)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://reporter.nih.gov/project-details/10262925)
[![NIH-NIBIB-R01EB030896](https://img.shields.io/badge/NIH_NIBIB-R01EB030896-green.svg)](https://reporter.nih.gov/project-details/10428625)
[![NIH-NIMH-R01MH126699](https://img.shields.io/badge/NIH_NIMH-R01MH126699-green.svg)](https://reporter.nih.gov/project-details/10460628)
[![NIH-NIDCD-R01DC020088](https://img.shields.io/badge/NIH_NIDCD-R01DC020088-green.svg)](https://reporter.nih.gov/project-details/11140284)
[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-2203524](https://img.shields.io/badge/NSF_BCS-2203524-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2203524)
[![NSF-IIS-1636893](https://img.shields.io/badge/NSF_IIS-1636893-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-OAC-2148729](https://img.shields.io/badge/NSF_OAC-2148729-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148729)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NSF-IIS-2148700](https://img.shields.io/badge/NSF_IIS-2148700-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148700)
[![NSF-OAC-1916518](https://img.shields.io/badge/NSF_OAC-1916518-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1916518)

<sub>brainlife.io, which runs this App, is publicly funded by Wellcome, the U.S. National Institutes of Health and the U.S. National Science Foundation; acknowledging that support helps keep it running.</sub>

## License

See [LICENSE](LICENSE).
