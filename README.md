<h1 align="center">Streamlines Linear Registration (slr)</h1>

<p align="center">
  Registers a moving .trk tractogram to a static one with DIPY Streamline-based Linear Registration (dipy_slr) and outputs the moved tractogram.
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/brainlife.app.332"><img src="https://img.shields.io/badge/Brainlife-brainlife.app.332-blue.svg" alt="Run on brainlife.io"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-see_LICENSE-lightgrey.svg" alt="License"></a>
</p>

## At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Registers a moving .trk tractogram to a static one with DIPY Streamline-based Linear Registration (dipy_slr) and outputs the moved tractogram.**

Wraps the DIPY 1.1.1 dipy_slr workflow: filters streamlines by length, clusters them with QuickBundles, removes small clusters and finds the affine, rigid or similarity transform that aligns the moving bundle set to the static one. Use it to align tractograms across subjects or to an atlas tractogram. Both inputs must be TrackVis .trk files.

| | |
|---|---|
| **Inputs** | `neuro/track/trk` ×2 |
| **Outputs** | `neuro/track/trk` |
| **Container** | `brainlife/dipy:1.1.1` |
| **Resources** | 8 CPUs · 16 GB memory · 10 h walltime |
| **Run it** | [doi.org/10.25663/brainlife.app.332](https://doi.org/10.25663/brainlife.app.332) |

#### Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `static_tracks` | `neuro/track/trk` | yes | Reference (static) tractogram in .trk format. |
| `moving_tracks` | `neuro/track/trk` | yes | Tractogram in .trk format to be moved onto the static one. |

#### Outputs

| Output | Datatype | Description |
|---|---|---|
| `output` | `neuro/track/trk` | The moving tractogram after linear registration (track.trk). |

<details>
<summary><b>Parameters</b> (6)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `x0` | enum | `affine` | Affine, rigid, or similarity transformation model (default affine) Options: `affine`, `rigid`, `similarity`. |
| `rm_small_clusters` | number | `50` | Remove clusters that have less than rm_small_clusters |
| `greater_than` | number | `50` | Keep streamlines that have length greater than this value |
| `less_than` | number | `250` | Keep streamlines have length less than this value |
| `nb_pts` | number | `20` | Number of points for discretizing each streamline |
| `progressive` | boolean | `true` | Use progressive registration (dipy_slr --progressive), fitting translation, rigid, similarity and affine stages in turn. |

</details>

<!-- brainlife-app:end -->

## Running the App

### On brainlife.io

Open the App at [doi.org/10.25663/brainlife.app.332](https://doi.org/10.25663/brainlife.app.332), choose `neuro/track/trk`, `neuro/track/trk` from your project, set the parameters and press **Execute**. The results are saved to your project as `neuro/track/trk`.

### Locally

You need [Singularity/Apptainer](https://apptainer.org/) (the App runs in `brainlife/dipy:1.1.1`), [`jq`](https://jqlang.github.io/jq/).

1. Clone this repository.
2. Create `config.json` with the paths to your inputs and the parameters:

   ```json
   {
       "static_track": "/path/to/static_tracks/static_track",
       "moving_track": "/path/to/moving_tracks/moving_track",
       "x0": "affine",
       "rm_small_clusters": 50,
       "greater_than": 50,
       "less_than": 250,
       "nb_pts": 20,
       "progressive": true
   }
   ```

3. Run `./main`.

## DIPY

- This is a Brainlife wrapper App stemming from the [`dipy_slr`](https://dipy.org/documentation/latest/reference_cmd/dipy_slr/) workflow.
- This single wrapper is exposed through an apps registered on [Brainlife.io](https://brainlife.io).
- More information about DIPY : [https://dipy.org/](https://dipy.org/).
- More information about the command line `dipy_slr`: [Command line Reference](https://dipy.org/documentation/latest/reference_cmd/dipy_slr/).

## Citing

If you use this App, please cite it, the software it builds on and brainlife.io:

- Streamlines Linear Registration (slr). brainlife.io App. [doi:10.25663/brainlife.app.332](https://doi.org/10.25663/brainlife.app.332)
- Garyfallidis E, Brett M, Amirbekian B, et al. Dipy, a library for the analysis of diffusion MRI data. Front Neuroinform 8:8 (2014). [doi:10.3389/fninf.2014.00008](https://doi.org/10.3389/fninf.2014.00008)
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## Authors

- Serge Koudoro
- Javier Ricardo Guaje Guerra

**Contributors**

- Soichi Hayashi

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
