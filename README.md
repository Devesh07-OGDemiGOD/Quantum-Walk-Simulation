# Quantum Walk Simulation

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Devesh07-OGDemiGOD/Quantum-Walk-Simulation/blob/main/quantum_walk_simulation.ipynb)

A NumPy simulation of a **discrete-time quantum walk** (Hadamard walk) on a 1D line, compared side by side with a **classical random walk**. It shows how quantum interference makes the walker spread out far faster than any classical walker can.

> This is a mathematical simulation in NumPy. It does not run on real quantum hardware or use a quantum SDK.

---

## What it does

- Simulates a quantum walker using complex **probability amplitudes**, a **Hadamard coin**, and a **conditional shift**
- Simulates **50,000 independent classical random walks** to estimate the classical distribution
- Tracks **mean and variance at every step** for both walks
- Plots the final distributions, overlays them, and shows variance growth
- Generates an **animation** of the quantum distribution evolving step by step
- Verifies that total probability stays equal to 1

---

## The idea

### Classical random walk
At each step the walker moves left (-1) or right (+1) with equal probability. After many steps the distribution forms a bell curve centred at 0, and the variance grows **linearly** with the number of steps:

```
Variance ~ N
```

### Quantum walk
Instead of flipping a coin and moving, the quantum walker carries a two-state **coin** (|0> and |1>) and exists in a superposition of positions. Each step has two parts:

1. **Coin operation:** apply the Hadamard gate to the coin state

   ```
   H = 1/sqrt(2) * [[1,  1],
                    [1, -1]]
   ```

2. **Conditional shift:** coin |0> moves the walker left, coin |1> moves it right

The walker starts at position 0 with the coin in the state `(|0> + i|1>) / sqrt(2)`. The relative phase `i` makes the walk symmetric. Because amplitudes can add and cancel (**interference**), the distribution is not a bell curve. It has two large peaks near the edges and a spread-out middle.

For the Hadamard walk the variance grows **quadratically**:

```
Variance ~ (1 - 1/sqrt(2)) * N^2  ~  0.293 * N^2
```

This is the key result of the project: a **ballistic** quantum spread versus a **diffusive** classical spread.

| Property | Classical walk | Quantum walk |
|---|---|---|
| State | Definite position | Superposition of positions |
| Describes the walker with | Probabilities | Complex amplitudes |
| Distribution shape | Bell curve | Two edge peaks plus interference |
| Variance growth | ~ N | ~ N^2 |
| Spread (std. deviation) | ~ sqrt(N) | ~ N |

---

## Getting started

### Requirements
- Python 3.8+
- NumPy
- Matplotlib
- IPython / Jupyter (for the animation display)

### Install

```bash
git clone https://github.com/Devesh07-OGDemiGOD/Quantum-Walk-Simulation.git
cd Quantum-Walk-Simulation
pip install -r requirements.txt
```

### Run

The animation uses `IPython.display`, so this runs best in **Jupyter Notebook, JupyterLab, or Google Colab**. You can also click the **Open in Colab** badge at the top to run it in your browser with no setup.

```bash
jupyter notebook
```

Open `quantum_walk_simulation.ipynb`, run the cell, and enter the number of steps when prompted:

```
Enter number of steps (e.g., 20): 50
```

---

## Output

The program prints:

- Total probability for both walks (should be ~ 1.0)
- A step-by-step table of quantum vs classical variance
- Final mean and variance for both walks

It also produces:

1. Side-by-side bar charts of the final quantum and classical distributions
2. An overlay plot comparing both distributions
3. A variance vs number of steps plot
4. An animation of the quantum walk evolving

<!-- Add screenshots here once you've uploaded them, for example:
![Distribution comparison](images/distribution.png)
![Variance growth](images/variance.png)
-->

---

## Code overview

| Section | Purpose |
|---|---|
| Setup | Grid of positions from -N to N, two coin states per position |
| Quantum evolution | Hadamard coin, then conditional left/right shift, repeated N times |
| Classical simulation | 50,000 random +/-1 walks, positions via `cumsum` |
| Analysis | Mean, variance and probability at each step |
| Plots | Final distributions, comparison, variance growth |
| Animation | Frame-by-frame quantum probability using `FuncAnimation` |

A fixed random seed (`42`) is used, so classical results are reproducible.

---

## Possible improvements

- Try different coins (Grover, DFT) or different initial coin states
- Add a 2D quantum walk
- Add decoherence or measurement and watch the walk become classical
- Compare against the analytical variance formula
- Fit curves to show the N vs N^2 scaling
- Export the animation as a GIF
- Implement the walk as a real quantum circuit using Qiskit

---

## Concepts covered

`Quantum walk` · `Hadamard gate` · `Superposition` · `Interference` · `Probability amplitudes` · `Random walk` · `Variance and diffusion` · `Monte Carlo simulation`

---

## Author

Made by **OGDemiGOD**

## License

Released under the [MIT License](LICENSE).
