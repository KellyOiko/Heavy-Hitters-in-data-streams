# Heavy Hitters in Data Streams

This repository contains implementations and analysis of streaming algorithms for identifying heavy hitters and estimating frequencies in large data streams.  
It focuses on two fundamental approaches: the **Misra–Gries algorithm** and the **Count–Min Sketch**.  
The work is structured in four parts, each exploring a different aspect of the problem.  

---

## Part 1 – Misra–Gries Algorithm
- **Goal:** Identify all elements that occur more than `φ·n` times in a stream, with limited memory.  
- **Method:** Maintain up to `k = 1/φ – 1` counters and update them as the stream is processed.  
- **Guarantees:**  
  - At most `k` candidates are stored.  
  - Any true heavy hitter must be among the candidates.  
  - Final verification step ensures correctness.  
- **Conclusion:** The algorithm requires only `O(1/φ)` memory and provides exact identification of heavy hitters after one pass plus verification.

---

## Part 2 – Parameter Analysis
- **Example:** For `φ = 0.001`, the number of counters is `k = 999`.  
- **Observation:** The error bound for any non-candidate is at most `n / (k+1)`.  
- **Takeaway:** Choosing `k` based on the desired threshold ensures correctness with minimal memory.

---

## Part 3 – Count–Min Sketch
- **Goal:** Approximate the frequency of any element with probabilistic guarantees.  
- **Parameters:**  
  - Error factor `ε` (estimation within ±ε·n).  
  - Confidence `1 – δ`.  
  - Width `w = ⌈e / ε⌉`, depth `d = ⌈ln(1/δ)⌉`.  
- **Properties:**  
  - Always **overestimates** or gives the exact frequency (never underestimates).  
  - Requires only `O(log(1/δ)/ε)` space.  
- **Conclusion:** Suitable for large-scale streams where exact counting is infeasible. Provides fast updates and queries with bounded error.

---

## Part 4 – Variations and Extensions
- **Alternative counters:** Using a second counter can give **lower bounds** on frequencies.  
- **Hashing approaches:** Representing stream elements in different numeric bases and hashing digit vectors was explored as an alternative method.  
- **Observation:** While such variations may reduce error in special cases, Misra–Gries and Count–Min Sketch remain the standard efficient solutions.

---

## Summary
- **Misra–Gries** provides deterministic identification of heavy hitters using limited counters.  
- **Count–Min Sketch** offers fast, approximate frequency estimation with probabilistic guarantees.  
- Both methods scale efficiently to massive streams and form the foundation of modern streaming analytics.

---
