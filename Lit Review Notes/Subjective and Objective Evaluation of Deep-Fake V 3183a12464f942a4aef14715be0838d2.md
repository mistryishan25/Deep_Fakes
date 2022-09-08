# Subjective and Objective Evaluation of Deep-Fake Videos[5]

Files: http://publications.idiap.ch/downloads/papers/2021/Korshunov_ICASSP_2021.pdf
Person: Anonymous
Status: Read
Tags: Image Fakes
Type: Paper

60 images were tested, including both the real and the fakes. The original FDFC dataset contains only fake/real classification but the experiment has defined 5 new categories(Very Easy - Easy - Moderate - Difficult - Very Difficult)  

- AIM :
    
    This paper, presents a subjective study, which, using 60 na¨ıve subjects, evaluates how hard it is for humans to see if a video is a deepfake or not.
    
    SOTA Models evaluated -Xception and EfficientNet (B4 variant) neural network models pre-trained on two other public databases:
    
    1. Google and Jiqsaw subset from FaceForensics++ 
    2. CelebDF v2 dataset
- Datasets Mentioned
    1. VidTIMIT - [https://github.com/deepfakes/faceswap](https://github.com/deepfakes/faceswap)  
    2. Google and Jiqsaw subset from FaceForensics++
    3. CelebDF v2 dataset
    
    FaceForensics database
    
- Data and Subjective Evaluation -
    
    The subjective evaluation, to gauge human accuracy in detecting Deep-Fakes, was conducted using **QualityCrowd 2 framework**  designed for crowdsourcing-based. It claims fairness as the algorithm uses face sections tso identify and hence the humans are also shown the same facial highlights along with the video. Furthermore, **to evaluate the ‘trustworthiness’** of the subjects, we used the **‘honeypot’ method** [20, 21] to filter out scores from people who did not pay attention, ending up with 18.66 answers per video on average.
    
    To check **whether the difference between videos from the
    five deepfake categories is statistically significant** based on
    the subjective scores, we performed **ANOVA test**
    
- Evaluation of Algorithms-
    
    If evaluated on the test sets of the same
    databases they were trained on, both Xception and EfficientNet models demonstrate high accutacy with the area under
    the curve (AUC) metric equal to almost 100% in all cases.
    
    To compute the performance accuracy, we need to select the threshold. We chose the threshold corresponding to the attack presentation classification error rate (APCER) of 10%, selected on the development set of the respective database.
    
     APCER **** measures the proportion of attacks, deepfakes in this case, that are incorrectly classified as bonafide or original videos. The counterpart metric is bona fide presentation classification error rate (BPCER), which measures the proportion of incorrectly classified original videos.
    
    $$
    APCER = \frac{FP}{TN + FP}
    $$
    
    APCER = FP / (TN + FP)
    
    - Normal Presentation Classification Error Rate (NPCER ):
    
    NPCER = FN/(FN + TP)
    
    - Average Classification Error Rate (ACER):
    
    ACER = (APCER + NPCER) / 2
    
    - False Positive Rate (FPR):
    
    FPR = FP / (FP + TN)
    
    - True Positive Rate (TPR):
    
    TPR = TP / (TP + FN)
    
    Main results establised were:
    
    1. The accuracy of the algorithms have no
    correlation to the visual appearance of deepfakes.
    2. We can then notice that human subjects are significantly more accurate at detecting these videos with AUC value of 87.47%