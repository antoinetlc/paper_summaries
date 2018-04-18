<p align="center">
<b>Unpaired Image-to-Image Translation using Cycle-Consistent Adversarial Networks</b><br>
Jun-Yan Zhu*, Taesung Park*, Phillip Isola, Alexei A. Efros<br>
ICCV 2017<br>
(* denotes equal contribution) <br>
<a href="https://junyanz.github.io/CycleGAN/">Link to paper</a>
</p>

![Examples of image to image translation](https://github.com/antoinetlc/paper_summaries/blob/master/Papers/Unpaired_Image-to-Image_Translation_using_Cycle-Consistent_Adversarial_Networks_Zhu_et_al_ICCV_2017/Images/teaser.png)

### Context 

* The paper tackles the problem of image-to-image translation, i.e mapping an image to another image automatically without user intervention, using a set of **unpaired images**. Such a problem often arises in computer graphics and vision. An example could be mapping a sketch to a drawing or changing a satellite image to a map.

* This work differs from the work of Isola et al., [Image-to-Image Translation with Conditional Adversarial Nets](https://github.com/antoinetlc/paper_summaries/blob/master/Papers/Image-to-Image_Translation_with_Conditional_Adversarial_Nets_Isola_et_al_CVPR17/Pix2Pix.md), in the sense that the dataset is made of unpaired images.

#### What are unpaired images ?

* A dataset of *Paired images* consist of couples of images (x, y) that are linked to each other. The goal of an image-to-image translation algorithm with a dataset of *paired images* is to learn the mapping from x to y knowing that x is the input and y is the output.

* A dataset of *unpaired images* consist of **two** separate sets of images X and Y. The goal of an image-to-image translation algorithm with a dataset of *unpaired images* is to learn a mapping from X to Y without knowing which x should map to which y. In this case, the algorithm has to understand the specificity of the domain X and the domain Y and pair its input (in X) to an output (in Y) in a meaningful way.

* Pairing images can be a expensive process, therefore datasets of unpaired images are more widely accessible. This makes the problem very important in unsupervised learning.

* See figure 2 of the paper for a good visual understanding of paired and unpaired image sets.

### Novelty and contributions :

* Unpaired image-to-image translations is a highly under constrained problem as a given x can be mapped to an infinite number of different y (the mapping does not have a target output). In order to impose that the output of the mapping is paired to the input in a meaningful way, the paper proposes to train networks with a cycle consistency. Such framework is not application dependent and can be applied to a wide range of problems. 

### Approach taken

* The approach that the authors take is to train two sets of generative adversarial networks. The first one denoted (G, D_Y) (G is the generator and D_Y its corresponding discriminator) learns a mapping from the domain X to Y. The second one denoted (F, D_X) (F is the generator and D_X its corresponding discriminator) learns a mapping from the domain Y to X. These two networks are trained simultaneously in such a way that the two generators are inverse mappings of each other (also called cycle consistency - see figure 4 of the paper for a visual understanding of cycle consistency).

* `Loss function`. The loss function is made of two main terms : the adversarial losses for the mappings G and F and the cycle consistency losses.

  * `Adversarial losses`. The adversarial losses allow the training of the mappings G and F with their corresponding discriminator. This way G learns to map images from the domain X to the domain Y and conversely for F. The adversarial loss for the couple (G, D_Y) is given by the equation below. The couple (F, D_X) has a similar loss. Note that the authors obtained better results with a least-squares adversarial loss.

![Adversarial loss](https://github.com/antoinetlc/paper_summaries/blob/master/Papers/Unpaired_Image-to-Image_Translation_using_Cycle-Consistent_Adversarial_Networks_Zhu_et_al_ICCV_2017/Images/adversarial_loss.png)

  * `Cycle consistency`.  The cycle consistency losses are necessary, so that the mappings G and F try to pair their input and output in a meaningful way (G and F also become inverse of each other). Without cycle consistency the mapping G could match an input to any image in the domain Y. The cycle consistency loss is divided in two terms : the *forward cycle consistency* and the *backward cycle consistency*. Note that both directions are necessary to get F and G that act as inverses of each other (see figure 7 of the paper to see results with only a single direction).

![Cycle consistency loss](https://github.com/antoinetlc/paper_summaries/blob/master/Papers/Unpaired_Image-to-Image_Translation_using_Cycle-Consistent_Adversarial_Networks_Zhu_et_al_ICCV_2017/Images/cycle_consistency.png)

* The final optimization problem is :

![Optimization problem](https://github.com/antoinetlc/paper_summaries/blob/master/Papers/Unpaired_Image-to-Image_Translation_using_Cycle-Consistent_Adversarial_Networks_Zhu_et_al_ICCV_2017/Images/optimization_problem.png)

* `Network architecture`. The authors used CNNs for the generators and discriminator. In particular the discriminator is a patchGAN classifying wether 70x70 overlapping patches look real or not. The generator is based on Johnson et al. architecture [1]

### Results

* Please refer to the paper (pages 11 to 16) or the author's website for more results and limitations.

### References

* [1] Johnson, A. Alahi, and L. Fei-Fei. Perceptual losses for real-time style transfer and super-resolution. In ECCV, pages 694–711. Springer, 2016.
