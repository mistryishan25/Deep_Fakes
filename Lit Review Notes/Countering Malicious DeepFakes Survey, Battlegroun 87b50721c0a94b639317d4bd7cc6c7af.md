# Countering Malicious DeepFakes: Survey, Battleground, and Horizon[20]

Files: https://arxiv.org/pdf/2103.00218v1.pdf
Person: Anonymous, Anonymous
Status: Read
Tags: Facial DeepFakes
Type: Survey

Some Deep-Fakes pose more serious threat - Identity Swap> expression swap and attribute manipulation>entire face synthesis(lowest coz no soft or hard biometrics changed)

- Deep-Fake Generation
    - Generation Methods
        1. Entire Face Synthesis - 
        Input - Random Vectors : Output - High Quality non-existent faces
        Target- not needed (latent vector manipulated for results)
        Examples - 
            1. DCGAN - First work that does CNN+GAN. Focuses on unsupervised learning - had problems like balancing discrimator and generator
            2. [WGAN](https://machinelearningmastery.com/how-to-implement-wasserstein-loss-for-generative-adversarial-networks/) - This took care of the balance and provided reasonable and efficient approximation of the EM distance.
            WGAN uses weight clipping to enforce a **Lipschitz constraint. To improve the weight clipping operation, they have proposed to penalize the norm of the gradient of the discriminator with respect to its input fake image.** The new designs train stably when generating high-quality home images
            3. BEGAN - Also an improved WGAN. To further balance
            the power of the discriminator against the generator, they have suggested **pairing an equilibrium enforcing method with a loss derived from the Wasserstein distance together.**
            4. CrammerGAN - Simply using Wasserstein probability can not
            **simultaneously satisfy sum invariance, scale sensitivity, and
            unbiased sample gradients.Hence came CrammerGANS. It combined the best of the Wasserstein and Kullback-Leibler divergences to propose the Cramér distance**.
            5. PGGAN - Focus on high res images. The images are starting from a low resolution and being detailed step by step with the new layers added in the model. This method is very reasonable in that it can speed up the training as well as greatly stabilize the GAN.
            6. BigGAN - generate high res diverse images. They have
            applied **orthogonal regularization to enforce the generator to be satisfied with a simple “truncation trick”**. Thus, the user
            can **control the trade-off between image fidelity and variety** by reducing the variance of the generator’s input.
            7. StyleGAN - Automatically learn the **unsupervised separation of high-level attributes** such as pose and human identity. The architecture
            also leads to **stochastic variation in the generated images** (e.g.,
            freckles, hair). Furthermore, it enables intuitive, scale-specific
            control of the synthesis. They have encouraged good conditioning in the mapping from latent codes to images by the new design of generator normalization, progressive growing,
            and generator regularization.
            8. Glow - a flowbased generative model that uses an invertible 1 × 1 convolution. The method is based on the theory that a generative
            model optimized towards the plain log-likelihood objective has
            the ability to generate efficient realistic-looking synthesis and
            manipulate large images.
        2. Attribute manipulation -
        Target - not needed (latent vector manipulated for results)
            
            It is known as face editing, which can
            not only modify simple face attributes such as hair color, bald,
            smile, but also retouch complex attributes like gender, age, etc
            
            Examples :
            
            1. IcGAN - extension of cGANs(Conditional GANs) . They
            have **evaluated encoders** to map a real image into a latent space
            and a conditional representation, which allows the **reconstruction and modification of arbitrary attributes** of real human face
            images
            2. StarGAN -As previous studies only did image to image translation only for 2 domains - which is cumbersome and time consuming, StarGAN was devised to perfom translation to multiple domains.  It allows simultaneous training of multiple
            different-domain datasets within a single network.
            3. StarGAN2 - Maintains diversity of generated images as well as scalability over multiple domains as obtained in StarGAN. They replaced StarGAN’s domain label with their domain-specific
            style code. To adapt the style code, they have proposed two
            modules: **a mapping network(transforms random noise into style codes) and a style encoder(extract style code form a given ref image).**
            4. GANimation - StarGAN had the limitation of the
            content of the datasets, it can only generate a discrete number of
            expressions. To address this we have a novel GAN condditoning method based on action units (AU) annotations.It defines the human expression with a continuous manifold of the anatomical facial
            movements. The magnitude of activation of each AU can be
            controlled independently. Different AUs can also be combined
            with each other with this method.
            5. AttGAN - Previous methods have attempted to establish an attributeindependent latent representation for further attribute editing.
            However, since the facial attributes are relevant, requesting for
            the invariance of the latent representation to the attributes is
            excessive. Therefore, simply forcing the attribute-independent
            constraint on the latent representation not only restricts its
            representation ability but also may result in information loss,
            which is harmful to the attribute editing. To solve this problem,
            AttGAN (He et al., 2019b) has removed the strict attributeindependent constraint from the latent representation. It just
            applies the attribute classification constraint to the generated
            image to guarantee the correctness of attribute manipulation.
            Meanwhile, it groups attribute classification constraint, reconstruction learning, and adversarial learning together for
            high-quality facial attribute editing.
            6. STGAN - Improvement of AttGAN has selectively taken the difference between target and source attribute vectors as the input of the model. They have enhanced attribute editing by adding a selective transfer unit that can adaptively select and modifying the encoder feature to the encoder-decoder
        3. Identity swap (Target -Video/Single face image )
        4. Expression Swap (Target is Video)
        5. Other methods
            1. Style Transfer - 
                1. GatedGAN uses gated networks to transfer multiple
                styles in a single model. They have added a gated transformer
                into the encoder-decoder
                2. AAMS has developed an attention-aware multistroke style transfer model. They have enabled using different
                brush strokes to render the diverse levels of detail. They also
                have coordinated spatial distribution of visual attention between the content image and stylized image.
            2. Inpainting - 
                1. ContextAtten -The new architecture
                proposed by them can synthesize novel image structures as
                well as explicitly utilize surrounding image features as references to make better predictions.
                2. SC-FEGAN - a novel image editing system that generates images with the free-form masks, sketches, and color
                provided by the users.
            3. Rendering - 
                1. CRN (a single feed-forward network, trained end-to-end with a direct regression objective) has proposed a rendering network to produce a photographic image with a two-dimensional
                semantic specification of the scene. 
                2. GauGAN has proposed a simple yet effective layer
                for synthesizing photo-realistic images with an input semantic
                layout. They have proposed to use a spatially-adaptive, learned
                transformation to modulate the activation in normalization layers with the input layout.
            4. Super Resolution -
                1. SAN has proposed a second-order attention network for more powerful feature expression and feature correlation learning.
            5. Detection evasive - 
                1. SDGAN has proposed using a spectral discriminator
                to simulate the frequency distribution of the real data when
                generating images.
                2. WUCGAN has shown common up-sampling methods are causing the inability of GANs to reproduce spectral distributions of real images correctly. To overcome this drawback, they have proposed to add a spectral regularization term to the training optimization objective
                
                It has been found  that narrowing the frequency domain gap can improve the image synthesis quality.
                
            6. De-identification 
                1. They mainly obfuscate identities in photos by the head replacement for data privacy.A good area for research!

- Deepfake detection
    1. Spatial Based - 
        1. Image Forensics based detection - Differences between synthesised faces and real faces are revealed in the chrominance components, especially in the residual domain. Idea was proposing to train a one-class classifier on real faces by leveraging the differences in the chrominance components for tackling the unseen GANs. However, performance against perturbation attacks like image transformations is unknown. Similarly in tackling fake videos, researchers borrowed ideas from traditional video forensic by leveraging the local motion features captured from real videos to spot the abnormality of manipulated videos
        2. DNN-based detection - Completely data driven by utilising DNN models by extracting spatial feaatures to improve effectiveness and generalization detection. Severely weak against adversarial attacks with additive noises. Existing studies to leverage DNN to identify deep fakes are categorised by 1) Improving  generalisation abilities, 2) Investigating artifact clues and 3) Empowering CNN models
        3. Obvious artifact clues - Generated deepfakes exhibit obvious artifacts due to limitations in AI and can be leveraged. A full convolutional approach is applied for training classifiers. Two vectors from the aforementioned two networks are compared for detecting the identity-to-identity discrepancies. This approach also has a good generalization ability across GANs
        4. Detection and localisation - By locating manipulated regions that provide evidence for forensics, it was found that the imperfection of upsampling methods exhibits obvious clues for detection and forgery localization where the manipulated area could be precisely marked.
        5. Facial image preprocessing - Some studies propose preprocessing the facial images before sending them to binary classifiers for discrimination..Layer-by-layer neuron behaviors provide more subtle features for capturing the differences between real and fake faces. This provides a new insight for spotting fake faces by monitoring third-party DNN-based neuron behaviors, which could be extended to other fields like fake speech detection.
    2. Frequency based - 
        1. GAN-based artifacts - Investigating imperfect designs of existing GANs which provides obvious signals, it was observed that the internal value of the generator is normalized which limits the frequency of saturated pixels. Then, a simple SVM-based classifier is trained to measure the frequency of saturated and under-exposed pixels in each facial image for discriminating fake faces.
        2. Frequency Domain - Severe artifacts introduced due to the upsampling techniques in GANs, to which a classifier with a simple linear model and a CNN based model can acheive promising results on the entire frequency spectrum.
    3. Biological Signal based - 
        1. Visual-audio inconsistency - Specific words give that involve in lips touching is found inconsistent in fake videos. Lip sync inconsistencies are strong but not solid evidence towards deep fakes
        2. Visual Inconsistency - Indicates that synthesized faces are inconsistent and unnatural. In noticing general behavioural patterns in humans and deepfakes, a lot of artifacts can be found
        3. Biological Signals in video - Biological signals like heartbeat rhythms and monitoring blood flow to observe subtle color changes in the skin
    4. Other Detectors-
        1. Leveraging distributed ledger technologies (DLT) to combat digital deception, user behavior clues like the eye-gaze for DeepFake detection. Finding the artifacts which exist in the specific facial region could improve the detection performance by a large margin than the entire face.
- DeepFake Evasion
    1. With the fast improvement of DeepFake finders, specialists begin focusing on plan techniques to dodge the phony faces being distinguished. 
    2. In particular, given a genuine or phony face, avoidance strategies map it to another one that can't be accurately arranged by the cutting edge DeepFake identifiers, stowing away the phony appearances from being found. 
    3. We can generally separate all techniques into three kinds.
        
        i) The first type is based on the adversarial attack. 
        
        ii) The second type of methods focus on removing the fake traces in the frequency domain. These methods mainly focus on the mismatching between real and fake faces in the frequency domain while neglecting other potential factors that may make fake faces be identified easily.
        
        iii) The third kind of methods regard evasion as a general image generation process and use advanced image filtering or generative models to mislead DeepFake detectors.
        
- Interactions between Detection and Generation