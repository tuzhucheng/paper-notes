One Model to Learn Them All
===========================

Different problems require specific architectures and extensive effort to tune. This paper presents a single model concurrently trained on multiple datasets. If a building block is not required for a task, adding it doesn't hurt and often improves performance.

Two Key Insights
----------------

* "Small modality-specific sub-networks convert into a unified representation and back from it"

Modality refers to different domains like images, speech, and text. Inputs from different domains have different sizes, making it necessary to use sub-networks to convert them into a joint unified representation. Sub-networks should be minimal and promote feature extraction - the domain agnostic "body" that all the sub-networks lead into is where the heavy computation happens.

    * Unified representation is variable size to avoid limiting performance.
    * Different tasks from same domain share modality nets - encourages generalization.

Unified representation needs to be converted back to output space.

* "Computational blocks of different kinds are crucial for good results on various problems"

    * Depthwise-separable convolution from Xception (for vision)
    * Attention mechanism (for language)
    * Sparsely-gated mixture-of-experts (for language)

TODO: Add mores notes on model architecture when the time comes.

