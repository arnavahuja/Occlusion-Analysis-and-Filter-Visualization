# Occlusion-Analysis-and-Filter-Visualization
This is a part of my learning experiences with CNNs

## Occlusion Analysis
Occlusion sensitivity is a simple technique for understanding which parts of an image are most important for a deep network's classification. 
This can be achieved by drawing a heat map of the features to observe. This can be very useful in finding the parts of interest in an image.

<img src="https://www.researchgate.net/profile/Patrick_Zschech/publication/332935515/figure/fig2/AS:756220138897422@1557308339760/Heat-map-visualization-results-after-using-occlusion-sensitivity.jpg">

## Filter Visualization
Filter visualization is done to realize what exactly are the filters learning in a CNN, so that the outputs can be better understood. Since the filters are performing a convolution operation, it is similar to the dot product of two vectors (if we think about them in the form of 1D vedctors). Since the dot product is proportional to the cosine of the angle between the the vectors, this means that to maximize the cosine the filters much align themselves to to be as close to the image as possible. This means that the filters are learning features of an image which are exactly like them as shown in the code.

<img src="https://www.oreilly.com/library/view/deep-learning/9781491924570/assets/dpln_0416.png">
