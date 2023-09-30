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
    

## More Resources

* [Learn Prompting](https://learnprompting.org/)
    
* [A Guide to Prompt Engineering](https://github.com/dair-ai/Prompt-Engineering-Guide/blob/main/lecture/Prompt-Engineering-Lecture-Elvis.pdf?ref=mlq.ai)
    
* [Prompt Papers](https://github.com/thunlp/PromptPapers)