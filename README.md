SCOPE-Art Anonymous Reproducibility Package

This repository contains the anonymous reproducibility materials for SCOPE-Art. The package is organized around data-manifest preparation, duplicate auditing, grouped cross-validation, the SCOPE-Art model components, retrieval and calibration evaluation, robustness and ablation analyses, statistical testing, and manuscript-output generation.

Package Structure

SCOPE-Art_Anonymous_Reproducibility_Package/
├── configs/
│   ├── data.yaml
│   └── scope_art.yaml
├── docs/
│   ├── DATA.md
│   └── PROTOCOL.md
├── logs/
│   └── reference_outputs/
│       ├── cv_run_reference.log
│       └── external_run_reference.log
├── manifests/
│   └── smoke_test_inputs/
│       ├── mini_met.csv
│       └── mini_prado.csv
├── results/
│   └── reference_outputs/
│       ├── audit_summary_reference.json
│       ├── cv_metrics_reference.json
│       └── external_metrics_reference.json
├── scripts/
│   ├── 01_build_manifest.py
│   ├── 02_audit_duplicates.py
│   ├── 03_make_folds.py
│   ├── 04_train_cv.py
│   ├── 05_aggregate_cv.py
│   ├── 06_external_prado.py
│   ├── 07_matched_gallery.py
│   ├── 08_robustness.py
│   ├── 09_ablation.py
│   ├── 10_statistics.py
│   └── 11_make_tables_figures.py
├── src/
│   └── scope_art/
│       ├── __init__.py
│       ├── calibration.py
│       ├── data.py
│       ├── losses.py
│       ├── metrics.py
│       ├── model.py
│       ├── robustness.py
│       ├── statistics.py
│       └── utils.py
└── tests/
    └── smoke_test.py

Configuration Files

configs/data.yaml

Defines dataset metadata locations, image directories, harmonized field mappings, perceptual-hash settings, duplicate-audit parameters, and grouped cross-validation settings.

configs/scope_art.yaml

Defines the SCOPE-Art experiment configuration, including the pretrained backbone specification, image and embedding dimensions, random seeds, training settings, optimizer and scheduler parameters, expert-routing settings, retrieval configuration, calibration settings, matched-gallery settings, and external-evaluation constraints.

Documentation

docs/DATA.md

Describes the expected public data sources, required harmonized metadata fields, image-handling assumptions, and construction of final artwork-level manifests.

docs/PROTOCOL.md

Documents the internal validation protocol, external validation constraints, duplicate-screening policy, fold-specific evaluation rules, and matched-gallery analysis procedure.

Core Source Code

src/scope_art/model.py

Contains the main SCOPE-Art model components:

StructuralResidualTokenMixer

ContextLensFactorization

SharedBasisCrossModalExperts

ScopeArtCore

The module implements structural residual token integration, context-lens aggregation, sparse shared-basis cross-modal expert routing, and the image/text forward paths used by the SCOPE-Art core.

src/scope_art/data.py

Contains utilities for:

manifest loading and validation;

SHA-256 and perceptual-hash generation;

cross-collection exact and near-duplicate auditing;

Hamming-distance computation for perceptual hashes;

grouped fold construction.

src/scope_art/losses.py

Contains the symmetric image-text InfoNCE retrieval loss and the combined training objective with optional structural and context-lens loss terms.

src/scope_art/metrics.py

Contains retrieval and calibration metric utilities, including bidirectional recall, mean reciprocal rank, expected calibration error, and Brier score computation.

src/scope_art/calibration.py

Contains temperature-scaling utilities for similarity-based retrieval scores and functions for obtaining top-1 confidence and correctness indicators.

src/scope_art/robustness.py

Contains image perturbation utilities used by robustness analyses, including JPEG recompression, Gaussian blur, and desaturation.

src/scope_art/statistics.py

Contains statistical-analysis utilities for paired bootstrap estimation and Cliff's delta computation.

src/scope_art/utils.py

Contains shared utilities for random-seed control, SHA-256 file hashing, and JSON output handling.

Experiment Scripts

scripts/01_build_manifest.py

Builds harmonized raw manifests from the metadata mappings defined in configs/data.yaml.

scripts/02_audit_duplicates.py

Adds file hashes and perceptual hashes to manifests and performs cross-collection duplicate auditing.

scripts/03_make_folds.py

Constructs grouped cross-validation folds from the finalized development manifest.

scripts/04_train_cv.py

Provides the cross-validation training entry point and the integration point between dataset-specific image/text encoding and the SCOPE-Art core.

scripts/05_aggregate_cv.py

Loads fold-level machine-readable metric files and aggregates them for cross-validation reporting.

scripts/06_external_prado.py

Defines the external-evaluation contract for frozen-checkpoint inference without external-data fitting, model selection, early stopping, or recalibration.

scripts/07_matched_gallery.py

Implements fold-specific matched-gallery evaluation using repeated subsampling while preserving paired image-text candidates.

scripts/08_robustness.py

Defines the robustness-analysis entry point for image perturbations, context-lens masking, and reduced-training-data conditions.

scripts/09_ablation.py

Defines the ablation-analysis entry point for the principal SCOPE-Art components, loss terms, context construction, and expert architecture.

scripts/10_statistics.py

Defines the statistical-analysis workflow for paired comparisons, multiple-comparison handling, effect-size estimation, and fold-level interval reporting.

scripts/11_make_tables_figures.py

Defines the manuscript table and figure generation stage based on machine-readable result files.

Smoke-Test Materials

tests/smoke_test.py

Provides a lightweight functional test of the SCOPE-Art core, loss computation, embedding normalization, and retrieval-metric interface using synthetic tensors.

manifests/smoke_test_inputs/

Contains small manifest files used for package-level smoke testing:

mini_met.csv

mini_prado.csv

Reference Output Files

logs/reference_outputs/

Contains reference log files for the cross-validation and external-evaluation workflows.

results/reference_outputs/

Contains machine-readable reference-output files for:

duplicate-audit summaries;

cross-validation metric schemas;

external-evaluation metric schemas.

These files are included to document the expected organization and format of generated outputs.
