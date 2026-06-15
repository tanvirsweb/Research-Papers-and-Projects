# A Transformer-Based Framework for Multi-Agent Trajectory Prediction with Region-Aware Representation and Temporal Encoding

<p align="center">

> [Paper Link](https://www.researchgate.net/publication/404607984_A_Transformer-Based_Framework_for_Multi-Agent_Trajectory_Prediction_with_Region-Aware_Representation_and_Temporal_Encoding) 

> [Dataset Link](https://www.argoverse.org/#download-link) 

> [Author Presentation Slides link](A_Transformer-Based_Framework_for_Multi-Agent_Trajectory_Prediction_with_Region-Aware_Representation_and_Temporal_Encoding.pdf)

</p>

## Overview

Predicting the future movement of vehicles is one of the most important challenges in autonomous driving. A self-driving vehicle must continuously estimate where surrounding vehicles will move in the next few seconds to avoid collisions and make safe navigation decisions.

Many state-of-the-art trajectory prediction models achieve strong accuracy but often rely on complex architectures, multiple neural networks, graph construction mechanisms, or computationally expensive attention modules.

This work proposes a lightweight Transformer-based trajectory prediction framework that reduces computational complexity while maintaining competitive prediction accuracy.

Instead of modeling every neighboring vehicle individually, we introduce a Region-Aware Representation that summarizes surrounding traffic through eight directional regions around the target vehicle.

The framework was evaluated on the Argoverse 1.1 Motion Forecasting Benchmark and achieved competitive performance across standard trajectory prediction metrics.

---

## Why This Research Matters

Imagine a self-driving vehicle approaching an intersection.

To drive safely, it must answer questions such as:

* Will the vehicle ahead continue straight?
* Will a nearby vehicle change lanes?
* Will a neighboring vehicle slow down or accelerate?

Incorrect predictions can lead to unsafe decisions.

Most existing solutions use:

* Complex graph neural networks
* Multiple LSTM modules
* Diffusion models
* Heavy multi-stage architectures

These methods often require substantial computational resources and may be difficult to deploy in real-time systems.

Our goal was simple:

> Build a trajectory prediction model that is easier, lighter, faster, and still accurate.

---

## Key Contributions

### 1. Region-Based Interaction Modeling

Traditional methods model each neighboring vehicle independently.

We instead divide the space surrounding the target vehicle into eight directional regions:

```text
┌─────┬─────┬─────┐
│ NW  │  N  │ NE  │
├─────┼─────┼─────┤
│ W   │ Ego │ E   │
├─────┼─────┼─────┤
│ SW  │  S  │ SE  │
└─────┴─────┴─────┘
```

Each region stores whether neighboring vehicles are present.

This significantly reduces interaction complexity while preserving important spatial information.

### 2. Lightweight Temporal Encoding

Most trajectory prediction models rely heavily on velocity-based representations.

We introduce a modified temporal encoding strategy that uses timestamps directly within sinusoidal positional encoding.

Benefits:

* Better temporal awareness
* Simpler implementation
* Lower computational overhead

### 3. Single Transformer Architecture

Instead of combining multiple networks, we employ a unified Transformer Encoder-Decoder framework.

Advantages:

* Reduced model complexity
* Faster training
* Easier deployment
* Better scalability

---

## Methodology

### Step 1: Historical Trajectory Collection

For each target vehicle:

* Past trajectories are collected
* Neighboring vehicle information is extracted
* Spatial context is encoded

### Step 2: Region-Aware Representation

The surrounding environment is partitioned into eight regions.

Each region produces a binary occupancy value:

* 1 = Neighbor exists
* 0 = No neighbor present

This generates a compact interaction vector.

### Step 3: Temporal Encoding

Historical positions are enriched using modified sinusoidal temporal encoding.

This enables the Transformer to understand motion evolution over time.

### Step 4: Transformer Prediction

The encoded sequence is processed by:

* Transformer Encoder
* Transformer Decoder
* Prediction Head

The model then predicts future vehicle coordinates.

---

## Model Architecture

```text
Historical Trajectories
          │
          ▼
 Region-Aware Encoding
          │
          ▼
 Temporal Encoding
          │
          ▼
 Transformer Encoder
          │
          ▼
 Transformer Decoder
          │
          ▼
 Future Trajectory Prediction
```

---

## Dataset

### Argoverse 1.1 Motion Forecasting Dataset

The model is evaluated using the Argoverse benchmark.

Features:

* 320,000+ trajectory sequences
* Real-world urban driving scenarios
* Multiple interacting agents
* High-resolution map information
* Diverse traffic environments

Training Samples: 136,720

Testing Samples: 34,180

Total Processed Samples: 170,900

---

## Experimental Setup

Environment:

* Python 3.13
* PyTorch
* Google Colab GPU
* NumPy

Training Configuration:

* Optimizer: Adam
* Epochs: 25
* Multi-Head Attention: 2 Heads
* Encoder Layers: 4
* Decoder Layers: 6

---

## Results

### Average Displacement Error (ADE)

| Epoch | ADE    |
| ----- | ------ |
| 1     | 0.9065 |
| 5     | 0.7077 |
| 10    | 0.6378 |
| 15    | 0.6243 |
| 20    | 0.6268 |
| 25    | 0.5803 |

### Final Displacement Error (FDE)

| Epoch | FDE    |
| ----- | ------ |
| 1     | 0.9251 |
| 5     | 0.7606 |
| 10    | 0.6989 |
| 15    | 0.6957 |
| 20    | 0.6527 |
| 25    | 0.5971 |

### RMSE Comparison

| Horizon (s) | Proposed Method |
| ----------- | --------------- |
| 1           | 0.55            |
| 2           | 0.68            |
| 3           | 1.07            |
| 4           | 1.53            |
| 5           | 1.92            |

The proposed framework demonstrates strong medium- and long-term prediction performance while maintaining significantly lower architectural complexity.

---

## Advantages of the Proposed Framework

✓ Lightweight architecture

✓ Reduced computational cost

✓ Simple spatial interaction modeling

✓ Competitive forecasting accuracy

✓ Suitable for real-time deployment

✓ Easily scalable for autonomous driving applications

---

## Future Work

Potential future directions include:

* LiDAR integration
* Camera-based multimodal fusion
* Radar fusion
* Model pruning
* Knowledge distillation
* Safety-aware online learning
* Mixed-autonomy traffic prediction
* Adverse weather trajectory forecasting

---

## Citation

If this repository contributes to your research, please cite:

```bibtex
@inproceedings{basu2025transformer,
  title={A Transformer-Based Framework for Multi-Agent Trajectory Prediction with Region-Aware Representation and Temporal Encoding},
  author={Basu, Spandan and Sen, Barshon and Siddique, Tanvir Anjom and Gharami, Kanchon},
  booktitle={2025 28th International Conference on Computer and Information Technology (ICCIT)},
  year={2025},
  organization={IEEE}
}
```

---

## Contact

Tanvir Anjom Siddique

Email: [tanvir.anjom.siddique@gmail.com](mailto:tanvir.anjom.siddique@gmail.com)

For collaboration, discussion, or research inquiries, please feel free to reach out.
