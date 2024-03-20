---
title: "Prompting"
datePublished: Wed Mar 01 2023 17:27:10 GMT+0000 (Coordinated Universal Time)
cuid: clklfgr2u000q0ajthweo1qh2
slug: prompting

---

**Prompts** involve instructions and context passed to a language model to achieve a desired task.

**Prompt engineering** is the practice of developing and optimizing prompts to efficiently use language models (LMs) for a variety of applications.

Writing prompts are not just writing simple queries or instructions to find an answer. But it is a lot more than that.

Many companies have created a separate position for prompt writers known as `prompt engineers` after knowing how much effort, domain knowledge, time and iteration it takes to create an optimized prompt.

Examples of a few jobs and their responsibilities:

* Prompt Engineer & Librarian [here](https://jobs.lever.co/Anthropic/e3cde481-d446-460f-b576-93cab67bd1ed)
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690472218331/d28c151d-a42b-417b-bf44-5510b6e12bec.png align="center")

* NLP Prompt Engineer
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690470621968/bfe2ceee-cadd-4d09-bb71-1aebfd525f0d.png align="center")

* Prompt Engineer - LLM & NLP
    
    \- Linguistics knowledge
    
    \- Experience with foundational models like GPT-3/ChatGPT in
    
    * creating prompts,
        
    * validating the prompt responses,
        
    * refining the prompt
        
    * Need to close work with AI scientists.
        
    
    \- Moderate Python programming skills- Collaborate with product and design teams to create engaging and effective conversational prompts for our chatbots and virtual assistants.
    
