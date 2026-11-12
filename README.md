
# Dynamic Characteristics Interactive Toolkit

**ENCS4380: Interfacing Techniques [Birzeit University]**

## Team Members

| # | Name | Student ID |
|---|------|-----------|
| 1 | Sarah Akkawi | 1230448 |
| 2 | Jana Snaf | 1230446 |
| 3 | Sondos Hammad | 1230521 |
| 4 | Abdullah Murra | 1230534 |

---

## Homework 1: Dynamic Characteristics

This website helps students understand how first-order and second-order systems respond to changes in the input. It connects the mathematical model of the system with an interactive graph and numerical measurements.

The main goal is to make the dynamic behavior of a system observable, for example by showing:

- how a time constant slows down a response,
- why a sensor attenuates and delays a sinusoidal signal,
- how damping determines whether a second-order system oscillates or overshoots.

The toolkit consists of **4 modules**. Each module introduces the mathematical model, lets the user adjust the parameters, displays the resulting behavior, and provides a way to test understanding of the model. We also included validation checks in **Modules 1–3** to compare computed values against reference results from the course material.

---

## How We Built the Toolkit

We implemented the website with **HTML, CSS, and JavaScript**, using **Plotly.js**:

1. The mathematical responses are calculated in **JavaScript**.
2. The page structure and interactive controls are built using **HTML**.
3. The layout, cards, and responsive presentation are built using **CSS**.
4. Interactive response curves, frequency plots, phase-plane plots, and pole visualizations are designed using **Plotly.js**.

The toolkit runs in the browser and does not require a backend server. An internet connection may be needed to load Plotly.js from its CDN.

> **AI Usage Disclosure:** We used AI assistance during development to help draft and organize HTML/CSS/JavaScript code and improve the clarity and usability of the interface. AI-assisted code was used as a development aid, not as a substitute for understanding the underlying concepts. The engineering concepts, mathematical models, and validation targets were based on the ENCS4380 course materials.

---

## Modules

### Module 1: First-Order Time Response

This module introduces the two main first-order parameters:

- **Gain (K):** scales the response.
- **Time constant (τ):** determines how quickly the system reacts.

Users can change K and τ and select either a **step** or a **ramp** input.

- **Step input:** we calculate the exponential response and highlight the physical meaning of the time constant. After one τ the output has reached approximately **63.2%** of its total change, and after three τ approximately **95%**.
- **Ramp input:** we examine the delayed response, the asymptotic ramp lag, and the steady-state error.

We also included a **logarithmic error-fraction plot**, whose slope is related to −1/τ. This plot can be used to estimate the time constant from measurements.

**Predict, Then Check:** asks users to estimate the output at a selected time before revealing the calculated value.

**Validation:** checks the expected 63.2% and 95% response points.

---

### Module 2: First-Order Frequency Response

This module explores what happens when a first-order sensor receives a sinusoidal input. It imitates a real sensor that may not follow a rapidly changing signal perfectly: its output amplitude can become smaller, and its output can lag behind the input.

The user changes **τ** and the input angular frequency **ω**. We calculate and display:

- **Amplitude ratio:** `M = 1 / √(1 + (ωτ)²)`
- **Phase lag:** `φ = −atan(ωτ)`
- The input and output sine waves on the same graph
- Bode magnitude and phase plots, including the cutoff frequency `ωc = 1/τ`
- A **dynamic-error calculator** that estimates the maximum allowable time constant for a specified frequency and amplitude-error limit

**Predict, Then Check:** the user predicts whether the amplitude ratio and phase-lag magnitude will increase, decrease, or stay the same for chosen new parameter values. The program then compares the prediction with the model.

**Validation:** reproduces the lecture's frequency-response examples, including the amplitude and phase, and the maximum τ for a 100 Hz signal with a 5% amplitude-error limit.

---

### Module 3: Second-Order Response

In this module, we studied how a second-order system responds to a step input and how its behavior changes with different parameters.

We focused on two main parameters:

- **Damping ratio (ζ):** controls how much the system oscillates and whether it has overshoot.
- **Natural frequency (ωn):** controls how fast the system responds.

We used sliders to change these parameters and plotted the response immediately. This helped us understand the three types of damping:

| Type | Behavior |
|------|----------|
| **Underdamped** | The system oscillates before settling. |
| **Critically damped** | The system reaches its final value quickly without oscillating. |
| **Overdamped** | The system reaches its final value slowly without oscillating. |

We also calculated and displayed important response measurements: **rise time, peak time, overshoot, and settling time**.

#### State-Space Representation

We added a state-space section using a **mass-spring-damper** system. The user can change the mass (m), damping (b), and spring stiffness (k) to see how they affect the system.

We displayed the state-space matrices, eigenvalues, poles, and phase-plane plot to show how the system's internal behavior is related to its response.

---

### Module 4: Guess the Sensor Challenge

Module 4 is the interactive assessment of the toolkit. In Modules 1–3, users know the parameters and observe the response. In Module 4, we reverse the problem: the response is given, and the user must estimate the unknown parameters, as an engineer would when analyzing measurements from an unfamiliar sensor.

#### How a Round Works

1. The program randomly generates a first-order or second-order sensor. A first-order sensor has hidden **K** and **τ** values; a second-order sensor has hidden **ζ** and **ωn** values.
2. It chooses the input: a step or a sine for a first-order sensor. The sensor order and input type are displayed so that the challenge focuses on parameter estimation, not on guessing the model category.
3. The system calculates the ideal response from the hidden parameters and adds a small amount of random measurement noise. The noisy response is displayed, and users can hover to inspect time and output values.
4. The user studies the graph and enters two numerical estimates. A short conceptual hint is available on request.
5. The program calculates the percentage error of each estimated parameter, reveals the true values, and displays the clean true response and the response produced by the user's guessed parameters on top of the noisy measurements.
6. The page displays a worked solution showing how the parameters relate to measurable properties of the curve. **New Sensor** starts another challenge, while the **session average** summarizes the scores of completed rounds out of 100.

#### Feedback and Scoring

Each of the two parameters is worth **50 points**. The current implementation awards:

| Error | Points |
|-------|--------|
| ≤ 5% | 50 |
| > 5% and ≤ 10% | 35 |
| > 10% and ≤ 20% | 25 |
| > 20% | 0 |

The round score is out of 100; the session score is the average of completed rounds, also out of 100.
