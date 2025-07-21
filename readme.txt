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
