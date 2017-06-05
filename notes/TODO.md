# TODO

- [ ] Kondadadi, R., Howald, B., & Schilder, F. (2013, August). A Statistical NLG Framework for Aggregated Planning and Realization. In ACL (1) (pp. 1406-1415).

## 2017-05-11

- [ ] Check for scenarios (German?)
	- [x] wetter.de
	- [x] ~~wetteronline.de~~ – nur Texte, keine Daten
	- [x] wetter.com
	- [x] DWD – Trennung von manuell und automatisch generierten Texten?
	- [x] wetterdienst.de – Rückfrage Daten
	- [x] ZAMG (Ö)
	- [x] MeteoSchweiz (CH) – Rückfragen
	- [x] **meteoblue** (CH)
		- Aggregation nach Tag *und* Region möglich?
	- [ ] MeteoGroup?
- [ ] Try out alignment model (Liang 2009)
- [ ] Try out single features with `scikit-learn`/`SciPy`

## Research

* [ ] discourse treebank (Stent and Molina, 2009), e.g. PDTB
* [ ] Discourse Combinatory Categorial Grammar (Nakatsu & White, 2010)
* [ ] methods to automatically align input data with output text
	* Currently, there are a number of data-text corpora in specific domains, notably weather forecasting (Reiter et al., 2005; Belz, 2008; Liang et al., 2009) and sports summaries (Barzilay & Lapata, 2005; Chen & Mooney, 2008). These usually consist of database records paired with free text. **A promising recent trend is the introduction of statistical techniques that seek to automatically segment and align such data and text (e.g., Barzilay & Lapata, 2005; Liang et al., 2009; Konstas & Lapata, 2013).** (Gatt/Krahmer 2017: 30)