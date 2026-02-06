# Task 2 - Student Gradebook and GPA's (Build challenge)

## Overview
This project implements a student gradebook system in Python that tracks assignments across weighted grading categories, computes category averages, calculates final course grades (percentage + letter grade), computes GPA weighted by credit hours, and generates a formatted transcript.

Includes:
- Object-oriented design (`Assignment`, `Course`, `Student`, `GradeBook`)
- Category-weighted grading with validation
- Edge case handling (missing scores, empty categories)
- Unit tests for core behavior
- Demo with 3 students enrolled in 2–3 courses each

---

## Grading Rules

### Categories & Weights (must total 100%)
- HOMEWORK: 20%
- QUIZZES: 20%
- MIDTERM: 25%
- FINAL_EXAM: 35%

### Category Average
Category score = average across all assignments in that category:
- computed as `(totalPointsEarned / totalPointsPossible) * 100`

### Final Course Grade
Final grade = weighted sum of category averages.

**Edge case:** categories with **no assignments are excluded** from the calculation and the remaining weights are re-normalized.

### Letter Grades
- A: 90–100
- B: 80–89
- C: 70–79
- D: 60–69
- F: <60

### GPA Points
- A=4.0, B=3.0, C=2.0, D=1.0, F=0.0

GPA is weighted by credit hours.

---

## Prerequisites
- Python 3.10+ recommended
- pip

---

## Setup Instructions

### Create and Activate a Virtual Environment

```bash
python -m venv .venv
source .venv/bin/activate
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

---

## Run Unit Tests

From the `task_2` directory, run:

```bash
PYTHONPATH=src pytest -q
```

---

## Run Demo

```bash
PYTHONPATH=src python -m gradebook.demo
```

The demo includes three students, each enrolled in two to three courses, with varying assignments to demonstrate grading logic and edge cases.

---

## Assumptions

- **Missing Assignment Scores:** Missing assignment scores (`pointsEarned=None`) are treated as zero earned points.

- **Empty Categories:** Categories with no assignments are excluded from final grade calculation and remaining weights are re-normalized.

- **No Assignments in Any Category:** If a course has no assignments in any category, the final course grade is 0.00% (F).

- **GPA Calculation:** GPA is calculated using credit-hour weighted averaging.

