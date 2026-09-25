# Irony Detection Conversational AI MVP Plan

## 1. Problem and Objective

### Problem
Conversational systems can misinterpret short messages when they rely mainly on literal wording and miss a difference between surface meaning and intended attitude. Irony is a useful example because wording, context, and emojis can contribute to meaning.

### Objective
Build and evaluate a privacy-conscious English NLP web application that classifies one short message containing text and optional emojis as `Ironic` or `Non-ironic`, while demonstrating a sound dataset, modeling, evaluation, and error-analysis workflow relevant to Conversational AI.

### Primary outcome
A portfolio-ready demonstration of an NLP capability that could help a future chatbot or virtual assistant interpret user tone and intent more effectively. The MVP itself is not a chatbot and does not use multi-turn conversation history.

## 2. Users and Scope

### Target users
- Recruiters, hiring managers, and technical interviewers.
- Developers and ML practitioners reviewing the project.
- Portfolio visitors trying the demonstration.

### Non-target users
- Production conversational-system operators.
- Users requiring safety-critical or business-critical predictions.
- Users requiring multilingual, batch, or multi-turn analysis.
- Users seeking definitive classification of all irony forms or subtypes.

### Explicit MVP boundaries
- English only.
- One short message at a time.
- Text may contain emojis; emojis are preserved.
- Binary output: `Ironic` or `Non-ironic`.
- No conversation history or multi-turn context.
- No batch classification.
- No Portuguese or other multilingual support.
- No independent classification of parody, satire, understatement, or irony subtypes.
- No intentional storage of user messages.
- No confidence scores or explanations in the initial MVP.
- No production-grade conversational understanding claims.

## 3. Functional Requirements

### Must
- Accept one message and provide a `Classify` action.
- Reject empty or whitespace-only input before inference.
- Reject input over the final maximum length; never silently truncate it.
- Preserve emojis during processing.
- Display exactly `Ironic` or `Non-ironic`.
- Show loading, validation, and user-friendly failure states.
- Provide a `Retry` action after a classification failure.
- Avoid exposing technical error details.
- Include curated demonstration examples.
- Send curated examples through the same model path as user input.

### Should
- Provide a `Clear` action that removes the message and result.
- Display an English-only notice.
- Display a concise privacy notice advising users not to enter sensitive or personal information.
- Provide readable text, sufficient contrast, clear labels, keyboard-accessible controls, and visible status states.
- Work responsively on common desktop and mobile viewport sizes.

### Could
- Link to project methodology and evaluation documentation.
- Display model or dataset version information.
- Provide a convenient way to load another curated example.
- Explain how irony detection could support future Conversational AI systems.

## 4. Non-Functional Requirements

- Provisional normal-use classification latency target: under 2 seconds.
- Publicly deployable for portfolio use and easy to run locally.
- Latest common versions of major desktop browsers are the primary compatibility target.
- Mobile responsiveness is desirable; broad device testing is not required for the MVP.
- Raw messages must not be written to application logs.
- Anonymous request count, latency, and error metrics are acceptable without message content or user identity.
- Messages are processed for classification and are not intentionally stored.
- A concise in-page privacy statement should be shown:
  > Messages are processed for classification and are not intentionally stored. Do not enter sensitive or personal information.
- Practical accessibility is required; no formal WCAG compliance commitment is made.
- Evaluation must be reproducible through one documented training/evaluation notebook or script.
- Python is preferred, and the Hugging Face ecosystem should be used where appropriate.
- Infrastructure should be free or low cost and should not require permanent GPU access.

## 5. Data and Model Requirements

### Dataset
Use `cardiffnlp/tweet_eval` with its `irony` subset as the primary dataset candidate. Perform only necessary checks before use:

- Source, version, provenance, license, and relevant terms.
- Label meanings and compatibility with the project definition.
- Class distribution and message-length distribution.
- Emoji presence and examples.
- Train, validation, and test split availability and leakage risks.
- Limitations, annotation ambiguity, and potential bias.

Use a concise portfolio-level dataset summary, not a research-style data card. Retain original examples unless dataset documentation provides a clear reason to filter them.

### Operational definition
Treat a message as ironic when there is an apparent contrast or incongruity between its literal or surface meaning and the meaning or attitude apparently intended by the speaker. Sarcasm may be included when supported by the selected dataset labels. Keep the final definition aligned with the dataset annotation guidance.

### Baseline
Use TF-IDF features with Logistic Regression as the simple baseline. Compare it under the same data splits and evaluation protocol as the pre-trained approach.

### Proposed modeling approach
Evaluate the TF-IDF plus Logistic Regression baseline against one suitable pre-trained NLP approach from Hugging Face. Select the pre-trained approach later based on dataset checks, performance, latency, resource requirements, and local-serving feasibility. Prefer in-application inference over an external model API where feasible. The exact model architecture is intentionally undecided.

### Emoji experiment
If the dataset contains enough emoji examples for a meaningful comparison, compare performance with emojis preserved versus emojis removed. Document preprocessing and avoid claiming emoji benefit without a valid comparison.

### Evaluation
- Primary metric: Macro F1.
- Supporting metrics: precision, recall, per-class F1, accuracy, and confusion matrix.
- Analyze false positives and false negatives.
- Include short-message and emoji-containing cases where available.
- Discuss domain shift from Twitter-derived data to portfolio demonstration messages.
- Use the relative target that the selected pre-trained approach meaningfully outperforms the TF-IDF baseline on Macro F1.
- Set a numerical target only after dataset analysis, baseline results, and relevant published results are reviewed.

## 6. Risks and Limitations

