### VQA-EC-601

# Visual Question Answering

### Ajay Krishna Anand

## Problem Statement and Applications

Visual Question Answering (VQA) is a practical application for machine learning that allows computer systems to answer general questions about the content of an image. VQA combines vision and language processing with high-level reasoning.

Systems capable of answering general and diverse questions about the visual environment have direct practical utility in a wide range of applications: from digital personal assistants to aids for the visually impaired and robotics. 

A typical instance of VQA involves the provision of an image with an associated plain text question (see examples in Figure 1). The task for the system is to determine the correct answer to the question and provide an answer; typically in a few words or a short phrase. This task, while seemingly trivial for human beings, spans the fields of computer vision and natural language processing (NLP) since it requires both the comprehension of the question and the parsing of the visual elements in the image.

Another motivation for the study of VQA is its applications. A system that is able to process an image and answer based on it, such as a personal assistance, in surveillance, in robotics, or as a helping tool/bot for visually impaired. The recent interest in VQA originates from the latest advances in computer vision on low- and mid-level tasks. Deep learning has now been applied to virtually every problem imaginable in computer vision, and convolutional neural networks (CNNs) are approaching human performance in tasks such as image segmentation or object recognition. The success of deep learning on perceptual tasks drove an increasing enthusiasm for high-level tasks. VQA particularly embodies this confidence in achieving high-level image understanding. [1]

## Current Approach and Research

The common approach to VQA is to train a deep neural network with supervision which maps the given image and question to a relative scoring of candidate answers. The main idea is to learn a joint embedding of the visual and textual inputs. First, the image and the question are processed independently to obtain separate vector representations. Those features are then are mapped with learned functions to a joint space, then combined and fed to an output stage. We examine each of those elements next.

![image](https://user-images.githubusercontent.com/113374250/191607810-4f593a71-3642-4958-9b44-4f716729b08c.png)

### Image Encoding
In the computer vision (CV) part, the input image is generally processed with convolutional neural networks (CNN) to extract the features of the image. This CNN is typically a standard network architecture that has been pretrained to perform image recognition [2]. In comparison to classical handcrafted image features such as scale-invariant feature transform (commonly known as SIFT) [3] or histogram of oriented gradients (commonly known as HOG) [4], CNN features provide higher-level representations of the contents of the image, and are naturally produced as a fixed-size vector. 

### Language/Question Encoding
On the Natural Language Processing (NLP) side, the input question is also processed for fixed size representation. Initially, the ith word of the question is represented by an index xQi in the input vocabulary. Each word is then turned into a vector. This uses a mapping implemented as a lookup table W[·] that associates the index of any word of the input vocabulary to a learned vector [1].
Recurrent Neural Network (RNN) is also used used frequent to retrive the word features.

### Combination of both Image and Question Encoding
The feature vectors of both image and the question is each passed via a learned function before combined. The idea here is to map the features to a joint space, in which distances between both modalities become comparable. The learned function is then added as additional layers into the neural network. The mapped features are then combined before being fed to the output stage. [1]

### Output
The output stage of a VQA system can be seen either as a generation or as a classification task. The generation of a free-form answer has the advantage of being able to compose complex sentences. In practice however, such a model is difficult to learn [6]. The combined features (From above.) are passed to a classifier over candidate answers sets. The classifier assigns score to each candidate answer, and the top-ranked one is returned as the final output.

With a lot of cuncurrent researches going on in VQA, the performance has increased from 58% to 70% today. But there are still enough drawbacks and future works to look into. Some of the issues that exist in the VQA are dataset biases, unable to handle unknown and novel words and answering questions from external knowledge.
Several studies have recently pointed out a fundamental issue with VQA data sets [25]. The text questions alone often provide strong cues that can be sufficient to answer them correctly, with no regards to the contents of the input image. These issues of data sets biases has already been identified and there are many attempts to solve it like (balanced data sets). 
Even for the cases of unknown/ novel word errors, many recent works and papers has been published trying to solve them. Solutions specifically involve asking/including words that have not been seen in any training question.

## Open Source

On a kaggle competition and github forums, Liangke Gui and Borui Wang has proposed a multimodal task of VQA called Knowledge Augmented Transformer that acheives 6% better performance on the existing results. Their approach integrates implicit and explicit knowledge in an encoder-decoder architecture, while still jointly reasoning over both knowledge sources during answer generation.

![image](https://user-images.githubusercontent.com/113374250/191636234-6ebcf9d0-3825-4f53-8115-9e0df2d28562.png)

Their KAT model uses a contrastive-learning-based module to retrieve knowledge entries from an explicit knowledge base, and uses GPT-3 to retrieve implicit knowledge with supporting evidence. The integration of knowledge is processed by the respective encoder transformer, and jointly with reasoning module and the decoder transformer as an end-to-end training with the answer generation.

![image](https://user-images.githubusercontent.com/113374250/191636435-9c449cd8-c2d1-41b3-a001-91ed21dc7480.png)

Fig. Some examples from OK-VQA dataset that our model generates answers by jointly reasoning over both implicit and explicit knowledge.

![image](https://user-images.githubusercontent.com/113374250/191637623-88c7d9e3-c13e-439b-86dd-3ad86f2b1485.png)

Their table shows results of OK-VQA comparing to standard baselines show that thier KAT (large size) model achieves stateof-the-art performance on OK-VQA full testing set. It is important (see table sections) to compare methods based on their access to increasingly large implicit sources of knowledge and utilization of explicit knowledge sources. Their five KAT models variants make the relative importance of these decisions explicit. 

## Conclusion
The field of Deep Learning, Computer Vision and Natural Language Processing is vast, and combining them to solve real world problems is a promising future for us. Despite shortcomings of current practices for both training and evaluating VQA systems, we have identified a number of promising research avenues that could potentially bring future breakthroughs for both VQA and for the general objective of visual scene understanding.

## References

[1] D. Teney, Q. Wu and A. van den Hengel, "Visual Question Answering: A Tutorial," in IEEE Signal Processing Magazine, vol. 34, no. 6, pp. 63-75, Nov. 2017, doi: 10.1109/MSP.2017.2739826.

[2] A. Krizhevsky, J. Sutskever and G.E. Hinton, "Imagenet classification with deep convolutional neural networks", Proc. Advances in Neural Information Processing Systems, pp. 0106-1114, 2012.

[3] D.G. Lowe, "Object recognition from local scale-invariant features", Proc. IEEE Int. Conf. Computer Vision, vol. 2, pp. 1150-1157, 1999.

[5] N. Dalal and B. Triggs, "Histograms of oriented gradients for human detection", Proc. IEEE Conf. Computer Vision and Pattern Recognition, vol. 1, pp. 886-893, 2005.

[6] H. Gao, J. Mao, J. Zhou, Z. Huang, L. Wang and W. Xu, "Are you talking to a machine? Data set and methods for multilingual image question answering", Proc. Advances in Neural Information Processing Systems, pp. 2296-2304, 2015.

[7] Y. Goyal, T. Khot, D. Summers-Stay, D. Batra and D. Parikh, "Making the V in VQA matter: Elevating the role of image understanding in visual question answering", Proc. IEEE Conf. Comp. Vis. Patt. Recogn. (CVPR), 2017.




