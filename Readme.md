# <center>PowerMamba</center>

This repository contains the code and resources for the research project *"PowerMamba: A Deep State Space Model and Comprehensive Benchmark for Time Series Prediction in Electric Power Systems."*

We release a comprehensive dataset for the Electric Reliability Council of Texas (ERCOT) grid, which includes zonal loads, zonal electricity prices, ancillary service prices, and renewable generation time series with hourly granularity. This dataset spans five years and provides zonal-level spatial resolution, featuring 22 core time series and an extended version with 262 channels that includes external forecasts. The architecture and performance of our prediction model are presented in the following figures:


<div style="text-align: center;">
    <img src="pics/PowerMamba_arc.png" alt="PowerMamba Model">
</div>

**Left Figure**) PowerMamba architecture. The model uses dynamic time series
decomposition to separate seasonal and trend components and
applies linear projections to maintain a fixed size. Parallel
normal and inverse Mamba blocks enable dual tokenization,
capturing intra-series and inter-series dependencies. **Right Figure**) Average Mean Squared Error (MSE) comparison
between PowerMamba and state-of-the-art baselines with a
context length of 240 hours and a 24-hour prediction window.
The circle center represents the maximum possible error, and
closer to the boundary indicates better performance.

PowerMamba outperforms current benchmarks in all prediction tasks. We propose a time series processing block that seamlessly integrates high-resolution external forecasts into our models and other sequence-to-sequence frameworks. We evaluate its effectiveness by considering two scenarios: first, we train with historical data alone, and then we incorporate external forecasts and compare the results. The following Table shows the prediction results for the case without external predictions.

<img src="pics/without_pred.png" alt="Prediction results without external forecasts">

In this section, we integrate the external predictions provided for load and renewable generation into our dataset. The following Table compares the prediction accuracy of our model and the baselines with and without external predictions. A fixed context size of L = 240 and a prediction window size of W = 24 are used for all the baselines.

<img src="pics/With_pred.png" alt="Comparing prediction results with and without external forecasts">
The results indicate that our model performs improves for all time series even those without external predictions. For example, price
prediction error is reduced by 7%, despite the absence of external price predictions. 
<div style="text-align: center; margin-top: 20px;">
    <img src="pics/parameters.png" alt="at">

**Left Figure**) MSE of all models for different prediction window
sizes, with context length L = 240 and no external predictions. **Right Figure**) The number of model parameters with and without
external predictions, in log scale.

PowerMamba enhances the prediction accuracy of
TimeMachine by 7% while employing 43% fewer parameters,
thereby highlighting its superiority over this state-of-the-art
Mamba-based model. Furthermore, PowerMamba is consider-
ably smaller than Transformer-based models, with 78% fewer
parameters than the leading iTransformer.

<img src="pics/qualitative.png" alt="at">

The ground truth and 24-hour predictions of load and price by PowerMamba and TimeMachine for a fixed context size
of L = 240. Our model effectively captures the trend and provides predictions closest to the ground truth. 


<img src="pics/context.png" alt="at">
</div>

The impact of context size on the MSE of PowerMamba and TimeMachine (the second-best performing model) for a
24-hour prediction window. **Left Figure**) Without external prediction. **Right Figure**) With external prediction. It can be seen that the accuracy of our models consistently improves with longer context sizes.

## Getting Started

To set up the required environment, follow these steps:

```bash
conda env create -f environment.yml
conda activate mamba4ts
```

## Repository Overview

- **`PowerMamba`**: Contains the implementation of the proposed PowerMamba model along with baseline models.
- **`data`**: Includes the benchmark dataset used in this project.

Each folder contains a `README` file with more details about its contents.

# Maintainers
* [Ali Menati](https://scholar.google.com/citations?user=HPreuloAAAAJ&hl=en&oi=ao)
* [Fatemeh Doudi](https://fatemehdoudi.github.io/)



## Acknowledgement

We appreciate the following github repos very much for the valuable code base:
- Mamba (https://github.com/state-spaces/mamba)
- Time-Series-Library (https://github.com/thuml/Time-Series-Library)
- TimeMachine (https://github.com/Atik-Ahamed/TimeMachine)
- PatchTST (https://github.com/yuqinie98/PatchTST)
- iTransformer (https://github.com/thuml/iTransformer)
- Autoformer (https://github.com/thuml/Autoformer)
- TimesNet (https://github.com/thuml/TimesNet)
- DLinear (https://github.com/cure-lab/LTSF-Linear)

# Citation

If you find our codebase, dataset, or research valuable, please cite PowerMamba:

```
@misc{menati2024powermamba,      title={PowerMamba: A Deep State Space Model and Comprehensive Benchmark for Time Series Prediction in Electric Power Systems}, 
      author={Ali Menati and Fatemeh Doudi and Dileep Kalathil and Le Xie},      year={2024},
      eprint={2412.06112},      archivePrefix={arXiv},
      primaryClass={cs.LG},      url={https://arxiv.org/abs/2412.06112}, 
}
```


