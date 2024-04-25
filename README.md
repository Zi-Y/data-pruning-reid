# A Comprehensive Data Pruning Approach for Object Re-identification
This is the repository for TMLR paper [Data Pruning Can Do More: A Comprehensive Data Pruning Approach for Object Re-identification](https://openreview.net/pdf?id=vxxi7xzzn7)

### 1.Introduction
ReID datasets generally present two issues: 
<ol>
  <li>Less informative samples</li>
  <li>Noisy labels and outlier samples</li>
</ol>
To address these issues, we propose a comprehensive data pruning approach 
and apply it to ReID tasks. Our method not only prunes less informative samples more efficiently, 
but also corrects mislabeled samples and removes outliers in an end-to-end framework. 
We hypothesize that instead of quantifying sample importance using discrete events 
or coarse inter-class relations during training, 
fully leveraging the logit trajectory offers more insights. 
Accordingly, we propose a novel data pruning metric by fully utilizing 
the logit trajectory during training.


![pipline](https://raw.githubusercontent.com/Zi-Y/data-pruning-reid/main/figures/pipline.jpg)
* **Figure 1**: The workflow of data pruning. Our data pruning approach not only identifies 
___less important___ samples, but also rectifies ___mislabeled___ samples and 
removes ___outliers___ (boxes highlighted in grey). Figure (c) demonstrates 
an example of our method, where all images are from the same person (id 630, MSMT17 dataset). 
Our approach serves as a _pre-processing_ step, reducing the dataset size to save storage 
and training costs of ReID models while having minimal impact on their accuracy.



![Logit_trajectories](https://raw.githubusercontent.com/Zi-Y/data-pruning-reid/main/figures/Logit_trajectories.jpg)
* **Figure 2**: Logit trajectories for three samples (i.e., the evolution of the log probabilities of each sample
belonging to each class over the course of training): (a) easy sample, (b) hard sample and (c) harder sample.
There are three classes in total and each logit trajectory corresponds to one of such classes. The difference
between the logits for each class can reflect the level of difficulty of this sample. In general, the more
difficult the sample, the more important it is. The forgetting scores cannot distinguish (a) and (b), while the
EL2N score relies solely on the model’s prediction at the last epoch (thus without considering the history
or “training dynamics”), hence it cannot differentiate between (b) and (c). Our approach fully exploits the
training dynamics of a sample by utilizing the average logits values over all epochs to generate a more robust
soft label. Then, the entropy of this soft label is employed to summarize the importance of a sample. 




![examples](https://raw.githubusercontent.com/Zi-Y/data-pruning-reid/main/figures/examples.jpg)
* **Figure 3**: Illustration of the generated soft labels averaged over 12 training epochs for different sample types
(a)–(d) and their entropies. Multi-target coexistence (d) is one such type of outlier. We show the top 3
identities. Notably, our soft label can accurately indicate the ground-truth label of the mislabeled sample (c)
without being influenced by the erroneous label. Images are from Market1501 dataset.


