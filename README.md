# UPSC Essay Evaluator — LangGraph + OpenAI

An AI-powered essay evaluation agent built with LangGraph that runs parallel evaluation across three dimensions and generates a final summarized score and feedback.

## Features
- Parallel evaluation across 3 criteria simultaneously:
  - Language quality
  - Depth of analysis
  - Clarity of thought
- Structured scoring via Pydantic schema (score out of 10 per dimension)
- Auto-calculated average score across all dimensions
- Final summarized feedback combining all three evaluations

## Tech Stack
- Python, LangGraph, LangChain, OpenAI GPT-4o-mini
- Pydantic v2 for structured evaluation schema

## Graph Flow

```
START → [evaluate_language | evaluate_analysis | evaluate_thought] → final_evaluation → END
```

All three evaluation nodes run in parallel, then merge into final evaluation.

## Setup

```bash
pip install langgraph langchain langchain-openai python-dotenv pydantic
```

Create a `.env` file:
```
OPENAI_API_KEY=your_openai_api_key
```

## Run

Open and run `essay_analyser_workflow.ipynb` in Jupyter or VS Code.

## Example Usage

```python
initial_state = {
    'essay': "Your essay text here..."
}
result = workflow.invoke(initial_state)
print(result['overall_feedback'])
print(result['avg_score'])
```

## Example Output

```json
{
  "language_feedback": "...",
  "analysis_feedback": "...",
  "clarity_feedback": "...",
  "overall_feedback": "Summarized feedback across all dimensions...",
  "individual_scores": [8, 7, 9],
  "avg_score": 8.0
}
```