* More jobs [here](https://prompt-engineering-jobs.com/) and
    
* Resources for preparation
    

---

All these are done to harness the power of the LLM model and extract the right information from it.

*Model capabilities depend on context* When learning to work with GPT-3, one common conceptual mistake is to believe that its capabilities are fixed across all contexts. E.g., if GPT-3 gets a simple logic question wrong, then it must be incapable of simple logic.

But as the "Let's think step by step" example illustrates, apparent failures of GPT-3 can sometimes be remedied with a better prompt that helps the model steer itself toward the correct output.

**How to improve reliability on complex tasks**

* Give clearer instructions
    
* Split complex tasks into simpler subtasks
    
* Structure the instruction to keep the model on task
    
* Prompt the model to explain before answering
    
* Ask for justifications of many possible answers, and then synthesize
    
* Generate many outputs, and then use the model to pick the best one
    
* Fine-tune custom models to maximize performance
    

---

There are different techniques proposed by several researchers for different purposes and different cases such as:

* Zero shot [paper](https://arxiv.org/abs/2205.11916) 2022
    
* Few shot: [here](https://ai.googleblog.com/2022/05/language-models-perform-reasoning-via.html) Chain of Thought (CoT) Prompting, May 11 2022
    
* More techniques [here](https://github.com/openai/openai-cookbook/blob/main/techniques_to_improve_reliability.md)
    

But 2 things remain common

1. clarity: Clarity describes the use of simple, unambiguous language and
    
2. specificity: Its nothing but need for context source https://haystack.deepset.ai/blog/beginners-guide-to-llm-prompting
    

it doesn't matter whether it is a full-time job or it is part of your job, or you are using chatgpt, you will require a good prompt to get a quality result.

As writing efficiently and optimizing prompts requires an engineer to understand the task thoroughly

* The domain of the subject
    
* what kind of information are you expecting
    
* iterating over prompts to make it efficient.
    
* managing as the prompt grows.
    

## Prompt techniques

Prompt Techniques are [use-case/task](https://www.promptingguide.ai/introduction/examples) specific.

## COT

COT: has been shown to be effective in improving results on tasks like arithmetic, commonsense, and symbolic reasoning tasks

Examples from paper [https://hackmd.io/@tamera/chain-of-thought-examples](https://hackmd.io/@tamera/chain-of-thought-examples)

Zero shot COT

![](https://learnprompting.org/assets/images/zero_shot_example-f98e34cb8ed72c5520cfd08c3c1c2f44.webp align="left")

The extraction step often must be task-specific, *making Zero-Shot-CoT less generalizable than it appears at first*.

self-consistency with COT can be thought of an performing multiple time and asking for confidence among these 3 prompts, this is more suitable for generation and then filtering by classifying.

## Tree of thoughts

A framework that generalizes over chain-of-thought prompting and encourages exploration over thoughts that serve as intermediate steps for general problem solving with language models.

![TOT](https://www.promptingguide.ai/_next/image?url=%2F_next%2Fstatic%2Fmedia%2FTOT.3b13bc5e.png&w=3840&q=75 align="left")

source: [**Tree of Thoughts: Deliberate Problem Solving with Large Language Models**](https://arxiv.org/abs/2305.10601)\*\*,\*\**17 May 2023 ,*[*github*](https://github.com/princeton-nlp/tree-of-thought-llm)

Prompt Examples:

```json
Imagine three different experts are answering this question.
All experts will write down 1 step of their thinking,
then share it with the group.
Then all experts will go on to the next step, etc.
If any expert realises they're wrong at any point then they leave.
The question is...
```

Example 2

```json
standard_prompt = '''
Write a coherent passage of 4 short paragraphs. The end sentence of each paragraph must be: {input}
'''

cot_prompt = '''
Write a coherent passage of 4 short paragraphs. The end sentence of each paragraph must be: {input}

Make a plan then write. Your output should be of the following format:

Plan:
Your plan here.

Passage:
Your passage here.
'''


vote_prompt = '''Given an instruction and several choices, decide which choice is most promising. Analyze each choice in detail, then conclude in the last line "The best choice is {s}", where s the integer id of the choice.
'''

compare_prompt = '''Briefly analyze the coherency of the following two passages. Conclude in the last line "The more coherent passage is 1", "The more coherent passage is 2", or "The two passages are similarly coherent".
'''

score_prompt = '''Analyze the following passage, then at the last line conclude "Thus the coherency score is {s}", where s is an integer from 1 to 10.
'''
```

Example 3

```json
Here are 4 potential prompts for each function:

generate_thoughts
"Given the current state of reasoning:\n\n'{state_text}'\n\nGenerate the next logical thought to advance the reasoning process and find a solution. Consider the following factors: {self.ReAct_prompt}"
"Based on the current reasoning state:\n\n'{state_text}'\n\nProvide the next coherent thought that will help progress the reasoning process and reach a solution. Keep in mind: {self.ReAct_prompt}"
"With the current state of reasoning:\n\n'{state_text}'\n\nDetermine the next appropriate thought to enhance the reasoning process and achieve a solution. Take into account: {self.ReAct_prompt}"
"Considering the present state of reasoning:\n\n'{state_text}'\n\nFormulate the next rational thought to improve the reasoning process and obtain a solution. Remember: {self.ReAct_prompt}"

generate_solution
"Based on the following reasoning:\n\n'{state_text}'\n\nProvide the most effective solution for the task: {initial_prompt}"
"With the given reasoning:\n\n'{state_text}'\n\nDetermine the optimal solution to address the task: {initial_prompt}"
"Considering the reasoning provided:\n\n'{state_text}'\n\nDevise the best possible solution for the task: {initial_prompt}"
"Taking into account the reasoning:\n\n'{state_text}'\n\nFormulate the most suitable solution for the task: {initial_prompt}"

evaluate_states (value strategy)
"Given the current state of reasoning: '{state_text}', assess its value as a float between 0 and 1, considering potential risks and challenges in achieving {initial_prompt}. Provide only a float value."
"For the current reasoning state: '{state_text}', evaluate its worth as a float between 0 and 1, taking into account possible obstacles and difficulties in accomplishing {initial_prompt}. Respond with a float value only."
"With the present state of reasoning: '{state_text}', estimate its value as a float ranging from 0 to 1, while considering potential setbacks and issues in reaching {initial_prompt}. Only provide a float value."
"Considering the state of reasoning: '{state_text}', appraise its value as a float between 0 and 1, keeping in mind potential hindrances and complications in achieving {initial_prompt}. Respond solely with a float value."


evaluate_states (vote strategy)
"Given the following states of reasoning, assign a score between 1 and 10 for the best state, considering the probability of achieving {initial_prompt} while being very pessimistic:\n{states_text}\n\nProvide only a score."
"Based on the provided states of reasoning, rate the most promising state with a score from 1 to 10, taking into account the likelihood of accomplishing {initial_prompt} and being very pessimistic:\n{states_text}\n\nRespond with a score only."
"With the given reasoning states, evaluate the top state by giving it a score between 1 and 10, considering the probability of reaching {initial_prompt} while maintaining a pessimistic outlook:\n{states_text}\n\nOnly provide a score."
"Considering the states of reasoning, assess the best state by assigning a score from 1 to 10, keeping in mind the chances of achieving {initial_prompt} and being very pessimistic:\n{states_text}\n\nRespond solely with a score."
```

More examples, [1](https://github.com/dave1010/tree-of-thought-prompting) , [TOT-llm](https://github.com/princeton-nlp/tree-of-thought-llm/tree/master/src/tot/prompts)

The difference between COT and TOT according to official TOT paper is

> In decomposition of thoughts (e.g. intermediate phrase, a sentence, or a paragraph) is left ambiguous

> Thought decomposition. While CoT samples thoughts coherently without explicit decomposition, ToT leverages problem properties to design and decompose intermediate thought steps.

Note:

* These prompt techniques might not work for simple use-cases, as LLMs have been improved after these methods were proposed. So now you get a better results with simple prompts.
    

---

ReAct: synergizing reasoning and acting in language models [paper](https://arxiv.org/pdf/2210.03629.pdf)

---

## Parameters

Temprature: value range from 0 to 2, and

the output at temprature value 0.1 is more focused, concrete and have consistent output where as 2 will have more random and varied output.

you will have to figure out the balanced value through trial and error.

If you are building application in field like legal, medical prescription , technical domain here you might require temprature as 0.2 or so..

And if you are building applications for creative fields, marketing, sales, fiction writer, idea generation you might agree with higher temprature.

---

## Prompt tools

[LMQL](https://lmql.ai/)

---

## References

* [Prompting Guide](https://www.promptingguide.ai)
    
* Hugging face promt guide [here](https://huggingface.co/docs/transformers/main/en/tasks/prompting)
    
* Tips to enhance prompt by google [here](https://cloud.google.com/blog/products/application-development/five-best-practices-for-prompt-engineering)
    

## More Resources

* [Learn Prompting](https://learnprompting.org/)
    
* [A Guide to Prompt Engineering](https://github.com/dair-ai/Prompt-Engineering-Guide/blob/main/lecture/Prompt-Engineering-Lecture-Elvis.pdf?ref=mlq.ai)
    
* [Prompt Papers](https://github.com/thunlp/PromptPapers)
    
* [Azure](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/advanced-prompt-engineering?pivots=programming-language-chat-completions)