# JEPA-US-OA — Segmentation automatique et biométrie de la tête fœtale par échographie 2D

> **Auteur** : Olivier Ami  
> **Projet** : Recherche en imagerie obstétricale assistée par l'intelligence artificielle  
> **Statut** : En cours — préparation article scientifique

---

## Objectif

Ce dépôt contient l'intégralité du pipeline de recherche pour la **segmentation automatique
de la tête fœtale** (Fetal Head, FH) et la mesure automatique du **périmètre crânien** (Head
Circumference, HC) à partir d'images et vidéos échographiques 2D obstétricales.

La contribution centrale est l'évaluation empirique des architectures **JEPA (Joint-Embedding
Predictive Architecture)** pré-entraînées sur domaine échographique, comparées aux encodeurs
ImageNet classiques, pour la segmentation et la biométrie fœtale.

---

## Contexte scientifique

La biométrie fœtale par ultrasons est un acte clinique quotidien en obstétrique. La mesure
du périmètre crânien (HC) est un indicateur clé de la croissance fœtale et du diagnostic
de retard de croissance intra-utérin (RCIU). L'automatisation de cette mesure via des
modèles d'IA constitue un enjeu majeur pour réduire la variabilité inter-opérateur et
améliorer l'accessibilité aux soins dans les contextes à ressources limitées.

Les architectures JEPA (Assran et al., 2023 ; LeCun, 2022) représentent une avancée
majeure en apprentissage auto-supervisé : contrairement aux approches génératives
(GAN, Diffusion), elles apprennent des représentations latentes abstraites par prédiction
dans l'espace des embeddings, sans reconstruction pixel. Cette propriété les rend
particulièrement adaptées aux images médicales où la sémantique structurelle prime
sur le rendu visuel.

---

## Protocole expérimental

Le pipeline suit 6 étapes séquentielles :

1. **Ingestion & QC** : inventaire et contrôle qualité des 4 bases de données publiques
2. **Pré-entraînement I-JEPA** : adaptation domaine sur 12 400 images échographiques non annotées (FETAL_PLANES_DB)
3. **Fine-tuning supervisé** : entraînement d'un décodeur U-Net sur les annotations pixel-level (HC18, PSFHS)
4. **Évaluation ablative** : comparaison JEPA-UNet vs U-Net EfficientNet-b4 (baseline ImageNet)
5. **Post-traitement biométrique** : extraction HC par ajustement elliptique + formule de Ramanujan
6. **Validation et reproductibilité** : tests automatisés, overlays cliniques, push GitHub automatique

---

## Bases de données utilisées

| Base | N | Annotation | Licence | Usage |
|------|---|-----------|---------|-------|
| **HC18** | 1 334 images 2D | Contour tête fœtale + HC (mm) | CC BY 4.0 | Benchmark segmentation & HC |
| **FETAL_PLANES_DB** | 12 400 images | 6 classes de plan ultrason | CC BY 4.0 | Pré-entraînement JEPA (non annoté) |
| **PSFHS** | 1 358 images intrapartum | Tête fœtale + symphyse pubienne | CC BY 4.0 | Généralisation domaine |
| **IUGC 2024** | 774 vidéos / 68 106 frames | Annotations vidéo | CC BY 4.0 | Extension vidéo (V-JEPA) |

Sources :
- HC18 : https://hc18.grand-challenge.org/
- FETAL_PLANES_DB : https://zenodo.org/records/3904280
- PSFHS : https://zenodo.org/records/10969427
- IUGC 2024 : https://zenodo.org/records/16869288

---

## Modèles d'IA évalués

### Modèles JEPA (contribution principale)

| Modèle | Architecture | Usage | Licence | Source |
|--------|-------------|-------|---------|--------|
| **I-JEPA** | ViT-B/16 + Prédicteur Transformer | Pré-entraînement images 2D | CC BY-NC 4.0 | [facebookresearch/ijepa](https://github.com/facebookresearch/ijepa) |
| **LeJEPA** | ViT léger | Budget GPU limité | CC BY-NC 4.0 | [galilai-group/lejepa](https://github.com/galilai-group/lejepa) |
| **V-JEPA 2** | ViT vidéo | Extension clips ultrason | MIT/Apache-2.0 | [facebookresearch/vjepa2](https://github.com/facebookresearch/vjepa2) |

### Baseline de comparaison

| Modèle | Encodeur | Pré-entraînement | Usage |
|--------|---------|-----------------|-------|
| **U-Net + EfficientNet-b4** | EfficientNet-b4 | ImageNet | Référence état de l'art |
| **DPT + ViT-B/16** | ViT-B/16 | ImageNet | Ablation encodeur ViT seul |

### Architecture finale

```
JEPA-UNet = Encodeur ViT-B/16 (I-JEPA US-pretrained) + Décodeur U-Net 4 niveaux
```

---

## Métriques cibles

| Métrique | Seuil démo | Seuil publication |
|----------|-----------|------------------|
| Dice (FH) sur HC18 | ≥ 0.93 | > baseline ImageNet |
| HC MAE | ≤ 2.5 mm | ≤ 2.0 mm |
| HD95 | ≤ 5.0 px | ≤ 4.0 px |
| Taux d'échec silencieux | < 5% | < 3% |
| R² (HC prédit vs GT) | ≥ 0.95 | ≥ 0.97 |

---

## Structure du dépôt

```
JEPA-US-OA/
├── notebooks/
│   └── JEPA_US_COMPLET.ipynb   ← notebook principal (pipeline complet)
├── configs/
│   └── hc18_splits.json         ← splits patient-niveau 80/10/10
├── results/
│   ├── ablation_table.tex        ← tableau LaTeX publication-ready
│   ├── ablation_table.csv        ← résultats numériques bruts
│   └── test_results.csv          ← tests automatisés pass/fail
├── figures/                      ← overlays, courbes, Bland-Altman (générés)
└── README.md
```

---

## Infrastructure

- **GPU** : NVIDIA RTX PRO 6000 Blackwell (95 Go VRAM) via Google Colab Pro+
- **Framework** : PyTorch ≥ 2.0, CUDA 12.8, bf16 AMP
- **Segmentation** : segmentation-models-pytorch (smp.Unet, smp.DPT)
- **Encodeurs** : timm (ViT-B/16-224, ViT-B/16-384, EfficientNet-b4)
- **Durée estimée** : ~2h (pré-entraînement I-JEPA 75 min + fine-tuning 30 min)

---

## Cadre réglementaire (R&D uniquement)

Ce travail est un démonstrateur de recherche. Il ne constitue pas un dispositif médical
au sens du Règlement EU MDR 2017/745 et n'est pas destiné à un usage clinique direct.

- CNIL – IA & Santé 2026 : https://www.cnil.fr/fr/ia-et-sante-developper-et-evaluer-des-systemes-ia-conformes
- Guide HAS-CNIL 2026 : https://www.cnil.fr/sites/default/files/2026-03/guide_has_cnil_recommandations_ia.pdf
- EU MDR 2017/745 : https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=OJ:L:2017:117:FULL

---

## Citation

Si vous utilisez ce travail, merci de citer :

```bibtex
@misc{ami2026jepaus,
  author       = {Ami, Olivier},
  title        = {JEPA-US-OA: Fetal Head Segmentation and Biometry from 2D Ultrasound
                  using Joint-Embedding Predictive Architectures},
  year         = {2026},
  howpublished = {\url{https://github.com/Fetal-odyssey/JEPA-US-OA}},
}
```

---

*Olivier Ami — 2026*
