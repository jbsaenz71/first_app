# Beam Designer

## Purpose
Shear, moment, and deflection diagrams for a beam, with a check of
whether the beam is strong and stiff enough.

## Inputs
- Beam type
  - Unit: not applicable
  - Range: simply supported or cantilever
  - Default: cantilever
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
- Reactions, shear, and moment from statics
- Deflection along the beam
- Bending stress fb = M/S, compared to the allowable stress
- Deflection compared to L/360

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