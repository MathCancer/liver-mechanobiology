# Source code of liver tissue mechanobiology project
The model simulates the liver tissue mechanobiology (liver parenchyma-tumor interaction). The liver tissue is elastic-plastic: **Elastic**: on short times, when it’s deformed it elastically tries to return to its rest position and imparts forces on nearby tumor cells; **Plastic**: on long times, the resting position of these tissue elements relaxes back to the current position. We want to explore how tissue-tumor interaction affects the invasive growth of tumor.  

You can try to run our cloud-hosted **nanoHUB app** for fun!  https://nanohub.org/tools/pc4livermedium

We found that:
* In high-flow / well-perfused liver tissues, growth substrate limitations (oxygen in our case) alone are an insufficient growth control to prevent non-physical overlap of cells. Mechanobiologic feedbacks are necessary. These are modeled as a pressure that can reduce or completely shut down cycle entry.

* In some tissue regimes, this can arrest the growth of micrometastases, make tumor be under dormancy state.

* In other tissue regimes, tumors will develop invasive fingers into the surrounding tissue along mechanical weaknesses.

* * * 

## Release summary: 
### 0.1.0:
This is initial release. In this version, we explore the random metastasis of tumor within liver tissue. Tumor cells are
stochastically seeded through the tissue, using a constant of probability of seeding per voxel. 

