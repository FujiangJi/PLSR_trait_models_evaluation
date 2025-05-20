<div align="center">

<h1>Unveiling the transferability of PLSR models for leaf trait estimation: lessons from a comprehensive analysis with a novel global dataset</h1>


[Fujiang Ji](https://fujiangji.github.io/) <sup>1, *</sup>, [Fa Li](https://scholar.google.com/citations?user=lOAXHLwAAAAJ&hl=en) <sup>1</sup>, [Dalei Hao](https://scholar.google.com/citations?user=LapapmUAAAAJ&hl=en) <sup>2</sup>, [Alexey N. Shiklomanov](https://science.gsfc.nasa.gov/sci/bio/alexey.shiklomanov) <sup>3</sup>, [Xi Yang](https://uva.theopenscholar.com/plant-ecology-lab/people/xi-yang) <sup>4</sup>, [Philip A. Townsend](https://forestandwildlifeecology.wisc.edu/people/faculty-and-staff/philip-townsend/) <sup>1</sup>, [Hamid Dashti](https://hamiddashti.github.io) <sup>1</sup>, [Tatsuro Nakaji](https://nakaji-hokudai.jimdofree.com) <sup>5</sup>, [Kyle R. Kovach](https://scholar.google.com/citations?user=P_CRYLQAAAAJ&hl=en) <sup>1</sup>, [Haoran Liu](https://scholar.google.com/citations?user=8ZWSyekAAAAJ&hl=en) <sup>1</sup>, [Meng Luo](https://scholar.google.com/citations?user=Re7ufpAAAAAJ&hl=zh-CN) <sup>1</sup>, [Min Chen](https://globalchange.cals.wisc.edu/staff/chen-min/) <sup>1, 6</sup>

<sup>1</sup> Department of Forest and Wildlife Ecology, University of Wisconsin- Madison, Madison, WI, USA;  
<sup>2</sup> Atmospheric, Climate, & Earth Sciences Division, PaciﬁcNorthwest National Laboratory, Richland, WA, USA;  
<sup>3</sup> NASA Goddard Space Flight Center, 8800 Greenbelt Road, Mail code: 610.1, Greenbelt, MD, USA;  
<sup>4</sup> Department of Environmental Sciences, University of Virginia, VA, USA;  
<sup>5</sup> Uryu Experimental Forest, Hokkaido University, Hokkaido, Japan;  
<sup>6</sup> Data Science Institute, University of Wisconsin- Madison, Madison, WI, USA.

</div>

<p align='center'>
  <a href="https://doi.org/10.1111/nph.19807"><img alt="Pape" src="https://img.shields.io/badge/TPAMI-Paper-6D4AFF?style=for-the-badge" /></a>
</p>

## Summary
* Leaf traits are essential for understanding many physiological and ecological processes. Partial least-squares regression (PLSR) models with leaf spectroscopy are widely applied for trait estimation, but their transferability across space, time and plant functional types (PFTs) remains unclear.
* We compiled a novel dataset of paired leaf traits and spectra, with 47,393 records for >700 species and eight PFTs at 101 globally-distributed locations across multiple seasons. Using this dataset, we conducted an unprecedented comprehensive analysis to assess the transferability of PLSR models in estimating leaf traits.
* While PLSR models demonstrate commendable performance in predicting chlorophyll content, carotenoid, leaf water and leaf mass per area prediction within their training data space, their efficacy diminishes when extrapolating to new contexts. Specifically, extrapolating to locations, seasons, and PFTs beyond the training data leads to reduced _R<sup>2</sup>_ (0.12-0.49, 0.15-0.42, and 0.25-0.56) and increased _NRMSE_ (3.58-18.24%, 6.27-11.55% and 7.0-33.12%) compared to nonspatial random cross-validation (NRCV). The results underscore the importance of incorporating greater spectral diversity in model training to boost its transferability.
* These findings highlight potential errors in estimating leaf traits over multiple domains due to biased validation schemes and provide guidance for future field sampling strategies and remote sensing applications.

## Description of compiled dataset
1. The compiled dataset contained both common leaf traits and the corresponding leaf reflectance measurements:
  * Leaf spectra ranging from 450 to 2400 nm with 10 nm interval.
  * Total chlorophyll content (Chla+b, µg/cm<sup>2</sup>): 6,840 samples;
  * Total carotenoid content (Ccar, µg/cm<sup>2</sup>): 4,233 samples;
  * Equivalent water thickness (EWT, g/m<sup>2</sup>; a.k.a., leaf water content): 3,581 samples;
  * Leaf mass per area (LMA; g/m<sup>2</sup>): 45,417 samples.
2. Total 47,393 measurements, more than 700 species and 8 PFTs at 101 globally-distributed locations. 
  * Evergreen needleleaf forests (ENF, n = 891);
  * Evergreen broadleaf forests (EBF, n = 1,382);
  * Deciduous needleleaf forests (DNF, n = 77);
  * Deciduous broadleaf forests (DBF, n = 26,944);
  * Shrublands (SHR, n = 1,599);
  * Grasslands (GRA, n = 11,833);
  * Croplands (CRP, n = 3,409);
  * Vine (n = 637).
3. Access to the folder [**datasets**](datasets) for the compiled dataset.
  * `Paired leaf traits and leaf spectra dataset.csv`: The entire complied dataset.
  * `Description of compiled dataset.docx`: Description of the compiled dataset and links to the original dataset, users can access the links to original datasets.
<img src="figs/Fig 1_sites distribution.png" title="" alt="" data-align="center">
<p align="center">Fig.1. The distribution of leaf samples in (a) climate zones (Whittaker, 1970) and (b) geographic locations.</p>

## PLSR modeling
<img src="figs/Fig 2_Flowchart.png" title="" alt="" data-align="center">
<p align="center">Fig.2. The framework of this study for testing the transferability of PLSR modeling across sites, PFTs and time.</p>

## Requirements
* Python 3.7.13 and more in [`environment.yml`](environment.yml)

## Usage
* Clone this repository
  ```
  git clone https://github.com/FujiangJi/PLSR_trait_models_evaluation.git
  ```
* Navigate to the directory and download the dataset from github LFS
  ```
  git lfs ls-files
  git lfs pull
  ```
* Setup conda environment and activate
  ```
  conda env create -f environment.yml
  conda activate py37
  ```
* Navigate to the directory [**src_code**](src_code), change the output path in **[PLSR_modeling.py](src_code/PLSR_modeling.py)**, and uncomment the unnecessary functions.

(1) Example: runing on the Local PC:
  ```
  python main.py
  ```
(2) Example: runing on the high-performance computing (HPC) cluster: set the conda environment in [main.sh](src_code/main.sh):
```
sbatch main.sh
```
## Description of files in this repository
* coefficients_vips: contains the results of PLSR coefficients and VIP metrics for differents modeling strategies for each leaf trait.
* datasets: contains the compiled dataset and description of the dataset.
* models: contains the trained PLSR models based on different modeling strategies for each leaf trait.
* src_code:
  * **[datasets_compilation.ipynb](src_code/datasets_compilation.ipynb)**: the code for dataset compilation.
  * **[PLSR_modeling.py](src_code/PLSR_modeling.py)**: contains the necessarry functions for PLSR modeling.
  * **[main.py](src_code/main.py)**: the main code for running.
  * **[main.sh](src_code/main.sh)**: the script for runing on HPC.
  * **[visualization.ipynb](src_code/visualization.ipynb)**: the code for visualizing results.

## Reference
In case you use our dataset or code in your research, Please cite our paper and we kindly request that you consider the possibility of potential co-authorship:
* If you have any questions about the code or data, please feel free to reach me at fujiang.ji@wisc.edu.
```
Ji, F., Li, F., Hao, D., Shiklomanov, A.N., Yang, X., Townsend, P.A., Dashti, H., Nakaji, T.,
Kovach, K.R., Liu, H., Luo, M. and Chen, M. (2024), Unveiling the transferability of
PLSR models for leaf trait estimation: lessons from a comprehensive analysis with a
novel global dataset. New Phytol, 243: 111-131. https://doi.org/10.1111/nph.19807
```

## Contact
```
fujiang.ji@wisc.edu
min.chen@wisc.edu
```
## Credits
* Most of the data sources are from the EcoSIS Spectral Library, available at https://ecosis.org/.
* This project is supported by the National Aeronautics and Space Administration (NASA) through Remote Sensing Theory and Terrestrial Ecology programs.
* We acknowledge high-performance computing support from the UW-Madison Center for High Throughput Computing (CHTC) in the Department of Computer Sciences. 

