# histograph
historgraph is a graph database of four different handwritten historical documents, viz.

*  [George Washington (GW)](http://www.fki.inf.unibe.ch/databases/iam-historical-document-database/washington-database)
* [Parzival (PAR)](http://www.fki.inf.unibe.ch/databases/iam-historical-document-database/parzival-database)
* [Alvermann Konzilsprotokolle (AK)](https://www.prhlt.upv.es/contests/icfhr2016-kws/data.html) 
* [Botany (BOT)](https://www.prhlt.upv.es/contests/icfhr2016-kws/data.html)

Please cite the following papers (as well as the corresponding references of the handwritten historical documents, see above):

*[1] M. Stauffer, A. Fischer, K. Riesen, Keyword Spotting in Historical Handwritten Documents based on Graph Matching, Pattern Recognit. (2018).*

*[2] M. Stauffer, A. Fischer, K. Riesen, [A Novel Graph Database for Handwritten Word Images](https://www.researchgate.net/publication/310508538_A_Novel_Graph_Database_for_Handwritten_Word_Images), in: Int. Work. Struct. Syntactic, Stat. Pattern Recognit., 2016: pp. 553–563.*

# Image Preprocessing

The following image preprocessing steps have been employed for the four different manuscripts. Note that the segmentation of AK and BOT has been done in conjunction of the ICFHR2016 KWS benchmark competition, while the segmentation of GW and PAR has been done by ourself.

## GW and PAR

1. Remove noise by Difference of Gaussians
2. Binarisation by global thresholding
3. Semi-automatic segmentation of word line images to word images by means of projection profiles
4. Skew-correction by means of linear regression of lower baseline
5. Skeletonisation

## AK and BOT

1. Remove noise by Difference of Gaussians
2. Binarisation by global thresholding
3. Filtering of segmentation errors by means of morphological filtering
4. Skeletonisation

We denote segmented word images that are binarised by B. If the image is additionally skeletonised we use the term S from now on.

# Graph Representations

`Keypoint`: The first graph representation makes use of characteristics points (so called keypoints) in skeletonised word images S. These keypoints are represented as nodes that are labelled with the corresponding (x,y)-coordinates. Between pairs of keypoints (which are connected on the skeleton) further intermediate points are converted to nodes and added to the graph at equidistant intervals. Finally, undirected edges are inserted into the graph for each pair of nodes that is directly connected by a stroke.

`Grid`: The second graph representation is based on a grid-wise segmentation of binarised word images B into equally sized segments. For each segment, a node is inserted into the graph and labelled by the (x,y)-coordinates of its respective centre of mass. Undirected edges are inserted between two neighbouring segments that are actually represented by a node. Finally, the inserted edges are reduced by means of a Minimal Spanning Tree algorithm.

`Projection`: The third graph representation is based an adaptive and threshold-based segmentation of binarised word images B. Basically, this segmentation is computed on the horizontal and vertical projection profiles of B. The resulting segmentation is further refined in the horizontal and vertical direction by means of two distance-based thresholds. A node is inserted into the graph for each segment and labelled by the (x,y)-coordinates of the corresponding centre of mass. Undirected edges are inserted into the graph for each pair of nodes that is directly connected by a stroke in the original word image.

`Split`: The fourth graph representation is based on an iterative segmentation of binarised word images B. That is, segments are iteratively split into smaller subsegments until the width and height of all segments are below certain thresholds. A node is inserted into the graph and labelled by the (x,y)-coordinates of the point on the stroke closest to the centre of mass of each segment. For the insertion of the edges, a similar procedure as for `Projection` is applied.

## Graph Normalisation

The resulting graphs or more precisely the (x,y)-coordinates of the node labels are normalised by a z-score. Formally, we use normalised coordinates (x-norm, y-norm) derived by

`x-norm = (x - µ(x))\σ(x)` and `y-norm = (y - µ(y))\σ(y)`


where (µ(x),µ(y)) and (\σ(x),σ(y)) represent the mean and standard deviation of all (x,y)-coordinates in the graph under consideration.

# Keyword Spotting Setup

## GW and PAR



## AK and BOT

# Keyword Spotting Reference Results
For reference Keyword Spottings results of the four different handwritten historical documents with different fast suboptimal algorithms for Graph Edit Distance we refer to the following papers:

## Bipartite Graph Edit Distance

##### Baseline

*[1] M. Stauffer, A. Fischer, K. Riesen, Keyword Spotting in Historical Handwritten Documents based on Graph Matching, Pattern Recognit. (2018).*

##### Speed up approach by means of quadtree segmentations 

*[3] M. Stauffer, A. Fischer, K. Riesen, [Speeding-Up Graph-based Keyword Spotting by Quadtree Segmentations](https://www.researchgate.net/publication/318732820_Speeding-Up_Graph-Based_Keyword_Spotting_by_Quadtree_Segmentations), in: Int. Conf. Comput. Anal. Images Patterns, 2017.*

##### Speed up approach by menas of fast rejection

*[4] M. Stauffer, A. Fischer, K. Riesen, [Filters for Graph-Based Keyword Spotting in Historical Handwritten Do cuments](https://www.researchgate.net/publication/324125812_Filters_for_Graph-Based_Keyword_Spotting_in_Historical_Handwritten_Documents), Pattern Recognit. Lett. (2018).*

##### Ensembles

*[5] M. Stauffer, A. Fischer, K. Riesen, [Ensembles for Graph-based Keyword Spotting in Historical Handwritten Documents](https://www.researchgate.net/publication/321146023_Ensembles_for_Graph-Based_Keyword_Spotting_in_Historical_Handwritten_Documents), in: Int. Conf. Doc. Anal. Recognit., 2017: pp. 714–720.*

## Hausdorff Edit Distance

*[6] M.R. Ameri, M. Stauffer, K. Riesen, T.D. Bui, A. Fischer, [Keyword Spotting in Historical Documents Based on Handwriting Graphs and Hausdorff Edit Distance](https://www.researchgate.net/publication/317821942_Keyword_Spotting_in_Historical_Documents_Based_on_Handwriting_Graphs_and_Hausdorff_Edit_Distance), in: Int. Graphonomics Soc. Conf., 2017.*

## Context-aware Hausdorff Edit Distance

*[7] M. Stauffer, A. Fischer, K. Riesen, Graph-Based Keyword Spotting in Historical Documents Using Context-Aware Hausdorff Edit Distance, in: Int. Work. Doc. Anal. Syst., 2018.*