# AI assistance (2026)

## Table of Contents

+ [References](#references)
+ [LLM](#llm)
+ [GPT](#gpt)


## References

- [AI course 2026](https://www.youtube.com/watch?v=2aN_-m1uU4k)

### LLM

**AI**: Computer system that can perform tasks typically requiring human intelligence (learning, reasoning, problem-solving, perception, language understanding, decision-making…). LLM is one type of AI.

**LLM** (Large Language Model): Neural networks with thousands of millions of parameters trained to, given a context, predict the next token.

- Often, the term **AI** is used to refer to LLM, though AI is a much broader term.
- There're different LLM models (GPT 5.2, Opus 4.6, DeepSeek V2, GLM 5…).

**Training** an LLM involves 3 stages:

1. **Pre-training**: Provides good knowledge about the language by feeding the LLM with massive amounts of information. Most expensive stage.
2. **Fine tuning**: Provides communications skills. It gives the ability to easily keep a conversation (better structure, better question-answer quality). Learns to follow instructions.
3. **RLHF** (Reinforcement Learning from Human Feedback): Makes it more useful. Humans and other LLMs are involved here.

**Number of parameters**: Number of adjustable items in the model. They are adjusted through training. The more parameters, the greater the capacity/potential, the higher the cost, and lower the performance. This affects the LLM limitations (like halucinations, poor reasoning, context dependency).

**Prompt**: Input (context) you provide to the LLM. The LLM answers are based on the prompt you provide. The better the prompt, the better the answer you get.

**Context window**: Maximum number of tokens (context) that you can pass to the LLM as input.

Thus, an LLM is like a function that, given a set of tokens as input (context window), outputs another set of tokens (answer). Its inner mechanism is configured by adjusting its parameters.

## GPT

The [OpenAI platform](https://platform.openai.com/chat) provides a set of tools:

- **System message**: Prompt for configuring how the model will behave (like "Only answer questions about physics").
- **Prompt messages**: Allows the user to pass the conversation history, or a fabricated user-assistant conversation, as context. This let us provide the correct context.

If we develop an API that uses AI, we can limit its behavior for safety using the "system message". However, it is still vulnerable to a prompt injection that could override our "system message".

**Token**: LLMs don't process text, but tokens. It can be a word, a piece of word, a special character, etc. You pay for the tokens you use, not for the words or letters. Also, each model has its own types of tokens. Token-efficiency depends on the model and the language used.

