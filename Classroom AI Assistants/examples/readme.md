Automated Decision Tree Lab Grader

This repository contains an end-to-end automated grading system designed for the Supervised Learning – Decision Trees lab. The system uses a Large Language Model (LLM) "Gem" to evaluate Python notebooks, verify data processing logic, and issue tamper-proof grade reports.

🚀 Overview

The goal of this project is to streamline the grading of machine learning assignments while maintaining high academic integrity. By utilizing cryptographic signatures and automated code audit tools, the system ensures that student results are authentic and that feedback is immediate and consistent.

🛠 System Components

decision_tree_grader.txt: The system prompt (the "brain") for the automated grader. It contains the grading logic, rubric, and security protocols.

decision_tree_submission.ipynb: The student-facing template. It includes the required machine learning pipeline and an "Anti-Doctoring" block.

Tennis.csv: The standard dataset used for training the model.

🔐 Security & Integrity Features

To prevent students from manually altering accuracy scores or faking screenshots, the system employs two layers of verification:

1. The Verification Token (Student-Side)

Inside the Jupyter Notebook, a hidden code block generates a SHA-256 hash based on the student's unique ID, their model's accuracy, and the structural node count of their tree. If a student manually changes their accuracy in the text, the token will no longer match the internal model state.

2. The Grade Validation Hash (Instructor-Side)

When the grader issues a final report, it signs the grade with a "Secret Key" known only to the instructor.

Format: [Score]-[Student ID]-[Hash]

Purpose: This allows the instructor to verify that the 100% score the student uploaded to the LMS was actually issued by the grader and not edited in a text editor.

📝 Workflow

Instructor Setup

Create a Gem: Create a new Custom GPT or Gem in your environment.

Apply System Prompt: Copy the contents of decision_tree_grader.txt into the System Instructions.

Enable Tools: Ensure File Uploads, Code Execution, and Vision are enabled.

Upload Knowledge: Upload Tennis.csv to the Gem's knowledge base so it knows the "ground truth" of the data.

Student Submission

Complete the Lab: Students use the provided notebook to train their model.

Generate Token: Students run the verification cell to generate their unique token.

Interact with Grader: Students upload their .ipynb file and the three required screenshots (Dataset Head, Tree Visualization, Accuracy Score) to the Gem.

Receive Report: The Gem audits the files and provides a "Final Grade Report."

Final Grading

Students copy the Final Grade Report exactly and submit it to the course portal (e.g., Canvas or Blackboard).

Instructors can verify the authenticity of any grade by checking the Verification Code against the secret key logic.

📊 Rubric Summary

The system evaluates submissions out of 100 points:

Data Processing (30 pts): Proper Label Encoding and dropping of irrelevant features (Day ID).

Model Implementation (40 pts): Correct sklearn configuration, train/test split, and tree visualization.

Analysis & Logic (20 pts): Identification of the root node and interpretation of Gini impurity.

Future Optimization (10 pts): Critical thinking on how to improve models on small datasets.

🛑 Behavior Rules

The grader is programmed to be an Evaluator, not a Tutor. It will:

Refuse to provide "perfect" code examples.

Decline requests to ignore the rubric.

Flag integrity mismatches if the internal notebook math doesn't match the claims.
