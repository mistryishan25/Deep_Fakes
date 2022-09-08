# ArcFace: Additive Angular Margin Loss for Deep Face Recognition [12]

Files: https://sci-hub.st/https://ieeexplore.ieee.org/document/8953658
Person: Anonymous
Status: Read
Type: Paper

1. This paper proposes an Additive Angular Margin Loss also known as Arc Face (loss function) to obtain highly discriminative features of face recognition.
2. The proposed ArcFace has clear geometric interpretation due to it's exact correspondence to geodesic distance on a hypersphere.
3. To enhance intra class compactness and inter class discrepancy, there are four kinds of Geodesic Distance (GDis) constraint.
    
    3.1 Margin Loss: insert a geodesic distance margin between the sample and centers.
    
    3.2 Intra-Loss: decrease the geodesic distance between the sample and the corresponding center.
    
    3.3 Inter-Loss: increase the geodesic distance between different centers.
    
    3.4 Triplet-Loss: Insert a geodesic distance margin between triplet samples.
    
4. Additive Angular Margin Los (ArcFace) is exactly corresponded to the geodesic distance to enhance discriminative power of face recognition model.
5. Based on large-scale training data and the elaborate DCNN architectures, both the SoftMax-loss-based methods and the triplet loss based methods can obtain excellent performance on face recognition.
6. In the figure given below the dot product between DCNN feature and the last fully connected layer is equal to the cosine distance after feature and weight normalization

![Untitled](ArcFace%20Additive%20Angular%20Margin%20Loss%20for%20Deep%20Face%20bdf05b9a25194896bfa14d410fc9d4c9/Untitled.png)

1. The advantages of the proposed ArcFace are as follows:

7.1 Engaging: ArcFace directly optimizes the geodesic distance margin by virtue of the exact correspondence between the angle and arc in the normalized hypersphere. We intuitively illustrate what happens in the 512-D space via analyzing the angle statistics between features and weights.

7.2 ArcFace achieves state-of-the-art performance on ten face recognition benchmarks including large-scale image and video datasets.

7.3Easy:  ArcFace only needs several lines of code as given in Algorithm 1 and is extremely easy to implement in the computational-graph-based deep learning frameworks, e.g. MxNet, Pytorch  and Tensor flow . Furthermore, ArcFace does not need to be combined with other loss functions in order to have stable performance, and can easily converge on any training datasets

7.4 Efficient: ArcFace only adds negligible computational
complexity during training. Current GPUs can easily support millions of identities for training and the model parallel strategy can easily support many more identities.
    
    
2. SoftMax Loss Function: 

![Untitled](ArcFace%20Additive%20Angular%20Margin%20Loss%20for%20Deep%20Face%20bdf05b9a25194896bfa14d410fc9d4c9/Untitled%201.png)

x(i) belongs to R(d) denotes deep feature of the i(th) sample belonging to the y(i)(th) class.

![Untitled](ArcFace%20Additive%20Angular%20Margin%20Loss%20for%20Deep%20Face%20bdf05b9a25194896bfa14d410fc9d4c9/Untitled%202.png)

Embedding feature are distributed around each feature on hypersphere, we add an additive angular margin penalty m between x(i) and w(y).

![Untitled](ArcFace%20Additive%20Angular%20Margin%20Loss%20for%20Deep%20Face%20bdf05b9a25194896bfa14d410fc9d4c9/Untitled%203.png)

1. Comparison between SphereFace and CosFace

![Untitled](ArcFace%20Additive%20Angular%20Margin%20Loss%20for%20Deep%20Face%20bdf05b9a25194896bfa14d410fc9d4c9/Untitled%204.png)

By combining all of the margin penalties, we implement SphereFace, ArcFace and CosFace in united framework with m1, m2,m3 as the hyperparameters.

![Untitled](ArcFace%20Additive%20Angular%20Margin%20Loss%20for%20Deep%20Face%20bdf05b9a25194896bfa14d410fc9d4c9/Untitled%205.png)

Geometric Difference loss functions:

![Untitled](ArcFace%20Additive%20Angular%20Margin%20Loss%20for%20Deep%20Face%20bdf05b9a25194896bfa14d410fc9d4c9/Untitled%206.png)

1. Comparison with other losses: 
    
    Intra Loss: Designed to improve intra class compactness by decreasing the angle/arc between the the sample and the ground truth center.
    
    ![Untitled](ArcFace%20Additive%20Angular%20Margin%20Loss%20for%20Deep%20Face%20bdf05b9a25194896bfa14d410fc9d4c9/Untitled%207.png)
    
    Inter Loss: It targets at enhancing inter-class discrepancy by increasing the angle/arc between different centers.
    
    ![Untitled](ArcFace%20Additive%20Angular%20Margin%20Loss%20for%20Deep%20Face%20bdf05b9a25194896bfa14d410fc9d4c9/Untitled%208.png)
    

1. Datasets and it's features used in the paper: 
    
    ![Untitled](ArcFace%20Additive%20Angular%20Margin%20Loss%20for%20Deep%20Face%20bdf05b9a25194896bfa14d410fc9d4c9/Untitled%209.png)
    
    11.1 Preprocessing of the dataset is done by normalization of face image by cropping in to (112 X 112) frame size.
    
    11.2 CNN architectures such as ResNet 50 and ResNet 100 are used.
    
    11.3 After the last convolutional layer we explore the BN -Dropout - FC-BN structure to get the final 512-D embedding feature
    
    11.4 All the experiments are implemented by MXNet. 
    
    11.5 Batch Size of 512 and trains model on four NVIDIA Tesla P40 (24 GB) GPUs.
    
    11.6 On CASIA, the learning rate starts from 0.1
    and is divided by 10 at 20K, 28K iterations. The training
    process is finished at 32K iterations. On MS1MV2, we divide the learning rate at 100K,160K iterations and finish at 180K iterations.
    
2. Study of Losses:
    
    ![Untitled](ArcFace%20Additive%20Angular%20Margin%20Loss%20for%20Deep%20Face%20bdf05b9a25194896bfa14d410fc9d4c9/Untitled%2010.png)
    
3. Evaluation Results:
    
    ArcFace trained on MS1MV2 with ResNet100 beats
    the baselines (e.g. SphereFace and CosFace) by
    a significant margin on both LFW and YTF that the additive angular margin penalty can notably enhance the discriminative power of deeply learned features, demonstrating the effectiveness of ArcFace
    
    ![Untitled](ArcFace%20Additive%20Angular%20Margin%20Loss%20for%20Deep%20Face%20bdf05b9a25194896bfa14d410fc9d4c9/Untitled%2011.png)
    
    Results on Mega Face: The Mega Face dataset [12] includes
    1M images of 690K different individuals as the gallery set
    and 100K photos of 530 unique individuals from Face Scrub as the probe set. On Mega Face, there are two testing scenarios (identification and verification) under two protocols (large or small training set). The training set is defined as large if it contains more than 0.5M images.
    
    ![Untitled](ArcFace%20Additive%20Angular%20Margin%20Loss%20for%20Deep%20Face%20bdf05b9a25194896bfa14d410fc9d4c9/Untitled%2012.png)