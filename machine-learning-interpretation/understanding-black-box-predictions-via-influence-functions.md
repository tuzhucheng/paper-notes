---
title: Understanding Black-box Predictions via Influence Functions
header-includes:
    - \usepackage{mathtools}
---

Understanding Black-box Predictions via Influence Functions
===========================
\newcommand{\defeq}{\stackrel{\mathclap{\normalfont\mbox{def}}}{=}}

**Pang Wei Koh, Percy Liang**

These notes are based on the paper and video lecture from [YouTube](https://www.youtube.com/watch?v=0w9fLX_T6tY).

Most existing work on interpreting a model focuses on a fixing the model (characterized by its parameters) and trying to understand the behaviour of the fixed model. However, a model's behaviour comes from the training data. Instead of fixing the model, what if we instead trace back and find the data that is most responsible for the parameters of the model, given a prediction? The paper argues doing this helps with debugging model behaviour, debugging models, detecting dataset errors, and creating adversarial attacks.

To go about this, we can remove one training point at a time, retrain the model, and observe how the model parameters change. However, this is inefficient since models take a long time to train. Influence functions come to the rescue.

Influence functions were introduced in the 1970s in robust statistics. We have an estimator $T$ that acts on a distribution $F$ and want to know how does $T$ change if we perturb $F$.

Suppose we have training examples $z_1, ..., z_n$. Then for the new parameters we have

$$
\hat{\theta}_{\epsilon, z} \defeq \arg \min_{\theta \in \Theta} (1 - \epsilon) \frac{1}{n} \sum_{i=1}^n L(z_i, \theta) + \epsilon L(z, \theta)
$$

if $z$ is upweighted by some small $\epsilon$. If the loss is twice-differentiable and strictly convex around $\hat{\theta}$, we have a closed-form expression for the influence (see paper) and apply some tricks to efficiently calculate it. We skip those in the notes and brifly describe the applications.

## Understanding Model Behaviour

As an example, the authors train a Inception v3 network and SVM with RBF kernel on dog vs. fish from ImageNet. They pick a test image (fish) that both models got correct and found the two most helpful images that helped each model using influence. They were able to see that for the RBF SVM training images in which the object is far relative to the object position in the test image have little influence. In the Inception model, the distance didn't matter.

In the RBF SVM model, training images that fish close to the test image are helpful, while training images that are dog close to the test image are harmful. In the Inception model, dogs close to the test image can be extremely helpful.

## Adversarial Training Examples

Authors demonstrate a method to create adversarial training images that can flip a decision on a test image. For details, refer to the paper.

## Fixing Mislabeled Examples

Labels in the real world can be noisy and incorrect. Using influence functions, we can allow human labelers to focus on verifying the labels associated with training examples that actually matter. For details, refer to the paper.
