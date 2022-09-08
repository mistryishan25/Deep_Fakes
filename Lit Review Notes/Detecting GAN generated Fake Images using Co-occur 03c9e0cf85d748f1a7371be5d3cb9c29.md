# Detecting GAN generated Fake Images using Co-occurrence Matrices[10-1]

Files: https://doi.org/10.2352/ISSN.2470-1173.2019.5.MWSF-532
Person: Anonymous
Status: Read
Type: Paper

ABSTRACT:

In this paper, we propose a novel approach to detect GAN generated fake images using a combination of co-occurrence matrices and deep learning. We extract co-occurrence matrices on three color channels in the pixel domain and train a model using a deep convolutional neural network (CNN) framework. Experimental results on two diverse and challenging GAN datasets comprising more than 56,000 images based on unpaired image-to-image translations (cycleGAN [1]) and facial attributes/expressions (StarGAN [2]) show that our approach is promising and achieves more than 99% classification accuracy in both datasets. 

Introduction:

Inspired by steganalysis and natural image statistics, they proposed a novel method to identify GAN generated images using a combination of pixel co-occurrence matrices and deep learning. Here they pass the co-occurrence matrices directly through a deep learning framework and allow the network to learn important features of the co-occurrence matrices. They also avoid computation of residuals or passing an image through various filters, but rather compute the co-occurrence matrices on the image pixels itself. Experimental results on two diverse and challenging datasets generated using GAN based methods show that our approach is promising and generalizes well when the GAN model is not known during training.

Methodology:

To detect GAN images, we compute co-occurrence matrices on the RGB channels of an image. Co-occurrence matrices have been previously used in steganalysis to identify images that have data hidden in them [5, 6, 7, 8] and in image forensics to detect or localize tampered images [50, 9]. In prior works, cooccurrence matrices are usually computed on image residuals by passing the image through many filters and then obtaining the difference. Sometimes features or statistics are also computed on the matrices and then a classifier is trained on these features to classify data hidden or tampered images.

Conclusions:

In this paper, we proposed a novel method to detect GAN generated fake images using a combination of pixel co-occurrence matrices and deep learning. Co-occurrence matrices are computed on the color channels of an image and then trained using a deep convolutional neural network to distinguish GAN generated fake images from real ones. Experiments on two diverse GAN datasets show that our approach is both effective and generalizable.