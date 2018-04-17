<p align="center">
<b>Unpaired Image-to-Image Translation using Cycle-Consistent Adversarial Networks</b><br>
Jun-Yan Zhu*, Taesung Park*, Phillip Isola, Alexei A. Efros<br>
ICCV 2017<br>
(* denotes equal contribution) <br>
<a href="https://junyanz.github.io/CycleGAN/">Link to paper</a>
</p>

![Examples of image to image translation](https://github.com/antoinetlc/paper_summaries/blob/master/Papers/Unpaired_Image-to-Image_Translation_using_Cycle-Consistent_Adversarial_Networks_Zhu_et_al_ICCV_2017/Images/teaser.png)

### Context 

* The paper tackles the problem of image to image translation, i.e mapping an image to another image automatically without user intervention, using a set of **unpaired images**. Such problem often arises in computer graphics and vision. An example could be mapping a sketch to a drawing or changing a satellite image to a map.

* This work differs from the work of Isola et al., [Image-to-Image Translation with Conditional Adversarial Nets](https://github.com/antoinetlc/paper_summaries/blob/master/Papers/Image-to-Image_Translation_with_Conditional_Adversarial_Nets_Isola_et_al_CVPR17/Pix2Pix.md), in the sense that the dataset is made of unpaired images.

#### What are unpaired images ?

* *Paired images* consist of a set of couples of images (x, y). The goal of an image-to-image translation algorithm with a dataset of *paired images* is to learn the mapping from x to y knowing that x is the input and y is the output.

* *Unpaired images* consist of **two** sets of images X and Y taken from two probability distribution. The goal of an image-to-image translation algorithm with a dataset of *unpaired images* is to learn the mapping from X to Y with only separate samples of Xs and Ys. In this case, the mapping has to learn without knowing which x map to which y (in the dataset, some x in X might not have a corresponging y in Y).

* Datasets of unpaired images are more easily accessible, which makes the problem very important.

* See figure 2 of the paper for a good visual understanding of paired and unpaired image sets.

### Novelty and contributions :

* Unpaired image-to-image translations is a highly under constrained problem as a given x can be mapped to an infinite number of different y (the mapping does not have a target output). In order to impose that the output of the mapping is paired to the input in a meaningful way, the paper proposes train networks with cycle consistency. Such framework is not application dependent and can be applied to a wide range of problems. 

### How was it solved ?

* `Reconstruction loss` : the reconstruction loss is a sum of two terms : the conditional adversarial loss and a reconstruction loss using L1 distance between the target image and the image the generator creates. Using a L1 distance instead of L2 is prefered as L1 tends to gives less blurry results. The final loss function is :

![Loss function](https://github.com/antoinetlc/paper_summaries/blob/master/Papers/Image-to-Image_Translation_with_Conditional_Adversarial_Nets_Isola_et_al_CVPR17/Images/loss_function.png)

### Results

* Please refer to the paper to see a wide variety of results on many different type of image to image translation problems (see section 4)

* Christopher Hesse also made an interactive online demo available here : https://affinelayer.com/pixsrv/

### References

* [1] O. Ronneberger, P. Fischer, and T. Brox.   U-net:  Convoluional networks for biomedical image segmentation. In MICCAI, pages 234–241. Springer, 2015.
