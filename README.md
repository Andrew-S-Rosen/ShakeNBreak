[![Build status](https://github.com/SMTG-Bham/ShakeNBreak/actions/workflows/test.yml/badge.svg)](https://github.com/SMTG-Bham/ShakeNBreak/actions)
[![Documentation Status](https://readthedocs.org/projects/shakenbreak/badge/?version=latest&style=flat)](https://shakenbreak.readthedocs.io/en/latest/)
[![JOSS](https://joss.theoj.org/papers/10.21105/joss.04817/status.svg)](https://doi.org/10.21105/joss.04817)
[![PyPI](https://img.shields.io/pypi/v/shakenbreak)](https://pypi.org/project/shakenbreak)
[![Conda](https://img.shields.io/conda/pn/conda-forge/shakenbreak?label=conda)](https://anaconda.org/conda-forge/shakenbreak)
[![Downloads](https://img.shields.io/pypi/dm/shakenbreak)](https://shakenbreak.readthedocs.io/en/latest/)
[![npj](https://img.shields.io/badge/npj%20Comput%20Mater%20-Mosquera--Lois%2C%20I.%2C%20Kavanagh%2C%20S.R.%2C%20Walsh%2C%20A.%20%26%20Scanlon%2C%20D.O.%20--%202023-9cf)](https://www.nature.com/articles/s41524-023-00973-1)

# `ShakeNBreak` (`SnB`)
<a href="https://shakenbreak.readthedocs.io/en/latest/"><img align="right" width="400" src="https://raw.githubusercontent.com/SMTG-Bham/ShakeNBreak/main/docs/toc.png"></a> `ShakeNBreak` is a defect structure-searching method employing chemically-guided bond distortions to
locate ground-state and metastable structures of point defects in solid materials. [Docs here!](https://shakenbreak.readthedocs.io/en/latest/)

Main features include:
1. Defect structure generation:
   * Automatic generation of distorted structures for input defects
   * Optionally, input file generation for geometry optimisation with several codes (`VASP`, `CP2K`, `Quantum-Espresso`, `CASTEP` & `FHI-aims`)
2. Analysis:
   * Parsing of geometry relaxation results
   * Plotting of final energies versus distortion to demonstrate what energy-lowering reconstructions have been identified
   * Coordination & bonding analysis to investigate the physico-chemical factors driving an energy-lowering distortion
   * Magnetisation analysis (currently only supported for `VASP`)

The code currently supports `VASP`, `CP2K`, `Quantum-Espresso`, `CASTEP` & `FHI-aims`. Code contributions to support additional solid-state packages are welcome.

![ShakeNBreak Summary](https://raw.githubusercontent.com/SMTG-Bham/ShakeNBreak/main/docs/SnB_Supercell_Schematic_PES_2sec_Compressed.gif)

### Literature
- Preview: Mosquera-Lois, I.; Kavanagh, S. R. [In Search of Hidden Defects](https://doi.org/10.1016/j.matt.2021.06.003), _Matter_ 4 (8), 2602-2605, **2021**
- Code: Mosquera-Lois, I. & Kavanagh, S. R.; Walsh, A.; Scanlon, D. O. [ShakeNBreak: Navigating the defect configurational landscape](https://doi.org/10.21105/joss.04817), _Journal of Open Source Software_ 7 (80), 4817, **2022**
- Theory/Method: Mosquera-Lois, I. & Kavanagh, S. R.; Walsh, A.; Scanlon, D. O. [Identifying the Ground State Structures of Defects in Solids](https://doi.org/10.1038/s41524-023-00973-1), _npj Comput Mater_ 9, 25 **2023**
- News & Views: Mannodi-Kanakkithodi, A. [The Devil is in the Defects](https://doi.org/10.1038/s41567-023-02049-9), _Nature Physics_ **2023** ([Free-to-read link](https://t.co/EetpnRgjzh))

## Installation
`ShakeNBreak` can be installed using `pip`:
```bash
  pip install shakenbreak
```

Alternatively if needed, it can also be installed from `conda` with:
```bash
  conda install -c conda-forge shakenbreak
```

If using `VASP`, in order for `ShakeNBreak` to automatically generate the pseudopotential input files (`POTCAR`s), your local `VASP` pseudopotential directory must be set in the `pymatgen` configuration file `$HOME/.pmgrc.yaml` as follows:
```bash
  PMG_VASP_PSP_DIR: <Path to VASP pseudopotential top directory>
```
   Within your `VASP` pseudopotential top directory, you should have a folder named `POT_GGA_PAW_PBE`
   which contains the `POTCAR.X(.gz)` files (in this case for PBE `POTCAR`s). Please refer to the [`doped` Installation docs](https://doped.readthedocs.io/en/latest/Installation.html) if you have
   difficulty with this.

The font Montserrat ([Open Font License](https://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=OFL)) will be installed with the package, and will be used by default for plotting.

### Developer installation
For development work, ShakeNBreak can also be installed from a copy of the source directory:

1. Download `ShakeNBreak` source code using the command:
```bash
  git clone https://github.com/SMTG-Bham/ShakeNBreak
```
2. Navigate to root directory:
```bash
  cd ShakeNBreak
```
3. Install the code, using the command:
```bash
  pip install -e .
```
   This command tries to obtain the required packages and their dependencies and install them automatically.


## Usage

### Python API
`ShakeNBreak` can be used through a Python API, as exemplified in the [SnB Python API tutorial](https://shakenbreak.readthedocs.io/en/latest/ShakeNBreak_Example_Workflow.html), with more info available on the [docs](https://readthedocs.org/projects/shakenbreak).

### Command line interface
Alternatively, the code can be used via the command line:
![ShakeNBreak CLI](https://raw.githubusercontent.com/SMTG-Bham/ShakeNBreak/main/docs/SnB_CLI.gif)

The functions provided include:
* [`snb-generate`](https://shakenbreak.readthedocs.io/en/latest/shakenbreak.cli.html#snb-generate): Generate distorted structures for a given defect
* [`snb-generate_all`](https://shakenbreak.readthedocs.io/en/latest/shakenbreak.cli.html#snb-generate-all): Generate distorted structures for all defects present in the specified/current directory
* [`snb-run`](https://shakenbreak.readthedocs.io/en/latest/shakenbreak.cli.html#snb-run): Submit geometry relaxations to the HPC scheduler
* [`snb-parse`](https://shakenbreak.readthedocs.io/en/latest/shakenbreak.cli.html#snb-parse): Parse the results of the geometry relaxations and write them to a `yaml` file
* [`snb-analyse`](https://shakenbreak.readthedocs.io/en/latest/shakenbreak.cli.html#snb-analyse): Generate `csv` files with energies and structural differences between the final configurations
* [`snb-plot`](https://shakenbreak.readthedocs.io/en/latest/shakenbreak.cli.html#snb-plot): Generate plots of energy vs distortion, with the option to include a colorbar to quantify structural differences
* [`snb-regenerate`](https://shakenbreak.readthedocs.io/en/latest/shakenbreak.cli.html#snb-regenerate): Identify defect species undergoing energy-lowering distortions and test these distortions for the other charge states of the defect
* [`snb-groundstate`](https://shakenbreak.readthedocs.io/en/latest/shakenbreak.cli.html#snb-groundstate): Save the ground state structures to a ``Groundstate`` directory for continuation runs

More information about each function and its inputs/outputs are available from the [CLI section of the docs](https://shakenbreak.readthedocs.io/en/latest/shakenbreak.cli.html#commands) or using `-h` help option (e.g. `snb -h`).

We recommend at least looking through the [tutorials](https://shakenbreak.readthedocs.io/en/latest/Tutorials.html) when first starting to use `ShakeNBreak`, to familiarise yourself with the full functionality and workflow.

## Code Compatibility
`ShakeNBreak` is built to natively function using `pymatgen` `Defect` objects ([docs available here](https://materialsproject.github.io/pymatgen-analysis-defects/)) and be compatible with the most recent version of `pymatgen`.
If you are receiving `pymatgen`-related errors when using `ShakeNBreak`, you may need to update `pymatgen` and/or `ShakeNBreak`, which can be done with:
```bash
pip install --upgrade pymatgen shakenbreak
```

`ShakeNBreak` can take `pymatgen` `Defect` objects as input (to then generate the trial distorted structures),
**_but also_** can take in `pymatgen` `Structure` objects, `doped` defects or structure files
(e.g. `POSCAR`s for `VASP`) as inputs. As such, it should be compatible with any defect code
(such as [`doped`](https://doped.readthedocs.io/en/latest/index.html), [`pydefect`](https://github.com/kumagai-group/pydefect),
[`PyCDT`](https://github.com/mbkumar/pycdt), [`PyLada`](https://github.com/pylada/pylada-defects),
[`DASP`](http://hzwtech.com/files/software/DASP/htmlEnglish/index.html), [`Spinney`](https://gitlab.com/Marrigoni/spinney/-/tree/master),
[`DefAP`](https://github.com/DefAP/defap), [`PyDEF`](https://github.com/PyDEF2/PyDEF-2.0)...) that generates these files.
Please let us know if you have any issues with compatibility, or if you would like to see any additional features added to `ShakeNBreak` to make it more compatible with your code.

## Contributing

### Bugs reports, feature requests and questions
Please use the [Issue Tracker](https://github.com/SMTG-Bham/ShakeNBreak/issues) to report bugs or request new features.

Contributions to extend this package are very welcome! Please use the
["Fork and Pull"](https://docs.github.com/en/get-started/quickstart/contributing-to-projects)
workflow to do so and follow the [PEP8](https://peps.python.org/pep-0008/) style guidelines.

See the [Contributing Documentation](https://shakenbreak.readthedocs.io/en/latest/Contributing.html) for detailed instructions.

### Tests
Unit tests are in the `tests` directory and can be run from the top directory using [unittest](https://docs.python.org/3/library/unittest.html).
Automatic testing is run on the master and develop branches using Github Actions. Please run tests and add new tests for any new features whenever submitting pull requests.

## Acknowledgements
`ShakeNBreak` has benefitted from feedback from many members of the Walsh and Scanlon research groups who have used / are using it in their work, including Adair Nicolson, Xinwei Wang, Katarina Brlec, Joe Willis, Zhenzhu Li, Jiayi Cen, Lavan Ganeshkumar, Daniel Sykes, Luisa Herring-Rodriguez, Alex Squires, Sabrine Hachmioune and Chris Savory.

## Studies using `ShakeNBreak`

- B. E. Murdock et al. **_Li-Site Defects Induce Formation of Li-Rich Impurity Phases: Implications for Charge Distribution and Performance of LiNi<sub>0.5-x</sub>M<sub>x</sub>Mn<sub>1.5</sub>O<sub>4</sub> Cathodes (M = Fe and Mg; x = 0.05–0.2)_** [_Advanced Materials_](https://doi.org/10.1002/adma.202400343) 2024
- A. G. Squires et al. **_Oxygen dimerization as a defect-driven process in bulk LiNiO2<sub>2</sub>_** [_ChemRxiv_](https://doi.org/10.26434/chemrxiv-2024-lcmkj) 2024
- X. Wang et al. **_Upper efficiency limit of Sb<sub>2</sub>Se<sub>3</sub> solar cells_** [_Joule_](https://doi.org/10.1016/j.joule.2024.05.004) 2024
- I. Mosquera-Lois et al. **_Machine-learning structural reconstructions for accelerated point defect calculations_** [_arXiv_](https://doi.org/10.48550/arXiv.2401.12127) 2024
- S. R. Kavanagh et al. **_doped: Python toolkit for robust and repeatable charged defect supercell calculations_** [_Journal of Open Source Software_](https://doi.org/10.21105/joss.06433) 2024
- K. Li et al. **_Computational Prediction of an Antimony-based n-type Transparent Conducting Oxide: F-doped Sb<sub>2</sub>O<sub>5</sub>_** [_Chemistry of Materials_](https://doi.org/10.1021/acs.chemmater.3c03257) 2024
- X. Wang et al. **_Four-electron negative-U vacancy defects in antimony selenide_** [_Physical Review B_](https://journals.aps.org/prb/abstract/10.1103/PhysRevB.108.134102) 2023
- Y. Kumagai et al. **_Alkali Mono-Pnictides: A New Class of Photovoltaic Materials by Element Mutation_** [_PRX Energy_](http://dx.doi.org/10.1103/PRXEnergy.2.043002) 2023
- A. T. J. Nicolson et al. **_Cu<sub>2</sub>SiSe<sub>3</sub> as a promising solar absorber: harnessing cation dissimilarity to avoid killer antisites_** [_Journal of Materials Chemistry A_](https://doi.org/10.1039/D3TA02429F) 2023
- J. Willis, K. B. Spooner, D. O. Scanlon **_On the possibility of p-type doping in barium stannate_** [_Applied Physics Letters_](https://doi.org/10.1063/5.0170552) 2023
- J. Cen et al. **_Cation disorder dominates the defect chemistry of high-voltage LiMn<sub>1.5</sub>Ni<sub>0.5</sub>O<sub>4</sub> (LMNO) spinel cathodes_** [_Journal of Materials Chemistry A_](https://doi.org/10.1039/D3TA00532A) 2023
- J. Willis & R. Claes et al. **_Limits to Hole Mobility and Doping in Copper Iodide_** [_Chemistry of Materials_](https://doi.org/10.1021/acs.chemmater.3c01628) 2023
- I. Mosquera-Lois & S. R. Kavanagh, A. Walsh, D. O. Scanlon **_Identifying the ground state structures of point defects in solids_** [_npj Computational Materials_](https://www.nature.com/articles/s41524-023-00973-1) 2023
- B. Peng et al. **_Advancing understanding of structural, electronic, and magnetic properties in 3d-transition-metal TM-doped α-Ga₂O₃ (TM = V, Cr, Mn, and Fe)_** [_Journal of Applied Physics_](https://doi.org/10.1063/5.0173544) 2023
- Y. T. Huang & S. R. Kavanagh et al. **_Strong absorption and ultrafast localisation in NaBiS<sub>2</sub> nanocrystals with slow charge-carrier recombination_** [_Nature Communications_](https://www.nature.com/articles/s41467-022-32669-3) 2022
- S. R. Kavanagh, D. O. Scanlon, A. Walsh, C. Freysoldt **_Impact of metastable defect structures on carrier recombination in solar cells_** [_Faraday Discussions_](https://doi.org/10.1039/D2FD00043A) 2022
- Y-S. Choi et al. **_Intrinsic Defects and Their Role in the Phase Transition of Na-Ion Anode Na<sub>2</sub>Ti<sub>3</sub>O<sub>7</sub>_** [_ACS Applied Energy Materials_](https://doi.org/10.1021/acsaem.2c03466) 2022 (Early version)
- S. R. Kavanagh, D. O. Scanlon, A. Walsh **_Rapid Recombination by Cadmium Vacancies in CdTe_** [_ACS Energy Letters_](https://pubs.acs.org/doi/full/10.1021/acsenergylett.1c00380) 2021
- C. J. Krajewska et al. **_Enhanced visible light absorption in layered Cs<sub>3</sub>Bi<sub>2</sub>Br<sub>9</sub> through mixed-valence Sn(II)/Sn(IV) doping_** [_Chemical Science_](https://doi.org/10.1039/D1SC03775G) 2021 (Early version)
- (News & Views): A. Mannodi-Kanakkithodi **_The devil is in the defects_** [_Nature Physics_](https://doi.org/10.1038/s41567-023-02049-9) 2023 ([Free-to-read link](https://t.co/EetpnRgjzh))

<!-- Wenzhen paper -->
<!-- Se -->
<!-- Oba book -->
<!-- BiOI -->
<!-- Kumagai collab paper -->
<!-- Lavan LiNiO2 -->
<!-- Sykes Magnetic oxide polarons -->
<!-- Kat YTOS -->
<!-- Squires (and mention benchmark test against AIRSS? See Slack message) -->

## License and Citation
ShakeNBreak is made available under the MIT License.

If you use it in your research, please cite:
- Code: Mosquera-Lois, I. & Kavanagh, S. R.; Walsh, A.; Scanlon, D. O. [ShakeNBreak: Navigating the defect configurational landscape](https://doi.org/10.21105/joss.04817). _Journal of Open Source Software_ 7 (80), 4817, **2022**
- Theory/Method: Mosquera-Lois, I. & Kavanagh, S. R.; Walsh, A.; Scanlon, D. O. [Identifying the Ground State Structures of Defects in Solids](https://doi.org/10.1038/s41524-023-00973-1) _npj Comput Mater_ 9, 25 **2023**

You may also find this Preview paper useful, which discusses the general problem of defect structure prediction:
- Mosquera-Lois, I.; Kavanagh, S. R. [In Search of Hidden Defects](https://doi.org/10.1016/j.matt.2021.06.003). _Matter_ 4 (8), 2602-2605, **2021**

`BibTeX` entries for these papers are provided in the [`CITATIONS.md`](CITATIONS.md) file.

## Requirements
`ShakeNBreak` is compatible with Python 3.9 - 3.12 and requires the following open-source python packages:
* [Pymatgen](https://pymatgen.org/)
* [Ase](https://wiki.fysik.dtu.dk/ase/)
* [Hiphive](https://hiphive.materialsmodeling.org/)
* [Numpy](https://numpy.org/)
* [Matplotlib](https://matplotlib.org/)
* [Pandas](https://pandas.pydata.org/)
* [Seaborn](https://seaborn.pydata.org/)
* [Monty](https://pythonhosted.org/monty/index.html)
* [Click](https://click.palletsprojects.com/en/8.1.x/)
