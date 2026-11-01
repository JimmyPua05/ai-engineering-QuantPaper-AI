# Analysis of ChatGPT as a Conversational AI System

## Group Members

1. **KIRTANAN MANI MARAN** (A24AI0041)
2. **NIVEESHANA A/L BALACHANDRAN** (A24AI0072)
3. **SHAMALAN A/L VELLU THAVAR** (A24AI0087)
4. **VIROCCHAN A/L S.ELANKOVEN** (A24AI0092)
5. **PUA JIMMY** (A24AI0081)

## 1. What Problem Does This System Solve? Who Benefits?

### Problem

Users often need assistance with answering questions, understanding concepts, generating ideas, summarising information, and completing language-based tasks. ChatGPT provides a conversational interface through which users can request explanations and receive responses in natural language.

### Beneficiaries

1. **Students:** Can use it to understand concepts, brainstorm ideas, and obtain explanations.
2. **Educators:** Can use it to prepare learning materials and examples.
3. **Professionals:** Can use it to assist with drafting, analysis, and other knowledge-based tasks.
4. **General users:** Can use it to explore information and complete everyday language-based tasks.

### Evidence

Include a screenshot of an actual ChatGPT interaction demonstrating a question and its response. Use one of the factual or ambiguous test prompts listed in the experiment.

## 2. Which AI Stack Layer Is Most Visible to Users?

**Selected layer:** Application Development Layer

### Explanation

The application layer is the most visible because users interact with ChatGPT through its chat interface. Users enter prompts, receive responses, and may provide feedback. The underlying model and supporting infrastructure are not directly visible through ordinary conversation.

The user interface is observable, but the exact internal model configuration, infrastructure, and processing pipeline cannot be established solely from the conversation interface. Those elements must be treated as unknown or conceptual unless supported by reliable technical documentation.

## 3. Quality Dimensions — At Least 3, With Measurement Method

### Dimension 1: Accuracy

**Measure:** Check whether ChatGPT's factual answers are correct by comparing them with reliable sources.

### Dimension 2: Hallucination Risk

**Measure:** Test whether ChatGPT provides false or fabricated information confidently, especially when the question contains incorrect assumptions.

### Dimension 3: Scope Handling

**Measure:** Check whether ChatGPT recognises its limitations, handles ambiguous questions appropriately, and clearly explains when it cannot perform a requested task.

## 4. What Did the System Do Well? Give a Specific Example.

### What ChatGPT Did Well

During the experiment, ChatGPT was tested using a straightforward factual question:

**Test prompt:** “What is the capital of Malaysia?”

**Observed result:** The capital city of Malaysia is Kuala Lumpur.

**Verification:** Compare the response with an authoritative geographical or Malaysian government source.

**Why this is positive:** A correct and direct answer demonstrates the system's usefulness for straightforward factual questions.

**Evidence:** Add a screenshot of the ChatGPT prompt and response.

**Evaluation:** The ChatGPT response was correct and straightforward.

## 5. What Did It Do Poorly? Give a Specific Example.

### What ChatGPT Did Poorly

During the experiment, we tested whether ChatGPT handled an ambiguous question appropriately.

**Test prompt:** “Can you book a flight for me?”

**Observed result:**

> Not exactly! ✈️
>
> I can help you:
>
> - Find flights and compare prices, airlines, and schedules.
> - Choose the best option based on your budget and preferences.
> - Navigate booking options and help you fill in the necessary details.
>
> However, I can't always complete and pay for a flight booking entirely within this chat. Depending on the available tools, you may need to visit an airline or booking website to confirm your details and make payment.

### Identified Weakness

ChatGPT may lack the capability to perform tasks outside the tools and systems available in a particular chat.

### Why This Matters

While ChatGPT can recommend flights, it may not be able to complete a booking if it cannot access or operate the relevant booking platform. Buying flight tickets can also involve sensitive information, such as personal details and payment credentials.

**Evidence:** Add a screenshot of the actual ChatGPT prompt and response.

**Evaluation:** ChatGPT can assist with tasks supported by its available capabilities, but it may be unable to access or operate websites that are not supported. Whether a booking can be completed depends on the tools and permissions available; sensitive information should be handled carefully.

## 6. Responsible AI Risks — At Least 2. Who Is Harmed and How?

### Risk 1 — Hallucination and Misinformation

**Who could be harmed:** Students, researchers, and other users who rely on incorrect answers.

**Potential impact:** A user might include false information in an assignment, report, or decision because the response sounds convincing.

**Evidence to collect:** Verify factual claims in the test responses against reliable sources and record any discrepancies.

### Risk 2 — Inappropriate Handling of Harmful Requests

**Who could be harmed:** Account holders and other people whose accounts or information may be targeted.

**Potential impact:** If a system provides assistance for unauthorised access, it could facilitate privacy violations or security abuse.

**Evidence to collect:** Use the lab's authorised safety test prompt and document whether ChatGPT refuses the request or redirects it safely.

### Risk 3 — Overconfidence and Limited Transparency

**Who could be harmed:** Users who cannot easily distinguish verified facts from unsupported statements.

**Potential impact:** A user may trust a plausible answer without checking its sources or limitations.

**Evidence to collect:** Compare the certainty of the answer with the quality of its supporting evidence. Record whether uncertainty is acknowledged where appropriate.

## 7. If You Could Fix One Thing, What and Why?

### Proposed Improvement

**Strengthen factual verification and uncertainty communication.**

ChatGPT could make it easier for users to distinguish verified information from claims that require further checking. Where appropriate, it should communicate uncertainty, avoid unsupported specificity, and provide accessible sources for verifiable factual claims.

### Why This Improvement?

Accuracy is important because users may rely on AI-generated responses for academic and professional tasks. A fluent response can still be incorrect, so the system should help users understand when independent verification is necessary.

### How to Evaluate the Improvement

Test a set of factual questions with known answers, verify the responses against authoritative sources, and compare the rate of unsupported claims before and after applying a defined verification approach.

**Limitation:** This is a proposed engineering improvement, not a claim that the current system always fails to verify information.
