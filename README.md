# Semester_project-vWF_release

This project was aimed to estimation and comparison of von Willebrand factor release from endothelial cells treated by H2O2, Trombine and Histamin. 


Background: Endothelial cells (EC) line up the surface of blood and lymphatic vessels and regulate many aspects of human body physiology. The main functions of 
endothelial cells are the control of blood clotting and von Willebrand factor (vWF) is one of the major proteins in this reaction. Upon specific stimulation EC
releases vWF via exocytosis from specific storage organelles – Weibell-Pallade bodies. After exocytosis, vWF can form multimeric structures called “strings” on 
the surface of EC. These structures activate platelets aggregation and initiate clotting formation. Recently, reactive oxygen species (ROS) were recognized as 
second messengers together with Ca2+ and cAMP. Of all ROS, H2O2 is the best candidate for such a role due to its molecular properties. H2O2 is a mild relatively 
stable oxidant which is highly soluble in lipids. There are two main sources of cellular H2O2: superoxide dismutase and NADPH-oxidase NOX4, extracellularly H2O2 
can be generated during activation of platelets, monocytes and neutrophils. The effect of H2O2 on vWF release from EC is unknown.

Aim of the study: To estimate the effect H2O2 exposure on vWF release from EC.

Materials and Methods: All experiments were done on HUVECs – human umbilical cord endothelial cells. Briefly, cells were seeded in 48-well plate and cultured before
100% confluence and 2 days more. Then, cells were stimulated by 100 uM of H2O2. Histamine (100 uM) and Trombin (10 uM) were used as positive control, equal volume 
of phosphate-buffered saline were added as negative control. After 20 min of incubation, cells were fixed and stained by specific antibody to vWF, weat germ 
agglutinin for cell borders detection and by Hoechst 33352 for nuclei detection. 25 fields of view were taken from each well, each experimental group was present 
as 3 independent wells. Images were segmented and fluorescence parameters were measured by CellProfiler 4.07 software. Data was exported as a CSV file and 
processed by Rstudio 3.6.2. 


Results: 2 datasets which describe Cells and their vWF-positive structures were generated by image processing software CellProfiler with a user-defined algorithm. 
Final datasets contained ≈ 29000 cells and 6500 strings after outlier removing and data filtration. For estimation of statistical difference between our groups 
(control, H2O2, Histamine and Trombine) we choose 4 parameters in dataset Cells and 3 parameters from dataset Strings for analysis. Kruscall-Wallis test with Dunn 
post hoc test were used for estimation of difference between groups due to non-normal distribution of all variables in both datasets. Epsilon-squared criterion was 
used for estimation of size effect. In all cases epsilon-squared were very close to zero (0.01-0.1), so even if the difference was statistically significant the 
difference between groups was negligible or very weak. So, manually choosing variables did not show a significant result, so that is why we make a random forest 
classification of our data. Before classification, we add a new factor variable with 2 levels(stimulated/unstimulated) in all our datasets and split them for 3 
parts (test, train and validation sets) in ratio 0.25:0.25:0.5. Number of training variables for each iteration were determined automatically (for Strings) and 
manually for Cells, the number of trees were 500 for Cells and 1000 for Strings. OOB estimation for Cells random forest was 15.11%, AUC = 0.72. According to 
meanDecreaseGini index, the most important variable for Cells classification was Std of vWF Intensity.  OOB estimation for String random forest was 30.24%, 
AUC = 0.67 and the most important variable for classification was again Std of vWF intensity. 
Conclusion: Based on random forest classification, H2O2 treated cells and structures were classified as stimulated, and their characteristics were more close to 
Histamine or Trombine treated cells.


