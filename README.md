# HoneyBadger

Context-aware PII detection and de-identification for .NET. Fully offline, framework-agnostic,
no ML models required. Inspired by the architecture of [Microsoft Presidio](https://github.com/microsoft/presidio) (MIT).

## Features

- **Validated recognizers** - credit card (Luhn), IBAN (mod-97), crypto (base58/bech32), email,
  IP, URL, MAC, phone (libphonenumber). Always-on US pack (SSN, ITIN, routing, bank, driver
  license, passport, NPI, MBI, medical license) plus opt-in country packs (`uk`, `de`, `in`, `it`, `es`).
- **Confidence scoring** with lemma-aware context boosting (dependency-free Porter stemmer) and
  overlap/conflict resolution.
- **Anonymization operators** - replace, redact, mask, hash (salted SHA-256/512),
  encrypt/decrypt (reversible AES), keep, custom.
- **Reversible de-identification**, structured (JSON/CSV) redaction, and batch APIs.

## Quick start

```csharp
using HoneyBadger;

var engine = new PiiEngine();
var result = engine.Deidentify("Email me at jane@contoso.com or call +1 425 555 0100.");
Console.WriteLine(result.AnonymizedText); // Email me at <EMAIL_ADDRESS> or call <PHONE_NUMBER>.
```

See `THIRD_PARTY_NOTICES.txt` for attribution.

## Optional ONNX NER

The `HoneyBadger.Onnx` package adds offline, multilingual named-entity recognition
(PERSON / LOCATION / ORGANIZATION / DATE_TIME) via [Kyoto](https://github.com/filipw/kyoto)'s
GLiNER model, merged into the same analyzer/anonymizer pipeline.

## License

MIT
