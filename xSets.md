# The training, validation and testing sets #

This is the last step of signal processing before continuing with the  PatRec or more specific OfflinePatRec.

  * **trSets**. Training sets (used for training, yes, really!)
  * **vSets**. Validation sets (used for validation during training)
  * **tSets**. Testing sets (only to be used for testing the trained algorithm)

These are all matrices (r x c) of signal features values where:

  * r = rows = number of sets
  * c = columns = number of channels times number of features (set of features, or features vector)

Depending on the PatRec algorithms
([DA](DA.md), [MLP](MLP.md), [RFN](RFN.md),...), the use of the validation set can change, however, the testing set must be used only after the training is completed.

For each xSets there is a xOuts, these are:

  * **trOuts**
  * **vOuts**
  * **tOuts**

xSets and xOuts are ultimately 2 dimensional matrices where sets of a given phase (e.g. training) are stack over each other. Once all movements are merged, they can be distinguished by the xOuts matrices.

These are (r x c) matrices where

  * r = rows = number of data sets
  * c = columns = number of outputs

![https://biopatrec.googlecode.com/svn/wiki/img/Biopatrec_paper/Biopatrec_patternrecognition_thexSets.png](https://biopatrec.googlecode.com/svn/wiki/img/Biopatrec_paper/Biopatrec_patternrecognition_thexSets.png)
> [Fig. 5 from BioPatRec paper](http://www.scfbm.org/content/8/1/11)


Each data set in this case is a vector of 0s represent an _off_ output, and 1 an _on_ output. e.g. If the features vector r = 3 of xSets, corresponds to the class 2, then in r = 3 of xOut will be: 0 1 0 ...

In some parts of the code the xSets can be xSet, this is probably a mistake and has to be standardized to xSets and xOuts since xSet would represent better a single vector of data.

These matrices are constructed by the functions:

  * GetSets\_Stack\_IndvMov or,
  * GetSets\_Stack or,
  * GetSets\_Stack\_MixedOut

NOTE: It might seems like the second one is not need since the first one can handle both cases, however, if mixed movements want to be treated as individual movements, this can only be process by the first one.

  * The xSets are constructed by stacking sets of signal features.
  * Each set is constructed by obtaining the first signal features per each channel, then the second features per channel and so on, until all the selected features are part of the row.
  * This makes that all values for the same feature per channels can be found in the same column.