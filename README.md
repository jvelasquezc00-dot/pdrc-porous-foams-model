# pdrc-porous-foams-model

Python model that predicts the optical and thermal performance of porous polymer foams for **passive daytime radiative cooling (PDRC)**: materials that reflect sunlight and emit heat through the atmospheric window (8–13 µm), cooling below ambient without energy input.

Developed as part of my MSc thesis in Optics at CICESE (Ensenada, Mexico), *"Estudio de las propiedades espectrales de espumas sólidas para enfriamiento pasivo diurno"* (2026).

## What it does

The model links four physical scales in one pipeline:

| Step | Model | Scale | Output |
| --- | --- | --- | --- |
| 1 | Mie scattering | Single air pore | Scattering/absorption cross sections, asymmetry factor *g* |
| 2 | Maxwell-Garnett + Fresnel/TMM | Composite (infrared) | Effective index, spectral emissivity |
| 3 | Kubelka-Munk | Macroscopic slab (solar) | Diffuse reflectance vs. thickness |
| 4 | Thermal balance (ASTM E1980) | Surface | Net cooling power, equilibrium temperature |

- **Solar range (0.3–2.5 µm):** air pores in a polymer matrix scatter light; Kubelka-Munk turns single-scattering properties into diffuse reflectance, weighted by the AM1.5 solar spectrum to obtain the total solar reflectance (TSR).
- **Infrared (8–13 µm):** Maxwell-Garnett effective medium plus a transfer-matrix (Fresnel) calculation gives the emissivity, weighted by the 310 K blackbody spectrum.
- **Thermal balance:** hemispherical integration over wavelength and angle with measured atmospheric transmittance; the equilibrium surface temperature is solved symbolically (SymPy).

Fixed microstructure: pore radius *r* = 0.4 µm, air volume fraction *f*<sub>v</sub> = 0.1.

## Results

| Material | Solar reflectance (TSR) | Emissivity (8–13 µm) | Net cooling power (W/m²) |
| --- | --- | --- | --- |
| PET | 0.946 | 0.949 | 88.25 |
| PDMS | 0.938 | 0.955 | 82.33 |
| PEI | 0.915 | 0.945 | 57.04 |

Optical saturation is reached at thicknesses of roughly 350–546 µm, depending on the material.

## Repository structure

```
notebooks/   one notebook per material (PET, PDMS, PEI)
data/        optical constants and atmospheric transmittance
```

## Requirements

Python 3.11+ and:

```
numpy==2.3.5
scipy==1.17.0
sympy==1.14.0
matplotlib==3.10.8
miepython
jupyter
```

Install with `pip install -r requirements.txt`, then open the notebooks with `jupyter notebook`.

## Data sources

- **Optical constants (PDMS, PEI, PET):** [refractiveindex.info](https://refractiveindex.info), entries from Zhang et al. (2020), *Appl. Opt.* 59, 2337–2344 (0.4–2 µm) and *J. Quant. Spectrosc. Radiat. Transf.* 252, 107063 (2–20 µm).
- **Atmospheric transmittance:** Mauna Kea spectra from the Gemini Observatory, computed with ATRAN — Lord, S. D. (1992), NASA Technical Memorandum 103957. We acknowledge the Gemini Observatory for providing these data.

## Acknowledgments

Thesis advisors: Dr. Eugenio Méndez and Dr. Alma González Alcalde (CICESE).

## Author

José Alejandro Velásquez Castaño — Physicist, MSc in Optics
jvelasquezc00@gmail.com

## License

MIT — see [LICENSE](LICENSE).
