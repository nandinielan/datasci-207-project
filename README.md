# Detecting Money Laundering Rings with Graph Neural Networks

## Project Overview

This project explores whether illicit Bitcoin transactions can be detected more effectively by modeling transactions as a graph rather than treating each transaction independently. Using the Elliptic Bitcoin Dataset, we compare traditional machine learning approaches with graph-based methods that can incorporate relationships between transactions.

The primary task is binary classification of labeled transactions as **licit** or **illicit**.

## Team

- Dhruvi Kadhiwala
- Nandini Elangovan
- Shelly Muruganantham

UC Berkeley MIDS — DATASCI 207

## Dataset

We use the Elliptic Bitcoin Dataset, which represents Bitcoin transactions as a directed graph.

- 203,769 transaction nodes
- 234,355 directed edges
- 49 time steps
- 165 numerical transaction features used for modeling
- 42,019 labeled licit transactions
- 4,545 labeled illicit transactions
- 157,205 unlabeled transactions

The raw dataset is not stored in this repository because of its size.

## Data Preprocessing

The preprocessing pipeline:

- Validates transaction IDs, missing values, and duplicates
- Converts original class labels into a binary target
  - `0` = licit
  - `1` = illicit
- Retains unlabeled transactions for graph structure while excluding them from supervised evaluation
- Maps transaction IDs to consecutive graph node indices
- Constructs the directed graph edge representation
- Creates chronological training, validation, and test splits
- Produces GNN-ready node features, labels, edges, and masks

### Temporal Split

To evaluate performance on future transactions rather than using a random split:

| Split | Time Steps | Labeled Transactions | Illicit Rate |
|---|---:|---:|---:|
| Train | 1–34 | 29,894 | 11.58% |
| Validation | 35–41 | 7,829 | 8.62% |
| Test | 42–49 | 8,841 | 4.61% |

All graph edges connect transactions within the same time step, so no edges cross the training, validation, or test boundaries.

## Repository Structure

```text
datasci-207-project/
├── data_preprocessing.ipynb
├── EDA.ipynb
├── Baseline_Model.ipynb
├── processed_data/
│   └── elliptic_labeled_processed.csv.gz
└── README.md
