# Introduction #

Regulatory Feedback Networks were initially introduced by [Tsvi Achler](http://reason.cs.uiuc.edu/tsvi/) as an alternative to the traditional "feed forward" or "lateral inhibition" pattern recognition algorithms. In traditional pattern recognition, the learning takes places during a training phase, in RFN, the pattern recognition occurs during the testing phase by observing the stability of the outputs.

Feedback regulation is analogous to the negative feedback in control theory.

# Algorithm #

...

Salience is an integral part of RFN ...

...

# Implementation #

There are two key procedures for this algorithm

**1.- The creation of the connectivity matrix:**
  * connMat(#Movements x #Features)

RFN requires of a single vector to represent a class. However, in prosthetic control, there is normally several vectors of features (or data sets, [xSets](xSets.md)) per class. Therefore, we need to generate this vector in the following ways:

  * **Mean**. This is the average value of each feature per class
  * **Mean + PSO**. Additionally to taking the mean, a PSO is used to fine tune the resulting vectors.
  * **Exclusive Mean**. Excludes the mean values that are smaller than 2 times the standard deviation.

These different methods can be selected as "training algorithm" in the [GUI\_PatRec](GUI_PatRec.md)).

**2.- The testing function** where the stability of the output is evaluated (RegulationFeedbackTest)

NOTE: For this particular implementation the normalization "`UnitaryRange`" is necessary. This means a normalization between 0 and 1.

An additional implementation that utilizes a threshold to selected the predicted output is also available. The "RFNth" uses the standard RFN routines with the addition of a threshold.

# Functions Roadmap #
## Training ##

  * RegulationFeedback
    * 'Mean' training calls:
      * Get\_connMat\_TrV
    * 'Mean + PSO' training calls:
      * Get\_connMat\_TrV
      * InitPSO\_RFN
      * PSO\_RFN
    * 'Exclusive Mean' training calls:
      * Get\_connMat\_eMean
    * RegulationFeedbackAcc
      * RegulationFeedbackTest

  * RegulationFeedback\_thOut
    * RegulationFeedback
      * ...
    * RegulationFeedbackAcc
      * RegulationFeedbackTest


## Testing ##

  * RegulationFeedbackTest