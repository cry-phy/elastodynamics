# Elastodynamics

The goal of this project is to simulate soft bodies using non linear elastodynamics of hyperelastic materials.

## Target Geometries

Starting with simple bar deformation as test. The endgoal is to import 3D objects like the [Stanford Bunny](https://graphics.stanford.edu/data/3Dscanrep/) as deformation test subjects.

## Target equation

$$
\rho \frac{\partial^2 \mathbf{u}}{\partial t^2} = \nabla \cdot \mathbf{P} + \mathbf{f}_{\text{ext}}
$$
(Wikipedia)

Where:
- $\rho$ is the material density (mass per unit volume in the reference configuration),
- $\mathbf{u}$ is the displacement field,
- $\frac{\partial^2 \mathbf{u}}{\partial t^2}$ is the acceleration,
- $\mathbf{P}$ is the first Piola-Kirchhoff stress tensor,
- $\mathbf{f}_{\text{ext}}$ represents external forces applied to the body.

The Weak formulation is given by <span style="color:red">(Found online, rederive for assurance!!)</span>.:

$$
\int_{\Omega} \rho \frac{\partial^2 \mathbf{u}}{\partial t^2} \cdot \mathbf{v} \, d\Omega + \int_{\Omega} \mathbf{P} : \nabla \mathbf{v} \, d\Omega = \int_{\Omega} \mathbf{f}_{\text{ext}} \cdot \mathbf{v} \, d\Omega + \int_{\partial \Omega_t} \mathbf{t} \cdot \mathbf{v} \, d\Gamma
$$

Then we can choose one of the models to attain the correct Piola-Kirchhoff tensor:

$$
\mathbf{P} = \frac{\partial W}{\partial \mathbf{F}}
$$

Where:
- $\mathbf{F} = \nabla \mathbf{\phi}$ is the deformation gradient tensor ($\phi$ being the mapping function from the reference to the current configuration),
- $W(\mathbf{F})$ is the strain energy density function that characterizes the material's response.

## Possible Strain Energy Density Functions

First we will get Neo-hookean materials working then work up from there. <br>
<span style="color:red">The exact equations have to rechecked!</span>.

1. **Neo-Hookean Material**:

   $$
   W = \frac{\mu}{2} (\mathbf{F}:\mathbf{F} - 3) - \mu \ln J + \frac{\lambda}{2} (\ln J)^2
   $$
   Where:
   - $\mu$ and $\lambda$ are Lamé parameters,
   - $J = \det(\mathbf{F})$ is the determinant of the deformation gradient.

    Already implemented as [example in ngsolve](https://docu.ngsolve.org/latest/whetting_the_appetite/elasticity.html) to serve as basis.

2. **Mooney-Rivlin Material**:
   $$
   W = C_1 (\mathbf{I}_1 - 3) + C_2 (\mathbf{I}_2 - 3)
   $$
   Where:
   - $\mathbf{I}_1$ and $\mathbf{I}_2$ are the first and second invariants of $\mathbf{C} = \mathbf{F}^\top \mathbf{F}$,
   - $C_1$ and $C_2$ are material constants.

    More Realistic but also more complex than Neo-hookean. Able to capture shear effects, performs well under low strain.

3. **Ogden Material**:
   $$
   W = \sum_{p=1}^N \frac{\mu_p}{\alpha_p} \left( \lambda_1^{\alpha_p} + \lambda_2^{\alpha_p} + \lambda_3^{\alpha_p} - 3 \right)
   $$
   Where:
   - $\lambda_1, \lambda_2, \lambda_3$ are the principal stretches,
   - $\mu_p$ and $\alpha_p$ are material parameters.

    Able to capture broader range of material properties (extreme stretch ratios, strong deformation) which could be usefull for this use case.