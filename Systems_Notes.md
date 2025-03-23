## 2/27
goals
- figure out the general localization of the drug
- absorption modeling: intravenous injection. absorption is immediate and complete. model as a bolus input into the central compartment.
- distribution modeling: compartmentalized into central (blood), periphery (tissues), and tumor
- key considerations:
  - Tumor-homing ability: k_TUMOR
  - Limited circulation time: Unlike CAR-T cells, CAR-macrophages have a limited time in circulation. k_elimination
  - Biodistribution: Model the tendency of macrophages to accumulate in the liver and lungs after administration.
  - Lack of proliferation: Unlike CAR-T cells, CAR-macrophages do not proliferate post-administration. Your model should reflect this characteristic. (However much CAR-P exists in the dose is exactly how much the patient gets; there is no such thing as regeneration of CAR-M)
  - Tumor microenvironment (TME) effects: Consider incorporating parameters that represent the impact of the TME on CAR-macrophage function and persistence
- how to quantify these effects:
  - Tumor compartment concentration: Model the concentration of CAR-macrophages in the tumor compartment over time.
  - Efficacy threshold: Define a threshold concentration or exposure metric (e.g., AUC) in the tumor compartment that correlates with efficacy based on preclinical data.
  - Sensitivity analysis: Perform sensitivity analyses to identify key parameters affecting tumor penetration and efficacy.
  - PK-PD linking: Develop a PD model that links the concentration of CAR-macrophages in the tumor to the therapeutic effect (e.g., reduction in IL-6 levels or tumor size)1.
    Choose a PD endpoint, such as IL-6 levels or tumor size.
    Collect data on how CAR-macrophage concentration in the tumor correlates with changes in the PD endpoint over time.
    Develop a mathematical model that describes this relationship. Common models include:
    Direct effect model: Effect = Emax * C / (EC50 + C)
    Indirect effect model: dR/dt = kin - kout * (1 + Emax * C / (EC50 + C)) * R
    Where C is the concentration of CAR-macrophages, Emax is the maximum effect, EC50 is the concentration producing 50% of Emax, R is the response variable (e.g., IL-6 levels), and kin and kout are zero-order production and first-order elimination rate constants for the response variable.

- why model the liver accumulation?
"The organ most likely to experience significant non-target effects from an injected CAR-macrophage therapy is the liver. This is supported by several factors: Biodistribution Patterns, Potential Liver Toxicity, Immune Cell Processing, Preclinical Observations
- alternatively or additionally, model the intestine: The organ most dependent on homeostatic levels of IL-6 is the intestine, particularly the small intestine. IL-6 plays a critical role in maintaining intestinal crypt homeostasis and epithelial regeneration through its interaction with Paneth cells and the Wnt signaling pathway. Here are the key reasons:
assumptions:
- treat the therapy like a drug being intravenously injected. no proliferation of cells, only such thing as excretion and regular as-expected interactions with the rest of the compartments
TODO
- SENSITIVITY ANALYSIS / PARAMETER SWEEP
- translate the perplexity code into Steve's format for readability
- find some rate constants to start on
- PK/PD linking?

## 3/5
- [*new paper* (1/2025)](https://www.nature.com/articles/s41467-024-55770-1#Sec8) talking about CAR-M (macrophages) being used for murine experiments for sensitizing HER2+ solid tumors to PD1 blockade.   
"This finding was expected as macrophages are terminally differentiated cells that reside in tissues, do not circulate in the periphery, and accumulate in liver, spleen, tumor, and lung. Murine CAR-M trafficking mirrored that of human CAR-M and demonstrated a low rate of tumor infiltration by RNAscope. Trafficking and persistence are key limiting factors to the adoptive transfer of fully differentiated macrophages and less differentiated monocytes may enhance both parameters."
- this explains why we are so interested in modeling trafficking
- [cancer cachexia patients tend to have fatty liver](https://www.dkfz.de/en/news/press-releases/detail/liver-controls-cachexia-in-cancer) so they tend to have a higher rate of things accumulating in the liver than the average human
- [dosage on millions of cells for a 70kg patient for CAR-T cells](https://jitc.bmj.com/content/10/12/e005678)
- how to determine the "ideal dosage" for a patient?