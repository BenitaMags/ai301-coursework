I am going to investigate issue #53, "PII scrubber fails to redact parenthesized US phone numbers."

I plan to reproduce the reported behavior using the provided test cases in `tests/unit/test_pii_scrubber.py`, compare the handling of dashed and parenthesized US phone number formats, and report what I observe in my environment.
