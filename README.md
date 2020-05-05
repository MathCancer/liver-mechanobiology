# Source code of liver tissue mechanobiology project
The model simulates the liver tissue mechanobiology (liver parenchyma-tumor interaction). The liver tissue is elastic-plastic: **Elastic**: on short times, when it’s deformed it elastically tries to return to its rest position and imparts forces on nearby tumor cells; **Plastic**: on long times, the resting position of these tissue elements relaxes back to the current position. We want to explore how tissue-tumor interaction affects the invasive growth of tumor.  

You can try to run our cloud-hosted **nanoHUB app** for fun!  
https://nanohub.org/tools/pc4livermedium

We found that:
* In high-flow / well-perfused liver tissues, growth substrate limitations (oxygen in our case) alone are an insufficient growth control to prevent non-physical overlap of cells. Mechanobiologic feedbacks are necessary. These are modeled as a pressure that can reduce or completely shut down cycle entry.

* In some tissue regimes, this can arrest the growth of micrometastases, make tumor be under dormancy state.

* In other tissue regimes, tumors will develop invasive fingers into the surrounding tissue along mechanical weaknesses.

### Citing
If you use the code in your work, please cite [Impact of tumor-parenchyma biomechanics on liver metastatic progression: a multi-model approach](https://www.biorxiv.org/content/10.1101/2020.05.04.074989v1).
```text
@article {Wang2020.05.04.074989,
	author = {Wang, Yafei and Brodin, Erik and Nishii, Kenichiro and Frieboes, Hermann B and Mumenthaler, Shannon and Sparks, Jessica L and Macklin, Paul},
	title = {Impact of tumor-parenchyma biomechanics on liver metastatic progression: a multi-model approach},
	elocation-id = {2020.05.04.074989},
	year = {2020},
	doi = {10.1101/2020.05.04.074989},
	publisher = {Cold Spring Harbor Laboratory},
	URL = {https://www.biorxiv.org/content/early/2020/05/05/2020.05.04.074989},
	eprint = {https://www.biorxiv.org/content/early/2020/05/05/2020.05.04.074989.full.pdf},
	journal = {bioRxiv}
}
```

* * * 

## Release summary: 

### 1.1.0:
* Update to PhysiCell 1.6.0
* Update the resizable domain, which means the domain size can be dynamic, changing within `[-5000 5000] * [-5000 5000] micron`
* Parse parameters from `config/PhysiCell_settings.xml`, such as domain size, simulation time and custom parameters etc. For example:
  
  ```xml
	<domain>
		<x_min>-1000</x_min>
		<x_max>1000</x_max>
		<y_min>-1000</y_min>
		<y_max>1000</y_max>
	</domain>

	<overall>
		<max_time units="min">86400</max_time> <!-- 60 days * 24 h * 60 min -->
	</overall>

	<user_parameters>
	  <random_seed type="int" units="dimensionless" hidden="true">0</random_seed> 
    <tumor_transition_rate type="double" units="1/min" description="The proliferation rate of tumor    cells">0.0022956841138659324</tumor_transition_rate>
    <tumor_max_necrosis_rate type="double" units="1/min" description="The maximum necrosis rate of tumor cells">0.002777777777777778</tumor_max_necrosis_rate>
    <elastic_rate type="double" units="1/min" description="The elastic force rate for parenchyma">0.05 </elastic_rate>
    <plastic_rate type="double" units="1/min" description="The plastic reorganization force rate for parenchyma">0.0005</plastic_rate>
    <max_ECM_displacement type="double" units="micron" description="The maximum tolerated displacement for parenchyma">0.75</max_ECM_displacement> 
    <tumor_max_pressue type="double" units="dimensionless" description="The maximum pressure threshold for tumor cells proliferation">1.0</tumor_max_pressue>
    <if_random_seed type="bool" units="none" description="Boolean variable that used to enable or disable random seeding">false</if_random_seed>
	</user_parameters>

  ```


### 1.0.0:
* Clean up the core source code
* Closed off the random seeding function in `custom_modules/liver_functions.cpp`
* Add matlab source code of liver generator

Bugs fixed:
* Fix bugs in `custom_modules/liver_functions.cpp`

  ```c++
  void HCT116_phenotype_update_function( Cell* pCell , Phenotype& phenotype, double dt )
  {
      static int start_phase_index = Ki67_advanced.find_phase_index( PhysiCell_constants::Ki67_negative ); // 0
      static int end_phase_index = Ki67_advanced.find_phase_index( PhysiCell_constants::Ki67_positive_premitotic ); // 1
  }
  ```

### 0.1.0:
This is initial release. In this version, we explore the random metastasis of tumor within liver tissue. Tumor cells are
stochastically seeded through the tissue, using a constant of probability of seeding per voxel. 

