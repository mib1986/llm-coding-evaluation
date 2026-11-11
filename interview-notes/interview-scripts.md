# L3+ Software Engineering Interview Scripts

## Q1: If an assistant claims this function is “thread-safe because Python has a GIL,” how would you evaluate that claim for correctness and clarity, at a high level?
Full answer:
This claim is incorrect. The Global Interpreter Lock only lets one Python thread execute bytecode at a time. It does not automatically make code thread-safe.
Thread safety depends on whether the code shares mutable state without proper locks. Even with the GIL, race conditions can still happen between bytecode operations.
To evaluate the response, I check two things: first, whether the assistant correctly distinguishes the GIL’s real purpose versus thread safety. Second, whether it explains that shared mutable variables still need synchronization primitives like locks. If it mixes these two concepts up, the reasoning is flawed.

Short version:
The statement is wrong. Python’s GIL limits concurrent bytecode execution, but it does not guarantee thread safety. Race conditions on shared mutable data are still possible. True thread safety requires explicit locking, not just relying on the GIL.

## Q2: You’re reviewing a chat where the assistant answers a coding question with confident but incorrect complexity (e.g., claims O(1) when it’s O(n)). What evidence would you look for in the code/explanation to justify marking it incorrect?
Full answer:
First, I look at the actual operations in the code. I check whether there is a loop that scales with input size, linear scans, or repeated work over all elements.
Then I compare that against the assistant’s stated complexity. If the assistant ignores the linear pass, or misidentifies what changes when the input grows, that’s evidence the Big O assessment is wrong.
I also check its written explanation: if it fails to link the algorithm steps to input size, or gives a wrong justification for the complexity, that supports the mark.
My rationale would clearly state the real complexity, point to the specific line or logic causing linear scaling, and contrast it with the assistant’s wrong claim.

Short version:
I look for loops or scans that run proportional to the input size. If the code iterates over all elements, it is O(n). If the assistant confidently says O(1) without acknowledging that linear work, that is clear evidence of incorrect reasoning. I flag the mismatched complexity and point to the relevant code logic.

## Q3: How do you evaluate AI outcome?
Full version:
I evaluate AI outputs systematically, grounded in evidence from the given prompt, code and context, not my personal opinion.
First, I check correctness: Does the answer match technical facts? For coding questions, I verify logic, algorithm complexity, concurrency rules, definitions like Python GIL, and whether the code would behave as claimed. If the model makes wrong technical claims or produces buggy code, that is a major flaw.
Second, I assess reasoning quality: Does it explain its steps clearly? Can it support its conclusion with evidence? I watch for hallucinations, unfounded assumptions, overconfident statements, or logical gaps. Even if the final answer is right, flawed reasoning still gets marked down.
Third, relevance & adherence: Does it answer exactly what the user asked? I check if it ignores constraints, goes off-topic, or adds extra things that were not requested.
Fourth, clarity and usability: Is the explanation easy to follow? Is it structured properly? Are there confusing contradictions?
Finally, I write a concise rationale that points to specific evidence in the AI response, state the defect, and explain the right technical standard.

Short version:
I evaluate the AI result on correctness, reasoning, relevance, and clarity. I look for technical errors, hallucinations, and unsupported claims. All my judgement is backed by specific evidence from the output, and I document the issue in my rationale.

## Q4: What is the input and output?
Full version:
For this AI evaluation task, the input is the user prompt, any supporting context, code snippets, constraints, and the question given to the AI model. The output is the response the model generated back to the user.
My job is to compare the AI output against the input requirements and technical facts. I check whether the output correctly addresses what was asked, spot technical mistakes, flawed reasoning, hallucinations, or violations of the prompt rules, then produce my evaluation score and evidence-based rationale as my own deliverable.

Short version:
The input is the user’s question, prompt, context and code provided to the AI. The output is the answer the AI produced. I judge if that output is technically correct, relevant, and properly reasoned, then write my scoring rationale.

## Q5: How do you decide what AI can access?
Full version:
I decide what the AI can access strictly based on the given prompt and the provided context. Anything that is explicitly included in the input, such as code snippets, given parameters, tables, and stated facts, is accessible to the model.
Information that is not present inside the prompt or supporting context is out of bounds. That means the model cannot assume hidden external data, private API details, real-time internet results, or facts that were not supplied.
If the model uses information outside the provided scope, that counts as unsupported assumption or hallucination, and I note that in my rationale.

Short version:
The AI can only access information that is given in the prompt and supporting context. It cannot pull in outside knowledge, hidden data or real-time information unless the prompt explicitly allows it. When it uses unprovided information, I mark it as a flaw.

## Opening: Tell me about your background
I work as an AI evaluator focused on software engineering and coding reasoning. My core job is to examine model outputs, spot logical errors, incorrect algorithm analysis, misconceptions around concurrency and complexity, and write clear, evidence-based rationales to grade the response quality. I ground all critiques strictly on the code and facts provided, not personal guesses.
