# NGTS manuscript review — 5 November 2026

The active manuscript is `Paper.tex`; `paper_text.tex` is not included by it. The revised proof is `output/pdf/Paper.pdf`. This review covers the manuscript text, citations, and rendered layout. It does not validate the reduction implementation or recompute the scientific results.

## Changes made

- Copy-edited the active manuscript for spelling, grammar, British English, repetition, terminology, and clarity, retaining its high-level description of targeted operations and reduction.
- Tightened the abstract, introduction, scheduling description, methods, data-product descriptions, captions, and conclusions. Distinguished the historical survey workflow from rapid targeted reduction.
- Replaced the RASTI document class with the official MNRAS class and supplied `mnras.cls`, `mnras.bst`, and their licence/readme. Corrected keywords, table rules and wrapping, table-caption placement, software typography, and a duplicate figure label. Removed the unused template appendix.
- Retained all original figure files and every `\includegraphics` command unchanged.
- Used the author-confirmed parent sample of **3130** sources. The tracking caption no longer assigns this count to its plotted subset.
- Removed six repeated bibliography records and two duplicate/outdated aliases. Added the original SYSREM reference and the existing TIC v8 reference at first relevant use. Legitimate unused bibliography records remain available for future revisions.
- Removed the unsupported blanket precision sentence, stale TESS candidate counts, unverified numerical TFOP field-of-view comparison, and ambiguous 78 per cent site-quality statistic. These removals avoid replacing uncertain numbers with guesses.
- Removed the conclusion's reference to dilution/PRF products, since that method is commented out in the active manuscript.

## Author input needed before submission

1. **Complete the author list and metadata definitions.** The author line still contains `many more`. Seven table descriptions remain `ASK RICHARD`: `CI_ACTIONXXXXXX`, `AJ`, `EXT_XSLOPE`, `EXT_YSLOPE`, `AJ_ACTION`, `EXT_XSLOPE_ACTION`, and `EXT_YSLOPE_ACTION`. Please supply their definitions, units, dimensions, and relevant flag conventions. These placeholders have deliberately not been disguised or filled with inferred meanings. Accepted/received dates are publisher placeholders and can remain so.

2. **Specify the performance statistic and selection.** The old sentence claimed typical 0.01 per cent (100 ppm) precision in 1 h for stars brighter than T=14. The existing plot does not support that blanket statement: its ordinate is log10(RMS in per cent), and the bright-end cloud is visually nearer 0.1 per cent. This is a reading of the figure, not a recalculated result. The sentence has been replaced by a qualitative comparison. Please provide a validated precision range and explain how the 1-h RMS is calculated, what detrending/binning is applied, and which sources/nights are retained. The parent sample is 3130, as confirmed, but the plotted selections differ: the existing PDF streams contain approximately 2523 photometric marker positions and 311 tracking positions. Confirm whether cuts, axis limits, overlap, or separate selections explain this. No figures were modified.

3. **Reconcile the low-level file inventory.** The text says 12 files per action but explicitly describes nine. The commented example lists eleven, including PSF and FLAGS products. Confirm the current count and either enumerate the full set or avoid a fixed total.

4. **Document the integer encodings.** Explain the scaling/offset convention that preserves subpixel WCS and centroid positions in unsigned 16-bit arrays. Identify the time scale of the 2014-01-01T00:00:00 reference epoch and how integer-second timestamps map to BJD_TDB, including any quantization or stored scaling. The final photometry table should state time, position, PSF-width, and flux units where appropriate. Clarify that `BJD_SHORT` is a transformed plotting coordinate, and define its gap removal, if that is its purpose.

5. **Check the aperture prescription.** The table leaves D=0.6 mm undefined (`0.5 <= D < 0.6`, then `D > 0.6`), while the kernel calibration calls 0.6 mm the maximum defocus. Confirm the boundary and whether larger defocus is supported. The products still call the aperture “optimal”, whereas the active methods describe a defocus-based choice; confirm whether any additional target-specific optimization is actually performed.

6. **Clarify three methodological definitions.** The focused PSF is quoted as about 2 pixels in source detection and about 3 pixels in the WCS discussion; identify the statistic/sample if both are intentional. Define whether the WCS stopping threshold concerns the median residual, a fit step, or the change in successive improvements. Define the 9-pixel centroid window precisely: SEP `winpos` accepts a Gaussian sigma, with a separate integration extent. Also identify the scatter estimator/masking used for the laser's one-sigma threshold if this detail is needed for reproducibility.

