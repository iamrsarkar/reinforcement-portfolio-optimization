# Reinforcement Learning-Based Portfolio Optimization

## Overview
This repository contains a reinforcement learning-based approach for portfolio optimization using a combination of dilated causal convolutions and graph attention networks. The model learns to allocate assets in a portfolio by analyzing historical price data and optimizing for returns while considering transaction costs.

## Key Features
- **Dilated Causal Convolutions**: For temporal feature extraction from price sequences
- **Graph Attention Networks**: To model relationships between different assets
- **Sparse Allocation**: Uses sparsemax for differentiable sparse allocations
- **Transaction Cost Awareness**: Explicitly models trading costs during optimization
- **Multi-Objective Learning**: Combines price prediction and return optimization

## Requirements
- Python 3.7+
- PyTorch
- pandas
- numpy
- entmax (for sparsemax)

## Data Format
The model expects training data in Excel format with the following columns:
```
Date        Close       High        Low         Open        
2021-12-27  20.5909462  20.68205692 20.45428098 20.5909462  
2021-12-28  20.77316856 20.8642793  20.54539259 20.59094882
```

## Usage
1. Place your training data in Excel files in a `training/` directory
2. Update the `file_paths` list in `main()` to point to your data files
3. Run the notebook to train the model

## Model Architecture
The model consists of:
1. **Feature Extraction**: Three dilated causal convolution layers
2. **Cross-Asset Attention**: Self-attention mechanism across assets
3. **Graph Attention**: GAT layer for modeling asset relationships
4. **Prediction Heads**: 
   - Price prediction (regression)
   - Portfolio weights (optimization)

## Training
The model is trained with a combined loss function that:
- Maximizes portfolio returns (log returns)
- Minimizes price prediction error (MSE)
- Accounts for transaction costs

## Output
After training, the model will:
1. Predict next-period prices for all assets
2. Generate optimal portfolio weights
3. Save the trained model to a `.pth` file

## Notes
- The model enforces a minimum weight constraint (5% by default)
- Uses a blend of sparse allocation and rank-based weighting
- Includes learnable temperature parameter for the sparsemax operation







# RLBO Portfolio Testing

This project demonstrates how to evaluate a reinforcement learning-based portfolio optimization model using historical stock data. The notebook `rlbo_testing.ipynb` contains code to test a trained model on stock price sequences and evaluate portfolio performance.

## Files

- `rlbo_testing.ipynb` — Main notebook to evaluate portfolio performance using a trained RL model.

## Objective

The goal is to simulate portfolio performance using a pre-trained model, track portfolio values over time, and visualize how the model allocates weights among assets based on their past prices.

## Model Assumption

- The model used is likely a neural network trained to predict portfolio weights over time using past stock price sequences.
- It assumes the model has already been trained and saved, and can be loaded for evaluation.

## Requirements

Make sure you have the following Python libraries installed:

```bash
pip install torch pandas matplotlib numpy openpyxl
```

## How to Run

1. Clone the repository or place the notebook and your model/data files in the same folder.
2. Ensure you have stock data files (e.g., `.xlsx`) ready.
3. Modify the `file_paths` list in the code to point to your stock data files.
4. Run the notebook to evaluate the model's portfolio performance.
5. Visualizations of portfolio value and weight distributions will be shown at the end.

##Input Format

The notebook expects each stock's historical data in an Excel file (e.g., downloaded via `yfinance`), with columns like `Open`, `High`, `Low`, `Close`, and `Volume`.

##Output

- A graph of the portfolio value over time.
- Plots showing asset-wise allocation at each time step.
- Optionally, an Excel file storing portfolio simulation results.



