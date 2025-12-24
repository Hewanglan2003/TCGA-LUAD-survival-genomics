# TCGA LUAD Genomics Analysis and Survival Analysis

## 1 Dataset download and merging

We choose the TCGA-LUAD dataset and download the expression data and clinical data through GDCquery and GDCquery_clinic. 
For the expression data, we choose STAR-counts as default and HTseq-counts and the second choice.

In order to do the survival analysis, we need to get the OS data from the clinical dataset.
We use the vital_status(alive or dead) as OS_event and days_to_death or days_to_last_follow_up or days_to_last_known_disease_status as the OS_time_days.

Before we merge the expression data with the OS data, we need to screen duplicated case in expr and sort it by id.

Then we can get the merged dataset with expr and OS data as model_df.

## 2.Univariate and Multivariate Cox regression for phenotype variable(age, gender and stage)

We calculate the event rate first and make sure there is enough samples that the patiented was dead ultimately.

Then we do the Cox regression for three variables seprartely and we find that stage is the most significant factor for the OS .

After that, we do the multivariate Cox regression for three variables and find the most significant factor.

## 3.Genetics and Cox regression for Genomics

### [Part1]Screen the unimportant genes to simplify the process of Cox regression.

Original number of genes:60750

A.Screen the genes with at least 20% of it has expression counts over 10.

Number of genes:23840

B.Variance stabilizing transformation to make the genes with different expression levels have the variance in one fixed level.(To make genes more comparable)

C.Calculate the variances for genes and drop the genes with the smallest 25% variance.

Number of genes:17880

### [Part2] Univariate Cox regression for genes.

Get the results of univariate cox regression and save the results.

There are totally 862 genes with FDR(False Discovery Rate) < 0.5 and we consider them as significant genes for OS. We can draw a volcano plot to show the overall effect of genes.

### [Part3] Elastic Cox regression for genes.

We apply the Elastic Cox regression on 17880 genes and find that sig_min includes 47 genes and sig_1se includes 0 genes. So we need to use the sig_min and the 47 corresponding genes.
We save the result as “signature_lambdaMin_47genes”

### [Part4]Risk score & KM Plot

Use the 47 significant genes to calculate the risk scores for each case in the dataset. Then we divide the cases into two groups with the median of risk scores as Low group and High group.
Then we can draw the KM plot to show the difference of OS_time_days between Low risk score group and High risk score group.

### [Part5] Verify the significance of risk scores with univariate Cox regression.

We do univariate Cox regression on risk scores and risk groups. Both of them are significant with high HR.

### [Part6] Compare the effect of risk with other variables using multivariate Cox regression.

We do multivariate Cox regression on risk scores, age, gender and stage and draw a forest plot to show it. Risk score has the shortest confidence interval and highest average HR.
That means our result or choice of 47 genes and risk scores are useful for this survival analysis.

### [Part7] Map the gene id to concrete gene symbols.

Save the result as "ElasticNet_47genes_mapping_summary".







