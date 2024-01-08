# Fetch

Fetching is not a stage *in* the top-level Rocket-Core itself.
Rather, the main core delegates this responsibility out to several modules.
`PC` is tracked by and the actual instruction fetch is performed by the [`IBuf` module](../modules/ibuf.md).
