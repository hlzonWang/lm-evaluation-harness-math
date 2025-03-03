## **LM-Evaluation-Harness-MATH**

The public accuracy rate of Math500 for mainstream large language models.

| Model                           | Math-500 Accuracy |
| :--------------------------- | :---------- |
| Deepseek R1                  | 97.3        |
| Kimi K1.5 long-CoT           | 96.2        |
| Kimi K1.5 short-CoT          | 94.6        |
| Deepseek R1-Distill-Qwen-7B  | 92.8        |
| Deepseek V3                  | 90.2        |
| Openai o1-mini               | 90.0        |
| DeepSeek-R1-Distill-Llama-8B | 89.1        |
| Claude-3.5-Sonnet-1022       | 78.3        |
| GPT-4o                       | 74.6        |

Reference:

[GitHub - deepseek-ai/DeepSeek-R1](https://github.com/deepseek-ai/DeepSeek-R1)

[GitHub - MoonshotAI/Kimi-k1.5](https://github.com/MoonshotAI/Kimi-k1.5)



### Install Guide

To use this project, you need to download and install it completely on your computer first.

```bash
git clone --depth 1 https://github.com/hlzonWang/lm-evaluation-harness-math
cd lm-evaluation-harness-math
pip install -e .
pip install -e ."[api]"
```

```bash
pip install openai
```


### User Guide

To test the accuracy of LLM on the MATH-500 dataset using this project, the following command is required (with an example of an API call to Deepseek R1).

```bash
HF_ENDPOINT=https://hf-mirror.com OPENAI_API_KEY=<Your DeepSeek API key> lm_eval \
--model openai-chat-completions     \
--model_args model=deepseek-reasoner,timeout=30,max_retries=10 --limit 500    \
--tasks math-500 \
--apply_chat_template \
--num_fewshot 0 \
--log_sample \
--output_path ../result_math500_deepseekr1 \
--use_cache ./cache/cache.db \
--cache_requests true
```

You should to replace \<Your DeepSeek API key> to your deepseek api key. The api key can be get from following website.

[DeepSeek | 深度求索](https://www.deepseek.com/)


### Final Result
DeepSeek R1 MATH-500 accuracy is 97.0%(It was 94.4% before correction). This can be found in the deepseek-r1-result.

File "math-500\_replace.txt" is a modified replacement file for the answer format in math500, where many latex symbols are not uniform, such as \frac and \dfrac, which is disastrous for the Exact Match.

Many of the original correct answers, due to the project's "Answer" capture mechanism(\boxes), were judged to be wrong(or \[invaild]), the file "math-500-mistake-correct.txt" is a correction of this error, the original accuracy of 94.4% was improved to 97%.



DeepSeek R1-Distill-Qwen-7B MATH-500 accuracy can be found in the deepseek-r1-Qwen-result. The accuracy is lower than expected, possibly due to Prompt's failure, and most cases occur due to a large number of thoughts (usually more than 2048 tokens) being truncated and unable to give a final answer.



This project is derived from the following project, modified to apply to mathematical reasoning and Deepseek API calls.

[EleutherAI/lm-evaluation-harness: A framework for few-shot evaluation of language models.](https://github.com/EleutherAI/lm-evaluation-harness)



