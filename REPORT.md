# JEPA-US-OA — Rapport de consolidation

_Généré le 2026-06-17 07:14 — 13/13 expériences avec résultats enregistrés._

## Vue d'ensemble

| # | Expérience | Objectif / cible | Statut | Métriques clés |
|---|------------|------------------|--------|----------------|
| 1 | I-JEPA — pré-entraînement 120k | gain de Dice >= +1.5 % vs baseline | ✅ fait | dice_best=0.8468 |
| 2 | LoRA rank-8 sur backbone JEPA | Dice >= 0.90 | ✅ fait | dice_best=0.8887 |
| 3 | Benchmark SSL (I-JEPA / MAE / DINOv2) | I-JEPA > MAE > DINOv2 | ✅ fait | — |
| 4 | RANSAC-Fitzgibbon (fit d'ellipse) | biais < 5 mm | ✅ fait | mae_mm=46.306, bias_mm=-15.044 |
| 5 | Calibration isotonique | biais <= 1 mm | ✅ fait | — |
| 6 | V-JEPA2 — vidéo IUGC | jitter <= 3° | ✅ fait | — |
| 7 | Ablation — 12 runs | tableau complet | ✅ fait | — |
| 8 | PSFHS — zero-shot | Dice >= 0.85 | ✅ fait | — |
| 9 | SAM2 + LoRA | comparaison segmentation | ✅ fait | — |
| 10 | Ellipticity Score | rho(ES) > rho(Dice) | ✅ fait | rho_es=0.1898 |
| 11 | MC Dropout — incertitude | taux d'échec silencieux < 5 % | ✅ fait | silent_fail_rate=0.355, pass_fail=FAIL |
| 12 | Stratification par tertile d'AG | stable T1 / T2 / T3 | ✅ fait | — |
| 13 | LeJEPA | ratio >= 0.90 | ✅ fait | dice_le=0.8875, ratio=1.0481, pass_fail=PASS |

## Détail par expérience

### EXP01_IJEPA_120K — I-JEPA — pré-entraînement 120k
- **Objectif / cible** : gain de Dice >= +1.5 % vs baseline
- **Résultats** :
    - `dice_best` : 0.8468
    - `delta_vs_exp2` : -0.0419
- **Figures** : `EXP01_finetune.png`, `EXP01_ssl_loss.png`

### EXP02_LORA — LoRA rank-8 sur backbone JEPA
- **Objectif / cible** : Dice >= 0.90
- **Résultats** :
    - `dice_best` : 0.8887
    - `hc_mae_mm` : -1.0
- **Figures** : `EXP02_training.png`

### EXP03_SSL_BENCHMARK — Benchmark SSL (I-JEPA / MAE / DINOv2)
- **Objectif / cible** : I-JEPA > MAE > DINOv2
- **Résultats** :
    - `I_JEPA_dice` : 0.8799
    - `MAE_dice` : 0.879
    - `DINOv2_dice` : 0.8839
- **Figures** : `EXP03_I-JEPA_vitb16.png`, `EXP03_MAE_vitb16.png`, `EXP03_benchmark.png`

### EXP04_RANSAC — RANSAC-Fitzgibbon (fit d'ellipse)
- **Objectif / cible** : biais < 5 mm
- **Résultats** :
    - `mae_mm` : 46.306
    - `bias_mm` : -15.044
    - `sd_mm` : 57.435
    - `n` : 186
    - `scale_factor` : 2.5
    - `erosion_px` : 12
- **Figures** : `EXP04_bland_altman.png`

### EXP05_CALIBRATION — Calibration isotonique
- **Objectif / cible** : biais <= 1 mm
- **Résultats** :
    - `bias_before_mm` : -15.639
    - `bias_after_mm` : -1.664
- **Figures** : `EXP05_calibration.png`

### EXP06_VJEPA2 — V-JEPA2 — vidéo IUGC
- **Objectif / cible** : jitter <= 3°
- **Résultats** :
    - `n_clips` : 200
    - `embed_dim` : 1024
    - `rho_norm_dice` : -0.0607

### EXP07_ABLATION — Ablation — 12 runs
- **Objectif / cible** : tableau complet
- **Résultats** :
    - `n_runs` : 12
    - `best_dice` : 0.889
    - `best_run` : JEPAUNet_standard_lr2e-04
- **Figures** : `EXP07_ablation.png`

### EXP08_PSFHS_ZEROSHOT — PSFHS — zero-shot
- **Objectif / cible** : Dice >= 0.85
- **Résultats** :
    - `dice_psfhs_zeroshot` : 0.2485
    - `n` : 200

### EXP09_SAM2_LORA — SAM2 + LoRA
- **Objectif / cible** : comparaison segmentation
- **Résultats** :
    - `dice_jepa` : 0.8887
    - `dice_sam2` : 0.8916
- **Figures** : `EXP09_comparison.png`

### EXP10_ELLIPTICITY — Ellipticity Score
- **Objectif / cible** : rho(ES) > rho(Dice)
- **Résultats** :
    - `rho_es` : 0.1898
    - `rho_dice` : 0.2283
    - `n` : 200
- **Figures** : `EXP10_ellipticity.png`

### EXP11_MC_DROPOUT — MC Dropout — incertitude
- **Objectif / cible** : taux d'échec silencieux < 5 %
- **Résultats** :
    - `silent_fail_rate` : 0.355
    - `n_cases` : 200
    - `pass_fail` : FAIL
- **Figures** : `EXP11_uncertainty.png`

### EXP12_STRATIFICATION — Stratification par tertile d'AG
- **Objectif / cible** : stable T1 / T2 / T3
- **Résultats** :
    - `T1` : 0.8298
    - `T2` : 0.7898
    - `T3` : 0.7946
    - `n` : 200
- **Figures** : `EXP12_stratification.png`

### EXP13_LEJEPA — LeJEPA
- **Objectif / cible** : ratio >= 0.90
- **Résultats** :
    - `dice_le` : 0.8875
    - `dice_ij` : 0.8468
    - `ratio` : 1.0481
    - `pass_fail` : PASS
- **Figures** : `EXP13_lejepa.png`

## Checkpoints (sur Drive — hors dépôt git)

- `EXP03_DINOv2_best.pt` — 353 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/EXP03_DINOv2_best.pt`
- `EXP03_I-JEPA_vitb16_best.pt` — 351 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/EXP03_I-JEPA_vitb16_best.pt`
- `EXP03_MAE_vitb16_best.pt` — 351 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/EXP03_MAE_vitb16_best.pt`
- `best_baseline_unet.pt` — 82 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/best_baseline_unet.pt`
- `best_dpt_vitb16.pt` — 488 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/best_dpt_vitb16.pt`
- `best_jepa_unet.pt` — 378 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/best_jepa_unet.pt`
- `exp01_best.pt` — 351 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/exp01_best.pt`
- `exp02_best.pt` — 353 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/exp02_best.pt`
- `ijepa_ep0004.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0004.pt`
- `ijepa_ep0009.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0009.pt`
- `ijepa_ep0014.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0014.pt`
- `ijepa_ep0019.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0019.pt`
- `ijepa_ep0024.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0024.pt`
- `ijepa_ep0029.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0029.pt`
- `ijepa_ep0034.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0034.pt`
- `ijepa_ep0039.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0039.pt`
- `ijepa_ep0044.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0044.pt`
- `ijepa_ep0049.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0049.pt`
- `ijepa_ep0054.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0054.pt`
- `ijepa_ep0059.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0059.pt`
- `ijepa_ep0064.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0064.pt`
- `ijepa_ep0069.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0069.pt`
- `ijepa_ep0074.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0074.pt`
- `ijepa_ep0079.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0079.pt`
- `ijepa_ep0084.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0084.pt`
- `ijepa_ep0089.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0089.pt`
- `ijepa_ep0094.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0094.pt`
- `ijepa_ep0099.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0099.pt`
- `ijepa_us_vitb16.pt` — 732 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa_us_vitb16.pt`
- `lejepa_dapt_best.pth` — 87 Mo — `/content/drive/MyDrive/JEPA-US-OA_backup_20260617_0618/lejepa_dapt_best.pth`
- `sam2_hiera_base_plus.pt` — 323 Mo — `/content/drive/MyDrive/JEPA_US/outputs/checkpoints/sam2_hiera_base_plus.pt`
- `EXP03_DINOv2_best.pt` — 353 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/EXP03_DINOv2_best.pt`
- `EXP03_I-JEPA_vitb16_best.pt` — 351 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/EXP03_I-JEPA_vitb16_best.pt`
- `EXP03_MAE_vitb16_best.pt` — 351 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/EXP03_MAE_vitb16_best.pt`
- `best_baseline_unet.pt` — 82 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/best_baseline_unet.pt`
- `best_dpt_vitb16.pt` — 488 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/best_dpt_vitb16.pt`
- `best_jepa_unet.pt` — 378 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/best_jepa_unet.pt`
- `exp01_best.pt` — 351 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/exp01_best.pt`
- `exp02_best.pt` — 353 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/exp02_best.pt`
- `ijepa_ep0004.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0004.pt`
- `ijepa_ep0009.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0009.pt`
- `ijepa_ep0014.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0014.pt`
- `ijepa_ep0019.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0019.pt`
- `ijepa_ep0024.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0024.pt`
- `ijepa_ep0029.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0029.pt`
- `ijepa_ep0034.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0034.pt`
- `ijepa_ep0039.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0039.pt`
- `ijepa_ep0044.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0044.pt`
- `ijepa_ep0049.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0049.pt`
- `ijepa_ep0054.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0054.pt`
- `ijepa_ep0059.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0059.pt`
- `ijepa_ep0064.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0064.pt`
- `ijepa_ep0069.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0069.pt`
- `ijepa_ep0074.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0074.pt`
- `ijepa_ep0079.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0079.pt`
- `ijepa_ep0084.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0084.pt`
- `ijepa_ep0089.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0089.pt`
- `ijepa_ep0094.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0094.pt`
- `ijepa_ep0099.pt` — 687 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa/ijepa_ep0099.pt`
- `ijepa_us_vitb16.pt` — 732 Mo — `/content/drive/MyDrive/jepa1/outputs/checkpoints/ijepa_us_vitb16.pt`
- `sam2_hiera_b+.pt` — 323 Mo — `/content/drive/MyDrive/jepa1/repo/sam2_hiera_b+.pt`
- `lejepa_dapt_best.pth` — 87 Mo — `/content/lejepa_dapt_best.pth`
