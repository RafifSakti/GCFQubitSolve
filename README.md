# Noise protected qubit energy level & wave function solver

This project provides a numerical framework to solve the Hamiltonian of noise-protected superconducting qubits, specifically focusing on energy levels and wavefunctions. The solver is designed to explore the parameter space of the **0-$\pi$ qubit** and the **Bi-fluxon qubit regime**.

## Purpose
The primary purpose of this tool is to solve the noise-protected qubit Hamiltonian for various physical parameters, with a particular focus on:
* **External Flux ($\phi_{ext}$ / `phiE`)**
* **Offset Charge ($n_g$ / `ng`)**

By sweeping these parameters, users can analyze the qubit's spectral properties and its resilience to noise as described in [arXiv:2106.10296](https://arxiv.org/abs/2106.10296).

## How it Works
The solver implements the Hamiltonian using a grid-based finite-difference method in a pseudo-space defined by $\phi$ and $\theta$.

1.  **Grid Definition**: A 2D pseudo-space is defined for the partial derivatives of the Hamiltonian.
2.  **Flattening Logic**: The 2D grid is flattened into a 1D vector to construct the Hamiltonian matrix. The implementation iterates through the $\phi$ space first, then increments the $\theta$ value until the boundary is reached (flattening $\phi$ first, then $\theta$).
3.  **Dirac Formalism**: Once the Hamiltonian matrix is constructed, the system solves for its eigenvalues and eigenfunctions (wavefunctions) based on the Dirac quantum mechanics formalism.
4.  **Numerical Solvers**:
    * `maingeneralh`: Uses standard dense linear algebra (`np.linalg.eigh`).
    * `maingeneralsph`: Uses sparse solvers (`scipy.sparse.linalg.eigsh`) for better performance on larger grids.

## Installation
To set up the environment, you can use the provided `environment.yaml` file:

```bash
conda env create -f ./environment.yaml --prefix ./.conda
```

Alternatively, ensure you have the following libraries installed:
* `numpy`
* `scipy`
* `matplotlib`
* `pyvista` and `pyvistaqt` (for 3D plotting)

## Usage
* **Solver Functions**: The `main*` functions (e.g., `maingeneralsph`) are the primary entry points. You can input the specific physical parameters ($E_L, E_J, E_C, \phi_{ext}, n_g$) you wish to solve (uses as base, tpRatio, Alpha, and Beta as the parameter. Can be change by editing main function).
* **Data Generation**: Use the **Job Cells** in the notebooks to run batch simulations. These cells iterate through parameter ranges and save the resulting data (e.g., as `.npy` files) for further analysis.
* **Visualization**: The `Plotting-pyvista.ipynb` notebook uses the generated data to create interactive 3D plots of the energy surfaces and wavefunctions.

## Acknowledgments
Special thanks to:
* **Global Connect Fellowship**
* **Assoc Prof Rainer Helmut Dumke**
* **Centre for Quantum Technologies (CQT)**

## Reference
Based on the theoretical framework from:
> *Gyenis, A., et al. (2021). "Moving beyond the transmon: Noise-protected superconducting quantum circuits."* [arXiv:2106.10296](https://arxiv.org/abs/2106.10296)