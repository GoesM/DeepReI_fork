[notice]: 

原文时间过去太久，部分环境不适配；因此对该项目进行复现的过程中，微调了其中的环境设置要求；并修改原readmd.md文档如下： ——GoesM

复现过程中，发现模型尺寸出现不匹配问题，因此对R源码中的数据处理部分也进行了一定的调整，所以请下载本仓库代码而非原仓库代码； ——GoesM

# DeepReI
 Deep Learning-based Gas Chromatographic Retention Index Predictor
 
 Details are published in: Tomáš Vrzal, Michaela Malečková, Jana Olšovská,DeepReI: Deep learning-based gas chromatographic retention index predictor,Analytica Chimica Acta 1147, 2021, 64 - 71, https://doi.org/10.1016/j.aca.2020.12.043
 
 Development was suported by the Ministry of Agriculture of the Czech Republic within the institutional support MZE-RO1918.

# INSTRUCTIONS FOR INSTALLATION:

## prepare base-program
(If R, keras package and 7-Zip are already installed, step 1 – 4 could be skipped.)

1) Download and install R (https://www.r-project.org/) and RStudio (https://rstudio.com/products/rstudio/download/).

2) Download and install 7-Zip (https://www.7-zip.org/).

## prepare base-lib
3) Run RStudio and install keras package according instructions at https://tensorflow.rstudio.com/guide/keras/.
		
		install.package(“keras”)
		library(keras)
		install_keras()
	
During the installation, R will ask if miniconda should be installed -> type y to the R console and press Enter button.

4) Install ChemmineR and ChemmineOB packages by typing the following code in R.

		if (!requireNamespace("BiocManager", quietly = TRUE))
    		install.packages("BiocManager")

		BiocManager::install("ChemmineR")

		if (!requireNamespace("BiocManager", quietly = TRUE))
	    	install.packages("BiocManager")

		BiocManager::install("ChemmineOB")

 
5) Install DeepReI by typing the following code in R.
	
	devtools::install_github("GoesM/DeepReI_fork")
 
6) set-up tensorflow environment
During this first test of the DeepReI, it is beneficial to see notifications appearing in R console. In some cases, a “Tensorflow not found” error could appear, and, it is possible to fix it by typing the following code to R console (after stopping the DeepReI by clicking on red “stop” button).

	tensorflow::install_tensorflow(version = “2.5.0")

At this moment, the DeepReI uses demo model – prediction will not be performed.


## prepare the AI-Model (as .h5 file)
6) Open 7-Zip File Manager (installed in step #3), find extdata folder in directory where DeepReI package was installed (e.g. Documents\R\win-library\4.0/DeepReI). Click on the model_DeepReI.zip.001 by right mouse button in the 7-Zip File Manager and select „Combine files…“. This procedure creates model_DeepReI.h5 file in zip folder. Unzip the .h5 file and replace the original model_DeepReI.h5 file in extdata folder with unzipped model_DeepReI.h5 file.

 
## Go for It !

INSTRUCTIONS FOR USE:

After successful installation, type following code to the R console.

	library(DeepReI)

  	library(keras)

	DeepReI()

DeepReI application will be opened in a web browser.
In the SMILES input tab, select file (.csv or .txt) with SMILES in a first column. If the first row represents header of the column, tick the Header box.

At this stage, retention index prediction could be performed by clicking on "Predict Retention Index" button (in Prediction tab).

After few seconds, table with predicted value of retention index together with respective SMILES will appear. This table could be copied and/or exported to Excel format by the appropriate buttons in Export results tab.
