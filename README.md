# Circuits Reading List 

## Demonstrational Work on Circuits
> Justifies the usefulness of circuits as they allow us to:
> 1. visualise the behaviour of specific submodules that causally contribute to task efficacy, demystifying internal computation
> 2. intervene on behaviours in surgical ways

- [Interpretability in the Wild: A Circuit for Indirect Object Identification in GPT-2 Small](https://arxiv.org/abs/2211.00593)
- [How Does GPT-2 Compute Greater-Than? Interpreting Mathematical Abilities in a Pre-Trained Language Model](https://arxiv.org/abs/2305.00586)
- [Does Circuit Analysis Interpretability Scale? Evidence from Multiple Choice Capabilities in Chinchilla](https://arxiv.org/abs/2307.09458)

## Circuit Discovery Methods

### Traditional Circuit Discovery

- [Towards Automated Circuit Discovery for Mechanistic Interpretability (ACDC)](https://arxiv.org/abs/2304.14997)

- [Attribution Patching Outperforms Automated Circuit Discovery (EAP)](https://arxiv.org/abs/2310.10348)
  - less accurate than activation patching, but faster

- [Finding Transformer Circuits with Edge Pruning (Differential Masking)](https://arxiv.org/abs/2407.00886)

### Sparse Autoencoder (SAE)-based Feature Circuits
> Expresses the output of each submodule as a sparse combination of transformed directions in residual stream space (c.f. "feature")  
> Sparsity allows us to interpret the output, and thus the function of each submodule, without needing to craft our own hypotheses

- [Sparse Feature Circuits: Discovering and Editing Interpretable Causal Graphs in Language Models](https://arxiv.org/abs/2403.19647)
- Feature interpretability enables SHIFT, which surgically removes spurious features to improve circuit faithfulness.
  - For an application, see [Scaling Sparse Feature Circuits For Studying In-Context Learning](https://arxiv.org/pdf/2504.13756)

### Transcoders
> Learns to decompose the MLP activations of a model into a set of sparse features, deriving *input-invariant* feature circuits.

- [Transcoders Find Interpretable LLM Feature Circuits](https://arxiv.org/abs/2406.11944)

- [Transformer Circuits Thread - Circuit Tracing: Revealing Computational Graphs in Language Models](https://transformer-circuits.pub/2025/attribution-graphs/methods.html)

### Sheaf Discovery: Combined Edge-Weight Pruning
> Finds "sheaves" (edge & weight-pruned sets) with better task fidelity than traditional circuits.
- [Sheaf Discovery with Joint Computation Graph Pruning and Flexible Granularity](https://arxiv.org/pdf/2407.03779v2)

## Faithfulness & critiques of circuit discovery

- [Transformer Circuit Faithfulness Metrics Are Not Robust](https://openreview.net/pdf?id=zSf8PJyQb2)
  - Finds that faithfulness metrics are sensitive to small changes in ablation methodology and task setups, calling into question the generalizability of discovered circuits.

- [Have Faith in Faithfulness: Going Beyond Circuit Overlap When Finding Model Mechanisms](https://arxiv.org/abs/2403.17806)
  - Argues that high overlap between discovered circuits and “ground truth” paths is not enough; compares different ablation/patching-style faithfulness tests and shows they can disagree.

- [Rethinking Circuit Completeness in Language Models: AND, OR, and ADDER Gates](https://arxiv.org/abs/2505.10039)
  - Treats circuits as compositions of logical gates and shows that common methods systematically miss OR-like structures, which are important for applications such as unlearning and can be guaranteed through finding complete circuits.

## Phenomenon-specific breakdown of circuit studies

Fine-tuning:
- [Fine-Tuning Enhances Existing Mechanisms: A Case Study on Entity Tracking](https://arxiv.org/abs/2402.14811)

Multi-linguality:
- [On the Similarity of Circuits across Languages: a Case Study on the Subject-verb Agreement Task](https://arxiv.org/abs/2410.06496)

Multi-modality: 
- [Same Task, Different Circuits: Disentangling
Modality-Specific Mechanisms in VLMs](https://arxiv.org/pdf/2506.09047)

Factual Recall: 
- [Knowledge Circuits in Pretrained Transformers](https://arxiv.org/abs/2405.17969)

- [How do LLMs acquire new knowledge? a knowledge circuits perspective on continual pre-training](https://arxiv.org/abs/2502.11196)

- [Discovering Knowledge-Critical Subnetworks in Pretrained Language Models](https://arxiv.org/abs/2310.03084)

Answer extraction and attribution:
- [On Mechanistic Circuits for Extractive Question-Answering](https://arxiv.org/pdf/2502.08059)

Discourse Relations: 
- [How Do Language Models Understand Discourse Relations? Discursive Circuits for Coherent Understanding of Discourse Relations](https://arxiv.org/abs/2510.11210)

## Compositionality and modularity
> Preliminary results show that certain subcircuits are reused across tasks, while serving nearly the same purpose.

- [Break It Down: Evidence for Structural Compositionality in Neural Networks](https://arxiv.org/abs/2301.10884)

- [Circuit Component Reuse Across Tasks in Transformer Language Models](https://arxiv.org/abs/2310.08744)

- [Circuit Compositions: Exploring Modular Structures in Transformer-Based Language Models](https://arxiv.org/abs/2410.01434)

- [Sheaf Discovery with Joint Computation Graph Pruning and Flexible Granularity](https://arxiv.org/pdf/2407.03779v2)
  - Finds sheaf compositionality in GPT2-Small.

## Attention-specific capabilities
> Certain capabilities can be isolated to specific attention heads, without concerning MLP layers. 
  - Induction heads: [In-context Learning and Induction Heads](https://transformer-circuits.pub/2022/in-context-learning-and-induction-heads/index.html)
  - Successor heads: [Successor Heads: Recurring, Interpretable Attention Heads in the Wild](https://arxiv.org/pdf/2312.09230) 
  - Entrainment heads: [Llama See, Llama Do: A Mechanistic Perspective on Contextual
Entrainment and Distraction in LLMs](https://aclanthology.org/2025.acl-long.791.pdf)
  - Attention head composition: [Talking Heads: Understanding Inter-layer Communication in Transformer Language Models](https://arxiv.org/abs/2406.09519)

## Training interpretable models 

- [Weight-sparse transformers have interpretable circuits](https://arxiv.org/pdf/2511.13653)

## Surveys 
- Phenomenon-centric: [A Primer on the Inner Workings of Transformer-Based Language Models](https://arxiv.org/pdf/2405.00208)
- Task-centric: [A Practical Review of Mechanistic Interpretability for Transformer-Based Language Models](https://arxiv.org/pdf/2407.02646)
- Framework-centric: [The Quest for the Right Mediator: A History, Survey, and Theoretical Grounding of Causal Interpretability](https://arxiv.org/abs/2408.01416)


## Dataset-centric analysis of circuit interpretability-focused papers
|Dataset|Original Paper|Example Prompt| Correct Answer|
|-----|-------|------|-----|
|IOI|Wang et al., 2022| When Mary and John went to the store, John gave a drink to _ |Mary|
|mathematical ordering|Hanna et al., 2023| The (noun) lasted from the year XXYY to the year XX__ |>YY|
|entity tracking| Kim & Schuster, 2023| Box 0 contains the painting, Box 1 contains the bell, Box 2 contains the guitar, Box 3 contains the egg and the mirror and the sheet, Box 4 contains the chemical, Box 5 contains the disk and the wire, Box 6 contains the glass and the knife. Move the glass from Box 6 to Box 4. Put the gift into Box 5. Move the guitar from Box 2 to Box 6. Put the milk into Box 4. Re- move the mirror and the sheet from Box 3. Box 6 __|contains the guitar and the knife.|
|relational knowledge| Hernandez et al., 2024|The official language of France is ___ | French| 

