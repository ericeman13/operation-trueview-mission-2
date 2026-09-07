# Operation TrueView — Mission 2 Methods Note

**Title:** Apparent horizon dip from stratospheric balloon altitudes: water-tube-referenced
imaging, an extinction-rim model, and a tangent-floor falsification test
**Author:** Eric Eman (Operation TrueView) — [GitHub handle / ORCID if held]
**Version:** 1.0 — 2026-09-08
**License:** CC-BY-4.0
**Flight:** Mission 2, 2026-03-14 (Pi Day). Validation flight (Mission 3) planned 2026-12.

## 1. Abstract
Opposed, water-tube-referenced cameras on a high-altitude balloon (barometric apogee
≈30.5 km; sensitivity case 25.0 km) measured the apparent horizon — the atmospheric
contrast-extinction rim — at a depression of 2.51° ± 0.30°. The spherical-Earth geometric
tangent at these altitudes is 5.59° (30.5 km) and 5.06° (25.0 km); with standard atmospheric
refraction the apparent tangent floor is ≈4.9° and ≈4.4° respectively. Because extinction can
remove surface contrast but can never create it above the (refracted) tangent, any
surface-derived visible rim on a spherical Earth must lie at or below that floor. The measured
rim lies 1.6–2.4° above the floor and is therefore incompatible with a surface tangent under
any standard-atmosphere extinction profile. A plane + extinction model (Beer–Lambert;
Koschmieder 2% contrast threshold; standard refraction) predicts a rim at 2.0–2.9° across the
joint altitude and extinction-coefficient uncertainty, consistent with the measurement. This
note defines the observable, calibration, uncertainty budget, falsification tests, and the
Mission 3 in-situ validation plan (photometric σ, T/P-derived ray curvature, multi-altitude
dip profile, dual-wavelength rim test, pre-registered predictions).

## 2. Observable definition
- **Feature:** sky-to-ground transition band in near-horizontal imagery.
- **Primary row (rim edge):** shallowest pixel row at which identifiable surface-feature
  contrast against local haze exceeds C = 0.02 (Koschmieder threshold).
- **Secondary row (fade midpoint):** row of maximum |dL/dy| in the transition band, averaged
  over a masked central column window, sub-pixel parabolic fit.
- **Reference:** physical water-tube true level, ground-locked to the optical center row.
- **Angle conversion:** dip = arctan((y_row − y_center)/f_px), with
  f_px = (H/2)/tan(VFOV/2); H = image height (px), VFOV from per-camera bench calibration.
Mission 2 reports the primary (rim-edge) row; Mission 3 reports both rows algorithmically.

## 3. Instrumentation (Mission 2)
- **Audit pair:** two Raspberry Pi Camera V2 modules (62.2° nominal HFOV; per-camera VFOV
  bench-calibrated), mounted opposed fore/aft on one rigid plate.
- **Context cameras:** GoPro 12 (linear, 95°); Sony a6400 + Laowa 9mm f/2.8 Zero-D
  (rectilinear; ≈105.1° × 72.6° H×V in 16:9); Pi Camera HQ + 3.2mm lens, IR-block filter
  removed (≈100°).
- **Attitude/telemetry:** ICM-20948 and MPU-9250 9-axis IMUs at 50 Hz; LoRa 915 MHz downlink
  (GPS, barometric altitude, pressure, attitude); GPS/APRS position logging.
- **Level reference:** water tube imaged during ground calibration; camera center row aligned
  to the water line; rig bonded thereafter.

## 4. Calibration and tilt algebra
- Ground lock establishes center row = true local horizontal, per camera.
- Opposed-camera algebra: with residual rig tilt t projected into the measurement plane,
  dip_fore = D + t and dip_aft = D − t, hence D = (fore + aft)/2 and t = (fore − aft)/2.
- Mission 2: fore 2.66°, aft 2.36° → D = 2.51°, t = 0.15°.

## 5. Models
**5.1 Spherical Earth + atmosphere (null model).** Geometric tangent dip
δ_g = arccos(R/(R+h)). Apparent floor δ_a = δ_g − r_t with r_t ≈ 0.6–0.7° (standard refraction
at the tangent). Constraint ("tangent floor"): rays shallower than δ_a never intersect the
surface; extinction acts only on intersecting rays; therefore any surface-derived visible rim
must satisfy dip ≥ δ_a. Values: h = 30.5 km → δ_g = 5.59°, δ_a ≈ 4.9°; h = 25.0 km →
δ_g = 5.06°, δ_a ≈ 4.4°.
**5.2 Plane + extinction medium ("soup" model).** Visual range V = 3.912/σ (Koschmieder,
C = 0.02). Predicted rim dip = arctan(h/V) − V/(2·R_ray), where R_ray is the atmospheric ray
curvature radius; in surveying convention R_ray = R/k (k ≈ 0.13), giving the equivalent form
arctan(h/V) − kV/(2R). The refraction term is half the total ray bend over the path
(chord–tangent angle at the observer end); it is an atmosphere property and carries no
surface-curvature assumption (R-free form shown).
**5.3 Wavelength dependence.** σ(λ) decreases toward IR ⇒ V_IR > V_vis ⇒ rim_IR at shallower
depression than rim_vis. A geometric tangent is wavelength-independent. A wavelength-dependent
rim shift implies medium control.
**5.4 Altitude dependence.** Null model scales ≈√(2h/R); soup model scales ≈arctan(h/V).
Different curve shapes; discriminated by a multi-altitude dip profile.

