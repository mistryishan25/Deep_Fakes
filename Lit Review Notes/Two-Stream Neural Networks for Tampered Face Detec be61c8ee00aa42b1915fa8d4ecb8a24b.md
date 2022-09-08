# Two-Stream Neural Networks for Tampered Face Detection[10-29]

Files: Two-Stream%20Neural%20Networks%20for%20Tampered%20Face%20Detec%20be61c8ee00aa42b1915fa8d4ecb8a24b/Paper_10_-_29.pdf
Person: Anonymous
Status: Read
Tags: Image Fakes, Steganalysis
Type: Paper, SciHub

Current methods for tampering detection depend on a particular source of tampering evidence - for example : local noise analysis fails to deal with tampered images constructed using careful post processing and Color Filter Array (CFA) models cannot deal with resized images. **CNNs** proven powerful in **learning the tampering evidence** and **rich models for detecting the noise residuals/Steganalysis features. 

The approach :** The premise behind local noise estimation based techniques is that the **difference between global noise characteristics and local noise characteristics** reveals the hidden tampered regions. One stream is a **CNN trained to classify** if the image is real or fake. The patch triplet stream, which is **trained on Steganalysis features of image patches with a triplet loss, models the traces left by in camera processing and local noise characteristics** 

Assumption : Different imaging devices produce different CFA regions wrt tampered and authentic images.

One approach was to use light/illumination features from the images and **use a SVM to classify** tampered parts. But some techniques might use only small sections to change hence not much global change in the illumination.

Steganalysis features : 
The steganalysis feature ( low level features) is a local descriptor based on cooccurrence statistics of nearby pixel noise residuals obtained from multiple linear and non-linear filters. First attempt was made for the above technique by modelling it **as a Gaussian Model,** which was later improved by treating the task **as anomaly detection** which used **a discriminative learning autoencoder outlier removing method based on steganalysis features** Noteworthy for CNNs :  **The performance degrades significantly when multiple post processing techniques are applied to tampered regions.**

For steganlaysis they have a Deep CNN that is based on triple loss - in order to ensure that two parts of the image from the same image are closer in the learned embedding whereas the difference between those from different images are large.

This is implemented by simply constraining the distances between the features of the patches by some margin $m$ .
Formally, given Image patch $x_a$ (anchor patch), a patch $x_p$ (positive patch) from the same image, and $x_n$ (negative patch) from a different image.

$$
d(f(r(x_a)),f(r(x_p))) + m<d(f(r(x_a)),f(r(x_n)))
$$

where $r(x)$ is the steganalysis features of patch $x$, $f(r(x))$ - is the embedding we want to learn of $x$, and $d()$ is the sum of squares distance measure.
Loss function is hence : 

$$
L(f) = \sum_{a,p,n}{\max(0,m+d(f_a,f_p)-d(f_a,f_n))}
$$

In laymen terms, the triplet network tells if the two patches under study are from the same image or not .This means if the patches are from the same image then they are closer in distance based on the learned embedding and if they are farther then they come from a different image - hence tampered.

Combined metric : Steganlysis + SVM

$$
F(q) + \lambda \frac{1}{N_q}\sum_{x\in q}{S(x)}
$$

where $N_q$ is the number of patches inside face $q$

Key approaches tested against  : 

1. Face Classification stream 
2. Patch Triplet Stream 
3. Steganalysis features + Linear SVM 
4. CFA Pattern - This method estimates the CFA pattern and uses a GMM algorithm to classify the variance of prediction error using the estimated CFA pattern. The output of this method is a local level tampering probability map. For the face region, an average probability is calculated as the final score
5. Improved DCT Coefficient - This method estimates the DCT coefficients for all the regions in the given image to find the singly JPEG compressed regions and classifies them as tampered regions. The output of this method is a probability map indicating tampering

The end product analysed was the Class Activation Maps(CAMs) from the trained GoogLeNet.