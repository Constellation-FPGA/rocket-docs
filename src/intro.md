# Introduction

Rocket-Core is a 5-stage pipelined, in-order, non-superscalar, non-speculative CPU design that implements RV32/64 GCV, along with full support for the standard 3-privilege level model (M-, S-, and U-modes).
As of 2024-01-05, the authors are not sure Rocket-Core fully and correctly implements the ratified 4-privilege level model (M-, H-, VS-, VU-modes).

<div class="warning">
<strong>We are not the original authors of Rocket-chip!</strong><br>
All of the documentation present in this Wiki is gathered through testing, trial-and-error, manually reading through the code, and the authors' prior knowledge of computer architecture.
</div>
