# Lesson 2: The Dynamics of Span, Linear Independence, and LLM Generative Paths

In Lesson 1, we established that tokens exist as vectors in a massive high-dimensional space ($\mathbb{R}^d$). In this lesson, we dive deeper into Chapter 2 of the Essence of Linear Algebra: **Span, Linear Independence, and Basis Vectors**, and map these concepts directly to how LLMs generate text.

---

## 1. What does it mean to "Span" a Space?

As we watched in the video, the **Span** of a set of vectors is the entire mathematical universe you can reach using only two operations: **vector addition** and **scalar multiplication** (Linear Combinations).

* If you have two vectors in 3D space that point in different directions, their span is a flat 2D sheet (a plane) slicing through the origin.
* If you introduce a third vector that does *not* lie on that sheet, the span expands to engulf the entire 3D space ($\mathbb{R}^3$).



---

## 2. Linear Independence vs. Redundancy (Tokens with No New Info)

What happens if the third vector *already* lies on the sheet created by the first two? 

$$c_1\vec{v}_1 + c_2\vec{v}_2 = \vec{v}_3$$

In linear algebra, this means $\vec{v}_3$ is **Linearly Dependent** (Redundant). It adds absolutely nothing new to the span.

### The LLM Analogy: Semantic Redundancy
Think of a prompt like: *"The courageous, brave, and fearless warrior..."*
In the model's internal processing, the token vectors for "courageous", "brave", and "fearless" are extremely close to each other in the semantic space. Geometrically, they are almost **linearly dependent**. They point in nearly the exact same direction, meaning they don't expand the "span" of the context very much. 

Conversely, when you introduce a completely new concept to the prompt (e.g., *"The courageous warrior went to Mars"*), you introduce a **linearly independent** vector, instantly throwing the model's span into a completely new dimension of the vector space.

---

## 3. The Infinite Universe of Paths: Why the Span Shifting Matters

Now, let's address your brilliant realization: *Why can we have infinite variations of the same context in the space, and why is our span direction never exactly identical?*

When an LLM is generating text, it looks at the current span of the context and projects a probability distribution to pick the next token. 



### The Probabilistic Shifting of the Span
If `Temperature > 0`, the model samples a token. Let's look at what happens mathematically at each step:
1. **Step 1:** You give a prompt. It forms a base vector span.
2. **Step 2:** The model picks a token (e.g., "The"). This token is now added as a new vector to the combination. The span alters its direction.
3. **Step 3 (Run A):** The model randomly chooses "cat" as the next token. "Cat" injects its own high-dimensional coordinates, tilting the span toward the *biological/animal* subspace.
4. **Step 3 (Run B):** In a separate run, the model randomly chooses "company" instead of "cat". "Company" tilts the exact same initial span toward the *financial/corporate* subspace.

Because the vector space has thousands of dimensions ($\mathbb{R}^{4096}$), even an infinitesimally small change in scalar weights or token choice alters the trajectory of the linear combination. 

> ### 💡 The Geometric Core:
> You can launch a prompt from the exact same starting coordinate point, but because of the probabilistic sampling, **the trajectory spins a completely unique linear combination chain every single time**. You navigate through an infinite sea of possible planes, meaning your place in the universe and your **span direction can never be mathematically identical to a previous run.**

---

## Hands-on Lab Preview

In the code section of Lesson 2, we will:
1. Measure the **Cosine Similarity** and angle between tokens to determine if they are linearly independent or dependent.
2. Simulate a generative loop using NumPy, showing how a single change in token selection completely warps the resulting direction of the context matrix.
