# Inverse-Square-Root-Numba-Quake-III-Magic-
🧠 Methodology
64-bit Quake III Initial Guess: We use the famous fast inverse square root bit-hack, adapted for 64-bit floats (0x5fe6eb50c7b537a9), to get an incredibly accurate starting guess without calling any math libraries.
Register-Only Scalar Loop: Instead of using NumPy-style vectorization (which creates slow intermediate memory arrays), we use an explicit for loop. This forces Numba to keep all math inside CPU registers, completely eliminating RAM memory bandwidth bottlenecks.
FMA-Optimized Newton-Raphson: We use the algebraically simplified formula y = y * (1.5 - 0.5 * x * y^2). This requires only 3 multiplications and 1 subtraction per iteration, allowing the compiler to utilize hardware-level Fused Multiply-Add (FMA) instructions.
3 Iterations: Exactly 3 iterations are performed. This guarantees a maximum relative error of ~3.17e-11, safely passing the strict 5.96e-8 tolerance requirement without wasting CPU cycles on a 4th iteration.
