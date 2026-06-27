---
title: Semantic AI for BIM/IFC Public Harness
emoji: 🧪
colorFrom: blue
colorTo: gray
sdk: gradio
sdk_version: 5.33.0
app_file: app.py
pinned: false
license: mit
---

# Semantic AI for BIM/IFC Public Harness

This space hosts the interactive public research validation harness for Semantic AI in BIM/IFC models.

> [!WARNING]
> **Reduced Research Scope**: This is a reduced public research harness loaded with 20 sanitized records.
> 
> - It **does not generate 3D IFC meshes/geometry** (LOD).
> - It **does not execute live model inference** or call private model endpoints. All matching is solved against the static 20-record research database.

---

## Tab Guide

### 1. Search Public Cases
Allows you to explore the 20 public research records.
- Filter records by target IFC Class (e.g. `IfcColumn`, `IfcWall`, `IfcBeam`).
- Search using free text keywords like "column", "wall", "beam", "pump", or enter a specific record's sample ID.
- Selecting a case prints its full metadata and schema contract JSON.

### 2. Try Semantic Input
Simulates semantic parsing by mapping user inputs to the closest matching record in the database.
- Input a natural language prompt or select a predefined example from the dropdown.
- Returns a structured, illustrative JSON output capturing semantic intent, suggested IFC class, Level of Information (LOI) notes, and evidence traces.

### 3. Validate JSON
Tests a prediction payload against the required structured research contract.
- Enter any custom JSON.
- Verifies compliance against mandatory contract keys: `status`, `canonical_output`, `validation`, and `metadata`.

### 4. Run Public Harness
Runs the reproducibility and integrity suite over all 20 records inside the database.
- Verifies that all 20 files parse successfully and are fully schema-compliant.

---

## Usage Examples

To test semantic matching, try entering one of the following prompt patterns in the **Try semantic input** tab:
1. *"I need a reinforced concrete column with IFC classification and LOI information."*
2. *"Classify a partition wall and suggest IFC semantic information."*
3. *"Validate whether a window request can map to Pset_WindowCommon."*
4. *"Explain what information is missing to classify this BIM element."*
