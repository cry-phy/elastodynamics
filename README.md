
# Elastodynamics
The goal of this project is to simulate soft bodies using non linear elastodynamics of hyperelastic materials.

Full Documentation is found in [PDF](Elastodynamics.pdf)

![Wiggle](bunny3.gif)


## Target Geometries

Starting with simple bar deformation as test. The endgoal is to import 3D objects like the [Stanford Bunny](https://graphics.stanford.edu/data/3Dscanrep/) as deformation test subjects.

## Target equation

$$
\rho \frac{\partial^2 \mathbf{u}}{\partial t^2} - \frac{\partial \mathbf{c}}{\partial t} + \nabla \mathbf{P} + \mathbf{F} = 0
$$

Where:
- $\rho$ is the material density (mass per unit volume in the reference configuration),
- $\mathbf{u}$ is the displacement field,
- $\frac{\partial^2 \mathbf{u}}{\partial t^2}$ is the acceleration,
- $\mathbf{c}$ is the damping tensor modelling viscoelastic (Maxwell)
  damping with viscosity $\eta$,
- $\mathbf{P}$ is the stress tensor; for linear elasticity it reduces to
  the Cauchy stress $\sigma = 2\mu\varepsilon + \lambda \operatorname{tr}(\varepsilon) I$
  with strain $\varepsilon$ and Lamé parameters $\mu$, $\lambda$,
- $\mathbf{F}$ is the force term (assumed $0$ for a relaxed initial
  state).

More infos are in the [documentation PDF](Elastodynamics.pdf)
## Files
Easy to run files are:
- [Elastostatics](Static_Brick.ipynb)
- [Undampened Elastodynamics Test](Timestepping_Brick.ipynb)
- [Dampened Elastodynamics Test](Timestepping_Dampened.ipynb) 

These need large amounts of RAM: 
- [Tacoma Narrows Simulation](bridge_without_damping.ipynb)
- [Bunny Simulation](Bunny_Simulation.ipynb) (min 42GB)

## Results
- [Wiggle Brick](Wiggle_Brick1.gif) 
- [Wiggle Brick](Wiggle_Brick2.gif) 
- [Wiggle Brick](Wiggle_Brick3.gif)
- [Tacoma Bridge](Bridge.gif)
- [Stanford Bunny](bunny.gif)
- [Stanford Bunny](bunny2.gif)

## Contributors
- Christof Stein
- Max Hirtenlehner
- Tobias Gröfler

## License
- **Code** (all `.ipynb` notebooks) is licensed under the
  [GNU General Public License v3.0 or later](LICENSE).
- **Resources** (documentation PDF, GIFs, images and README text) are
  licensed under
  [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).
- **Exception:** `Bunny.stl` is the Stanford Bunny from the
  [Stanford 3D Scanning Repository](https://graphics.stanford.edu/data/3Dscanrep/)
  and remains subject to Stanford's terms of use. It is not covered by
  the licenses above.

The simulations use [NGSolve](https://ngsolve.org/), which is licensed
under the LGPL-2.1.
