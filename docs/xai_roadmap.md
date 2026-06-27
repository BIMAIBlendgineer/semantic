# Explainable AI (XAI) Roadmap for BIM/IFC Semantic Interpretation

This document outlines the capabilities currently implemented in the Semantic AI research harness and the structured roadmap to transition from simple traceability to formal Explainable AI (XAI) systems.

---

## 1. What Exists Today (Traceability and Validation)

The current public research harness provides fundamental structural validation and execution trace replay. It does **not** yet implement formal model explainability methods, but rather sets up the structured data contracts required to support them.

The active capabilities include:
- **Execution Replay**: The ability to reload predictions from a JSONL database (`sample20_public_predictions.jsonl`) to review how a user prompt was structured and what variables were output.
- **Trace Evidence**: Basic metadata capture (`source_split`, `risk_level`, `latency_ms`, and `created_at_utc`) to log the conditions of inference.
- **Schema Validation**: Checking the output format against target IFC parameters using the validation contract to ensure no critical properties (like `ifc_class`) are missing.
- **Syntactic Matching**: Logging error flags if the parsed JSON output is syntactically invalid or misses mandatory keys.

---

## 2. What DOES NOT Exist Today

> [!WARNING]
> **No Formal XAI Implemented Yet**: The current system is a structural validation harness, not a completed XAI framework.
> 
> The following capabilities are **not** present in the current codebase:
> - **Feature Attribution (e.g., SHAP, LIME)**: There is no mathematical allocation of weight showing which specific words in the prompt caused the model to choose one IFC class over another.
> - **Causal Explanations**: The system does not explain the causal relationship between parameter selections.
> - **Counterfactual Prompts**: We do not currently generate alternative prompts to show what minimal change would alter the classification.
> - **Formal XAI Benchmarks**: No standardized metric exists in this codebase yet to grade the quality, readability, or engineering accuracy of AI-generated explanations.

---

## 3. The Future XAI Roadmap for BIM/IFC

To transition from structural validation to complete, audited Explainable AI, this research will implement the following seven core development phases:

### Phase 1: Explanation Trace (Conceptual Justification)
- **Objective**: Capture textual justifications alongside classifications.
- **Details**: Force the model to output a step-by-step reasoning path (Chain-of-Thought) explaining *why* a particular IFC class is appropriate based on the input text before outputting the final JSON.

### Phase 2: Evidence Mapping
- **Objective**: Link parsed parameters directly back to source regulations or standard specifications.
- **Details**: Establish database mapping links connecting the proposed `Pset` parameters (e.g. fire rating) to the specific clauses in the building codes or project briefs that mandated them.

### Phase 3: Uncertainty and Alternatives
- **Objective**: Expose the model's confidence and alternative options.
- **Details**: Return a probability distribution of candidate IFC classes (e.g., *IfcColumn: 85% confidence, IfcPile: 12% confidence, IfcBeam: 3% confidence*) so engineers can evaluate high-uncertainty predictions.

### Phase 4: Counterfactual BIM Prompts
- **Objective**: Implement counterfactual testing.
- **Details**: Generate and test "what-if" prompts (e.g., *"If you change the word 'concrete' to 'steel', the system switches the suggested class from IfcColumn/Concrete to IfcColumn/Steel"*), allowing engineers to understand model decision boundaries.

### Phase 5: Human Engineering Review Gate
- **Objective**: Implement a Human-in-the-Loop validation pipeline.
- **Details**: Create an administrative review interface where professional engineers audit high-risk AI predictions, accepting or adjusting them before mutating any IFC databases.

### Phase 6: Explanation Quality Metrics
- **Objective**: Establish metrics for evaluating AI explanation quality.
- **Details**: Implement scoring functions to grade explanations on semantic faithfulness, structural consistency, and clarity to civil engineering reviewers.

### Phase 7: Optional Model Attribution Layer (SHAP/LIME)
- **Objective**: Mathematical feature attribution.
- **Details**: Integrate local model interpreters to map gradient-based or perturbation-based token attributions, visually highlighting which prompt words contributed to the classification.
