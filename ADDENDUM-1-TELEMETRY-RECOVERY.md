# Operation TrueView — Mission 2, Addendum 1: Telemetry Recovery and Apogee Correction
**Version:** 1.1
**Supersedes:** altitude statements in METHODS.md v1.0.0 (§3, §6): nominal ≈30.5 km with 25.0 km sensitivity is replaced by the METAR-validated apogee below.

## A1.1 Recovery
A per-camera service log (CAM 1, rear audit camera) was recovered after publication. It recorded barometric pressure, relative humidity, and internal/external temperature entries that the primary mission log did not retain. Two entries bracket the flight.

## A1.2 Clock offset
The service-log wall clock ran +5:00:00 relative to true UTC (no NTP in flight). Decoded:
Entry 1 = 09:11:55 CDT (ground boot, ~6 min before the 09:18 CDT launch).
Entry 2 = 10:56:23 CDT (T+1:38:23, consistent with observed burst at T+1:39).

## A1.3 Ground validation
Entry 1: 996.10 hPa, sensor altitude field 471 ft, RH 82.4%. Launch area: Uhland/Buda, TX (south of Austin). Regional synoptic pressure validated against Austin METAR altimeter setting 29.94 inHg (1013.9 hPa sea-level-referenced) → station pressure at ~471 ft ≈ 996.6 hPa. Agreement ≈0.5 hPa. Sensor calibration validated at launch; aloft readings inherit that validation. Launch-site elevation difference vs the METAR station (<200 ft) affects apogee geometry by <0.01°.

## A1.4 Apogee
Entry 2 (burst): 12.99 hPa, RH 7.6% (stratospheric dry-air signature), T_int 37.7 °C, T_ext 17.6 (sun-heated sensor, not ambient; see A1.7). US Standard Atmosphere 1976 pressure altitude for 12.99 hPa (20–32 km layer): 29.32 km = 96,200 ft.

## A1.5 Derived-column caveat
Any derived altitude field reporting ≈82,000 ft concurrent with 12.99 hPa uses a troposphere-only lapse formula invalid above 11 km. Raw pressure is the primary observable; derived columns are secondary and flagged where inconsistent.

## A1.6 Corrected predictions at sealed apogee (h = 29.32 km)
- Null model (spherical Earth + standard refraction): geometric tangent 5.50°; apparent floor ≈4.8°.
- Extinction-medium ("soup") model, σ = 0.0065–0.0071 km⁻¹ (V = 551–602 km): dip = arctan(h/V) − kV/(2R) = 2.43–2.72°.
- Measured rim (Mission 2): 2.51° ± 0.30°. Inside the medium-model band; excluded from the null-model floor by ≥2.0°.
