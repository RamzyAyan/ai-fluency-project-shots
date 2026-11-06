# Project proposal

## 1. The problem and goal

(Explain the problem you want to solve and why it matters. Describe what you
want to improve, how you will measure improvement, and which limits or
requirements must be respected. A short example can help someone outside your
field understand the problem.)

**The problem and goal in my project:**

A continuous stirred-tank reactor turns A into B, and a side reaction turns B into an unwanted C. I want the highest yield of B the reactor can give while its temperature stays below 350 K, for safety. Yield is the measure: moles of B out per mole of A in.

## 2. The simulator

(Describe a program or model that could simulate your system and calculate what
happens under different conditions. Explain what inputs it takes and what
results it produces. State whether it can run on your computer and accept inputs
in a text file, such as JSON or YAML. If you have not chosen a simulator yet,
name an option you want to explore and explain what you need to check.)

**The simulator in my project:**

A small Python model of the reactor: the mass and energy balances, with Arrhenius rates for both reactions. It reads one JSON file (temperature set point, feed flow, feed concentration) and returns the conversion, the yield of B and the peak temperature. It runs on my laptop in under a second.

## 3. The agent's role

(Explain what the language-model-based agent will decide or change, and how it
will use the simulator's results to choose its next action. If known, list the
variables it may change and their allowed ranges. Explain what you expect the
language model to contribute: could a simple program that tries different
options and picks the best result achieve the same goal? Include one question
you still need to answer.)

**The agent in my project:**

The agent proposes the next set point and feed flow, within 300–350 K and 0.5–2.0 L/min, runs the model, reads the yield and the peak temperature, and adjusts. A grid search over the same ranges could also find the best yield; the agent has to earn its place by explaining the trade-off between conversion and the side reaction, and by reacting when a run breaks the safety limit. My open question: how many runs does the agent need to beat a 10-by-10 grid?

## Explain your project to someone outside your field

(Now describe your whole project again, as if you were explaining it to someone
from another field who has no background in your topic. For example, if you
study chemical engineering, imagine explaining it to a physicist; if you study
aeronautical engineering, imagine explaining it to someone in medicine; if you
study data science, imagine explaining it to a materials engineer. In one or two
short paragraphs, connect all three parts: the problem you want to solve, how
the simulator helps you test ideas, and what the agent will decide or change.
Use everyday language, explain any technical terms you need, and avoid
unexplained abbreviations. Do not simply copy your answers above.)

**My project in simple words:**

A reactor is a heated tank where one chemical becomes another. If it runs too cool, little reacts; too hot, the good product breaks down into waste, and the tank can overheat. I have a small computer model that predicts what the tank does for any setting. An AI assistant will try settings on that model, read what happened, and choose the next try, looking for the setting that makes the most good product without getting too hot. The model does the chemistry; the assistant decides what to try next; I check its choices.