| Risk or limitation | Response or validation |
|---|---|
| Dataset labels may not match the practical definition of irony. | Review annotation guidance and document any mismatch before modeling. |
| Twitter language may not generalize to conversational demo inputs. | Report domain limitations and include qualitative demo examples separately from benchmark results. |
| Irony often depends on context unavailable in one message. | Keep the limitation explicit; do not imply full conversational understanding. |
| Emoji examples may be too sparse for a meaningful experiment. | Check counts first; omit the comparison if evidence is insufficient. |
| Class imbalance or label noise may distort accuracy. | Use Macro F1, per-class metrics, confusion matrix, and dataset analysis. |
| A pre-trained model may miss the latency or resource target. | Prefer a smaller locally runnable approach or document the tradeoff. |
| Public hosting may transmit messages to infrastructure providers. | Document the deployment path and avoid external model APIs unless necessary. |
| Raw messages could leak through logs or diagnostics. | Exclude message content from application logs and review observability settings. |
| Dataset or model licensing may restrict portfolio use. | Check terms before adoption and record the result in the dataset summary. |
| Confidence scores could be misleading. | Exclude them from the MVP unless calibration is later demonstrated. |

## 7. First MVP Definition

### MVP user journey
1. A visitor opens the public web demo.
2. The visitor enters one short English message, optionally containing emojis.
3. The visitor clicks `Classify`.
4. The application runs the selected model.
5. The application displays `Ironic` or `Non-ironic`.
6. The visitor can clear the result, retry after failure, or choose a curated example.

### Included
- Public single-message web demonstration.
- Binary irony classification.
- Emoji-preserving input path.
- Input validation and loading/error/retry states.
- Curated examples sent through the deployed model.
- Concise privacy and English-only notices.
- Reproducible training/evaluation notebook or script.
- Portfolio documentation covering dataset, baseline, model comparison, metrics, limitations, and error analysis.

### Excluded
- Chatbot behavior, conversation history, and multi-turn context.
- Batch classification.
- Portuguese or other languages.
- Irony subtypes.
- Confidence scores, explanations, and emoji-signal visualizations.
- User accounts, saved history, analytics tied to users, or intentional message persistence.
- External model APIs unless local inference becomes infeasible.

### MVP learning goal
Determine whether a practical, locally deployable pre-trained NLP approach provides a meaningful Macro F1 improvement over TF-IDF plus Logistic Regression, and document where both approaches fail, especially for emoji-containing messages.

## 8. MVP Planning

### Workstreams and sequence

1. **Dataset audit**
   - Inspect the `tweet_eval` irony subset.
   - Confirm labels, splits, license/terms, class distribution, lengths, emoji coverage, and limitations.
   - Record the concise dataset summary.

2. **Reproducible evaluation workflow**
   - Establish deterministic data preparation and evaluation splits.
   - Train and evaluate TF-IDF plus Logistic Regression.
   - Report Macro F1 and supporting metrics.
   - Perform the emoji-preserved versus emoji-removed comparison if justified.

3. **Pre-trained model evaluation**
   - Select one suitable Hugging Face approach after the dataset audit.
   - Evaluate it with the same protocol.
   - Compare performance, latency, resource use, and error patterns.
   - Select the approach for the demo based on the documented tradeoff.

4. **Error analysis and readiness decision**
   - Review representative false positives and false negatives.
   - Assess domain shift and context limitations.
   - Decide the input-length limit using dataset lengths and tokenizer constraints.
   - Confirm the selected approach meets the portfolio performance and latency goals.

5. **Web MVP design and implementation preparation**
   - Define the interface states and public deployment requirements.
   - Choose the Python web framework, hosting platform, and deployment architecture only after evaluation evidence is available.
   - Confirm privacy-preserving logging and local inference behavior.

6. **Validation before release**
   - Test input validation, classification, loading, errors, retry, clear, curated examples, privacy notice, and English-only notice.
   - Measure normal-use latency.
   - Verify no raw message content appears in logs.
   - Confirm local setup and public deployment procedures.

### Implementation readiness
Implementation may begin only when:

- The dataset audit is complete and acceptable.
- The baseline and pre-trained approach have been evaluated.
- The demo model and input-length limit are selected.
- The deployment approach is chosen and its privacy implications are documented.
- The user approves this plan and any remaining conditions.

### Definition of done
The MVP is done when the public demo supports the approved single-message flow, the documented evaluation is reproducible, the selected model meets the agreed relative performance goal or its limitation is clearly reported, the latency target is assessed, privacy requirements are verified, and the portfolio documentation is complete.

## 9. Review Before Implementation

### Confirmed plan
- Build a simple public English web demo for one-message binary irony classification.
- Use `cardiffnlp/tweet_eval` irony as the primary dataset candidate after necessary checks.
- Use TF-IDF plus Logistic Regression as the baseline.
- Compare it with one suitable Hugging Face pre-trained NLP approach.
- Use Macro F1 as the primary metric and report supporting metrics.
- Preserve emojis and perform the emoji-removal comparison only if data coverage supports it.
- Include a documented evaluation notebook or script and curated demo examples.
- Prefer local inference and avoid permanent GPU or unnecessary data persistence.

### Assumptions documented for minor decisions
- Empty input and over-limit input are rejected client-side or at the request boundary before model inference.
- Curated examples are maintained as presentation data and are classified live by the selected model.
- Anonymous operational metrics are disabled by default unless they can be guaranteed not to contain message content or identity.
- The public demo uses the same preprocessing and model artifact evaluated in the reproducible workflow.
- The exact input length, model, framework, host, and deployment architecture are selected after the dataset and model checks.

### Truly blocking open questions
None currently block the MVP plan. Dataset licensing/terms, label compatibility, and technical feasibility remain validation gates before implementation, not requests for new product decisions.

### Approval gate
This document is the first MVP plan. No application implementation should begin until the plan and its validation gates have been reviewed and explicitly approved.
