# Ethical AI-Driven Insurance Claim Prediction & Premiuming

This repository contains an end-to-end experiments on building, explaining, and auditing insurance-claim models, culminating in a small LLM for personalized policy recommendations.

---

## 1. Task Overview

Tackled four sequential objectives on the same insurance dataset:

1. **Predictive Modeling**  
   - Classification: will a customer file a claim?  
   - Regression: if so, how much will it cost?  
2. **Explainability**  
   - Uncover “why” through feature-importance and counterfactual methods.  
3. **Fairness & Disparate Impact**  
   - Detect and mitigate group-level bias around protected attributes.  
4. **LLM-Based Policy Advisor**  
   - Toy LLM that ingests model outputs and customer info to suggest premiums and answer follow-up questions safely.

---

## 2. Our Approach

### Update 1: Predictive Models & Feature Selection  
- Built tree-based classifier and regressor to output a claim probability and cost.  
- Evaluated multiple feature subsets—excluding sensitive attributes per data-protection guidelines—and compared accuracy/AUC and RMSE.  

### Update 2: Explainability  
- Applied SHAP for global and local feature-importance.  
- Used DiCE counterfactuals to show actionable “what-ifs.”  
- Assessed risks of over-exposure and designed aggregated explanations.  

### Update 3: Fairness & Mitigation  
- Defined “protected” features from Update 1.  
- Measured Demographic Parity & Equalized Odds via FairLearn.  
- Applied post-processing mitigation to reduce disparities with minimal accuracy loss.  

### Update 4: LLM-Powered Policy Recommendations  
- Deployed Meta Llama 3.1 (8B) in LM Studio with RAG access to documentation.  
- Prompted the model to ingest claim-probability, cost predictions, and customer metadata to propose premiums.  
- Benchmarked safety & adversarial resistance using ALERT & SALAD-Bench.  

---

## 3. Key Results
 
- **Explainability Insights:**  
  - Top drivers: prior-claim history, vehicle age, driver-license status.  
  - Counterfactuals revealed minimal feature tweaks that flip decision boundaries.  
- **Fairness Metrics:**  
  - Pre-mitigation Disparate Impact (DP gap: 0.0017; EO gap: 0.0046).  
  - Post-mitigation DP ≈ 0.0005, EO ≈ 0.0018; accuracy drop < 0.3%.  
- **LLM Safety:**  
  - Rejected 100% of disallowed prompts (race-based pricing, fraud instructions).  
