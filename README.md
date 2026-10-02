# 🔄 Loop Engineering

> Stop Prompting. Design the Loop.

A hands-on workshop demonstrating the difference between **Prompt Engineering** and **Loop Engineering** by using an AI model to fix and verify a broken Sri Lankan phone number normalizer.

The core idea is:

> **A loop is a task plus a check.**

The notebook shows how adding an automated verifier, feedback, retry mechanism, and stop rules makes AI-generated solutions more reliable.

---

## 🎯 What This Project Demonstrates

The notebook solves the same task in two different ways:

| Approach | Verification |
|---|---|
| Prompt Engineering | Manually checked by the developer |
| Loop Engineering | Automatically checked by the system |

### Prompt Engineering

```text
Prompt → AI Model → Answer
```

The model generates an answer, but the system does not automatically verify whether it is correct.

### Loop Engineering

```text
Task
 ↓
AI Model
 ↓
Verifier
 ↓
Pass? ── Yes → Stop
   │
   No
   ↓
Feedback
   ↓
AI Model
   ↓
Retry
```

---

## 🧪 Main Task

The notebook starts with a deliberately broken function:

```python
def normalize_phone(raw):
    return "+94" + raw[1:]
```

The goal is to normalize different Sri Lankan phone-number formats into:

```text
+94771234567
```

and return `None` for invalid input.

The test suite checks:

- Local format
- International format
- `00` international prefix
- Spaces
- Dashes
- Whitespace
- Invalid numbers
- Empty input

---

## 🤖 AI Model

The project uses the **Google GenAI SDK** and Gemini models.

A fallback model ladder is implemented so that if one model is unavailable or busy, the system can try another model.

Example fallback:

```text
gemini-3.5-flash
        ↓
gemini-3-flash-preview
        ↓
gemini-3.1-flash-lite
```

---

## 🔁 Loop Engineering

The loop contains four important components:

1. **Trigger** — starts the process
2. **Goal** — all tests must pass
3. **Verifier** — automatically checks the generated code
4. **Stop Rules** — stops when the goal is achieved or the iteration limit is reached

The loop follows:

```text
Generate
   ↓
Check
   ↓
Observe failures
   ↓
Provide feedback
   ↓
Generate again
   ↓
Repeat until success / limit
```

---

## 📊 Key Demonstration

The notebook demonstrates:

- Broken code failing the test suite
- Prompt engineering producing inconsistent results
- Automated verification
- Failed tests becoming feedback for the next attempt
- Automatic retries
- Iteration limits
- Failure reporting
- The importance of a reliable verifier

It also demonstrates two failure cases:

### Impossible Goal

An unsatisfiable test causes the loop to reach its iteration limit instead of running indefinitely.

### Weak Verifier

A weak test can cause the system to incorrectly accept broken code.

This demonstrates:

> **The loop is only as good as the check at the centre of it.**

---

## 🛠️ Technologies

- Python
- Jupyter Notebook
- Google GenAI SDK
- Gemini Models
- Python Standard Library
- Automated Test Verification

---

## 📦 Installation

Install the Google GenAI SDK:

```bash
pip install google-genai
```

Start Jupyter:

```bash
jupyter notebook
```

Open:

```text
LoopEng.ipynb
```

---

## 🔑 API Key

The notebook supports:

### Google Colab

Store your API key as:

```text
GEMINI_API_KEY
```

in Colab Secrets.

### Local Jupyter / VS Code

Create a `.env` file:

```env
GEMINI_API_KEY=your_api_key_here
```

**Never commit your API key to GitHub.**

---

## 📁 Project Structure

```text
Loop-Engineering-Template/
│
├── LoopEng.ipynb
└── README.md
```

---

## 👨‍💻 Author

**Ilmaan Ahamed**  
Software Engineering Undergraduate  
SLTC Research University  

---

## 💡 Key Takeaway

Prompting asks an AI model to produce an answer.

**Loop Engineering builds a system that can produce, check, learn from failure, retry, and stop reliably.**

> **The intelligence lives in the model.  
> The reliability lives in the loop.**
