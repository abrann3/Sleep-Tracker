# Sleep Debt & HRV Analytics

## Overview
A personal sleep analytics project investigating the relationship between 
cumulative sleep debt and autonomic recovery, measured via Heart Rate 
Variability (HRV). Motivated by neuroscience research on sleep deprivation 
mechanisms in Drosophila (Tabuchi Laboratory, CWRU School of Medicine).

## Background
Current consumer wearables reduce complex sleep physiology to single 
nightly scores. This project takes a longitudinal approach — modeling 
sleep debt accumulation using a two-process inspired decay model and 
validating it against HRV as a physiological recovery signal.

## Current Status
- ✅ Pipeline built and validated on simulated wearable data
- ✅ Sleep debt model implemented with tunable decay parameter
- ✅ HRV correlation analysis (r = -0.89 on simulated data)
- 🔄 Awaiting real wearable data for personal calibration
- 📋 Planned: self-calibrating decay estimation via HRV feedback
- 📋 Planned: behavioral annotation layer (caffeine, exercise, stress)

## Methods
**Sleep Debt Model**
Cumulative sleep debt is modeled as:
debt_today = (debt_yesterday × decay) + max(0, target - actual_sleep)

Decay constant initialized at 0.85 based on Borbély (1982). 
Will be empirically calibrated against personal HRV data using 
grid search optimization once sufficient real data is collected.

**HRV Analysis**
RMSSD and pNN50 extracted from wearable exports. Used as 
physiological validation signal for sleep debt model — 
testing the hypothesis that autonomic recovery degrades 
as sleep debt accumulates.

## Key Finding (Simulated Data)
Strong negative correlation between sleep debt and HRV RMSSD 
(r = -0.89, p < 0.001), consistent with literature on autonomic 
dysregulation under sleep pressure.

## Tech Stack
- Python, Jupyter Notebook
- pandas, numpy, matplotlib, scipy

## Roadmap
1. ✅ Sleep debt model
2. ✅ HRV correlation layer  
3. 🔄 Personal device data collection
4. 📋 Self-calibrating decay parameter
5. 📋 Behavioral annotation layer

## References
- Borbély, A.A. (1982). A two process model of sleep regulation
- Van Dongen et al. (2003). The cumulative cost of additional wakefulness
