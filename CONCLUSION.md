# Lab 05 — Conclusion

<!--
Read this before you write.

This file is graded by your instructor, by hand, and it is worth 6 of the 15 points.

- Type it yourself. Do not use a chatbot, an AI assistant, an AI autocomplete or a "rewrite my
  text" tool for any part of it, not even for grammar. English that is plain and a little
  clumsy but yours is better than polished text that is not.
- Use your own numbers. Every number you quote must be one your own notebook printed. Copy
  the number exactly as it appeared. A number your notebook did not print is marked as wrong.
- Answer in your own words, about 80-200 words per question. A short answer that uses your
  numbers beats a long answer that could have been written by anyone.
- Delete these comment lines if you like. Keep the three headings and the last line.
-->

## 1. Which layer changed your results the most?

Give the numbers before -> after for that layer (correct / wrong / no answer, out of 20) and say
whether it changed what the agent *can do* or only what it *admits*. If no layer changed the
number of correct answers, say so and explain what the layers did change instead.

(Layer 1 change the number of correct answers most. Before it was 16 correct, 4 wrong and 4 no answer, out of 24. After it was 18 correct, 6 wrong and 0 no answer. It changed what the agent can do, not only what it admit. Agent not stop when tool give an error, it keep working. Four questions got answer, but only two was correct, so we have more correct answers but also more wrong.

Layer 2 changed nothing, numbers stay 18, 6 and 0. Layer 3 keep 18 correct. Wrong went from 6 to 4 and two questions become NO ANSWER. It did not fix them, it only block answers what it could not check. In q18 agent said 0.55, but tool said 0.055, so Layer 3 return UNVERIFIED.)

## 2. One failure the full harness did not fix

Pick one question that the full harness (layer 3) still gets wrong or refuses. Give its id
(q01 ... q20). Open its trace in the notebook: at which step did it go wrong, and what did
the model do instead? Name one thing you would add to the harness, and what it would cost
(extra model calls, tokens, time, or a new way to fail).

(I choosing q08, question about region with lowest average wage in 2024. Agent answered “Jambyl” and this are wrong. Model called compare_regions with right arguments, and tool returned list of regions. Then model wrote only “Jambyl”. Harness said no_answer_line, and model wrote “ANSWER: Jambyl”. This flag is only about format. Real mistake is model chose wrong region from the list.

Layer 3 not catch it because it check if answer come from tool data, and “Jambyl” is in data. But grounded not mean correct. I would add tool rank_regions what find lowest and highest region with Python. Cost is one more tool and few more tokens. New risk is model ask for wrong direction.)

## 3. Workflow or agent for the monthly ranking?

Dala Insight wants to publish, every month, "which region is highest and which is lowest on one
indicator in one year". Would you ship the fixed workflow or the agent? Use the accuracy, the
number of model calls, the tokens and the time you measured in Part 1. Then say in one sentence
what kind of question would make you choose the other one.

(I would ship fixed workflow. Monthly ranking are same task every time, so we not need the model to decide what to do. In Part 1 workflow was better in all numbers. It got 13/15 correct, and agent got 9/15. It used 15 model calls, agent used 26. It used 3,852 tokens, agent used 19,835. It took 16 seconds, agent took 48.6. For monthly publish this is more cheap and more stable. I would choose agent for open question with many steps, for example how wage in one region changed over years and why.)

---

I wrote this file myself, without any AI tool.
