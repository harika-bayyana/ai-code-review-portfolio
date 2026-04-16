# JavaScript Task: Array Deduplication - Airbnb Style Compliance

**Platform:** RLHF Studio (Language-Specific Pitfalls)
**Goal:** Identify cross-language hallucinations and evaluate modern JavaScript idiomaticity.

## Prompt
Write a JavaScript function that removes duplicates from an array of primitive values (numbers, strings). Preserve the order of first occurrence. Return a new array; do not mutate the input.

---

## Responses

### Response A (Model Alpha)
```javascript
function getUniqueValues(arr) {
    if (!Array.isArray(arr)) {
        return [];
    }
    const seen = new Set();
    const result = [];
    for (const item of arr) {
        if (!seen.has(item)) {
            seen.add(item);
            result.push(item);
        }
    }
    return result;
}
```

### Response B (Model Beta)
```javascript
function get_unique_values(arr) {
    if (arr == null || !Array.isArray(arr)) return [];
    const seen = new Set();
    const result = [];
    for (const item of arr) {
        if (!seen.has(item)) {
            seen.add(item);
            result.push(item);
        }
    }
    return result;
}
```

### Response C (Model Gamma)
```javascript
function getUniqueValues(arr) {
    if (!Array.isArray(arr)) return [];
    return [...new Set(arr)];
}
```

---

## Evaluation & Ranking

| Rank | Response | Score | Verdict |
|:---:|:---|:---:|:---|
| 1 | **Response A** | 5/5 | Professional, explicit, and style-compliant. |
| 2 | **Response C** | 4.5/5 | Very idiomatic, but slightly less explicit on braces. |
| 3 | **Response B** | 2/5 | Fail due to cross-language naming hallucination. |

### Preference: A > C >> B

### Justification (CEIA)

**Claim**: Response A is preferred for its strict adherence to Airbnb style guidelines. Response B is significantly penalized for using Pythonic naming conventions in a JavaScript context.

**Evidence**:
- **Response B (Line 1)**: Uses snake_case for the function name (get_unique_values). While valid in Python, this is a major style violation in JavaScript (Airbnb Rule 1.1 requires camelCase). This is a classic "cross-language hallucination" where the model mixes up language conventions.
- - **Response A**: Uses proper camelCase and provides explicit braces for the if block (Line 2-4), which is safer and preferred for maintenance.
  - - **Response C**: Uses the most modern/idiomatic approach ([...new Set(arr)]), but the lack of braces on the guard clause (Line 2) makes it slightly less desirable than A in strict enterprise style environments.
   
    - **Implication**: B's code demonstrates a lack of language fluency. In a production codebase, it would break naming consistency. A and C are both functionally correct, but A's explicitness makes it a better model for training AI on robustness.
   
    - **Actionable**: Response B must change get_unique_values to getUniqueValues and add braces to all control flow blocks.
    - 
