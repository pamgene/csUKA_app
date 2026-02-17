# csUKA_app
The `confidence-scoring (cs)UKA app` converts peptide signal into kinases using two types of analysis:

* Comparison-type: Performs kinase enrichment analysis based on group comparisons (e.g. test vs control), using replicate data to compute significance and specificity scores.

* FC-type: Computes kinase enrichment based on fold changes between conditions, without using replicates; significance scores are not calculated.

## Relationship to the UKA_app

Confidence scoring is a newer algorithm compared to the previous UKA algorithm. Confidence scoring is a way of mapping Kinase Substrate Relations (KSR) in a biologically interpretable way. It combines evidence from multiple databases, accounts for peptide specificity, and has a clear Bayesian interpretation, making it a generic and extensible tool for kinase activity analysis. Additionally computation is faster than the UKA_operator, as no rank scanning is done. 

## App input wizard / crosstab projection of cs_uka_operator

The app wizard sets the input (crosstab projection) of the cs_uka_operator.

Wizard question|Crosstab projection|UKA-type|Description
---|---|---|---
Quantitation type|`y-axis` | Comparison, FC | Normalized data (log / VSN / Combat-corrected), single value / cell. For FC-type UKA, this is the fold change coming from a previous FC_app. 
Peptides|`row` | Comparison, FC | Peptide ID
Test condition|`x axis` | Comparison | A factor defining comparison groups (e.g. Test Condition, Supergroup)
Supergroup or Observation|`column` | Comparison, FC | For Comparison-type UKA, this is a factor defining supergroups (e.g. Supergroup, Test condition). Groups are compared within each Supergroup. For FC-type UKA, this is a single factor defining samples (e.g. Sample name, Replicate).
Single Data Value per Cell|`label` | Comparison|A factor defining samples (e.g. Sample name, Barcode & Row)

## Input Parameters of the cs_uka_operator:

In the wizard first page, Advanced tab, you can set the input parameters of the cs_uka_operator.

Input parameters|Default value|Description
---|---|---
`Kinase_family`| PTK | Type of kinase family, either PTK or STK.
`MinimumSetSize` | 3 | Minimum peptide set size for a kinase
`rmDualSpecKinases` | True | Remove dual specificity kinases. For PTK, only TYR group is kept. For STK, TYR group is excluded.
`useKL` | True | Use Kinase Library in UKAdb or not
`UKAType` | Comparison | Type of algorithm: based on comparing replicates ('Comparison'), or based on Fold Change ('FC').
`MinimumSequenceHomology`| 0.9 | Minimum sequence homology between peptides and phosphosites
`MinimumKxsScore` | 300 | Minimum PhospoNET score for upstream kinases
`NumberOfPerms` | 500 | Number of permutations to calculate significance and specificity scores
`MaxRank` | 12 | Maximum PhospoNET rank for upstream kinases
`ReverseContrast` | True | The direction of the contrast (Test vs Control or Control vs Test). True means "Test vs Control" type comparison.