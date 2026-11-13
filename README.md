# Cubic equations of state for real gases

Python calculator for pure-component real-gas PVT properties, enthalpy, entropy and fugacity using van der Waals (vdW), Redlich-Kwong (RK), Soave-Redlich-Kwong (SRK) and Peng-Robinson (PR) equations of state.

This repository draft contains the supplied calculator and project report. The calculator includes a database of 29 species, phase-root selection, saturation-pressure calculations, latent heat and optional plots.

## Files

- `cubic_eos.py`: supplied calculator, unchanged.
- `CHL2002_Project_Report.pdf`: supplied project report with the author line corrected to Geetansh Jain at the author's request.
- `requirements.txt`: required numerical libraries and the plotting library.

## Run

Use Python 3.10 or newer.

```sh
python -m pip install -r requirements.txt
python cubic_eos.py n-butane -T 500 -P 50 --eos RK
python cubic_eos.py CO2 -T 300 -P 40 --compare --psat
python cubic_eos.py methane -T 200 -P 30 --plots
python cubic_eos.py
```

The last command opens the interactive menu. Plot mode writes `isotherms.png`, `zchart.png` and `props.png` in the current directory.

## Units and reference state

- Temperature: K.
- Pressure and fugacity: bar.
- Molar volume: cm^3/mol.
- Enthalpy: J/mol.
- Entropy: J/(mol K).
- Default reference: ideal gas at 298.15 K and 1 bar.

The built-in species data and ideal-gas heat-capacity constants are described in the report. Model inputs are not a substitute for checking the range of validity of those correlations.

## Validation status

A smoke check of the supplied code for n-butane with RK at 500 K and 50 bar returned Z = 0.68519, fugacity = 37.178 bar and residual enthalpy = -4502.8 J/mol, consistent with the report's displayed sample. This is one execution check, not an independent reproduction of all reported validation results.

The report discusses textbook and CoolProp comparisons and references a `validate.py` script. That script and the underlying benchmark data are not included in the supplied files, so those tables have not been independently reproduced for this draft.

## Scope and limits

This code models pure components. It does not include mixture rules, a trained regression surrogate, a machine-learning training pipeline or measured surrogate speedups. Those parts of the broader CV project are not included here.

Cubic equations of state are approximations. The report discusses limits for polar fluids and low-temperature heat-capacity extrapolation. Check numerical convergence and physical validity before using results for engineering decisions.

## References

- Smith, Van Ness, Abbott and Swihart, *Introduction to Chemical Engineering Thermodynamics*, 8th edition, 2018, chapters 3, 6 and 13 and appendices B and C, as cited in the report.
- Bell et al., *Industrial & Engineering Chemistry Research* 53 (2014), 2498, as cited in the report for CoolProp.
