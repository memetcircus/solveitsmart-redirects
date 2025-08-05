# Solve It Smart

Solve It Smart is an interactive, AI-powered companion app designed to work alongside the *Catch the Fish: The Evolutionary Playbook of Problem Solving Techniques* iBook. It takes a math or logic problem from the book—along with its provided solution and the underlying strategy—and uses that information to guide a step-by-step explanation using Polya-inspired techniques.

But it goes beyond just explaining the answer.

Solve It Smart allows users to ask follow-up questions about the strategy used (e.g. *Why use cases?*, *Why a table?*, *What does working backwards mean here?*), and it responds conversationally—like a smart tutor embedded inside the book.

In short: **Solve It Smart doesn’t just solve problems—it teaches how to think through them.**

---

## 📱 Platform & Deployment

- Target: **iPad (iOS)**
- Orientation: **Landscape only**
- Deployment Target: **iOS 16.0**
- Inference: **Fully offline using Google’s Gemma 3n model** (.gguf format)

---

## ✨ Features

Solve It Smart includes several standout features:

- **Offline AI support**: The app runs entirely on-device using the Gemma 3N model. This means users can explore and solve problems—even complex ones involving figures and equations—without needing an internet connection.

- **Conversational AI explainers**: Rather than just giving answers, the app explains how and why a strategy works. It applies Polya-style techniques like working backwards or use cases, adapting its response to the specific problem and the user’s follow-up questions.

- **Math rendering and LaTeX output**: The app dynamically generates LaTeX for each step of the solution. Math is rendered cleanly on-screen, and users can copy any part of the output as LaTeX to reuse elsewhere—perfect for students or educators working in Overleaf or Markdown environments.

- **Chat-based interface**: Engages users in dialogue, simulating a personal tutor experience.

- **Deep link support**: Opens directly to a problem from the iBook using a GitHub-based redirect.

---

## 🚀 How It Works

### User Flow:

When users tap a "Solve It Smart" link inside the *Catch the Fish* iBook, the app launches directly into the relevant problem. The app loads:

- The full problem statement
- The book-provided solution
- The problem-solving strategy (e.g. *Use Logic*, *Guess & Test*)

It then begins a Polya-style explanation of how and why the problem was solved that way.

### Ask Questions:

The user can ask things like:

- "Why did you use cases here?"
- "Which techniques did you use in this problem?"
- "Can you explain working backwards technique?"

The AI responds in context, drawing from the model's understanding of the problem, solution, and the chosen strategy.

---

## 🔗 Deep Linking & Redirects

Since Apple Books doesn't support native deep links, each problem link redirects through a GitHub-hosted redirector. Safari opens briefly, then redirects into the app with the correct problem loaded.

Example redirect:

```
https://memetcircus.github.io/solveitsmart-redirects/?id=2.2
```

### Developer Testing Links:

You can test the app without the iBook by tapping any of the links below on iPad:

#### Guess and Test

- [https://memetcircus.github.io/solveitsmart-redirects/?id=2.2](https://memetcircus.github.io/solveitsmart-redirects/?id=2.2)
- [https://memetcircus.github.io/solveitsmart-redirects/?id=2.3](https://memetcircus.github.io/solveitsmart-redirects/?id=2.3)
- [https://memetcircus.github.io/solveitsmart-redirects/?id=2.6](https://memetcircus.github.io/solveitsmart-redirects/?id=2.6)

#### Use a Variable

- [https://memetcircus.github.io/solveitsmart-redirects/?id=3.2](https://memetcircus.github.io/solveitsmart-redirects/?id=3.2)

#### Solve an Equation

- [https://memetcircus.github.io/solveitsmart-redirects/?id=4.2](https://memetcircus.github.io/solveitsmart-redirects/?id=4.2)

#### Draw a Diagram

- [https://memetcircus.github.io/solveitsmart-redirects/?id=6.4](https://memetcircus.github.io/solveitsmart-redirects/?id=6.4)

#### Make a List / Table

- [https://memetcircus.github.io/solveitsmart-redirects/?id=7.4](https://memetcircus.github.io/solveitsmart-redirects/?id=7.4)

#### Use Logic

- [https://memetcircus.github.io/solveitsmart-redirects/?id=10.3](https://memetcircus.github.io/solveitsmart-redirects/?id=10.3)

#### Indirect Reasoning

- [https://memetcircus.github.io/solveitsmart-redirects/?id=11.6](https://memetcircus.github.io/solveitsmart-redirects/?id=11.6)

#### Use Cases

- [https://memetcircus.github.io/solveitsmart-redirects/?id=15.4](https://memetcircus.github.io/solveitsmart-redirects/?id=15.4)

#### Working Backwards

- [https://memetcircus.github.io/solveitsmart-redirects/?id=14.3](https://memetcircus.github.io/solveitsmart-redirects/?id=14.3)

#### Look for a Formula

- [https://memetcircus.github.io/solveitsmart-redirects/?id=17.2](https://memetcircus.github.io/solveitsmart-redirects/?id=17.2)
- [https://memetcircus.github.io/solveitsmart-redirects/?id=17.4](https://memetcircus.github.io/solveitsmart-redirects/?id=17.4)

#### Consider Extreme Cases

- [https://memetcircus.github.io/solveitsmart-redirects/?id=22.4](https://memetcircus.github.io/solveitsmart-redirects/?id=22.4)
- [https://memetcircus.github.io/solveitsmart-redirects/?id=22.5](https://memetcircus.github.io/solveitsmart-redirects/?id=22.5)

---

## 💡 Local Inference with Gemma 3n

- Model file: `google_gemma-3n-E2B-it-Q4_K_M.gguf`
- Requires no server or internet connection

**Installation Note:** The model file is not included in the repository. Users must download the `.gguf` file separately and place it inside the project directory under a folder named `models` (lowercase `m`), which is already listed in `.gitignore`.

To download the model, run the following command in your macOS terminal:

```bash
huggingface-cli download bartowski/google_gemma-3n-E2B-it-GGUF \
  --include "google_gemma-3n-E2B-it-Q4_K_M.gguf" \
  --local-dir ./models
```

> 🧠 Note: Other Gemma 3n variants were tested on the iPad Air 5th generation, but due to memory constraints, this is the most comprehensive model that runs reliably.

---

## 🛠 llama.cpp Build (iOS)

To compile the backend AI engine on iOS, follow these steps:

```bash
git clone https://github.com/ggerganov/llama.cpp.git
cd llama.cpp

mkdir build-ios && cd build-ios
cmake .. \
 -DLLAMA_METAL=on \
 -DLLAMA_STATIC=on \
 -DCMAKE_OSX_ARCHITECTURES=arm64 \
 -DCMAKE_SYSTEM_NAME=iOS \
 -DCMAKE_OSX_SYSROOT=iphoneos

make
```

This will generate a Metal-optimized static build for iOS.

---

## 🚷 Dependencies

- [SwiftMath](https://github.com/phimage/SwiftMath)
- [MathJaxSwift](https://github.com/phimage/MathJaxSwift)
- [LaTeXSwiftUI](https://github.com/phimage/LaTeXSwiftUI)
- [SwiftDraw](https://github.com/swhitty/SwiftDraw)
- [HTMLEntities](https://github.com/IBM-Swift/HTMLEntities)

---

## ⚖️ License

MIT License

---

## ✍️ Contributing

Pull requests welcome! If you're interested in contributing or adapting this architecture for your own educational app, feel free to fork or contact us via GitHub Issues.

---

## 🌐 Project Site

GitHub: [https://github.com/memetcircus/solveitsmart](https://github.com/memetcircus/solveitsmart)

