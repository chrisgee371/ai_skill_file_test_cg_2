# Forbidden patterns

Do not do any of the following.

1. Guess joins or keys that are not supported by the source manifest or profile files.
2. Use `{{ source() }}` for models created in earlier stages of the same pipeline.
3. Reference prior canvas gems directly when continuing the same staged pipeline.
4. Collapse the whole pipeline into one giant query.
5. Discard `NULL` UTM values without explicit justification.
6. Compare page or campaign variants outside their valid overlap windows.
7. Ignore refunds when computing net value.
8. Over-engineer product hierarchy logic; this dataset only has four products.
9. Pretend chronology does not matter. Product launches and page variants are introduced over time.
10. Emit severity scores without a supporting metric trail.
