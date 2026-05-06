# capstone-radar

**This skill has moved.** It now lives inside [radar-suite](https://github.com/Terryc21/radar-suite), a bundle of six audit skills for iOS/macOS Swift apps. Installing the bundle is the intended experience because the skills work together: they share findings, update each other's reports, and feed into a unified ship-or-don't-ship grade.

## What `capstone-radar` does

It's the final step in a radar-suite audit. After the other five radar skills finish their scans, capstone-radar gathers their findings, runs five checks of its own, and writes a single A-F report grouped into "Fix Before Shipping" (release-blocking issues) and "Hygiene Backlog" (everything else, doesn't affect the grade). Tracks velocity over time and celebrates fixes between runs.

## How to install (via radar-suite)

Two commands in Claude Code, run one at a time:

```
/plugin marketplace add Terryc21/radar-suite
```

```
/plugin install radar-suite@radar-suite
```

That's it. capstone-radar is now available as `/capstone-radar`, along with the other five audit skills.

## Why the standalone repo still exists

So that anyone who finds this URL through an old link, blog post, or cached search result lands on a clear pointer to the current home. Old `git clone` commands against this repo still work; they just clone a near-empty redirect.

## Other Claude Code skills I've built

- [radar-suite](https://github.com/Terryc21/radar-suite) — the bundle this skill lives inside now
- [code-smarter](https://github.com/Terryc21/code-smarter) — annotated tutorials from your own codebase
- [prompter](https://github.com/Terryc21/prompter) — rewrites prompts for clarity before Claude acts
- [bug-echo](https://github.com/Terryc21/bug-echo) — finds sibling bugs after a fix
- [bug-prospector](https://github.com/Terryc21/bug-prospector) — finds bugs in code that compiles fine but breaks on real-world input
- [workflow-audit](https://github.com/Terryc21/workflow-audit) — 5-layer audit of SwiftUI user flows

All free, all Apache 2.0, all built while shipping [Stuffolio](https://stuffolio.app).

## License

Apache 2.0. See [LICENSE](LICENSE) and [NOTICE](NOTICE).

## Author

Terry Nyberg, [Coffee & Code LLC](https://stuffolio.app/).
