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
- ✅ Sleep debt model with asymmetric accumulation/decay (Ti > Td)
- ✅ HRV correlation layer (r = -0.891 on simulated data)
- ✅ Grid search parameter calibration across Ti/Td space
- ✅ Self-calibrating EWMA update system with physiological safeguards
- ✅ Parameter bounds grounded in Borbély two-process framework
- 🔄 Awaiting real wearable data for genuine calibration
- 📋 Planned: cross-validation layer
- 📋 Planned: behavioral annotation (caffeine, exercise, stress)

## Model Architecture

### Sleep Debt Model
Asymmetric two-parameter debt accumulation based on Borbély (1982):

debt_today = (debt_yesterday × Td) + (deficit × Ti)  [if undersleeping]
debt_today = max(0, debt_yesterday × Td + surplus)    [if oversleeping]

Ti (accumulation rate) > Td (decay rate), reflecting the 
empirical finding that sleep pressure builds faster than it 
dissipates — consistent across humans and Drosophila 
(Guillaumin et al., Sleep 2024).

### Self-Calibrating Parameter System
Parameters initialized from literature defaults (Ti=1.2, Td=0.85) 
and updated via EWMA blending as personal data accumulates:

updated_param = (current × 0.85) + (new_estimate × 0.15)

Update safeguards:
- Positive correlation windows rejected
- Weak signal windows rejected (|r| < 0.4)
- Hard physiological bounds: Ti ∈ [1.0, 2.0], Td ∈ [0.75, 0.95]

### Calibration Phases
| Phase | Data | Approach |
|-------|------|----------|
| Days 1-14 | Insufficient | Literature defaults |
| Days 14-30 | Early | Full grid search, 0.05 resolution |
| Days 30-60 | Establishing | Grid search + cross-validation |
| Days 60+ | Mature | Biweekly EWMA updates |

## Key Hypothesis
The asymmetric model (Ti > Td) will outperform simple decay 
on real physiological data, with Ti stabilizing at a personally 
calibrated value reflecting individual sleep pressure accumulation 
kinetics. This hypothesis is directly untestable on simulated data 
and represents the core scientific question of the project.

## Connection to Laboratory Research
This project extends the author's concurrent research on 
dopaminergic sleep regulation in Drosophila (Tabuchi Laboratory, 
CWRU School of Medicine). The two-process model has been 
validated in Drosophila (Guillaumin et al., 2024), revealing 
interdependence between circadian clock speed and sleep pressure 
decay rate — the same Ti/Td relationship this project 
investigates in humans via wearable data.
## References
- Borbély, A.A. (2022). The two‐process model of sleep regulation: Beginnings and outlook
- Van Dongen et al. (2003). The cumulative cost of additional wakefulness
- Thayer et al. (2010). The relationship of autonomic imbalance, heart rate variability and cardiovascular disease risk factors
- Abhilash, L., & Shafer, O. T. (2023). A two-process model of Drosophila sleep reveals an inter-dependence between circadian clock speed and the rate of sleep pressure decay
