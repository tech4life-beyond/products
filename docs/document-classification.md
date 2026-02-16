# Document classification policy

## Classes
- **Public**: safe for public release
- **Internal**: operational details for contributors (default)
- **Confidential**: sensitive terms (royalties, private partner terms), not for public repos

## Rule
Documents containing royalty splits, partner negotiation terms, or private legal terms MUST be marked Confidential and must not be stored in public repositories.

If a document must exist for workflow reasons, store a Public redacted version and keep the Confidential original in a private repository (e.g., `legal-private` / `finance-private`).
