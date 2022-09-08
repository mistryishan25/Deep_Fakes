# Deepfake Videos in the Wild: Analysis and Detection

Files: https://arxiv.org/pdf/2103.04263.pdf
Person: Anonymous
Status: Read
Type: Paper

Abstract:
We collect and present the largest dataset of deepfake videos in the
wild, containing 1,869 videos from YouTube and Bilibili, and extract
over 4.8M frames of content. Second, we present a comprehensive
analysis of the growth patterns, popularity, creators, manipulation
strategies, and production methods of deepfake content in the realworld.
Third, we systematically evaluate existing defenses using our
new dataset, and observe that they are not ready for deployment in
the real-world. Fourth, we explore the potential for transfer learning
schemes and competition-winning techniques to improve defenses.

INTRODUCTION:
We introduce a new deepfake dataset called DF-W, comprised of
deepfake videos created and shared by the Internet community.We present a comprehensive analysis of the videos in DF-W. We
examine the differences in content between deepfake videos in
DF-W, and datasets released by the research community.We systematically evaluate the performance of state-of-the-art
deepfake detection schemes on videos in DF-W. We evaluate 7
deepfake detection schemes, including 5 supervised and 2 unsupervised
schemes. We find that all detection schemes perform
poorly on DF-W videos, with the best approach (CapsuleForensics,
a supervised approach) having an F1 score of only 77% in
catching deepfakes. This means that these existing detection
schemes are not ready for real-world deployment. Poor performance
can be attributed to distributional differences between
real-world deepfake videos, and those used to train existing detection
schemes. Failure cases can also be partially attributed to
racial bias, a well known problem with DNN-based facial analysis. We also attempt to interpret the classification decisions
using a state-of-the-art model interpretation scheme, called Integrated
Gradients . We leverage this tool to infer features
that can be used to either improve detection schemes, or create
more evasive deepfakes.We explore approaches to improve detection performance. Finally, to
improve detection performance on DF-W, we leverage a transfer
learning-based domain adaptation scheme, which shows promising
results on the DF-W dataset. However, domain adaptation
still requires a small number of deepfake videos from the target
distribution/domain (DF-W in this case). Therefore, the attacker
still has an upper hand, putting the defender in a difficult situation,
unless we come up with defenses that can generalize better.
We also investigate the performance of the winning DNN model
from Facebook’s DFDC competition. While this winning
model outperforms the existing models (without domain adaptation),
its performance on DF-W is still inadequate with an F1
score of 81% and low precision of 71%.

DEEPFAKE DATASETS:
our deepfake dataset called DFW,
contains deepfakes found in the wild (i.e., produced by the
Internet community). We also present details of existing deepfake
datasets produced by the academic/industry research community.

DF-W: Our New Deepfake Dataset:
Step 1: Searching and identifying potential deepfake videos.Step 2: Filtering and downloading videos
DF-W dataset. Using the above methodology, we prepared the
DF-W dataset containing a total of 1,869 deepfake videos, of which
1,062 are from YouTube, and 807 are from Bilibili. Dataset statistics
are shown in Table 1. In total, our dataset contains over 48 hours of
video content, with over 4.8 million frames (extracted at the native
frame rate). Video resolutions range from (360 x 360) to a high
resolution of (2560 x 1080). Additionally, we collected the following
metadata for each video using the YouTube API and Bilibili HTML
source: publishing date, number of views, number of subscribers
for the channel (content creator), and the total number of videos
associated with the video’s channel.

Research Community Datasets:
We additionally prepare a dataset representing all
the research community datasets, by sampling deepfake videos from
the 6 datasets, and call it the DF-R dataset. This simplifies analysis,enabling us to compare detection performance on the DF-Wdataset,
with a single deepfake dataset representing the research community.
We strive to keep the number of deepfake videos similar to that in
the DF-W dataset, and therefore sample 500 random videos (or less
if fewer are available) from the deepfake and real classes of each
research community dataset. The DF-R dataset contains a total of
2,369 deepfake videos, and 2,316 real videos.

DETECTING DEEPFAKES:
supervised methods
(1) CapsuleForensics
(2) Xception
(3) MesoNet
(4) Multi-Task
(5) VA
Unsupervised methods
(1) FWA
(2) DSP-FWA

CONCLUSION:
We presented a measurement and analysis study of deepfake videos
found in the wild. We collected and curated a novel dataset, DF-W,
comprising 1,869 deepfake videos—the largest dataset of real-world
deepfake videos to date. Our analysis revealed that DF-W videos
differ from the deepfake videos in existing research community
datasets in terms of content, and generation methods used, raising
new challenges for detection of deepfake videos in the wild. We
further systematically evaluated multiple state-of-the-art deepfake
detection schemes on DF-W, revealing poor detection performance.
This suggests a distributional difference between in-the-wild deepfakes,
and deepfakes in research community datasets. We also attributed
detection failures to be related to racial biases, and using
model interpretation schemes, we investigated features that can be
leveraged to either improve or evade detection. Finally, we show
that domain adaptation via transfer learning, which retrains the
model on a small set (50 videos) of DF-W videos, is a promising
approach to improving performance on DF-W. Overall, our findings
indicate a need for incorporating in-the-wild deepfake videos into
future work.