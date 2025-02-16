Keywords: knowledge distillation, computation capacity, resource, lightweight, compression, resource-constrained edge devices, large-scale, *memory* capacity, mixture-of-expert, prune



## On the Opportunities and Risks of Foundation Models

#### ***4 Technology - 4.1 Modeling - 4.1.2 Scalability***

- **Hardware Compatibility.** Consequently, foundation models should ideally be amenable to schemes such as **distributed training**, which is gaining popularity, as is the case for e.g., **Mixture-of-Experts**, and possibly leverage properties such as sparsity of the computation or representation, as is the case for the Longformer [Beltagy et al. 2020], BigBird [Zaheer et al. 2020], and Sparse Transformer [Child et al. 2019] approaches, and which likely will become more central in future hardware and processors.

#### ***4 Technology - 4.1 Modeling - 4.1.5 Compositionality***

- **Computation.** Models such as Module Networks [Andreas et al. 2016] and **Mixture-of-Experts** [Shazeer et al. 2017] go further along this direction, exhibiting not only structural modularity, but also compositional computation, supported by the specialization of sub-networks to different operations, in a manner that adapts and tailors the model behavior to the input at hand.

#### *4 Technology - 4.5 Systems - 4.5.4 Productionization of foundation models*

- For applications with strict cost and latency constraints, **model compression techniques** like **distillation** [Hinton et al. 2015; Li et al. 2020d; Sanh et al. 2019], **quantization** [Polino et al. 2018; Gholami et al. 2021; Zhou et al. 2018], **pruning** [LeCun et al. 1990; Gordon et al. 2020; McCarley et al. 2019; Wang et al. 2019c; Sajjad et al. 2020], and **sparsity** [Gale et al. 2020; Elsen et al. 2020] could aid deployment by transforming larger models to obtain desired inference-time properties. **Parallelization techniques** like **tensor model parallelism** [Shoeybi et al. 2019], traditionally used for training, might also be useful to reduce inference latency, and also provide additional memory capacity across GPUs to fit the model’s parameters.



## Towards Personalized Federated Learning

#### *IV. Strategy II: Learning Personalized Models - A. Architecture-Based Approaches - 2) Knowledge Distillation*

- enable a greater degree of flexibility to accommodate personalized model architectures for the clients
- 1 distillation of knowledge to each FL **client** to learn stronger personalized models; 2 distillation of knowledge to the FL **server** to learn stronger server models; 3 **bidirectional** distillation to both the FL clients and the FL server; and 4 distillation **amongst clients**.
- 1 Li and Wang [42] proposed **FedMD**, a distillation-based FL framework, which allows clients to design diverse models using their own private data via KD.
- 1 Zhu et al. [55] proposed **FedGen**, a data-free distillation framework that distills knowledge to the FL clients.
- 2 Lin et al. [56] proposed the **FedDF** algorithm. It assumes a setting in which the edge clients require different model architectures due to diverse computational capabilities.
- 3 He et al. [57] proposed group knowledge transfer (**FedGKT**) to improve model personalization performance for resource-constrained edge devices.
- 4 Bistritz et al. [58] proposed an architecture agnostic distributed algorithm for on-device learning—**D-Distillation**.
- A **representative proxy dataset** is often required in the KD process [42], [56]
- As it may be difficult for the student model to learn well if there is a **huge capacity gap** between the large teacher model and the small student model [73], [74], it is imperative to determine an optimal design for both the server and client models.

#### *VI. Promising Future Research Directions - A. Opportunities for PFL Architectural Design - 3)PFL Architectural Search*

- Neural architecture search (NAS) [93] is a promising technique to help PFL reduce manual design effort to optimize the model architecture based on given scenarios. It will be particularly beneficial for parameter decoupling and **KD-based PFL methods**.

#### *VI. Promising Future Research Directions - A. Opportunities for PFL Architectural Design - 4)Spatial Adaptability - 2)dropouts and stragglers*

- Developing communication efficient algorithms to mitigate the problem of stragglers is an ongoing research direction, where **gradient compression** [97] and asynchronous model updates [98] are common strategies for addressing FL communication bottlenecks.



## Privacy and Robustness in Federated Learning: Attacks and Defenses

- However, homomorphic encryption (HE) and secure multiparty computation (SMC) may not be applicable to large-scale FL, as they incur substantial communication and computation overhead.

#### *IV. Defenses Against Privacy Attacks - C. Privacy-Preservation through Differential Privacy*

- **Local Differential Privacy (LDP).** Although the privacy concern is mitigated with random noise perturbation, it brings a new problem with a substantial tradeoff between privacy budget and model utility. Sun et al. [87] filled in this gap by proposing a novel framework called **FEDMD-NFDP**, which integrated a novel Noise-Free Differential Privacy (NFDP) mechanism into federated model **distillation**.

#### *VI. Defenses Against Poisoning Attacks - B. Defenses against Targeted Attacks*

- The current state-of-the-art erasing methods are Mode Connectivity Repair (MCR) [155] and **Neural Attention Distillation** (NAD) [54]. NAD leverages knowledge distillation to erase triggers. Other previous methods, including finetuning, denoising, and **fine-pruning** [153], have been shown to be insufficient against the latest attacks [156], [53].

![image-20221128021924305](https://raw.githubusercontent.com/ailianligit/ailianligit.github.io/main/images/202212/20221206_1670321682.png)



## A Survey on Security and Privacy of Federated Learning

#### *4 Security in federated learning - 4.4 defensive techniques for security vulnerabilities of FL*

- **Knowledge Distillation**: The concept of sharing the knowledge only instead of model parameters can be leveraged in FL to enhance the security of the client data. The authors in [137] proposed a **federated model distillation** framework, which provides flexibility to use personalized ML models and uses translators to collect knowledge to be shared with each client.

- **Trusted Execution Environment (TEE)**: A Trusted Execution Environment (TEE), in general, is defined as a high-level trusted environment for executing code. This technique has been also utilized for privacy-preserving in different ML models where private areas of computing resources are isolated for a particular task [160]. This approach is also applicable in federated learning where we have very **limited computing resources**.
- **Pruning**: To address such issues authors in [108,109] propose a pruning technique. As it is not required to share the full-fledged model in this approach, it helps to address **backdoor attacks** (&fine-tuning) and communication bottlenecks more efficiently.

![image-20221128023320046](https://raw.githubusercontent.com/ailianligit/ailianligit.github.io/main/images/202212/20221206_1670321694.png)