# Beam Designer

## Purpose
Shear, moment, and deflection diagrams for a beam, with a check of
whether the beam is strong and stiff enough.

## Inputs
- Beam type
  - Unit: not applicable
  - Range: simply supported or cantilever
  - Default: simply supported
  - Control: segmented control
- Span
  - Unit: feet
  - Range: 1.0 to 100.0 feet
  - Default: 20.0 feet
  - Control: numeric input
- Point loads
  - Entry count: zero or more
  - Default: no point loads
  - Control: Add Point Load and Remove Point Load buttons
  - Magnitude unit: kips
  - Magnitude range: -100.0 to 100.0 kips
  - Magnitude default: 0.0 kips
  - Magnitude control: numeric input
  - Negative magnitudes act upward; positive magnitudes act downward
  - Location unit: feet from the left end
  - Location range: 0.0 to the beam span
  - Location default: midpoint of the beam span
  - Location control: numeric input
- Uniform load
  - Entry count: one or more
  - Default: one load
  - Control: Add Uniform Load and Remove Uniform Load buttons
  - Load unit: kips per foot
  - Load range: -10.0 to 10.0 kips per foot
  - Load default: 1.0 kips per foot
  - Load control: numeric input
  - Negative loads act upward; positive loads act downward
  - Coverage: entire beam span
- Member material
  - Unit: not applicable
  - Range: steel or lumber
  - Default: steel
  - Control: segmented control or radio group
- Steel W-shape
  - Unit: not applicable
  - Range: all standard US W-shapes in the built-in catalog
  - Default: W12x26
  - Control: searchable dropdown
  - Shown only when steel is selected
- Lumber species
  - Unit: not applicable
  - Range: species in the built-in lumber catalog
  - Default: Douglas Fir-Larch
  - Control: dropdown
  - Shown only when lumber is selected
- Lumber grade
  - Unit: not applicable
  - Range: grades in the built-in lumber catalog
  - Default: No. 2
  - Control: dropdown
  - Shown only when lumber is selected
- Lumber size
  - Unit: nominal inches, shown as a standard lumber designation
  - Range: sizes available for the selected species and grade
  - Default: the first valid size in the selected catalog
  - Control: dropdown
  - Shown only when lumber is selected
- Member properties
  - Cross-sectional area, section modulus, moment of inertia, modulus of
    elasticity, and allowable bending stress are read-only catalog properties
  - Unit: standard US customary values
  - Range: values supplied by the selected member catalog entry
  - Default: determined by the selected member
  - Control: no direct user control

## Behavior
- Use US customary units throughout
- Add or remove point loads and uniform loads
- Recalculate when the user explicitly selects Calculate or Analyze
- Show clear inline validation for missing or invalid inputs
- Do not show analysis results for an invalid or incomplete input set
- Preserve the entered values while validation or recalculation is displayed

## Calculations
- Use upward force and upward reaction values as positive. Define positive
  point-load and uniform-load values as downward, matching the signed input
  values. The beam's left end is x = 0 ft and the right end is x = L ft.
- Define H(t) = 1 when t >= 0 and H(t) = 0 otherwise. Positive internal
  shear satisfies V(x) = dM(x)/dx between point loads.
- Combine all uniform loads acting over the full span into one distributed
  load:
  - w = sum of uniform-load magnitudes, in kip/ft
- Point-load resultant:
  - P_i = signed point-load magnitude, in kip
  - x_i = point-load position measured from the left end, in ft
- Reactions:
  - Simply supported:
    - R_B = [sum(P_i x_i) + wL^2/2] / L
    - R_A = sum(P_i) + wL - R_B
  - Cantilever:
    - R_A = sum(P_i) + wL
    - M_A = sum(P_i x_i) + wL^2/2
  - R_A is the left vertical reaction, R_B is the right vertical reaction,
    and M_A is the counterclockwise external fixed reaction moment. The
    internal beam moment at the cantilever root is M(0) = -M_A.
- Shear at position x:
  - Simply supported:
    - V(x) = R_A - sum[P_i H(x-x_i)] - w x
  - Cantilever:
    - V(x) = sum[P_i H(x_i-x)] + w(L-x)
  - V is in kip
- Moment at position x:
  - Simply supported:
    - M(x) = R_A x - sum[P_i(x-x_i)H(x-x_i)] - w x^2/2
  - Cantilever:
    - M(x) = -sum[P_i(x_i-x)H(x_i-x)] - w(L-x)^2/2
  - M is in kip-ft
  - Include exact support and point-load positions when sampling diagrams
- Deflection:
  - EI y''(x) = M(x), with consistent sign units
  - y is vertical deflection, positive upward; E is modulus of elasticity,
    and I is moment of inertia about the bending axis
  - Express length in inches and loads in kips for numerical calculations:
    E in ksi, I in in^4, M in kip-in, and y in inches
  - Apply support boundary conditions for the selected beam type and integrate
    M/EI twice along the full span
  - Simply supported: y = 0 at both x = 0 and x = L
  - Cantilever: y = 0 and y' = 0 at x = 0
- Bending stress:
  - f_b = M_max_in / S
  - M_max_in is the largest absolute moment converted to kip-in
  - S is section modulus in in^3
  - f_b is in ksi
  - Bending pass condition: f_b <= F_b, where F_b is the catalog allowable
    bending stress in ksi
- Deflection limit:
  - L_in = L * 12
  - y_limit = L_in / 360, in inches
  - Deflection pass condition: |y_max| <= y_limit
- Maximum output values:
  - V_max = maximum absolute shear in kip
  - M_max = maximum absolute moment in kip-ft
  - y_max = maximum absolute deflection in inches
- Overall result:
  - Pass only if both the bending and deflection checks pass

## Outputs
- Beam and load diagram
- Shear diagram
- Moment diagram
- Deflection diagram
- Maximum shear, maximum moment, and maximum deflection
- Pass or fail for bending and deflection
- A clear overall pass/fail result

## Look and feel
- Clean and professional
- Example beam loaded when the app opens
- The example may be replaced by direct user edits
- Responsive enough to remain usable on desktop and mobile screens
- Use clear labels and legend text for supports, loads, and diagram values
- Show no result-only elements until valid analysis is available

## Validation
20 ft simply supported W12x26 with 1 kip/ft: M = 50.0 kip-ft,
deflection 0.609 in.

## Out of scope
Continuous beams and buckling.

## Resolved notes
- Default beam type: simply supported.
- Span: 1.0 to 100.0 feet, default 20.0 feet.
- Point-load magnitude: -100.0 to 100.0 kips, default 0.0 kips.
- Point-load location: 0.0 feet to the beam span, default at midspan.
- Uniform load: -10.0 to 10.0 kips/ft, default 1.0 kip/ft.
- Uniform loads apply over the full beam span.
- Upward point and uniform loads use negative magnitudes.
- Steel uses the full standard US W-shape catalog.
- Lumber defaults to Douglas Fir-Larch, No. 2.
- Lumber species and grade are selectable.
- Member properties come from the selected built-in catalog entry.
- The example is a 20 ft simply supported beam with W12x26 and 1 kip/ft
  of uniform load.