# Beam Designer

## Purpose
Shear, moment, and deflection diagrams for a beam, with a check of
whether the beam is strong and stiff enough.

## Inputs
- Beam type: simply supported or cantilever
- Span in feet
- Point loads: magnitude in kips and location along the beam in feet
- Uniform loads: magnitude in kips per foot
- Member:
  - A steel W-shape selected from a built-in size catalog
  - A lumber size selected from a built-in size catalog
- Loads must be within the span and all required values must be positive,
  except that load magnitude may be zero
- Steel and lumber member properties, including modulus of elasticity and
  allowable bending stress, must come from the built-in catalogs

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