7. **Check literal FITS identifiers and statistics.** Names were preserved rather than silently corrected. Confirm whether `$i$ mag`, `PFSSEP`, `PFSTOM`, and `PFSRICH` are the actual column identifiers. Ensure that `SIGMA_XS` is described consistently: the current text alternates between a source-specific metric and a frame-wide metric. Confirm `Gaia_id` release and magnitude-band definitions where relevant.

8. **Confirm the faint-target exception and current operations.** The final-product magnitude cut is now explicitly described as the default, consistent with the earlier provision to relax T<16 for a requested faint target; confirm that such targets survive into final products. Check that disk shipment, storage and turnaround descriptions still match current practice. The comparison of calibration-frame handling is explicitly with the published survey pipeline; confirm whether the present survey pipeline has since changed.

9. **Check the remaining contextual details.** Confirm whether the lunar-spectrum dashed markers are harmonics rather than aliases, and whether the stated plans for additional laser-guide-star systems remain current. If retaining a quantitative weather statistic, distinguish a fraction of nights from a fraction of night-time and supply its source.

10. **Complete the availability statement.** The statement preserves availability of data on request. Specify the actual access route for the pipeline code and the version/release described, or state any access restrictions. Confirm that the funding acknowledgements and author initials are complete for the final author list. MNRAS requests a data-availability statement and encourages access to underlying data and software; see the [author instructions](https://academic.oup.com/mnras/pages/General_Instructions).

## Verified factual and citation corrections

- NGTS first light was 2015 and full survey operations began in 2016, rather than 2017: [Wheatley et al. instrument paper](https://www.eso.org/public/archives/releases/sciencepapers/ann170xx_ngts/ann170xx_ngtsa.pdf).
- TESS full-frame cadence is 200 s from Cycle 5 onwards, rather than the old 10-min description: [NASA HEASARC data-products documentation](https://heasarc.gsfc.nasa.gov/docs/tess/data-products.html). The stale PLATO launch year was removed; [ESA's factsheet](https://www.esa.int/Science_Exploration/Space_Science/Plato_factsheet) provides mission status.
- Kaye et al. (2022) supports NGTS measurements of TOI-270 TTVs: [published paper](https://doi.org/10.1093/mnras/stab3483). Kaye (2022) and Leleu (2024) were attached to an orbital-decay claim; the text now correctly describes TTV monitoring. Chote (2021) is used for white-dwarf variability rather than transits/eclipses.
- SYSREM is credited to [Tamuz, Mazeh & Zucker (2005)](https://arxiv.org/abs/astro-ph/0502056), rather than solely to the later implementation proceedings.
- SEP background filtering uses a 3-by-3 array of background boxes, not a 3-pixel PSF-sized filter: [SEP Background API](https://sep.readthedocs.io/en/stable/api/sep.Background.html). Circular apertures are specified by radius: [sum_circle API](https://sep.readthedocs.io/en/stable/api/sep.sum_circle.html). Check the centroid-window definition against the [winpos API](https://sep.readthedocs.io/en/stable/api/sep.winpos.html).
- HJD_UTC and BJD_TDB now describe the reported time scales without the old physical-clock/Greenwich analogy: [Astropy time documentation](https://docs.astropy.org/en/stable/time/index.html).

Bibliographic spot checks used primary papers and official documentation; direct ADS access returned errors. This was not a new literature survey or a claim-by-claim scientific reanalysis.

## Verification

- British English dictionary pass, followed by manual review of astronomical terms, acronyms, proper names, and FITS identifiers.
- No missing citation keys, duplicate bibliography keys, duplicate active labels, or unresolved cross-references in the revised source.
- All original figure assets match their Git versions byte for byte; all 14 graphics-inclusion commands are unchanged.
- MNRAS proof compiles successfully with Tectonic, including BibTeX. The build has minor font/underfull-box and duplicate PDF-destination warnings, but no overfull boxes or unresolved citations/references. Rendered pages were inspected for clipping, overlap, table overflow, and missing glyphs.
- `output/pdf/Paper.bbl` is retained with the proof for convenient submission preparation. The proof remains an author-review draft while the explicit placeholders and queries above are unresolved.
