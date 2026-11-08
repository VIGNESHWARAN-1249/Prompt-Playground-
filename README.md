Prompt Engineering – Practical Experiments

Introduction

This project focuses on understanding three important prompt engineering techniques used to improve the quality and reliability of Large Language Model (LLM) responses.

The main aim is to learn how different prompting methods affect the way an AI model understands instructions, solves problems, and generates structured responses.

The following three techniques are explored:

1. Zero-shot and Few-shot Prompting
2. Chain-of-Thought Prompting
3. Structured JSON Output

Experiment 1: Zero-shot vs Few-shot Prompting

Objective

To understand the difference between zero-shot and few-shot prompting by performing a sentiment classification task.

1. Zero-shot Prompting

In zero-shot prompting, the model is asked to perform a task without providing any examples.

Prompt Used:

Classify the sentiment of the following
sentence as Positive, Negative, or Neutral.

Sentence:
"The delivery was late, but the product
quality is excellent."

Return only the sentiment.

Actual Model Output:

Neutral

2. Few-shot Prompting

In few-shot prompting, a few examples are provided before asking the model to perform the task. This helps the model understand the expected output format.

Prompt Used:

Classify the sentiment as Positive,
Negative, or Neutral.

Examples:

Input: I love this product.
Output: Positive

Input: The service was terrible.
Output: Negative

Input: The package arrived yesterday.
Output: Neutral

Input: The delivery was late, but the
product quality is excellent.
Output:

Actual Model Output:

Neutral


Comparison

Zero-shot| Few-shot
No examples provided| Examples provided
Uses only instructions| Learns the expected pattern from examples
Simple prompt| More detailed prompt

Analysis

In this experiment, I observed how providing examples changes the model's response.

Zero-shot prompting was useful for completing a simple classification task. Few-shot prompting provided additional guidance about the expected labels and output format.

Both methods can produce correct results, but few-shot prompting can improve consistency when the task requires a specific pattern.

---

Experiment 2: Chain-of-Thought Prompting

Objective

To compare a direct prompt with a step-by-step prompting approach for solving a mathematical problem.

Problem

A shopkeeper buys 5 notebooks for ₹40 each. He sells 3 notebooks for ₹60 each and the remaining 2 notebooks for ₹35 each.

Calculate the total profit or loss and the profit/loss percentage.

1. Direct Prompting

Prompt Used:

Calculate the profit or loss percentage.

A shopkeeper buys 5 notebooks for ₹40 each.
He sells 3 notebooks for ₹60 each and the
remaining 2 notebooks for ₹35 each.

Actual Model Output:

The profit percentage is 25%.


2. Step-by-Step Prompting

Prompt Used:

Solve this problem by breaking it into
clear calculation steps.

Show:
1. Total cost price.
2. Total selling price.
3. Profit or loss.
4. Profit or loss percentage.

A shopkeeper buys 5 notebooks for ₹40 each.
He sells 3 notebooks for ₹60 each and the
remaining 2 notebooks for ₹35 each.

Actual Model Output:

1. Total cost price: 5 notebooks × ₹40 = ₹200
2. Total selling price: (3 notebooks × ₹60) + (2 notebooks × ₹35) = ₹180 + ₹70 = ₹250
3. Profit: ₹250 - ₹200 = ₹50
4. Profit percentage: (₹50 / ₹200) × 100 = 25%

Expected Answer for Verification

- Total Cost Price = 5 × 40 = ₹200
- Total Selling Price = (3 × 60) + (2 × 35) = ₹250
- Profit = ₹250 - ₹200 = ₹50
- Profit Percentage = (50 / 200) × 100 = 25%

Final Answer: 25% Profit


Analysis

The direct prompt asked the model to calculate the answer without specifying the steps.

The step-by-step prompt clearly mentioned the calculations that were required. This made it easier to understand and verify the result.

I observed that asking for an organised explanation helps make multi-step mathematical answers easier to check. However, step-by-step instructions do not automatically guarantee correctness, so the final calculation should still be verified.

---

Experiment 3: Structured JSON Output

Objective

To make the AI model extract information from different text inputs and return the results in a fixed JSON format.

JSON Schema

The following structure is used for all test cases.

{
  "name": "string or null",
  "date": "YYYY-MM-DD or null",
  "amount": "number or null"
}

Prompt Used

Extract the person's name, date and amount
from the given text.

Return ONLY valid JSON.

Rules:
- Follow the exact JSON structure.
- Name must be a string or null.
- Date must use YYYY-MM-DD format or null.
- Amount must be a number or null.
- If a field is missing or cannot be
  determined, use null.
- Do not add explanations or Markdown.

Required structure:

{
  "name": "string or null",
  "date": "YYYY-MM-DD or null",
  "amount": "number or null"
}

Test Cases

Test 1

Input:

Rahul paid ₹500 on 12 March 2026.

Actual Output:

{ "name": "Rahul", "date": "2026-03-12", "amount": 500 }


Test 2

Input:

Priya purchased a laptop for ₹45,000 on 5 June 2026.

Actual Output:

{ "name": "Priya", "date": "2026-06-05", "amount": 45000 }


Test 3

Input:

Arjun paid 1200 rupees on 2026-08-15.

Actual Output:

{ "name": "Arjun", "date": "2026-08-15", "amount": 1200 }


Test 4

Input:

Meena made a payment of ₹750 yesterday.

Actual Output:

{ "name": "Meena", "date": null, "amount": 750 }


Test 5

Input:

Karthik paid ₹2,500 on 1 January 2026.

Actual Output:

{ "name": "Karthik", "date": "2026-01-01", "amount": 2500 }


Result Evaluation

After running all five test cases, I checked whether the model returned valid JSON and followed the defined structure.

Test Case| Valid JSON| Schema Followed
Test 1| [Yes]| [Yes]
Test 2| [Yes]| [Yes]
Test 3| [Yes]| [Yes]
Test 4| [Yes]| [Yes]
Test 5| [Yes]| [Yes]

Success Rate Calculation:

Success Rate = (5/ 5) × 100

My Result:100%
Analysis

The structured output experiment helped me understand how specific instructions can control the format of AI responses.

Defining the JSON structure, specifying data types, and clearly mentioning what to do when information is missing helped improve consistency.

Some inputs can be ambiguous, especially when dates are mentioned using words like "yesterday". Such cases need clear instructions to avoid incorrect extraction.

---

Overall Comparison

Technique| Main Purpose| Observation
Zero-shot| Perform a task without examples| Simple and direct
Few-shot| Guide the model using examples| Helps maintain consistency
Chain-of-Thought| Encourage organised reasoning| Makes calculations easier to verify
Structured Output| Generate data in a fixed format| Improves response consistency

---

Conclusion

Through these experiments, I gained a practical understanding of how prompt engineering affects AI model responses.

I learned that providing examples can help the model follow a particular pattern, clear step-by-step instructions can make complex answers easier to verify, and defining a JSON structure helps generate organised data.

I also understood that prompt engineering does not guarantee perfect results. Testing different inputs and checking the outputs are important for improving reliability.

Overall, this task helped me understand how to write better prompts and get more consistent results from Large Language Models.

---

References

- OpenAI Prompt Engineering Guide: https://platform.openai.com/docs/guides/prompt-engineering
- Prompting Guide: https://www.promptingguide.ai/
- Google AI Studio: https://aistudio.google.com/

Project Status: Practical experiments and documentation.
