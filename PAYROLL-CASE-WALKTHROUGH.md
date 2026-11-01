# Payroll case walkthrough: employer 401(k) match dispute

This is an operational checklist for a **real** employee's logs; amounts below are placeholders rather than actual match rules.

## Step 1 — Prepare case evidence

- Work only in an enterprise-approved environment. Refer to the employee by a masked token in generated notes.
- Gather business question, **actual** employer match, **expected** employer match, pay period, pay date, payroll run ID/job ID/step, environment and source/build version.
- Add relevant job logs and application-level transaction traces as accessible Copilot workspace files or approved chat attachments. A JES log alone may not contain employee-level transaction data.
- Identify available effective-dated 401(k) match plan configuration, eligible earning types, employee deferral details, YTD balances and any reversal/retro/off-cycle context.

## Step 2 — First invocation

```text
Use payroll-run-investigator. Case: 401(k) employer match for [masked employee].
Run [run ID], period [dates], logs [paths], actual [amount], expected [amount].
Read all relevant source and attachments. Reconstruct event processing order with log locators and link each event to a COBOL/DB2 branch when evidence permits.
Produce separate Business Investigation Note and Technical Recommended Fix Note. Do not make edits or execute jobs.
```

## Step 3 — Ask for a sequence ledger

Copilot must show at least:

| Sequence / event ID | Run / job step | Event | Input or amount | Rule / COBOL source | State after event | Evidence status |
|---|---|---|---|---|---|---|
| ... | ... | ... | ... | ... | ... | Observed / Calculated / Inferred / Unknown |

The transaction order must come from reliable sequence keys or trace evidence. Printed log order and timestamps can be misleading in multi-step or parallel batch processing.

## Step 4 — Reconcile match calculations

Request a **stepwise** computation from evidenced amounts and plan rules, with earned vs eligible wages, employee contributions, plan formula, caps/limits, YTD, true-up, pre-tax/Roth, retro and reversals. Explain any residual variance. Do not assume a formula without verified plan documents/configuration.

## Step 5 — Request two separate notes

### Note A — Business Investigation

1. Question and run identity (masked)
2. Observed outcome and expected outcome with source for expectation
3. Relevant event ledger / transaction sequence
4. Calculation and business-rule application with evidence
5. Verified root cause, or ranked hypotheses + decisive missing facts
6. Plain-English summary to send the business team

### Note B — Technical Recommended Fix

1. Defect classification: program / configuration / input / operational / expected behavior / unresolved
2. Affected assets with exact file and paragraph/SQL/line references
3. The incorrect condition, if proven, and recommended **proposed** behavior
4. Side effects, interfaces, DB2 and batch dependencies
5. Regression and boundary tests: regular, bonus, retro, reversal, YTD limits, multiple checks, effective-dated plans
6. Open assumptions, approvals, data remediation and rollback/restart risks
7. **State 'No program fix recommended' when a code defect is not supported**

## Step 6 — Check answer quality

Reject outputs that: fabricate a match formula, confuse earnings with eligible wages, mix runs or employees, treat a feasible code branch as observed execution, neglect effective dates, lack citations, or propose source changes without proving a defect.

## Example follow-ups

```text
Show the earliest log event after which the employer-match calculation diverged from the expected result. Link that event to source; mark any inferred branch explicitly.
```

```text
Audit whether bonus earning code [code] is match-eligible under the effective-dated plan and identify which DB2 record or COBOL condition supplies that rule.
```

```text
Based only on verified evidence, provide a minimal COBOL fix design in a separate technical note, plus tests. If the defect is not verified, do not suggest a patch.
```
