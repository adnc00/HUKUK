# HUKUK: Turkish Statutory Compliance for Claude Code

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Built for Claude Code](https://img.shields.io/badge/Built%20for-Claude%20Code-D97757)](https://claude.com/claude-code)
[![Jurisdiction: Türkiye](https://img.shields.io/badge/Jurisdiction-T%C3%BCrkiye-E30A17)](https://www.mevzuat.gov.tr)

**A Claude Code skill for Turkish legal and compliance questions. It answers from
the official statute texts and cites the article, instead of relying on what the
model remembers.**

It bundles 40 official Turkish laws, regulations and communiqués covering consumer
and e-commerce rules, KVKK secondary rules, labour, competition, procedure,
criminal and tax law. A `SKILL.md` tells Claude how to find the governing text,
read it, cite the exact article and turn it into a compliance checklist.

> **Coverage note:** 6098 TBK, 6102 TTK, 6698 KVKK (the law itself), 6563 ETK and
> 6493 are not bundled yet. For those, the skill tells Claude to say so and point
> to mevzuat.gov.tr rather than quote from memory.

## Why this matters

- **Turkish law is underserved.** Most AI legal tooling targets US and EU law.
  Turkish statutes are scattered across `.doc` and `.pdf` files that are awkward to
  process programmatically.
- **Recall isn't citation.** Models paraphrase Turkish statutes from memory and get
  article numbers or amendments wrong. This skill instructs Claude to read the
  primary text and quote it (e.g. *6502 s. TKHK m. 48/4*, the 14-day right of
  withdrawal).
- **Compliance is a developer problem.** Teams building e-commerce, fintech or SaaS
  for Türkiye need distance-sales, consumer, commercial e-message and data rules
  checked against their product. This puts that check in the same terminal where
  the code is written.

## Install

```bash
git clone https://github.com/adnc00/HUKUK.git ~/.claude/skills/hukuk
```

On Windows (PowerShell):

```powershell
git clone https://github.com/adnc00/HUKUK.git "$HOME\.claude\skills\hukuk"
```

Restart Claude Code. Claude picks up the skill when a question involves Turkish law,
or you can call it directly with `/hukuk`.

**Requirements:** `pdftotext` (Poppler) for the PDFs, and `antiword` or LibreOffice
(`soffice`) for the `.doc` files. Without one of them, the 22 `.doc` texts can't be
read. Git for Windows already ships `pdftotext` and `antiword`.

## Usage examples

```text
> Review our checkout against Mesafeli Sözleşmeler Yönetmeliği: pre-contract
  information, right of withdrawal, refund deadline. Cite the articles.

> We want to send SMS campaigns to existing customers. What does the Ticari
  İletişim ve Ticari Elektronik İletiler Yönetmeliği require for consent and opt-out?

> A customer asked us to delete their personal data. What do the KVKK deletion
  regulation and the Veri Sorumlusuna Başvuru Tebliği require, and by when?

> Bir işçiyi geçerli neden olmadan feshedersek 4857 sayılı Kanun'a göre
  sonuçları nelerdir? Madde numaralarıyla açıkla.
```

A typical answer lists the governing texts and the cited articles with short quotes.
It adds an obligations checklist (what, who, when), the sanction articles, and a
note to confirm the current version on mevzuat.gov.tr.

## Repository layout

```text
HUKUK/
├── SKILL.md         # Skill definition: workflow, citation rules, index of texts
├── README.md
├── LICENSE          # MIT (applies to the original files in this repo)
├── .gitignore
├── .gitattributes
└── *.doc|*.pdf|*.txt   # Official Turkish statutes, regulations, communiqués
```

| Area | Examples |
|---|---|
| Consumer & e-commerce | 6502 TKHK, Distance Contracts Regulation, Commercial Advertising Regulation, Commercial E-Messages Regulation |
| Data protection | KVKK regulations and communiqués on the controller registry, data subject applications, deletion and anonymisation |
| Labour | 4857 Labour Law, 6331 Occupational Health & Safety, 5510 Social Security, 7036 Labour Courts |
| Competition | 4054 Competition Law, Mergers communiqué 2010/4, Vertical Agreements block exemption 2002/2 |
| Procedure & enforcement | 6100 HMK, 2004 İİK, 6325 Mediation, 7201 Notification |
| Tax | 213 VUK, 193 GVK, 5520 Corporate Tax, 3065 VAT, 488 Stamp Tax, 492 Fees |

The full index is in [`SKILL.md`](SKILL.md).

## Roadmap

- [ ] Add the core laws still missing: 6098 TBK, 6102 TTK, 6698 KVKK, 6563 ETK, 6493 Payments Law
- [ ] Convert the remaining `.doc` files to UTF-8 `.txt` so no converter is needed
- [ ] Article-level index (law → article → file offset) for faster lookups
- [ ] A script that checks each text against mevzuat.gov.tr and flags amendments
- [ ] Ready-made compliance checklists (KVKK, e-commerce, e-messages)

## Contributing

Issues and pull requests are welcome, especially new official texts and
up-to-date versions of existing ones.

- Add **only official texts**: laws, regulations and communiqués as published in
  the Official Gazette or on mevzuat.gov.tr. Textbooks, commentaries, lecture notes
  and paid database exports are copyrighted and will be rejected.
- Name files `<law number> <official title>.<ext>` and add the text to the index
  in `SKILL.md`.
- PDFs are git-ignored by default; add a `!` line to `.gitignore` for a new official PDF.

## Licensing and disclaimer

The original work in this repository (`SKILL.md`, `README.md` and the configuration
files) is released under the [MIT License](LICENSE). The bundled texts are official
Turkish legislation without third-party commentary. Under Article 31 of Law No.
5846 (FSEK), officially published laws, Presidential decrees, regulations,
communiqués, circulars and court decisions may be freely reproduced, distributed
and used.

This project provides legal information, not legal advice. The bundled texts are
snapshots and may be out of date. Always confirm the current text on
[mevzuat.gov.tr](https://www.mevzuat.gov.tr) and consult a licensed Turkish
attorney for decisions with legal consequences.
