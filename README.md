# Blockchain-Backed Quantum Federated Learning for Financial Fraud Detection

This project combines **quantum machine learning** with **federated learning (FL)** to detect fraud across financial institutions without sharing raw data. 
<!--It was built for the Quantum Fraud Detection Competition organized by NYU Abu Dhabi.-->

Clients train locally on a synthetic fraud dataset using quantum-enhanced models, then contribute to a shared global model through an adaptive, encrypted aggregation process secured by blockchain.

## Table of Contents
- [Key Features](#key-features)
- [Technologies Used](#technologies-used)
- [Adaptive Federated Learning Process](#adaptive-federated-learning-process)
- [Project Structure](#project-structure)
- [How to Run](#how-to-run)
- [Results](#results)
- [Future Work](#future-work)
- [Contact](#contact)

## Key Features
- **Quantum models**: Quantum Support Vector Machines (QSVM), Variational Quantum Circuits (VQC), and Quantum Neural Networks (QNN) for fraud prediction.
- **Federated learning**: Privacy-preserving, decentralized training across multiple clients, with client contributions weighted by local performance.
- **Homomorphic encryption**: Client model updates are encrypted during aggregation.
- **Shamir's Secret Sharing**: Splits model weights so no single client can access the full model.
- **Quantum Key Distribution (QKD, simulated)**: Secures the exchange of encryption keys between clients.
- **Blockchain integrity**: Aggregated weights are hashed and stored on a simulated Ethereum blockchain for tamper-proof, transparent tracking.

## Technologies Used

| Area | Tools |
|---|---|
| Quantum models | [PennyLane](https://pennylane.ai/) |
| Classical ML | TensorFlow / Keras |
| Homomorphic encryption | [TenSEAL](https://github.com/OpenMined/TenSEAL) |
| Secret sharing | Shamir's Secret Sharing |
| Blockchain | Ethereum via Web3, simulated locally with [Ganache](https://trufflesuite.com/ganache/) |
| Data balancing | SMOTE (Synthetic Minority Oversampling Technique) |

### Note on the blockchain setup
The Ethereum blockchain used for model aggregation is simulated locally with Ganache rather than a public testnet or mainnet, since running a real node and paying gas fees isn't practical for local development and testing. Install Ganache from Truffle Suite, run it locally, and the smart contract will deploy to that instance via the Web3 setup already in the code.

## Adaptive Federated Learning Process

1. **Client-side training** – Each client trains a local model (quantum + classical layers) on its own homomorphically encrypted data.
2. **Adaptive client selection** – The global model is evaluated against each client's local test set; clients below an accuracy threshold are excluded from aggregation.
3. **Weighted aggregation** – Selected clients' updates are combined via a weighted average based on local accuracy, so stronger-performing clients have more influence.
4. **Secure update & encryption** – Weights are encrypted (homomorphic encryption + Shamir's Secret Sharing) and keys are exchanged via simulated QKD.
5. **Blockchain integrity check** – The updated global weights are hashed with a quantum-resistant hash (Qhash) and stored on-chain for a tamper-proof record.
6. **Global model update** – Decrypted aggregated weights update the global model, which is redistributed for the next training round.

## Project Structure
```
QFL-Fraud-Detection/
├── src/                      # Core implementation
│   ├── Aggregation_Methods/  # Weighted/adaptive aggregation logic
│   ├── Blockchain/           # Smart contract + Web3 integration
│   ├── Data_Process/         # Dataset loading and preprocessing
│   ├── Encryption_Hashing/   # Homomorphic encryption, secret sharing, hashing
│   ├── encryption.py
│   ├── evaluation_model.py
│   ├── model_weights_update
│   ├── plot_results.py
│   └── qml_model_architecture.py
├── Experiments/              # Jupyter notebooks with full end-to-end runs
│   └── Results/              # Evaluation outputs and plots
├── requirements.txt
└── README.md
```

## How to Run

### Prerequisites
- Python 3.7+
- TensorFlow 2.10.0
- A virtual environment (recommended)

### Installation
```bash
git clone https://github.com/EpameinondasDouros/Quantum-Fraud-Detection-.git
cd Quantum-Fraud-Detection-
pip install -r requirements.txt
```

To use blockchain aggregation, install and run [Ganache](https://trufflesuite.com/ganache/) locally, then deploy the smart contract using the Web3 setup in `src/Blockchain/`.

## Results

Each client trains locally, and contributions are aggregated into a global model weighted by local accuracy. The table below shows per-client performance on the Bank Dataset (20k samples):

| Model     | Accuracy (%) | Recall (%) |
|-----------|--------------|------------|
| Client 0  | 98.04        | 94.87      |
| Client 1  | 98.53        | 97.43      |
| Client 2  | 98.53        | 98.29      |
| Client 3  | 98.53        | 97.43      |
| Client 4  | 99.51        | 98.29      |
| Client 5  | 98.04        | 95.72      |
| Client 6  | 99.26        | 97.43      |
| Client 7  | 98.53        | 98.29      |
| Client 8  | 99.02        | 96.58      |
| Client 9  | 99.26        | 100        |

## Future Work
- **Real quantum hardware**: Move from simulators to real quantum devices to assess noise and coherence effects.
- **Full blockchain aggregation**: Extend the current simulation to a real-world testnet deployment.
- **Scalability**: Support larger datasets and more clients.
- **Advanced quantum algorithms**: Explore further optimizations for fraud detection accuracy.

## Contact
- Epameinondas Douros — epadouros@gmail.com
- Konstantinos Dalampekis — konstantinosdalampekis@gmail.com

## Acknowledgments
This project was supported by NYU Abu Dhabi, CQTS, and eBRAIN Lab.
