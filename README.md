# 2D Burgers Equation in Python

An educational Python/Jupyter Notebook project for exploring the **two-dimensional viscous Burgers equations**, creating a computational grid, defining velocity initial conditions, and visualizing the initial velocity fields.

> **Project status:** The included `Burgers_2D_main.ipynb` currently contains grid setup, initial conditions, and contour plots. It **does not yet contain the time-stepping loop** needed to compute the time-evolving solution. The equations and numerical-solver notes below describe the intended next step.

## Governing equations

The coupled 2D viscous Burgers equations for horizontal velocity `u` and vertical velocity `v` are:

$$
\frac{\partial u}{\partial t}
+u\frac{\partial u}{\partial x}
+v\frac{\partial u}{\partial y}
=\nu\left(\frac{\partial^2u}{\partial x^2}+\frac{\partial^2u}{\partial y^2}\right)
$$

$$
\frac{\partial v}{\partial t}
+u\frac{\partial v}{\partial x}
+v\frac{\partial v}{\partial y}
=\nu\left(\frac{\partial^2v}{\partial x^2}+\frac{\partial^2v}{\partial y^2}\right)
$$

Here, `nu` is kinematic viscosity, and the left-hand-side spatial-derivative terms represent nonlinear convection.

## Notebook parameters

| Parameter | Value | Meaning |
|---|---:|---|
| `nx`, `ny` | 51, 51 | Grid points in each spatial direction |
| `x`, `y` | 0 to 2 | Spatial domain |
| `dx`, `dy` | 0.04, 0.04 | Grid spacing |
| `nt` | 500 | Planned number of time steps |
| `dt` | 0.001 | Time-step size |
| `nu` | 0.1 | Intended viscosity coefficient |

**Initial conditions:** Both velocity components start at 1 throughout the domain, with a central square region (approximately `0.75 <= x,y <= 1.25`) set to 5. Contour plots show the initial `u` and `v` fields.

## Project structure

```text
2d-burgers-equation-python/
├── Burgers_2D_main.ipynb   # Original notebook: setup and initial fields
├── README.md               # Project documentation
├── requirements.txt        # Python dependencies
└── .gitignore              # Files excluded from Git
```

## Getting started

1. Clone or download the repository.
2. Create and activate a Python virtual environment (optional but recommended).
3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Start the notebook:

   ```bash
   jupyter notebook Burgers_2D_main.ipynb
   ```

5. Run notebook cells from top to bottom, after applying the corrections noted below.

## Important notes about the current notebook

- The variable `nu` is initialized as `0.1`, but a later cell reassigns `nu = np.zeros((ny, nx))`. This **overwrites the viscosity coefficient**. Rename that array to `un` (if intended for storing the previous time step), and keep `nu = 0.1`.
- The plotting cells both call `x, y = np.meshgrid(x, y)`. To avoid applying `meshgrid` twice when running all cells in order, construct the mesh only once (for example, `X, Y = np.meshgrid(x, y)`) and use `X, Y` for both plots.
- For a full simulation, add a time loop, update both components using a stable finite-difference scheme, apply boundary conditions, and save each time step in `uf`/`vf`.
- A standard positive-velocity upwind scheme is not suitable unchanged for negative velocities. Use direction-aware upwinding when testing left/down transport.

## Next steps

- Implement and validate the full time-stepping solution.
- Compare convection and diffusion for different viscosity values.
- Plot the evolution of the velocity fields through time.

## License

No license has been assigned yet. Add a `LICENSE` file if you decide to release the code for reuse.

