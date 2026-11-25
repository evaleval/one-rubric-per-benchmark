# Preregistration 

This preregistration is the basis for the project plan. It is not binding, but is a commitment that all reported outcomes from the project will reference this preregistration, will report results of any hypotheses tested, and note what departures from the preregistration occurred, if any. 

# Conceptual Approach 

Benchmark rubrics for AI evaluations are often either expensive to create, requiring significant expert investment, or ill-suited to the tasks. The central question this project is attempting to answer is the extent to which a single rubric can be used across tasks in ways that reduce the cost, and the mismatch. 

**Note:** This single benchmark across tasks implicitly relies on moving the task-specific features of a rubric into either a reference answer, or into the LLM-as-a-judge as implicit information. It is conceivable that even the non-task specific features needed for grading are implicit in the test or the background knowledge of the LLM-as-a-judge. To ensure the single benchmark is in fact providing the information needed for scoring, we also test against a no-rubric case. 

## **Specific hypothesis 1:** 

We can develop a generic rubric for HealthBench by extracting the common features of task-specific rubrics from a small subset of questions. On held-out HealthBench questions, the generic rubric will produce scores that agree more closely with original expert-rubric scores than no-rubric judging. 

**Criterion:** The generic rubric will have statistically similar model rankings to the full set. We will We will test this using both exact permutation distributions for Kendall’s Tau for overall model ranking, and Spearman’s rank correlation (ρ) using the Student’s t-approximation for per-item scoring. Success is that the new rubric is not statistically significantly different from the expert rubric is statistically significantly better than no-rubric<sup>1</sup> . 

For all ratings, we will also report mean absolute score error, directional bias, and agreement in pairwise model ordering. We will also report the same for each of the five HealthBench subscore axes, and the seven conversation-theme subscores. 

## **Specific Hypothesis 2:** 

The generic rubric will perform statistically better than no-rubric, each compared to the expert-rubric baseline. 

> 1 For a small sample, failing to reject the null is itself a less meaningful result. We are using the criterion of failing to reject the null for equivalence rather than performing a test of range-specific correlations because this is a subjective choice that depends on sample sizes and number of items and models which are not yet decided on across the different hypotheses, which makes using prespecified equivalence criteria on the basis of absolute score error and agreement infeasible - but the metrics will be reported. Note that rejecting the null of statistical significance for Tau is weaker than doing so for rank-correlation for per-item scoring, which has higher statistical power. Passing one or both tests is therefore weaker or stronger evidence that this approach is effective. 

# Methodological Approach 

1. Randomly sample 100 criteria from the UK AISI’s Inspect AI implementation of HealthBench 

2. Perform manual annotation on whether the criteria is generic or question-specific. Generic parts of the rubric can be extracted directly, and question-specific aspects will be generalized, so that the information necessary for grading is contained in the generic question plus (task-specific) reference answers. 

_3._ **_Review the audit._** _Count generic versus question-specific criteria and discuss ambiguous cases. A high question-specific share would motivate testing reference answers, but wouldn’t prove they are necessary._ 

_4._ **_Agree on one fixed generic rubric._** _Use the audit to identify reusable evaluation requirements. Freeze its wording and scoring rules before the comparison; use the same rubric for every question._ 

_5._ **_Choose about 50 HealthBench questions and obtain responses from a few models._** _We should first check whether your existing runs provide suitable responses. Each selected question needs its_ **_complete original rubric_** _—the 100 sampled criteria are only for the audit. (We keep these evaluation questions separate from those used to develop the generic rubric.)_ 

_6._ **_Grade each saved response three times, using the same judge and settings:_** 

|**_Condition_**|**_What the judge receives_**|
|---|---|
|_Expert-rubric baseline_|_Conversation + model response + that question’s full HealthBench_<br>_rubric_|
|_Generic-rubric_|_Same conversation +_**_same model response_**_+ the fixed generic_|
|_baseline_|_rubric_|
|_No-rubric-response_|_Conversation + model response + information about the scale_|



_7._ **_Compare the paired scores._** _For Expert vs. Generic, Expert vs. No-rubric, and Generic vs. No-rubric, Check the statistical tests, absolute score differences, systematic over/underscoring, correlation, and whether model rankings agree. We will also analyze and discuss the capability on different axes._ 

# Preregistered Modifications 

## **Modification 1** 

6. Depending on the outputs from step 7, if the generic rubric is insufficient, alternative (weaker) approaches will be considered. 

   - a. In place of the generic rubric alone and the no-rubric alone, give the LLM-as-a-judge the "physician responses" portion of the rubric as a separate input. 

   - b. As in (a) but with full “reference correct” answers as a separate input to the LLM-as-a-judge. 

   - c. In place of the generic rubric alone, we build full “reference correct” answers and “reference incorrect” answers as separate inputs to the LLM-as-a-judge. 

7. Compare as above. 

**Note:** These modifications would significantly weaken the claim that a generic rubric alone is sufficient, and are closer to the work done with Dynamic Evaluation Rubrics. 

# Next steps 

Depending on project timing and status, further work is planned either as part of the paper, or as extensions. 

**Specific Hypothesis 3 - Approach Generalization:** The same process will generalize to other benchmarks. 

**Steps:** Use the same approach outlined above to build generic rubrics for other benchmarks, likely starting with LexRubric, and test it as performed above. 

(Note that LexRubric is more challenging for the research team due to Chinese language and legal jargon; success would imply that this method is fairly robust for human-expert level tasks in hard-to-verify domains.) 

**Specific Hypothesis 4a - Single Intra-domain Rubric:** We can create a single generic rubric which can work across disparate benchmarks within a given domain (For health, potentially HealthBench Professional, CSEDB, and/or MedHELM. For legal work, PLawbench, also for Chinese / in China, and for more intra-domain generalization across languages and countries, KCL-Essay South Korea / Korean, BenGER, German / Germany, Legal Research Bench, English / US). 

To test, we will check that this single rubric statistically significantly outperforms no-rubric and is not statistically significantly different from the expert rubric. 

**Specific Hypothesis 4b - Single Cross-domain Rubric:** We can create a single generic rubric which can work across disparate benchmarks in a cross-domain fashion. To test, we will check that this single rubric statistically significantly outperforms no-rubric and is not statistically significantly different from the expert rubric. 

Steps: Use the approach above to build a merged rubric across several benchmarks (a) within / (b) across domains, then apply it to all of the included benchmarks and test that this single rubric statistically significantly outperforms no-rubric and is not statistically significantly different from the expert rubric on each/all included benchmarks. 

## **Specific Hypothesis 5a/b - Generalization of Single Generic Rubric:** 

Steps: We will identify an out-of-sample benchmark with a per-item rubric, and test whether the single (a) cross-benchmark or (b) cross-domain rubric statistically significantly outperforms no-rubric and is not statistically significantly different from the expert rubric on each/all included benchmarks. 

