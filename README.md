

# Mechanistic Interpretability Reading List (Circuits-Focused)

## High-level interpretability & mechanistic overviews

- **The Quest for the Right Mediator: A History, Survey, and Theoretical Grounding of Causal Interpretability** (Mueller et al., 2024) ([paper](https://arxiv.org/abs/2408.01416))
  - Highlight: Provides a broad overview on the methodology of causal interpretability, as well as the pros and cons of different interpretability frameworks(e.g. feature learning vs circuit discovery).

- **A Practical Review of Mechanistic Interpretability for Transformer-Based Language Models** (Rai et al., 2024) ([paper](https://arxiv.org/abs/2407.02646))
  - Highlight: Good “field map” of methods of mechanistic interpretability for transformers: objects of study (features, circuits, SAEs), common techniques (patching, probing, SAEs), evaluation criteria, and a taxonomy of current work.

- **Transformer Circuits Thread (Anthropic)** ([index](https://transformer-circuits.pub))
  - Highlight: Anthropic’s umbrella for circuits work (induction heads, toy models of superposition, etc.); historically important for the circuits mindset.

---

## Circuit discovery methods

### 1. Gradient / patching–based methods

- **Towards Automated Circuit Discovery for Mechanistic Interpretability (ACDC)** (Conmy et al., 2023) ([paper](https://arxiv.org/abs/2304.14997))
  - Highlight: Introduces a greedy edge-pruning algorithm that iteratively removes connections while using activation patching to obtain the minimal computational subgraph (circuit) that preserves model behavior.

- **Attribution Patching Outperforms Automated Circuit Discovery** (Syed, Rager, Conmy, 2023) ([paper](https://arxiv.org/abs/2310.10348))
  - Highlight: Relies on the gradient of the backward pass to identify influential edges for a certain task, reducing computational overhead relative to ACDC. However, linearisation can introduce error into importance estimates.

- **Position-aware Automatic Circuit Discovery** (Haklay et al., 2025) ([paper](https://arxiv.org/abs/2502.04577))
  - Highlight: Extends attribution/ACDC-style methods to track *positional* roles, handling variable-length inputs and cross-position interactions.

### 2. Pruning / masking–based methods

- **Finding Transformer Circuits with Edge Pruning** (Bhaskar et al., 2024, NeurIPS) ([paper](https://arxiv.org/abs/2407.00886))
  - Highlight: Optimizes a mask of edges to identify a sparse circuit that optimally reproduces model behaviour at a given sparsity. 

- **Efficient Automated Circuit Discovery in Transformers using Contextual Decomposition (CD-T)** (Hsu et al., 2024) ([paper](https://arxiv.org/abs/2407.00886))
  - Highlight: Attributes model outputs to contributions from specific input tokens and intermediate components, improving data efficiency and stability. 

### 3. Sparse-feature / SAE-based circuit methods

- **Sparse Feature Circuits: Discovering and Editing Interpretable Causal Graphs in Language Models** (Marks et al., 2024/ICLR 2025) ([paper](https://arxiv.org/abs/2403.19647))
  - Highlight: Builds circuits over SAE features rather than neurons/heads, giving more monosemantic units and enabling edits like SHIFT (surgically removing spurious features).
    - For an application, see **Scaling Sparse Feature Circuits For Studying In-Context Learning** ([paper](https://arxiv.org/pdf/2504.13756))

- **Transcoders Find Interpretable LLM Feature Circuits** (Dunefsky et al., 2024) ([paper] https://arxiv.org/abs/2406.11944)
    - Highlight: Transcoders learn the latent features of an MLP layer, together with a transformed weight matrix that encodes how these features activate one another. This allows circuit identification without patching or pruning. 
    - see also: [Circuit Tracing: Revealing Computational Graphs in Language Models](https://transformer-circuits.pub/2025/attribution-graphs/methods.html)

---

## Faithfulness & critiques of circuit discovery

- **Causal Scrubbing: A Method for Rigorously Testing Interpretability Hypotheses** (Chan et al., 2022, Alignment Forum) ([post](https://www.lesswrong.com/posts/JvZhhzycHu2Yd57RN/causal-scrubbing-a-method-for-rigorously-testing))
  - Highlight: An early proposal to test faithfulness of circuits via mean ablating irrelevant paths.

- **Transformer Circuit Faithfulness Metrics Are Not Robust** (Miller et al., 2024, COLM) ([paper](https://openreview.net/pdf?id=zSf8PJyQb2))
    - Highlight: Finds that faithfulness metrics are sensitive to small changes in ablation methodology and task setups, calling into question the generalizability of discovered circuits.

- **Have Faith in Faithfulness: Going Beyond Circuit Overlap When Finding Model Mechanisms** (Hanna, 2024) ([paper](https://arxiv.org/abs/2403.17806))
  - Highlight: Argues that high overlap between discovered circuits and “ground truth” paths is not enough; compares different ablation/patching-style faithfulness tests and shows they can disagree. 

- **Rethinking Circuit Completeness in Language Models: AND, OR, and ADDER Gates** (Chen et al., 2025, ICLR) ([paper](https://arxiv.org/abs/2505.10039))
  - Highlight: Treats circuits as compositions of logical gates and shows that common methods systematically miss OR-like structures, which are important for applications such as unlearning and can be guaranteed through finding complete circuits. 

---

## Circuit discovery experiments in language models

- **Interpretability in the Wild: A Circuit for Indirect Object Identification in GPT-2 Small** (Wang et al., 2022, ICLR) ([paper](https://arxiv.org/abs/2211.00593))
  - Highlight: Canonical end-to-end circuit case study: 26 attention heads grouped into 7 roles for the IOI task; showcases a full toolkit of patching/ablation evaluations, but also highlights gaps (residual unexplained loss, incomplete mechanisms).

- **How Does GPT-2 Compute Greater-Than? Interpreting Mathematical Abilities in a Pre-Trained Language Model** (Hanna, Liu, Variengien, NeurIPS 2024) ([paper](https://arxiv.org/abs/2305.00586))
  - Highlight: Dissects a greater-than comparison circuit in GPT-2; strengthens the case that circuits can capture seemingly “abstract” reasoning, but also exposes how narrow and brittle some of these mechanisms are.

- **Does Circuit Analysis Interpretability Scale? Evidence from Multiple Choice Capabilities in Chinchilla** (Lieberum et al., 2023) ([paper](https://arxiv.org/abs/2307.09458))
  - Highlight: Scales circuit-style analysis for a large Chinchilla model; finds meaningful circuits but at substantial computational and human cost.

- **Fine-Tuning Enhances Existing Mechanisms: A Case Study on Entity Tracking** (Prakash et al., 2024, ICLR) ([paper](https://arxiv.org/abs/2402.14811))
  - Highlight: Tracks an entity-tracking circuit before and after fine-tuning on math; shows that fine-tuning mostly amplifies existing circuits rather than inventing new ones, and uses cross-model patching to compare mechanisms across checkpoints.

- **Discovering Knowledge-Critical Subnetworks in Pretrained Language Models** (Bayazit et al., 2024, EMNLP) ([paper](https://arxiv.org/abs/2310.03084))
  - Highlight: Uses differentiable masking to find sparse subnetworks that are critical for particular facts; conceptually close to circuits but operates on weights rather than activations, and demonstrates precise “knowledge deletion” with limited collateral damage.

- **On the Similarity of Circuits across Languages: a Case Study on the Subject-verb Agreement Task** ([paper](https://arxiv.org/abs/2410.06496))
    - Highlight: Investigates a circuit for subject-verb agreement, and notes that it is highly language-agnostic. 

- **Knowledge Circuits in Pretrained Transformers** (Yao et al., 2024, NeurIPS) ([paper](https://arxiv.org/abs/2405.17969))
  - Highlight: Explicitly identifies “knowledge circuits” spanning attention and MLPs for factual relations in GPT-2/TinyLLaMA, and studies how knowledge editing perturbs those circuits.

- **How Do Language Models Understand Discourse Relations? Discursive Circuits for Coherent Understanding of Discourse Relations** (Miao et al., 2025) ([paper](https://arxiv.org/abs/2510.11210))
    - Highight: Uses circuit ideas to study discourse-level behavior.

---

## Compositionality & modularity of circuits

- **Break It Down: Evidence for Structural Compositionality in Neural Networks** (Lepori, Serre, Pavlick, 2023, NeurIPS) ([paper](https://arxiv.org/abs/2301.10884))
  - Highlight: Prunes networks to find subnetworks implementing distinct subroutines across vision and language; shows that models often decompose tasks into modular pieces.

- **Circuit Component Reuse Across Tasks in Transformer Language Models** (Merullo, Eickhoff, Pavlick, 2023/ICLR 2024) ([paper](https://arxiv.org/abs/2310.08744))
  - Highlight: Takes the IOI circuit and shows it largely reappears for a different “Colored Objects” task and in larger GPT-2 models, providing strong evidence for component reuse across tasks.

- **Circuit Compositions: Exploring Modular Structures in Transformer-Based Language Models** (Mondorf, 2024/ACL 2025) ([paper](https://arxiv.org/abs/2410.01434))
  - Highlight: Uses probabilistic context-free grammars to elicit multiple string-edit subtasks and then compares the resulting circuits; gives a more formal treatment of how similar circuits are, how they compose, and where modularity breaks down.

---

## Applications of circuits & causal subgraphs

- **Sparse Feature Circuits: Discovering and Editing Interpretable Causal Graphs in Language Models** (Marks et al., 2024/ICLR 2025) ([paper](https://arxiv.org/abs/2403.19647))
  - Highlight: Beyond discovery, this paper shows how feature-level circuits can be edited to debias classifiers by identifying irrelevant sparse circuits, thus helping to change model behavior.

- **Discovering Knowledge-Critical Subnetworks in Pretrained Language Models** (Bayazit et al., 2024, EMNLP) ([paper](https://arxiv.org/abs/2310.03084))
  - Highlight: Practical example of using subnetwork/circuit ideas to perform targeted knowledge removal while preserving most capabilities.

- **On Mechanistic Circuits for Extractive Question-Answering** (Basu et. al. 2025, COLM) ([paper](https://arxiv.org/pdf/2502.08059))
    - Highlight: Provides
tangible applications of circuits in the form of
reliable data attribution and model steering.

- **How do LLMs acquire new knowledge? a knowledge circuits perspective on con-
tinual pre-training** ([paper](https://arxiv.org/abs/2502.11196))
    - Highlight: Investigates the evolution of knowledge circuits through pre-training, providing insights on improving pre-training strategies for better performance.

--- 
## Training interpretable models 

- **Weight-sparse transformers have interpretable circuits** (Gao et. al. 2025) ([paper](https://arxiv.org/pdf/2511.13653))
    - Highlight: Trains inherently sparse models and finds a capability-interpretability tradeoff in their circuits. Proposes mapping these activations over to dense models for mechanistic scaffolding. 

## Helpful references
### Courses for mechanistic interpretability

- **Interpretability of Large Language Models, Tel Aviv University (Fall 2025)** ([link](https://github.com/mega002/llm-interp-tau))






