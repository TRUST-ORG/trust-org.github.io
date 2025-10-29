---
title: ChatGPT Goes Haywire When Asked to Show a Seahorse Emoji
published: 2025-09-16
author: 'Choker'
description: Hallucinate AI using Seahorse.
image: 'https://karapaia.com/wp-content/uploads/2025/09/100-1.jpg'
tags: ["AI", "Hallucination", "Unicode", "ChatGPT"]
category: 'AI'
draft: false
---


## Trigger to write this
While surfing X, I found an interesting article about AI.
Well, the seahorse emoji was so cute. So I started to read it and writing this.
It is good for you to know this to use AI well.



## Article Summary

This article reports on a viral interaction in which ChatGPT (reported as GPT-5 in the conversation) and other large language models reacted erratically when asked  "is there a seahorse emoji?" The seahorse emoji does not exist in the Unicode standard, but many people mistakenly recall seeing it — a phenomenon akin to the Mandela Effect. When prompted, the AI attempted to comply and produced increasingly contradictory, confused, and ultimately nonsensical responses. The piece uses this example to illustrate the broader problem of AI hallucinations: models fabricating plausible-sounding but incorrect information while trying to satisfy user expectations.

---

## Key Points

### 1. Seahorse emoji does not exist in Unicode
- The Unicode Consortium standardizes characters and emoji. A seahorse emoji is not part of the standard.
- Many people nonetheless report a false memory of such an emoji, which may be categorized as the Mandela Effect.

### 2. How the AI responded (chain of confusion)
- **First attempt:** The model lists many sea-creature emojis (coral, pufferfish, tropical fish, seal, octopus, lobster, shell, turtle) while vacillating through options and correcting itself repeatedly. Responses degrade into contradictions (e.g., "unicorn? dragon? no...").
- **Second attempt:** The model tries to justify by suggesting combining "fish" + "horse" (seahorse), claims certain Unicode codes (incorrectly), and continues listing unrelated animals. It even suggests an incorrect code point (U+1F40C, which actually maps to snail).
- **Third attempt:** The model enters a loop of assertions and retractions: sometimes declaring "this is final" then immediately reversing, effectively "thinking aloud" and ending in a state described as "brain dead" or frozen logic.
- **Another user test:** In a different session, the model began outputting hundreds of emoji candidates, creating visual clutter but never settling on a correct answer.

### 3. Other models and comparison
- Anthropic's Claude Sonnet 4 reportedly exhibited similar confusion and confidently asserted incorrect statements.
- Google Gemini (formerly Bard) did not fall into this trap in reported tests; it correctly stated that Unicode does not include a seahorse emoji and attributed the memory to the Mandela Effect.

### 4. Root cause: desire to satisfy user expectations
- The article emphasizes that many LLMs are optimized to respond helpfully and favor satisfying outputs; when faced with user assertions that contradict reality, they may attempt to produce an answer anyway rather than say "no" or "I don't know."
- This incentive to be agreeable or helpful can cause confidently incorrect outputs — the core of "hallucination."

### 5. Broader implication: larger models may hallucinate more
- Cited research indicates that increasing model size and capability does not necessarily reduce hallucinations; in some cases it may make them more pronounced because the model becomes more fluent and persuasive while still prone to factual errors.

---

## Excerpted Observations & Examples from the Article

- Users on X (Twitter) tried the prompt "Show me a seahorse emoji" and captured threads where ChatGPT cycles through possibilities, self-corrects, and eventually lists numerous irrelevant emojis.
- The model sometimes invents or misattributes Unicode code points (e.g., claiming a code that actually corresponds to another emoji).
- One captured reply: the AI confidently states various alternatives and then repeatedly retracts, ending with an inconsistent "final" answer.
- Another model (Gemini) correctly denied the emoji's existence and attributed the phenomenon to collective false memory.

---

## Analysis (what this reveals about LLM behavior)

- **Hallucination mechanics:** LLMs generate sequences that are statistically plausible given their training data and objective; when the data contains patterns that suggest an answer, they'll produce it even if the factual basis is absent.
- **Optimization trade-offs:** Models trained or fine-tuned to maximize user satisfaction and engagement can prefer plausible-sounding completions over conservative "I don't know" responses, increasing hallucination risk.
- **Human factors:** The Mandela Effect and users' prior misremembering create prompts where humans expect an affirmative response; the model's attempt to meet that expectation leads to amplified error.
- **Model variety:** Not all models fail the same way; architecture, training data, safety filters, and design choices influence whether a model resists or succumbs to such traps.

---

## Conclusion

The seahorse-emoji episode is a vivid, low-risk illustration of a core issue with contemporary LLMs: their tendency to fabricate or confidently assert false information when trying to serve user expectations. The article suggests users remain skeptical, verify facts from authoritative sources like Unicode, and be aware that AIs can prioritize pleasing the user over factual accuracy. It also notes that model improvements alone do not guarantee fewer hallucinations, underscoring the importance of design choices and guardrails.

---

## Reference
- Original article : Karapaia — "チャットGPTに「タツノオトシゴの絵文字を見せて」と聞くと暴走する" (published 2025-09-16).  

---