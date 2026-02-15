Guidelines
==========

This document outlines the components of our framework. Use this guide to structure your inputs for the **Visualizer Tool**.

The Logic of the Framework
--------------------------

The framework operates on a "diagnosis-intervention" logic derived from Non-Ideal Theory. Instead of assuming perfect conditions, we explicitly map how we move from an **Ideal Value** to a **Technical Intervention** via specific **Constraints**.

The 5 Components
----------------

When documenting your workflow, first identify the following five components:

Undesirable Properties (UP)
~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Definition:**
The specific "Non-Ideal" conditions—properties of the data, environment, or system structure—that hinder the Realized Goals. This is the **Diagnosis** phase.

* **Question to Ask:** *"What conditions prevent us from achieving the Realized Goal perfectly?"*
* **Examples:**
    * High-cardinal categorical features.
    * Incomplete operationalization of seasonal variations.
    * Target variable confounders.
    * Missing sensitive attribute labels.

Abstract Values (AV)
~~~~~~~~~~~~~~~~~~~~
**Definition:**
The high-level normative ideals you strive to uphold in your ML system. These are often broad, ethical concepts.

* **Question to Ask:** *"What is the ultimate ethical goal of this system?"*
* **Examples:** Robustness, Fairness, Privacy, Explainability.

Realized Goals (RG)
~~~~~~~~~~~~~~~~~~~
**Definition:**
The specific, operationalizable sub-goals derived from the Abstract Value. This layer translates the "fuzzy" ethical value into concrete technical objectives.

* **Question to Ask:** *"What does [Abstract Value] specifically look like in the context of my data and task?"*
* **Examples:**
    * *For Robustness:* Robustness to class imbalance; Robustness to distribution shift.
    * *For Fairness:* Equalized Odds across gender; Demographic Parity by region.

Interventions (IV)
~~~~~~~~~~~~~~~~~~
**Definition:**
The technical or procedural actions taken to mitigate the Undesirable Properties. This is the **Action** phase. Note that Interventions address *UPs*, not *AVs* directly.

* **Question to Ask:** *"What technical step are we taking to fix or mitigate the Undesirable Property?"*
* **Examples:**
    * Selecting highest-performing data encoding.
    * Implementing a new evaluation metric for model tuning.
    * Reweighting the loss function.

Known Assumptions (KA)
~~~~~~~~~~~~~~~~~~~~~~
**Definition:**
The premises you must accept for the Interventions to be valid. Every technical fix relies on assumptions; this layer makes them explicit. To learn more about how to articulate assumptions, check out our other work: https://github.com/uofthcdslab/AsAP.

* **Question to Ask:** *"For this Intervention to actually work, what must we assume is true about the world/model?"*
* **Examples:**
    * Negligible effects of model hyperparameters.
    * No influence of other operationalizations of the target variable.
    * The proxy variable is sufficiently correlated with the ground truth.

Example Mapping
---------------

Below is a complete example of a mapping for the value **Robustness**, illustrating how the layers connect:

1.  **AV:** Robustness
2.  **RG:** Robustness to class imbalance
3.  **UP:** Target variable confounders
    * *(Reasoning: We want robustness to imbalance (RG), but our target variable is confounded (UP), making standard metrics unreliable.)*
4.  **IV:** Implementing a new evaluation metric for model tuning
    * *(Action: We create a specific metric to handle the confounder.)*
5.  **KA:** No influence of other operationalizations of target variable
    * *(Justification: This new metric is only valid if we assume other operationalizations don't matter.)*

Check out our visualizer tool to see a complete example.
