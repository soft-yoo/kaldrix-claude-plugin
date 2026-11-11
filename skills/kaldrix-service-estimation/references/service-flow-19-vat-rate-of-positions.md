## VAT rate of positions

The VAT rate of a new position comes from the estimate, never from the price list (KDX-217). By default the estimate
follows the project. The following housing suggestions apply only to the Polish company profile: a single-family house up to 300 m² of usable floor area or a dwelling up to 150 m² gets 8%, above
the limit the base is split proportionally (8% on limit / area of the base, 23% on the rest, `vatReducedShare`), and a
non-residential object gets 23%. `create_estimation_item` without `vatRate` takes the estimate rate; set `vatRate`
when the contractor chooses a different rate for that row.
`get_estimate_checks` reports `VAT_RATES_MIXED` (positions with another rate than the estimate) and
`VAT_PROJECT_MISMATCH` (the estimate rate chosen by hand differs from the project); after confirming with the user,
`apply_project_vat_to_estimate` gives the estimate and every position the project rate. This is not tax advice.

For a Quick quote, ask which rate the contractor wants to use for this job. The company’s rates are suggestions.
On creation send `vat: "CUSTOM"` and `customVatRate` as a fraction (for example, `0.135` for 13.5%).
Use `0` for a taxable 0% rate; use `vat: "EXEMPT"` without a percentage for an exemption.
To change a draft with `set_quick_quote_vat`, confirm the new rate with the user: it applies to every position.
