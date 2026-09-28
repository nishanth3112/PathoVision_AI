# PathoVision AI

**A research-only digital pathology triage platform.**

PathoVision AI analyzes real breast-cancer histopathology images, identifies potentially suspicious metastatic tissue, generates localization heatmaps, estimates uncertainty, and prioritizes whole-slide images for expert review.

> ⚠️ **Research and educational use only.** This system is a decision-support prototype. It is not a medical device, has not been clinically validated, and must never be used for actual patient diagnosis or treatment decisions.

## What it does

1. Validates slide/image quality (blur, exposure, artifacts).
2. Segments tissue from background.
3. Extracts patches at a fixed magnification.
4. Encodes patches using frozen DINOv2 / DINOv3 vision foundation models.
5. Classifies patches as normal or potentially metastatic.
6. Aggregates patch-level results into a slide-level score via attention-based Multiple-Instance Learning (MIL).
7. Generates a suspicion heatmap over the original slide.
8. Estimates calibrated uncertainty and abstains on low-confidence cases, routing them for manual review.

## Datasets

- **[PatchCamelyon](https://patchcamelyon.grand-challenge.org/)** — 327,680 labeled 96×96 histopathology patches. Used for patch-level model development and benchmarking.
- **[CAMELYON16](https://camelyon16.grand-challenge.org/)** — ~400 real H&E-stained whole-slide lymph-node images. Used for whole-slide ingestion, MIL, and heatmap generation.

Both are real public medical-imaging datasets. See `docs/data-card.md` (once written) for licensing, provenance, and permitted usage.

## Tech stack

- **ML/Imaging:** PyTorch, DINOv2/DINOv3, OpenSlide, MONAI, OpenCV, Albumentations, scikit-learn
- **Backend:** FastAPI, Pydantic v2, Boto3
- **MLOps:** MLflow, SageMaker Pipelines, Docker, Terraform, GitHub Actions
- **Quality:** uv, Ruff, MyPy, Pytest, Pandera, pre-commit

## Project status

Early development. Following a phased roadmap (see `AGENTS.md`) with an AWS deployment budget capped at $30 total. No cloud infrastructure is provisioned until each phase is explicitly reviewed and approved.

## Repository structure

See `AGENTS.md` for engineering rules and `docs/` for architecture, data, and model documentation as the project progresses.

## Disclaimer

This project makes no clinical claims, has no FDA clearance, and is not validated for real-world diagnostic use. It exists to demonstrate applied ML engineering, computer vision, and MLOps practices on real medical-imaging data.