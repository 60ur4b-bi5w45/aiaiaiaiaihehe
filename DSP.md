Let's solve the given parts of the question in detail:

---

### **b) Derive the expression for decimation in time (DIT) FFT algorithm and draw the butterfly flow graph for N = 4**

#### **Decimation-In-Time (DIT) FFT:**

For a DFT of a sequence $x(n)$ of length $N$, the DFT is given by:

$$
X(k) = \sum_{n=0}^{N-1} x(n) W_N^{nk}, \quad k = 0, 1, ..., N-1
$$

Where $W_N = e^{-j\frac{2\pi}{N}}$ is the twiddle factor.

**DIT-FFT** splits the input into even and odd indexed terms:

$$
X(k) = \sum_{n=0}^{N/2-1} x(2n) W_N^{2nk} + \sum_{n=0}^{N/2-1} x(2n+1) W_N^{(2n+1)k}
$$

$$
X(k) = X_{even}(k) + W_N^k X_{odd}(k)
$$

$$
X(k + N/2) = X_{even}(k) - W_N^k X_{odd}(k)
$$

This reduces the DFT complexity from $O(N^2)$ to $O(N \log N)$.

---

#### **Butterfly Diagram for N = 4:**

Let $x(0), x(1), x(2), x(3)$ be the input.

**Stage 1 (Bit reversal and grouping):**

Group into even and odd:

* Even: $x(0), x(2)$
* Odd: $x(1), x(3)$

Apply 2-point DFT on each group.

**Stage 2: Combine results with twiddle factors $W_4^k$**

Twiddle factors:

* $W_4^0 = 1$
* $W_4^1 = -j$
* $W_4^2 = -1$
* $W_4^3 = j$

Resulting in the butterfly diagram:

```
x(0) ----+                        +---- X(0)
         |----> [1]        [1] <----|
x(2) ----+                        +---- X(2)

x(1) ----+                        +---- X(1)
         |----> [1]        [W4^1] <----|
x(3) ----+                        +---- X(3)
```

---

### **c) i. Frequency domain parameters for evaluating a low-pass filter**

Important parameters include:

1. **Cutoff Frequency (fc):** Frequency at which the magnitude response drops to 70.7% (-3 dB) of its maximum.
2. **Passband:** Range of frequencies passed with minimal attenuation.
3. **Stopband:** Range of frequencies that are significantly attenuated.
4. **Transition Band:** Frequency range between passband and stopband.
5. **Ripple:** Variations in the passband or stopband.
6. **Attenuation:** Measure of how much the signal is reduced in the stopband.

**Illustration (Magnitude Response):**

```
|         _________
|        /         \
|       /           \___________
|      /
|_____/_________________________
     0    fc      ft     freq →
     |    |       |
   Pass   Cutoff  Stopband
```

---

### **c) ii. Obtaining high-pass filter using low-pass filter h(n):**

Let $h(n)$ be the impulse response of a low-pass filter. The high-pass filter impulse response $h_{hp}(n)$ can be obtained by:

$$
h_{hp}(n) = \delta(n) - h(n)
$$

Where $\delta(n)$ is the discrete-time delta function.

**Explanation:** This process inverts the frequency response of the low-pass filter, turning it into a high-pass filter by subtracting from an all-pass system.

Would you like the butterfly diagram in image form as well?
