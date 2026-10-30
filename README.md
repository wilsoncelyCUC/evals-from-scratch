# Evals from Scratch

> An agent that "seems to work" is not a launch decision. A measured pass rate is.

How to prove an AI agent works before it ships, explained for the people who sign off on it:
program and project managers, product managers, and finance leads who learned enough code to be dangerous.

Twin repo of [tokenomics-from-scratch](https://github.com/wilsoncelyCUC/tokenomics-from-scratch).
That one answers *what does it cost?* This one answers *does it work?* You need both before you ship.

## Why agents need different testing

Normal software gives the same answer every time, so a test passes or fails.
An agent can give a different answer to the same question, take a different route each time,
and still be right, or be wrong while sounding right. So you test two things, not one:

- **The answer.** Did it do the job?
- **The path.** Did it get there sensibly, without breaking a business rule on the way?

## The pipeline in one picture

```
 1 DEFINE GOOD   2 TEST CASES   3 RUN      4 SCORE                5 READ TRACES   6 DECIDE      7 WATCH LIVE
 what a good     real requests  the agent  code checks            every step it   ship, fix,    every failure
 answer and a    + the answer   on every   · AI judge             took, to see    or stop       becomes a new
 good path are   and path you   case       · human review         WHY it failed                 test case
                 expect                                                                         ↺ back to 2
```

As a program manager you own steps 1, 2 and 6. Engineers own 3 to 5. Step 7 is shared.

## The notebooks

Each notebook runs top to bottom in a few minutes on the Gemini free tier, and the results are already saved
in the file, so you can read it on GitHub without running anything.

| Notebook | The job it teaches | The lesson you leave with |
| --- | --- | --- |
| [01 · Judge the answer and the path](notebooks/01-judge-the-answer-and-the-path.ipynb) | Know whether an agent did the job and took sensible steps | A word-match score fails right answers and passes wrong ones. And a right answer can hide a broken business rule. |
| [02 · Goal, plan, act](notebooks/02-goal-plan-act.ipynb) | Find where an agent goes wrong: the plan, following the plan, or wasted steps | Most failures are in the plan, not the answer. And the evaluation itself costs tokens: budget for it. |

## Run them

```bash
pip install -r requirements.txt
export GOOGLE_API_KEY=your-key   # free key at https://aistudio.google.com/apikey
jupyter notebook notebooks/
```

## Where the ideas come from

- **Notebook 01** follows the method of Google's *Agent Quality* whitepaper and its Kaggle evaluation codelab
  (5-Day AI Agents Intensive, Kaggle × Google, codelab under Apache-2.0): judge the final answer and the tool path
  separately. The scenario and code here are new.
- **Notebook 02** follows Snowflake's Goal-Plan-Action (GPA) way of breaking agent failures down, as taught in
  their agent-evaluation course and implemented in the open-source [TruLens](https://github.com/truera/trulens) library.
  The scenario and code here are new.

## License

MIT
