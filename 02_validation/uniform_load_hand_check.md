# Simply Supported Uniform-Load Hand Check

## Inputs
- Beam: simply supported
- Span: 20 ft
- Uniform load: 1 kip/ft downward over the full span
- Point loads: none
- Member: W12x26
- Section modulus: 33.4 in^3
- Moment of inertia: 204 in^4
- Modulus of elasticity: 29,000 ksi

## Independent hand calculation
- Total load = (1 kip/ft)(20 ft) = 20 kip.
- By symmetry, each support reaction is 20/2 = 10 kip upward.
- Shear: V(x) = 10 - x kip, with x in feet. The maximum absolute shear is
  10 kip.
- Moment: M(x) = 10x - x^2/2 kip-ft. Setting dM/dx = 10 - x = 0 gives
  x = 10 ft and M_max = 50 kip-ft.
- For a simply supported beam with full-span uniform load:
  - w = 1/12 kip/in and L = 20(12) = 240 in.
  - Delta_max = 5wL^4/(384EI)
  - Delta_max = 5(1/12)(240^4)/(384(29,000)(204))
    = 0.608519 in, which rounds to 0.609 in.
- Bending stress = (50 kip-ft)(12 in/ft)/(33.4 in^3) = 17.964 ksi.
- Deflection limit = 240/360 = 0.666667 in.

## App comparison
- Reactions: 10.00 kip at each support
- Maximum shear: 10.00 kip
- Maximum moment: 50.00 kip-ft
- Maximum deflection: 0.609 in
- Bending stress/reference Fb: 17.96/23.80 ksi; pass
- Deflection/limit: 0.609/0.667 in; pass
- Overall: pass

The app agrees with the hand calculation to the displayed precision. Its
steel bending-stress reference value is a demo assumption, not an adjusted
design allowable.
