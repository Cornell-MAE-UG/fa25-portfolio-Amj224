---
layout: project
title: MAE 4272 Wind Turbine Blade
description: Wind Turbine Blade Optimization 
technologies: [Autodesk Fusion, MATLAB, Python]
image: /assets/images/ProjectTitle.png
---

We set out to design, print, and test a 6 inch horizontal axis wind turbine blade that maximizes power extraction while meeting strict geometry, strength, and printability limits. Because wind power scales with U^3, we framed the operating environment using an energy weighted wind speed = 5.04 m/s from a Weibull model tuning our geometry to the winds that matter energetically, not just the average. Within this context, the blade had to respect R≤6 in, axial projection ≤2 in, 6–60 mm chord, and we chose to pursue a NACA 4412 section; structurally, flexural stress had to remain < 44 MPa, and the surface needed to be printable at 0.1 mm resolution.

Our aerodynamic model was Blade Element Momentum Theory (BEMT) with practical corrections: quasi-2D station aerodynamics, Prandtl/Glauert tip loss effects, and spanwise interpolation of NACA 4412 polars at Re = 50k, 100k, 200k so each station “saw” an appropriate lift/drag ratio. We assumed an isotropic material and steady, uniform inflow appropriate for early rotor design and our bench setup. Geometrically, we hypothesized that keeping more chord outboard would leverage higher tangential velocity and tip torque authority, and we set pitch near ~8.5° (lift rich, stall safe for 4412). The initial design used TSR design=3, R=6 in, chord taper ~12%R → 4%R, and uniform 8.5° twist. Our BEMT workflow proceeded in three steps: (1) a diagnostic pass (revealed unstable induction near root/tip where local TSR is small), (2) a 30 station converged solve for axial/tangential induction (accurate but noisy at the ends), and (3) root/tip smoothing (quadratic near the root, linear near the tip) to yield a manufacturable surface while keeping axial projection ≤2 in. At the design point, the model predicted ~812 RPM at TSR ≈3 with T≈0.0117 N\cdotpm and P≈1.0 W, and a flapwise bending check kept stress comfortably below 44 MPa.

![Shaded rendering of earlier version]({{ "/assets/images/chord+twist_g.png" | relative_url }}){: .inline-image-c style="width: 600px"}


![Photo of Angled CAD]({{ "/assets/images/CADProfileAngled.png" | relative_url }}){: .inline-image-l}

![Photo of Blades in the Holder]({{ "/assets/images/BladesInHolderBack.png" | relative_url }}){: .inline-image-l}

Testing translated theory into data. We fixed setpoints (R=6 in), (A=πR^2), (ρ=1.225 kg/m^3), mapped fan frequency → wind speed, and enforced a safe envelope for brake voltage and RPM. For each condition we recorded U, RPM, and brake current, then derived torque, power, tip speed ratio λ=ωR/U, and power coefficient CP=P/(0.5ρAU^3). We then built the P–U, τ–RPM, and CP–λ curves to compare with predictions. Two findings stood out: (i) peak measured power reached 1.29 W at ~5.56 m/s, and power continued rising within our tested range (suggesting additional headroom), and (ii) the rotor operated near λ≈6 about 2× the design TSR—without structural issues. A 2100–2500 RPM resonance band produced temporary power dips but did not threaten integrity. We deemed our wind terbine was reaching resisance frquencies at this RPM and this apeared to only be an issue with higher preforming teams as the force applied on the outer edges of the blade were being compounded by a slight misalignment in the lab set up making the turbine vibrate and dip in power output. This apparent “outperformance” is consistent with BEMT: at higher λ (with stall margin preserved by our pitch and smoothing), the rotor can ride the rising limb of the power curve before profile losses dominate i.e., our outer-span geometry remained effective at the steeper inflow angles of λ≈6.

![Power vs RPM with Resisence]({{ "/assets/images/res_g.png" | relative_url }}){: .inline-image-c style="width: 600px"}


Outcome & next steps. We delivered a printable, constraint compliant blade that met strength requirements and exceeded 1 W in test. Going forward, we will retarget the geometry to λ≈6, rebalance tip side chord/twist for the steeper inflow, and shift the structural modes (thickness/taper/hub interface) so resonance sits outside the operating band. 

My contribution: I worked with the group in the design phase and focused on executed the root/tip smoothing to meet the axial projection/manufacturability limits. I also did the CAD model as well as built the post processing for τ, P, λ, and CP including the comparison plots with a focus on the resisance graphs.



<div style="clear: both;"></div>

