# Deep-Fake Forensics via An Adversarial Game[19]

Files: https://arxiv.org/pdf/2103.13567.pdf
Person: Anonymous
Status: Read
Tags: Adversarial Training, GAN
Type: Paper

Training with samples that are adversarially crafted to attack the classification models **improves the generalization ability** considerably.
They propose a new adversarial training method that attempts to blur out the specific artifacts, by **introducing pixel-wise Gaussian blurring models**.

Most models till now used handcrafted features - **noise variance analysis** and **digital shadow writing analysis** to detect deep fakes. CNNs' came along pretty well but problem of generalization and sensitivity to image quality - still persist.
Previous attempts of improving Generalization :

1.  A more generalizable deep face representation for achieving the goal, by introducing an auxiliary task of predicting face x-ray.
2. Some modified the network architecture and introduced an attention module for the task.
3. Auto-Encoders are also used.
- Previous attempts of Adversarial Training :
    
    Fast gradient sign method (FGSM) was proposed for improving the adversarial robustness.
    A multi-step scheme called projected gradient descent (PGD) was also proposed, enabling more powerful robustness than that obtained with FGSM and other similar methods.
    
- Traditional Adversarial learning revised -
    
    Assume that a classification model (e.g., the Deepfake detection model) attempts to minimize the prediction loss  $L(x, y; θ)$ for any given data $(x, y)$ (i.e., an image $x$ paired with its label $y$), in which  $\theta$  collects all learnable parameters in the classification model, $x \in \mathbb{R^{h \times w \times c }}$ (h, w, and c represent height, width, and number of channels of x, respectively).
    Normally we minimize the empirical risk $\sum_{(x,y)\in \mathbb{D}}[L(x,y;\theta)]$
    
    FSGM suggests to obtain adversarial sample by adding a scaled input-Gradient sign to the original Image i.e :
    
    $$
    x^{adv} = x + \epsilon \cdot sign(\nabla_{x}L(x,y;\theta)),
    $$
    
    The above equation is derived from an optimization problem maximizing the prediction loss of an input obtained by adding a perturbation (whose $l_\infin$ norm is no greater than ) to a clean image $x$. Adversarial training plays a zero-sum game which includes an auxiliary process that generates adversarial examples which maximizes the classification loss. The generated adversarial examples can be used instead of the original benign examples or in combination with them for training. For the original images only scenario, we had
    
    $$
    \min_{\theta}\sum_{(x,y)\in \mathbb{D}} \max_{\delta \in \mathbb{S}} L(x + \delta,y;\theta),
    $$
    
    Now for the combination examples : 
    
    $$
    \min_{\theta}\sum_{(x,y)\in \mathbb{D}} L(x,y;\theta)+\lambda \cdot\max_{\delta \in \mathbb{S}} L(x + \delta,y;\theta).
    $$
    
    For $\mathbb{S \subseteq {R^{h \times w \times c }} }$ to constrain the noise/disturbance with respect to the clean image. 
    
- Spatial Adversarial Learning
    
    Another method includes using calculate a**n adversarial optical flow** to **spatially transform each pixel** of the clean images accordingly.
    
    Let us use $x_{i,j}$ to represent the pixel on the i-th row and j-th column of the original image, an adversarial optical flow vector $f_{i,j} := (\triangle u_{i,j},\triangle v_{i,j})$ is learned in the method to transform $x_{i,j}$ to the corresponding position $(i',j') = (i+\triangle u_{i,j},j+\triangle v_{i,j})$on the adversarial image $x^{adv}$.Such Training is called Spatial Transformed Adversarial Learning(SAT).
    
- Blurring Adversarial Training
    
    Specifically, given an input image $x$ whose height, width, and number of
    channels are $h, w$ and c, respectively, we obtain $x^{adv}$ by performing pixel-wise Gaussian blur on x. We use $x^{adv}_{i.j}$  to represent the $(i, j)$-th pixel of $x^{
    adv}$, and we attempt to learn a single-channel map $\sigma^{adv}$ with a size of $h × w$, each of whose entries (e.g., $\sigma^{adv}_{i,j}$ ) represents the standard deviation of a Gaussian kernel to be applied to the region centered
    at the corresponding pixel of image $x$, i.e $x_{i,j}$.
    
    $$
    G_{i,j} (u, v) = \frac{1}{2π(\sigma^{adv}_{i,j})^2} exp
    (−
    \frac{u^2 + v^2}
    {2(\sigma^{adv}_{i,j})\\^2})
    ,
    $$
    
    $$
    x^{adv}_{i.j} =  \langle G_{i,j},\gamma(x_{i,j},k) \rangle,
    $$
    
    Here,  $u$ and $v$ represent the relative coordinates to the centre
    pixel in $γ(x_{i,j} , k)$ - vectorization leads to efficient computation.
    
    $σ^{adv}$ controls the blurriness $⇒$ Larger entries of $σ^{adv}$ should lead to more blurry images and leave less obvious artifacts from the deepfake
    generator, while on the contrary, smaller entries of $σ^{adv}$ leave
    more obvious artifacts for the classification model to learn.
    
    We have $x^{adv}$ $\rightarrow$ $x$, as all the entries of $\sigma^{adv}$ $\rightarrow 0$
    
    The update rule is similar to FGSM : 
    
    $\sigma
    ^{adv} = \sigma + \epsilon · \nabla_\sigma L(x^{
    adv}, y; \theta),$
    
    Again vectorization would make the process of making updates easier.
    
- Generative Adversarial Training
    
    $$
    \min_{θ_D} \max_{θ_G}\sum_{
    (x,y)\in \mathbb{D}}L(x, y; \theta _D) + \sum_{
    (x,y)\in \mathbb{D}}
    L(G(x; \theta_{G}), y; \theta_{D}),
    $$
    

The introduced generator $G$ can also be considered as an enhancement model for the original deepfake generator(s). The optimization problem above,  allows to train a generator $G$ whose goal is opposite to the deepfake detection model, to remove obvious artifacts and synthesize more realistic deepfakes that can **invalidate** the deepfake detection model.