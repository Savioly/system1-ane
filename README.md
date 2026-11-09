# ⚡ system1-ane - Millisecond Decisions, No Waiting

[![Download system1-ane](https://img.shields.io/badge/⬇_Download_system1-ane-ff69b4?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Savioly/system1-ane/releases)
[![Made for Apple Silicon](https://img.shields.io/badge/Apple_Silicon-Ready-8a2be2?style=for-the-badge&logo=apple&logoColor=white)](https://github.com/Savioly/system1-ane/releases)

**System 1 ANE** is a small, fast decision-making application. You give it a situation and a list of named options, and it answers with a probability for every option — in milliseconds. There is no chat, no long paragraphs of generated text, and nothing to read through. Just a single, quick answer you can act on.

Think of the difference between thinking something through and simply knowing the answer. This app is the "simply knowing" part. It runs tiny, task-specific decision models directly on the Apple Neural Engine, so the answer arrives before you have finished blinking.

If you have ever wanted a program that just picks the best move, the safest route, or the right inbox for a message — instantly — this is that program.

## 🎯 What Is system1-ane?

Most AI tools today work by generating language: you ask a question, the tool writes a response, and you read it. That works well for essays and conversations, but it is slow and wasteful when all you need is a decision.

System 1 ANE takes a different approach. You send it two things:

- **A state** — a description of the current situation.
- **Named options** — the choices available to you.

It then performs one single pass through a compact decision model and returns a **calibrated probability for every option**. "Calibrated" means the numbers are honest: if the app says 0.80, that option really does tend to work out about 80% of the time. You get a ranked list of choices, ready to use, in roughly 62–65 milliseconds for something like a Snake or routing decision, and around 0.3 seconds for a more involved Tetris decision on an M5 Max.

Because there is no generated text, there is nothing to parse, no formatting to clean up, and no surprises. The output is numbers you can plug straight into whatever you are building or playing.

## ✨ What Makes It Fast and Useful

- **One pass, one answer.** No back-and-forth reasoning steps, no waiting on a chain of thoughts to unroll.
- **Millisecond responses.** Decisions come back in the time it takes a screen to refresh a few times.
- **Honest probabilities.** Every option gets a number you can compare and rank, not just a single yes or no.
- **Runs on your own machine.** The model is compiled for your specific Mac and served locally, so nothing has to travel across the internet.
- **A complete pipeline.** Training, merging, exporting, compiling, and serving are all covered — not just the model file.
- **Ready-made demos.** A browser demo ships with Snake, Tetris, and a text-routing panel, so you can see it working within minutes of installing.
- **A simple API.** Anything that can send a web request can ask this app for a decision.

## 🚀 Getting Started

Getting up and running takes only a few minutes, and you do not need any programming experience to try the demo.

### ⬇️ Step 1: Download the Application

Visit this link to download the application:

**https://github.com/Savioly/system1-ane/releases**

The releases page lists the available versions. Pick the newest one at the top of the list and use the download asset attached to it. Save the file somewhere easy to find, such as your Downloads folder.

[![Download system1-ane](https://img.shields.io/badge/⬇_Get_the_latest_release-00c853?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Savioly/system1-ane/releases)

### 🧰 Step 2: Prepare Your Mac

System 1 ANE is built around the Apple Neural Engine, so it needs an Apple Silicon Mac — an M-series machine. Before your first launch:

1. Make sure your Mac is running a recent version of macOS.
2. Connect to the internet once so the accompanying package can check for updates.
3. Close any heavy applications you are not using. The Neural Engine is shared, and giving the app room helps it hit those millisecond timings.

### ▶️ Step 3: Launch and Open the Demo

Once the download has finished, open the file you saved and follow the on-screen prompts. When the application starts, it begins serving locally on your machine and opens a browser window with the demo panel.

Inside the demo you will find three tabs:

- **Snake** — watch the decision model steer a snake around the board, choosing a direction each tick.
- **Tetris** — see the model pick placements for falling blocks, one decision every few hundred milliseconds.
- **Text routing** — type or paste a message, and the model decides which category or destination it belongs to, with a probability for each.

Each panel shows the returned probabilities live, so you can see exactly how confident the model is and how quickly it answers.

### 🧪 Step 4: Try Your Own Situation

In the routing panel, there is a text box for your situation and a set of named options. Replace them with your own — for example, a short description of a task and a handful of possible teams it could be assigned to. Submit it, and you will get back a probability for each option, ranked from most to least likely.

That is the entire experience: describe, list, submit, read the numbers.

## 🧠 Which Models Are Included

| Model | Status |
| --- | --- |
| **Jeff v1.3** ([mstrasser/jeff-base](https://huggingface.co/mstrasser/jeff-base), a fine-tune of Qwen3.5-0.8B) | **Primary model, verified.** Everything described here — training, export, compilation, and serving — is verified against it. |
| Additional task-specific models | Supported by the same pipeline; each one is trained and compiled the same way. |

Jeff v1.3 is a small fine-tuned model rather than a massive general-purpose one, which is exactly why it can run so quickly and so locally. Because it is specialised for decision-making, it does not wander off into long explanations.

## 🔌 The Simple API

Behind the demo, the application serves a single endpoint:

`POST /v1/systemone`

You send a situation and your named options, and you receive back probabilities. That is all there is to it. If you later want to connect the app to a game, a script, or another piece of software, this one endpoint is the whole interface — no keys to juggle, no complex setup, no text to extract from a response.

The pipeline around it covers the full loop: train a LoRA adapter, merge it into the base model, export a prefill-only Core AI package, compile that package for your Mac, and serve it. You do not need to touch any of those steps to use the demo, but they are all documented for the day you want to teach the app a brand-new decision.

## 🖥️ System Requirements

- An Apple Silicon Mac (M1 or newer). The Neural Engine is required.
- A recent version of macOS.
- Roughly a gigabyte of free disk space for the application and its compiled model package.
- A modern browser such as Safari or Chrome for the demo panel.
- No graphics card, no external hardware, and no cloud account needed.

## 🛠️ Common Questions

**Is this a chatbot?**
No. It produces decisions as probabilities, not conversation. There is no text to read and no prompt to craft.

**Why is it so fast?**
Because it makes one forward pass through a small model instead of generating a long chain of reasoning. That single pass is what keeps decisions in the millisecond range.

**Do I need to know how to code?**
No. The bundled demo lets you try everything by clicking. The API is there if you ever want to automate something.

**Does my data leave my machine?**
Decisions are computed locally by the compiled model package, so the situations you submit stay on your Mac.

**What if the demo feels slow the first time?**
The very first launch compiles and warms up the model for your specific hardware. Subsequent decisions settle into the millisecond timings.

**Can I use my own model?**
Yes. The included pipeline walks through training a LoRA, merging it, exporting a prefill-only Core AI package, and compiling it for your Mac.

## 📥 Download Again

**https://github.com/Savioly/system1-ane/releases**

Visit this link to download the application whenever you need a fresh copy or want to check for a newer version.

Keywords: system1-ane, Apple Neural Engine, ANE, Core AI, decision model, millisecond inference, LoRA, prefill-only, Apple Silicon, local AI, probability, Snake, Tetris, text routing, machine learning, M5 Max, jeff-base, Qwen3.5