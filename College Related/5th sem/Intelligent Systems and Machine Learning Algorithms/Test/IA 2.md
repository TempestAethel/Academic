# Intelligent Systems and Machine Learning Algorithms (Module 4) - Question Bank

## Table of Contents

1. [Define Machine Learning. Explain with examples why machine learning is important.](#q1)
2. [Discuss some applications of machine learning with examples.](#q2)
3. [Explain how some disciplines have influenced machine learning.](#q3)
4. [What are well-posed learning problems?](#q4)
5. [Describe the problems with respect to Tasks, Performance, and Experience.](#q5)
6. [Explain the steps in designing a learning system in detail.](#q6)
7. [Explain different perspectives and issues in machine learning.](#q7)
8. [Define concept learning and discuss with examples.](#q8)
9. [Explain the General-to-Specific Ordering of Hypotheses.](#q9)
10. [Write FIND-S algorithm and explain with example.](#q10)
11. [What are the key properties and complaints of the FIND-S algorithm?](#q11)
12. [Define Consistent Hypothesis and Version Space.](#q12)
13. [Write a LIST-THEN-ELIMINATE algorithm.](#q13)
14. [Write the candidate elimination algorithm and illustrate with example.](#q14)
15. [Write the final version space for given training examples using candidate elimination algorithm.](#q15)
16. [Explain in detail the Inductive Bias of Candidate Elimination algorithm.](#q16)

---

## Questions and Placeholders

### 1. Define Machine Learning. Explain with examples why machine learning is important.  {#q1}
**Question:**  
Define Machine Learning. Explain with examples why machine learning is important.  

**Answer Placeholder:**  
<!-- Write your answer here -->

---

### 2. Discuss some applications of machine learning with examples.  {#q2}
**Question:**  
Discuss some applications of machine learning with examples.  

**Answer Placeholder:**  
<!-- Write your answer here -->

---

### 3. Explain how some disciplines have influenced machine learning.  {#q3}
**Question:**  
Explain how some disciplines have influenced machine learning.  

**Answer Placeholder:**  
<!-- Write your answer here -->

---

### 4. What are well-posed learning problems?  {#q4}
**Question:**  
What are well-posed learning problems?  

**Answer Placeholder:**  
<!-- Write your answer here -->

---

### 5. Describe the problems with respect to Tasks, Performance, and Experience.  {#q5}
**Question:**  
Describe the following problems with respect to Tasks, Performance, and Experience:  

a. A Checkers learning problem  
b. A Handwritten recognition learning problem  
c. A Robot driving learning problem  

**Answer Placeholder:**  
<!-- Write your answer here -->

---

### 6. Explain the steps in designing a learning system in detail.  {#q6}
**Question:**  
Explain the steps in designing a learning system in detail.  

**Answer Placeholder:**  
<!-- Write your answer here -->

---

### 7. Explain different perspectives and issues in machine learning.  {#q7}
**Question:**  
Explain different perspectives and issues in machine learning.  

**Answer Placeholder:**  
<!-- Write your answer here -->

---

### 8. Define concept learning and discuss with examples.  {#q8}
**Question:**  
Define concept learning and discuss with examples.  

**Answer Placeholder:**  
<!-- Write your answer here -->

---

### 9. Explain the General-to-Specific Ordering of Hypotheses.  {#q9}
**Question:**  
Explain the General-to-Specific Ordering of Hypotheses.  

**Answer Placeholder:**  
<!-- Write your answer here -->

---

### 10. Write FIND-S algorithm and explain with example.  {#q10}
**Question:**  
Write FIND-S algorithm and explain with the following example:  

| Instance | Sky   | AirTemp | Humidity | Wind   | Water | Forecast | EnjoySport |
|----------|-------|---------|----------|--------|-------|----------|------------|
| 1        | Sunny | Warm    | Normal   | Strong | Warm  | Same     | Yes        |
| 2        | Sunny | Warm    | High     | Strong | Warm  | Same     | Yes        |
| 3        | Rainy | Cold    | High     | Strong | Warm  | Change   | No         |
| 4        | Sunny | Warm    | High     | Strong | Cool  | Change   | Yes        |

**Answer Placeholder:**  
<!-- Write your answer here -->

---

### 11. What are the key properties and complaints of the FIND-S algorithm?  {#q11}
**Question:**  
What are the key properties and complaints of the FIND-S algorithm?  

**Answer Placeholder:**  
<!-- Write your answer here -->

---

### 12. Define Consistent Hypothesis and Version Space.  {#q12}
**Question:**  
Define Consistent Hypothesis and Version Space.  

**Answer Placeholder:**  
<!-- Write your answer here -->

---

### 13. Write a LIST-THEN-ELIMINATE algorithm.  {#q13}
**Question:**  
Write a LIST-THEN-ELIMINATE algorithm.  

**Answer Placeholder:**  
<!-- Write your answer here -->

---

### 14. Write the candidate elimination algorithm and illustrate with example.  {#q14}
**Question:**  
Write the candidate elimination algorithm and illustrate with an example.  

**Answer Placeholder:**  
<!-- Write your answer here -->

---

### 15. Write the final version space for given training examples using candidate elimination algorithm.  {#q15}
**Question:**  
Write the final version space for the below-mentioned training examples using candidate elimination algorithms:  

**Training Examples:**  


| Instance | Sky   | AirTemp | Humidity | Wind   | Water | Forecast | EnjoySport |
|----------|-------|---------|----------|--------|-------|----------|------------|
| 1        | Sunny | Warm    | Normal   | Strong | Warm  | Same     | Yes        |
| 2        | Sunny | Warm    | High     | Strong | Warm  | Same     | Yes        |
| 3        | Rainy | Cold    | High     | Strong | Warm  | Change   | No         |
| 4        | Sunny | Warm    | High     | Strong | Cool  | Change   | Yes        |

**Hypothesis Representation after Candidate Elimination Algorithm:**  

| Iteration | Specific Hypothesis              | General Hypothesis                                       |
|-----------|----------------------------------|---------------------------------------------------------|
| 0         | `< ∅, ∅, ∅, ∅, ∅, ∅ >`           | `< ?, ?, ?, ?, ?, ? >`                                  |
| 1         | `< Sunny, Warm, Normal, Strong, Warm, Same >` | `< ?, ?, ?, ?, ?, ? >`                                  |
| 2         | `< Sunny, Warm, ?, Strong, Warm, Same >`      | `< ?, ?, ?, ?, ?, ? >`                                  |
| 3         | `< Sunny, Warm, ?, Strong, Warm, Same >`      | `< ?, ?, ?, ?, ?, ? >, < Sunny, ?, ?, ?, ?, ? >`       |
| 4         | `< Sunny, Warm, ?, Strong, ?, ? >`            | `< Sunny, ?, ?, ?, ?, ?>, < ?, Warm, ?, ?, ?, ?>`       |

**Answer Placeholder:**  
<!-- Write your answer here -->

---

### 16. Explain in detail the Inductive Bias of Candidate Elimination algorithm.  {#q16}
**Question:**  
Explain in detail the Inductive Bias of Candidate Elimination algorithm.  

**Answer Placeholder:**  
<!-- Write your answer here -->

---
