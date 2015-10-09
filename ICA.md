# Introduction #

Independent Component Analysis (ICA) is a well known statistical technique for finding the hidden factors from multidimensional data or Signals. It builds a generative model for the observed multivariate(multidimensional) data in which the data is assumed to be a linear or nonlinear mixtures of unknown hidden variables. These variables are called as ''Independent Components (IC's) or sources'' of the observed data where the IC's are assumed to be mutually independent and nongaussian. It is a very powerful technique which is superficially related to Factor Analysis and Principle Component Analysis.

In Signal Processing applications ranging from speech signal to medical image analysis, source separation and identification techniques are widely used for separating the superposition of multiple signals.The separation of mixtures from a signal is achieved, by taking into account that the structure of the mixing process and by making assumptions about the sources(Signals).  When the information about these sources and mixing process is limited or unknown,then the problem is called ''Blind''. However, ICA is a suitable technique for these kind of blind source separation problems.

In order to find out the hidden sources in a given set of multidimensional observations, which are assumed to be a linear mixtures of unknown signals and also with unknown mixing process, the ICA algorithm performs a search for these mixtures and provides the independent source signals(IC's)as an output. ICA uses measures of nongaussianity to estimate the mixtures.


There are several ICA algorithms are available, but among them FASTICA (Aapo Hyvärinen) is chosen due to its simplicity and fastness. FASTICA is purely fixed point algorithm which uses higher order statistics to recover the independent sources from mixtures.

General model for ICA is a follows,
Assume that there areN statistical independent Source signals
> s(t) = <sub>[1....N]</sub>T and assume that these sources are obsercved from N sensors(Channels), then a set of N observed signals X(t) = <sub>[1....n]</sub>T are obtained from the mixtures of sources,then ICA models is represented as,    **` x(t) = As(t) `** where A is a mixing Matrix.

When the mixing matrix A and source signals S are unknown,in order to find the original signal one should first estimate the unmixing matrix 'W', such that, `s(t) = Wx(t) = WAs(t)`

# Algorithm #

Before applying ICA algorithm on the data, it is useful to do some preprocesing to the data in oreder to simplify the problem. This preprocessing step is not necessary in each and every aspect. It depends on the users intention either to performs or skip this preprocessing step.

**Preprocessing**
  * Centering
> > The most necessary and basic preprocessing is to center the data by subtracting the mean vectors for  the observed signal x. This is make the problem simple in order to do assumptions for computing mixing matrx. When the mixing and unmixing matrix are identified then add back the mean to complete the process.
  * Whitening
> > This is another useful preprocessing in ICA. After the process of centering , the data is to be whitened by transforming cenetered data linearly to new space. That is the components of the new transformed data are uncorrelated and have unit variance.

one popular method for whitening is PCA by using eigen value decomposition of the covariance matrix.

**FastICA**


> This the most popular and commonly used algorithm in ICA applications. This was introduced by 'Aapo Hyvärinen'. It is computationally efficient and uses fixed point iteration scheme to find the mixture matrix. This algorithms uses simple estimates of Negentropy based on the maximun entropy principal inorder to maximize the nongaussianity. There for the basic method of the FastICA algorithm is as follows

  1. Take a random intial vector W(0) and devide it by its norm.
  1. Let k = 1.
  1. Let w(k) = E{Z[ZTw(k-1)] 3}- 3w(k-1) (3.1)
  1. Divide w(k) by its norm .
  1. If |w T (k)w(k-1)| is not close enough to 1, let k = k+1, and go back to step 2.Otherwise the algorithm is convergent and outputs w(k) is one of the non gaussian source signal.

# Adding ICA in [BioPatRec](BioPatRec.md) #

  * GUI\_SigTreatment
    1. Creat a popup menu and tag it as 'pm\_ICAMethod'.
    1. Update the pb\_treat\_Callback function by adding ICA algorithm    which takes the input [sigTreated](sigTreated.md).
    1. The Algorithm isafter data segmentation.
  * [OfflinePatRec](OfflinePatRec.md)
> > The ICA algorithm is stored in [sigFeatures](sigFeatures.md) structure in PatRec for realtime test.

## Function RoadMap ##
  * Training
    * ICAPreprocess
    * ICA
  * Testing
    * ICARealtime


Add your content here.  Format your content with:
  * Text in **bold** or _italic_
  * Headings, paragraphs, and lists
  * Automatic links to other wiki pages