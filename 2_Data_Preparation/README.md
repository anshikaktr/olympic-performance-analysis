<img width="667" height="476" alt="Screenshot 2026-10-28 at 7 46 10 PM" src="https://github.com/user-attachments/assets/00864fee-bd74-4a0d-8c87-45d0852ec804" />

Calculated Efficiency Verification: medal_efficiency_pct was recomputed in Tableau as total ÷ athletes_sent × 100 (rounded to 2 decimals). The first check flagged 3 rows (11 rows differ in the file) with a 0.01-point difference, caused by rounding exact halves (e.g. 3.125) down in the source build versus up in Tableau. The column was rebuilt with half-up rounding, and the re-check returned 0 mismatches.

<img width="639" height="442" alt="Screenshot 2026-10-28 at 7 47 22 PM" src="https://github.com/user-attachments/assets/7e247089-798d-4d27-a3b0-c0ab421c3791" />
