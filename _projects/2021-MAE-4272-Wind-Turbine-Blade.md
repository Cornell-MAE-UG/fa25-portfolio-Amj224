---
layout: project
title: MAE 4272 Wind Turbine Blade
description: Wind Turbine Blade Optimization 
technologies: [Autodesk Fusion, MATLAB, Python]
image: /assets/images/ProjectTitle.png
---

We set out to design, print, and test a 6-inch wind turbine blade that could extract as much power as possible while meeting the lab’s geometry, structure, and printability limits. From the outset, we framed the operating environment with an energy-weighted wind speed (because power scales with (U^3)), computing (a weighted energy velocty (U_w) =5.04m/s) from a Weibull model so the geometry would be tuned to the winds that matter energetically, not just the average.

Within this context, the blade had to respect R ≤ 6 in, axial projection ≤ 2 in, 6–60 mm chord, and we chose to use a NACA 4412 geometry selection; structurally, flexural stress had to remain < 44 MPa, and manufacturing required a continuous surface printable at 0.1 mm resolution. These constraints shaped every downstream choice.
Our aerodynamic model was Blade Element Momentum Theory (BEMT) with practical corrections: quasi-2D station aerodynamics, Prandtl/Glauert tip-loss models, and airfoil polars for NACA 4412 at Re = 50k, 100k, 200k, interpolated spanwise so each station “saw” the right lift/drag ratio. The material was treated as isotropic, and the inflow steady and uniform—assumptions that are standard for early-stage rotor design and appropriate for our test rig.

![Shaded rendering of earlier version]({{ "/assets/images/Chord-R.png" | relative_url }}){: .inline-image-r style="width: 350px"}

![Shaded rendering of earlier version]({{ "/assets/images/Twist-Rad.png" | relative_url }}){: .inline-image-l style="width: 350px"}

![Shaded rendering of earlier version]({{ "/assets/images/design_spanTorque.png" | relative_url }}){: .inline-image-r}

We began with a clear geometric hypothesis: keep a relatively larger chord farther outboard because local tangential velocity scales with radius and torque authority grows near the tip; set pitch near the ~8.5° lift-rich, stall-safe region of NACA 4412. Initial parameters were TSRdesign = 3, R=6 in, chord taper ~12%R→4%R, and uniform 8.5° twist.
The BEMT workflow proceeded in three moves. A diagnostic first pass revealed unstable induction behavior at the root/tip (inner ~25% span), a common artifact where local TSR is small. We then solved 30 spanwise stations to convergence for axial/tangential induction, which produced accurate but noisy chord/twist at the ends. Finally, we smoothed the tip via linear extrapolation of the last stable points and smoothed the root via quadratic extrapolation from upstream stability—yielding a manufacturable surface without sacrificing the BEMT intent. We also verified that the axial projection stayed ≤ 2 in after smoothing.

At the design point the model predicted, at ~812 RPM and TSR≈3, about (T~0.0117N·m) and (P~W). A simple flapwise bending check with a rectangular-section approximation kept stress well below 44 MPa, satisfying the structural constraint with margin.

![Photo of Angled CAD]({{ "/assets/images/CADProfileAngled.png" | relative_url }}){: .inline-image-l style="width: 350px"}

![Photo of Blades in the Holder]({{ "/assets/images/BladesInHolderBack.png" | relative_url }}){: .inline-image-l style="width: 350px"}

Testing translated theretical calculations into real world data. We locked in setpoints ((R=6 in), (A= pi*R^2), (rho=1.225kg/m^3)), mapped fan frequency→wind speed, and enforced a safe envelope for brake voltage and RPM. For each condition we recorded U, RPM, brake current, and derived torque, power, tip-speed ratio (lambda=omega*R/U), and power coefficient (C_P=P/(0.5*rho*AU^3)). We then built the (P-U), (tau-RPM), and (C_P-lambda) curves for comparison to predictions.

![Power vs RPM with Resisence]({{ "/assets/images/ResGraph_power_rpm.jpg" | relative_url }}){: .inline-image-r style="width: 350px"}

![Power vs Torque Graph]({{ "/assets/images/PvsT_res.png" | relative_url }}){: .inline-image-r style="width: 350px"}

Two findings set the tone of the results. First, peak measured power hit 1.29 W at ~5.56 m/s, and power continued to rise across our test range—no clear peak was captured, implying headroom at higher winds. Second, the rotor ran near (lambda~6)—twice our design TSR—without structural issues. A resonance region around 2100–2500 RPM produced temporary power dips but did not threaten integrity.

Why did the rig outperform the 1 W prediction? The answer is embedded in BEMT physics: with higher operating RPM and (lambda) than assumed, and with healthy stall margin preserved by our pitch choice and smoothing, the machine can ride up the rising limb of the power curve before profile losses dominate. In short, our outer-span geometry and tip-friendly smoothing remained effective at the higher inflow angles of (lambda ~6). That interpretation matches the data and our original hypothesis about tip authority.
The structural story is straightforward: across runs the blade stayed well within the 44 MPa limit, confirming that the geometry choices that helped aerodynamics did not compromise safety.

Looking ahead, we’ll re-target the design to(lambda~6), rebalance chord and twist near the outer span for the steeper local inflow, and shift the modal landscape (thickness/taper/hub interface) to push resonance out of the operating band. Each of these steps is already grounded in our measurements and in the same BEMT framework that got us here.

Bottom line: We delivered a printable, constraint-compliant blade that exceeded 1 W and validated an iterative BEMT→fabrication→test loop. The data say the next iteration should embrace the turbine’s natural operating point at higher TSR and tune the structure to be as smooth dynamically as it is aerodynamically.



<div style="clear: both;"></div>

