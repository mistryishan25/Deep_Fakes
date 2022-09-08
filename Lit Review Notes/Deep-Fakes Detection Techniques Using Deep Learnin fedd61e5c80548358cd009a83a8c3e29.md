# Deep-Fakes Detection Techniques Using Deep Learning: A Survey[10]

Files: https://www.scirp.org/pdf/jcc_2021051813373227.pdf
Person: Anonymous
Status: Read
Tags: Datasets, Image Fakes, Video Fakes
Type: Survey

Primarily concerns with the Deep Fake detection using RNNs, CNNs and LSTMs.

- Current research studies
    
    Generation Methods : 
    
    1. FakeApp - Similar structure like GANs - Autoencoder for constructing latent features and decoder to re-extract the human features
    2. [VGGFace](https://github.com/rcmalli/keras-vggface) - Improved by addding two extra layers - adversarial loss and perceptual loss.
    3. CycleGANs - **Unsupervised** method that uses cycle loss function to learn latent features.
    
    Detection Methods : 
    
    1. [Neural net based](https://dl.acm.org/doi/10.1145/3267357.3267367)  - 
    Based on pre-processing to capture statistical features.
    2. Deep CNN - 
    An initial deep layer network used to extract the features and then a fine tuning step (post processing, I believe) to make the face features suitable for detetction
    3. Forensics CNN -
    Introduced to tacke the problem of using same dataset for training and testing, as was the case with the previous 2 methods. It uses 2 pre-processing  steps - Gaussian Blur and Gaussian Noise. These steps intend to ignore "l**ow level high frequency"** clues in GAN images and improve "**high frequency pixel noise in lowl level pixel statistics** "
    4. Two stream Neural Networks - 
    Again one stream(network) for generation and other for steganalysis (obseving hidden patterns and noise residuals) as feature extractor.
    
    Video Detection Methods:
    
    1. Biological Signal Analysis : (supervised)
    One approach (CNN + RNN) uses "**blinking of the eye**". Hearthbeat is used by another.
    **Siamese network based architecture**- simulataneously extracting speech and face  modalities - **converted to vectors using modality embedding networks -OpenFace and pyAudioAnalysis.** Finally a [triplet loss function](https://medium.com/analytics-vidhya/triplet-loss-b9da35be21b8) is used.
        
        ![https://miro.medium.com/max/875/1*EgT2EhqKW5hVrNYX6Y-rKg.png](https://miro.medium.com/max/875/1*EgT2EhqKW5hVrNYX6Y-rKg.png)
        
    2. Spatial and Temporal Features Analysis:
    Using not only single video frames - but analyzing the temporal sequence between frames.Basically CNN → LSTM →Softmax 
    
    Recycle-GAN - Uses conditional adversarial networks to merge spatial and temporal data.
    
    Spatial Transformer Network(STN) - pre-processing → RNN → Classify
- Datasets
    1. DFDC
    2. DeepfakeTIMIT dataset -[https://www.idiap.ch/en/dataset/deepfaketimit](https://www.idiap.ch/en/dataset/deepfaketimit)
    3. Flickr-Faces-HQ, FFHQ - [https://github.com/NVlabs/stylegan](https://github.com/NVlabs/stylegan)
    4. 100K-Faces - [https://generated.photos/](https://generated.photos/)
    5. DFFD(Fake Face Dataset) - [https://github.com/NVlabs/ffhq-dataset](https://github.com/NVlabs/ffhq-dataset)
    6. CASIA-WebFace - [https://paperswithcode.com/dataset/casia-webface](https://paperswithcode.com/dataset/casia-webface)
    7. VGGFace2 - [https://www.tensorflow.org/datasets/catalog/vgg_face2](https://www.tensorflow.org/datasets/catalog/vgg_face2)
    8. The Eye Blinking Datest - [http://www.cs.albany.edu/∼lsw/downloads.html](http://www.cs.albany.edu/%E2%88%BClsw/downloads.html)