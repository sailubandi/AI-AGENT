
````markdown
# 🤖 Smart Study Planner AI using CrewAI + Gemini Flash

This project builds a multi-agent AI system that generates a **30-day smart study plan** to help students crack a **40 LPA tech job** while managing a full-time college schedule. The system is built using **CrewAI**, **LangChain**, and **Google’s Gemini Flash 1.5** LLM.

---

## 🛠️ How It’s Built

### 🧠 1. Powered by CrewAI Agents

The system is composed of three collaborative agents using [CrewAI](https://github.com/joaomdmoura/crewai):

- **Study Planner Agent**: Designs the day-wise study plan.
- **Productivity Coach Agent**: Adds motivation and focus tips.
- **Evaluator Agent**: Reviews and refines the plan for realism and effectiveness.

Each agent is defined with:
- A clear role
- A specific goal
- A backstory to enhance LLM role-playing ability

### 🧪 2. Tasks Assigned to Agents

Each agent is assigned a `Task` object describing:
- Their responsibilities
- Expected output
- Order of execution

The tasks are:
- `plan_task`: Create the 30-day schedule
- `coach_task`: Add daily motivation & tips
- `evaluate_task`: Review and finalize the output

Tasks are executed **sequentially** using `Crew`, ensuring logical flow.

### 🔗 3. LLM Integration with Gemini Flash

The agents are powered by **Google’s Gemini 1.5 Flash**, a fast and free LLM:

```python
from langchain_google_genai import ChatGoogleGenerativeAI

llm = ChatGoogleGenerativeAI(
    model="gemini-1.5-flash-latest",
    google_api_key=userdata.get("GOOGLE_API_KEY")
)
````

Alternatively, a fallback to **Hugging Face models** (e.g., `tiiuae/falcon-rw-1b`) can be used with `HuggingFaceHub` if no API key is available.

### ✅ 4. Executed via CrewAI Runtime

A `Crew` is initialized using:

```python
crew = Crew(
    agents=[planner, coach, evaluator],
    tasks=[plan_task, coach_task, evaluate_task],
    verbose=2
)
```

It takes an input `topic` and sequentially triggers the agent pipeline to generate the final plan.

---

## 📦 Technologies Used

* [CrewAI](https://github.com/joaomdmoura/crewai)
* [LangChain](https://www.langchain.com/)
* [Google Generative AI (Gemini)](https://makersuite.google.com/)
* HuggingFace Hub (Optional)
* Google Colab (Execution Environment)

---

## 🖥️ How to Run (Google Colab Recommended)

1. Clone or open the notebook in [Google Colab](https://colab.research.google.com/).
2. Install the required packages:

   ```bash
   !pip install crewai==0.28.8 crewai_tools==0.1.6 langchain==0.1.16 google-generativeai
   ```
3. Add your Google API Key using:

   ```python
   from google.colab import userdata
   GOOGLE_API_KEY = userdata.get("GOOGLE_API_KEY")
   ```
4. Run all the cells to trigger the multi-agent pipeline.
5. View the final result as a Markdown-formatted plan.

---


```
