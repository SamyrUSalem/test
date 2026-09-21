
Points of Attention

Training Speed Is Not Guaranteed to Improve.
Although LoRA significantly reduces the number of trainable parameters, this does not necessarily translate into proportionally faster training. Additional LoRA operations can introduce computational overhead. Therefore, training throughput and total training time should be measured experimentally rather than inferred from the number of trainable parameters. Artigo(1).pdf

Trainable Parameters Do Not Directly Represent Memory Usage.
A very small percentage of trainable parameters does not automatically imply an equally large reduction in GPU memory consumption. The survey emphasizes that trainable parameter count is an imperfect predictor of actual memory requirements. Artigo(1).pdf

LoRA Rank Selection.
The rank r controls the capacity and parameter efficiency of the LoRA adaptation. A very small rank reduces computational and storage requirements but may limit the model’s ability to adapt to the downstream task. Larger ranks increase adaptation capacity at the cost of additional trainable parameters and computation. The rank should therefore be treated as an important experimental hyperparameter.

Target Layer Selection.
The layers where LoRA is applied can significantly affect the trade-off between efficiency and performance. The paper discusses applying LoRA to attention projections such as Q/V, while also noting evidence that applying LoRA to all weight matrices can improve performance. Artigo.pdf For HuBERT, comparing attention-only LoRA against broader application to attention and feed-forward layers would therefore be important.

Hyperparameter Sensitivity.
Rank, learning rate, LoRA scaling factor, dropout, target modules, and training duration can influence the final results. Comparisons with Full Fine-Tuning should use controlled experimental conditions whenever possible.

Inference Configuration.
LoRA can either remain as a separate adapter or be merged into the original weights. When merged, the survey notes that reparameterization-based methods such as LoRA can achieve the same inference speed as regular fine-tuning. Keeping LoRA modules separate, however, can introduce inference overhead while providing greater modularity. Artigo(1).pdf

Evidence for HuBERT Must Be Validated Experimentally.
A particularly important limitation for your documentation is that the paper’s main experiments are conducted on T5 models rather than HuBERT. Therefore, the efficiency and performance results reported in the survey should not be assumed to transfer directly to a speech foundation model. The LoRA configuration should be benchmarked specifically on the HuBERT architecture and the intended downstream tasks.