## 6. Mission 2 results and uncertainty
- Measured rim dip D = 2.51° (fore 2.66°, aft 2.36°).
- σ fitted from surface-feature contrast decay versus modeled range:
  σ = 0.0065–0.0071 km⁻¹ ⇒ V = 551–602 km.
- Soup-model prediction over joint h ∈ [25.0, 30.5] km and the σ band: 2.0–2.9°.
  Measurement lies inside the band.
- Null-model apparent floor: 4.4–4.9°. Measurement excluded by ≥1.6° (>5× the total budget).
- **Uncertainty budget (1σ):** residual tilt ±0.15°; FOV bench calibration ±0.10°;
  row selection ±0.20°; frame scatter / attitude sync ±0.10°; RSS = ±0.29° (reported ±0.30°).

## 7. Falsification tests
- **F1 (tangent floor):** measured rim above δ_a at all candidate altitudes ⇒ rim is not a
  surface tangent under any standard-atmosphere extinction/refraction profile. Lowering the
  floor to 2.5° requires sustained super-refraction k ≈ 0.4 over ≥500 km (mirage regime),
  excluded by absence of mirage artifacts and by logged T/P profiles (Mission 3).
- **F2 (wavelength):** rim shift with wavelength ⇒ medium control (Mission 2: qualitative IR
  witness; Mission 3: quantitative).
- **F3 (altitude profile):** curve-shape test, √h versus arctan(h/V) (Mission 3).
- **F4 (in-situ σ):** photometer-measured σ replaces fitted σ, converting the fit into a
  forward prediction. A forward miss exceeding the budget falsifies the soup model.

## 8. Limitations
- Mission 2 σ is fitted from the same imagery (addressed by F4).
- Mission 2 row selection is analyst-identified rim edge; algorithmic dual-metric pipeline
  deferred to Mission 3.
- First-order homogeneous-σ model; layered aerosol profile to be incorporated with Mission 3
  photometer and T/P data.
- Single flight, single launch site; repeats planned.

## 9. Mission 3 validation plan (2026-12)
- Dual TSL2591 photometers in baffle tubes (horizon-viewing and nadir-viewing), 1 Hz.
  Column σ via solar Langley-plot photometry during ascent (direct-beam decay vs air mass);
  path contrast via horizon/nadir radiance ratio.
- T/P logger → density profile → k and R_ray from standard refraction relations.
- Multi-altitude dip profile from the audit pair, 5–30 km.
- Dual-wavelength rim: visible channel vs IR-block-removed channel.
- Dual-metric row pipeline (threshold row + gradient-peak row), published code.
- **Pre-registration:** predicted dip-vs-altitude curves (both models) published before launch;
  post-flight comparison against the pre-registered bands.

## 10. Data and code availability
- Repository: github.com/[HANDLE]/trueview-mission2 (Zenodo DOI per release).
- Contents: this note (MD + PDF), analysis scripts (row selection, angle conversion, tilt
  algebra), FOV calibration tables, water-tube lock imagery, telemetry excerpts (CSV),
  representative frames with checksums.
- Full-resolution raw video: [archive.org item / public drive link]; checksums in repository.

## 11. References
1. Lambert, J. H., *Photometria*, Augsburg (1760).
2. Beer, A., *Annalen der Physik und Chemie* 86, 781–784 (1852).
3. Koschmieder, H., *Beiträge zur Physik der freien Atmosphäre* 12, 33–53 & 171–181 (1924).
4. WMO, *Guide to Meteorological Instruments and Methods of Observation*, WMO-No. 8
   (meteorological optical range, 2% contrast threshold).
5. NOAA/NASA/USAF, *U.S. Standard Atmosphere*, 1976.
6. *The American Practical Navigator* (Bowditch), NOAA (horizon dip, refraction conventions).
7. Bomford, G., *Geodesy*, Oxford University Press (refraction coefficient k).
8. Adjacent prior art: slant visual range / slant-range visibility literature in aviation
   meteorology (ICAO Annex 3; WMO visibility guidance). These compute visibility along a
   slant path; the present work computes the angular location of the extinction rim and uses
   it as a geometry discriminator.

## Appendix A — Row-selection pseudocode
prof[y] = mean luminance over masked central columns
threshold row: shallowest y where feature contrast C(y) > 0.02
gradient row:  y* = argmax |d prof/dy| over transition band; sub-pixel parabolic fit
dip = degrees(arctan((y_row − y_center)/f_px))

## Appendix B — Symbols
h observer height; R Earth radius (convention only, §5.2); σ extinction coefficient (km⁻¹);
V visual range (km); k refraction coefficient (≈0.13); R_ray ray curvature radius (km);
C contrast threshold (0.02); f_px focal length in pixels; D rim dip; t residual tilt.


---
## Change log
- v1.1.0 — Addendum 1: telemetry recovery, METAR-validated apogee 96,200 ft, corrected predictions; author metadata added.
- v1.0.0 — Initial publication.
