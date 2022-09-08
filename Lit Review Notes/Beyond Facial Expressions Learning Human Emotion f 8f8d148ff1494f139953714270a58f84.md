# Beyond Facial Expressions: Learning Human Emotion from Body Gestures[10-37]

Files: http://www.bmva.org/bmvc/2007/papers/paper-276.pdf
Person: Anonymous
Status: Read
Type: Paper

In this paper, affective body gesture analysis in videos was investigated, a relatively understudied problem.Spatial-temporal features are exploited for modeling of body gestures. They also present to fuse facial expression and body gesture at the feature level usingCanonical Correlation Analysis.The current spatial-temporal features based video description does not consider the position relations of cuboids detected.

- Affective Body Gesture Recognition
    - Spatial-Temporal Features
        - We extract spatial-temporal features by detecting space-time interest points in videos. we calculate the response function by application of separable linear filters. Assuming a stationary camera or a process that can account for camera motion, the response function has the form:
        $R = (I \cdot g \cdot h_{ev})^2 + (I \cdot g\cdot h_{od})^2$                                                            (1)
        where $I(x,y,t)$ denotes images in the video, $g(x, y;\sigma)$ is the 2D Gaussian smoothing
        kernel, applied only along the spatial dimensions $(x, y)$, and $h_{ev}$} and $h_{od}$ are a quadrature pair of 1D Gabor filters applied temporally, which are defined as
            
            $h_{ev}(t; τ,ω) = −cos(2πtω)e^{−t^ 2/τ ^2}$
            
            $$
            hod(t; τ,ω)=  −sin(2πt\omega)e^{−t^2/τ^2}
            $$
            
            In all cases we use $\omega = \frac{4}{\tau}$. The two parameters $\sigma$ and $\tau$ correspond roughly to the spatial and temporal scales of the detector. Each interest point is extracted as a local maxima of the response function.Any region with spatially distinguishing characteristics undergoing a complex motion can induce a strong response, while region undergoing pure translational motion, or areas without spatially distinguishing features, will not induce a strong response.
            
            - At each detected interest point, a cuboid is extracted which contains the spatio-temporally windowed pixel values. The side length of cuboids is set as approximately six times the scales along each dimension, so containing most of the volume of data that contribute to the response function at each interest point. After extracting the cuboids, the original video is discarded, which is represented as a collection of the cuboids. To compare two cuboids, different descriptors for cuboids have been evaluated, including normalized pixel values, brightness gradient andwindowed optical flow, followed by a conversion into a vector by flattening, global histogramming, and local histogramming. As suggested, we adopt the flattened brightness gradient as the cuboid descriptor. To reduce the dimensionality, the descriptor is projected to a lower dimensional PCA space. By clustering a large number of cuboids extracted from the training data using the K-Means algorithm, we derive a library of cuboid prototypes. So each cuboid is assigned a type by mapping it to the closest prototype vector. we use the histogram of the cuboid types to describe the video.
    - Recognition: SVM
        - The Support Vector Machine (SVM) classifier to recognize affective body gestures.  **For
        the cases where it is difficult to estimate the density model in high-dimensional space, the discriminant approach is preferable to the generative approach.**
            
            Given a training set of labeled examples ${(x_i, y_i),i = 1,...,l}$ where $x_i \in R$ n and yi ∈{1,−1}, a new test example x is classified by the following function:
            $f(x) = sgn({\sum_{i=1}^l} α_iy_iK(x_i ,x) +b)$ 
            where αi are Lagrange multipliers of a dual optimization problem that describe the separating hyperplane, $K(·,·)$ is a kernel function, and b is the threshold parameter of the hyperplane. The training sample $x_i$ with $α_i > 0$ is called the support vector, and SVM finds the hyperplane that maximizes the distance between the support vectors and the hyperplane. Given a non-linear mapping $\phi$ that embeds the input data into the high dimensional space, kernels have the form of 
            
                   $K(x_i , x_j) = h\cdot \phi(x_i) \cdot \phi(x_ j)\cdot i.$ 
            Adavntage of using SVM here is that it allows domain-specific selection of the kernel function, and the most commonly used kernel functions are the linear, polynomial, and Radial Basis Function (RBF) kernels.
            
- Fusing Facial Expressions and Body Gestures
    - Canonical Correlation Analysis
        - CCA is a statistical technique developed for measuring linear relationships between
        two multidimensional variables.  CCA to find corresponding points in stereo images was applied. CCA to model the relation between an object’s poses with raw brightness images for appearance-based 3D pose estimation was suggested. A method using CCA to learn a semantic representation to web images and their associated text was proposed.
            
            Given two zero-mean random variables  $x \in R_m$  and $y \in R_n$  , CCA finds pairs of directions wx and wy that maximize the correlation between the projections x and y are called canonical variates.
            
            $$
            \rho= \frac{E[xy]}{\sqrt{E[x^2]E[y^2]}} = \frac{E[W_{x}^Txy^{T}W_{y}^T]}{\sqrt{E[W_{x}^Txy^{T}W_{x}^T]E[W_{x}^Tyy^{T}W_{y}^T]}} = \frac{W_x^T C_{xy}W_y}{\sqrt{W_x^T C_{xx}W_xW_y^TC_{yy}W_y}}
            $$
            
            where $C_{xx} \in \mathbb{R}^{m \times m}$ and $C_{yy} \in \mathbb{R^{n \times n}}$ are the within-set covariance matrices pf x and y respectively and $C_{xy} \in \mathbb{R}^{m \times  n}$ denotes their between-sets covariance matrix. 
            
- Experiments
    - Affective Body Gesture Recognition
        - To evaluate the algorithms’ generalization ability , a 5-fold cross-validation
        test scheme in all recognition experiments is adopted. That is the data set is divided randomly into five groups with roughly equal number of videos, and then used the data from four groups for training and the left group for testing; the process was repeated five times for each group in turn to be tested. The average recognition rates here. In all experiments, the soft margin C value of SVMs set to infinity so that no training error was allowed. With regard to the hyper-parameter selection of RBF kernels, we carried out grid-search on the kernel parameters in the 5-fold cross-validation. The parameter setting producing the best cross-validation accuracy was picked. The SVM used implementation in the publicly available machine learning library SPIDER 1 in  experiments. The SVM classifier was compared with the 1-nearest neighbor classifier for affective body gesture recognition. The average recognition rates of SVM and 1-nearest neighbor classifier are 72.6% and 68.6% respectively.