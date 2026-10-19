# What JSONPath syntax is supported for the GitHub JSON Path Filter in CodeMie?

The GitHub JSON Path Filter supports two expression forms:

- **Existence check (plain path)**: Tests whether a field is present in the payload, regardless
  of its value. Example: `$.pull_request.draft`
- **Value comparison (filter predicate)**: Tests whether a field equals a specific value.
  Example: `$[?(@.pull_request.draft==false)]`

**Important limitations:**

- **Nested predicates inside a path never match.** The expression
  `$.pull_request[?(@.draft==false)]` looks valid but never matches GitHub payloads. Always
  use a root-level filter predicate: `$[?(@.pull_request.draft==false)]`.
- Expressions containing regex operations, arithmetic, or other complex constructs are rejected
  at save time with a validation error.
- Only simple path navigation and a single comparison predicate are supported. Complex
  multi-condition filter expressions are not allowed.
- A configured GitHub Webhook Secret is required whenever a JSON Path Filter is set. Without
  it, saving returns a validation error.

## Sources

- [Webhook](https://docs.codemie.ai/user-guide/tools_integrations/tools/webhook)
