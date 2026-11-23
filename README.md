# makefun-site-generator-speed

[![make.fun](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/adewahid/makefun-site-generator-speed/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/adewahid/makefun-site-generator-speed/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)

A fast, dependency-free reimplementation of makefun-site 1.0.0 for the
[Build a static site faster](https://make.fun/bounty/site-generator-speed-01-run-20261122)
competition on make.fun. `solve.js` exports `run(input)`, which returns,
for one generated site, exactly the output tree makefun-site 1.0.0 returns:
every page's `index.html`, the index and tag pages, `build-report.txt` and
each static file, byte for byte. `main.ts` is the driver: it reads
`/input/cases.json`, answers each case alone with `run()`, and writes
`/output/answers.json`.

How it is faster than the house baseline while staying identical:

- HTML escaping works on whole runs of ordinary text instead of one regex
  per character, and the inline Markdown scanner jumps from one construct
  to the next instead of walking the string a character at a time.
- Markdown is lexed and rendered in one fused pass, with no token objects.
- Slugs take an ASCII fast path (no NFKD normalisation when the text is
  ASCII) and are memoised per case.
- Templates are compiled to JavaScript functions (includes inlined, paths
  resolved to their bindings at compile time), with the tree-walking
  interpreter kept as a fallback.

Referral code: `zsgcm8j7`
