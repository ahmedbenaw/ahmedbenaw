# RESUME: OmniGlyph native Go port

Status on 2026-11-24: paused in the cloud session. Continue on Ben's Mac.

## Paused notes

- The cloud session could not reach the Mac. `list_computer_folders` returned 0 folders, checked twice.
- The Codex install and the port folder exist only on the Mac. Nothing from them has been read yet.
- Not installed in the cloud session, and run only on the Mac: Toolchain Operator, /tokeneconomizer:toolprune,
  /reverse-engineer-anything, /refactor-chain, /refactor-board, $goal (/Users/ben/.agents/skills/goal/SKILL.md).
- Reachable upstreams on 2026-11-24: pxpipe-go v0.1.0 to v0.4.20 (Go proxy), npm omniglyph 1.4.0
  (repo diegosouzapw/OmniGlyph).
- Nothing has been approved. Only Ben approves.

## How to move to a local Mac session

Option A, teleport. This keeps the cloud conversation. (Likely supported; check `claude --help`.)

1. On the Mac, run: `git clone https://github.com/ahmedbenaw/ahmedbenaw.git`
2. Run: `cd ahmedbenaw && git checkout claude/compassionate-gauss-jpsx1s`
3. Run: `claude --teleport` and pick this session.
4. Then open the Codex port folder from there.

Option B, fresh session. This always works.

1. Open a terminal in the Codex port folder and run `claude`. The desktop app also works:
   Claude Code, then new local session, then choose that folder.
2. Paste the prompt below, or tell it: "Read RESUME.md in ahmedbenaw and follow it."

## Rules (binding)

See RULES.md. In short:

- Only Ben approves.
- Plain words, no Mermaid, invented customer names only.
- Back up before each change. Add only, never remove.
- Save the rules as memories.
- Keep this file updated.
- Every self-audit searches the transcript from the first message.

## Steps

0. Validate every item below as found, missing or blocked. Update this file, then commit as backup point 0.
1. Audit, changing nothing:
   - Run Toolchain Operator, /tokeneconomizer:toolprune and /kaizen:kaizen on the Codex install.
   - Load $goal and set it to "Complete, stable, native Go release of OmniGlyph".
   - Report how Codex read "port everything to OmniGlyph in Go natively", and the percent done per feature (a to h).
2. Install and check the reference tools globally:
   - pxpipe:
     - `go install github.com/evan-choi/pxpipe-go/cmd/pxpipe@v0.4.20`
     - `pxpipe --version`
     - `go get github.com/evan-choi/pxpipe-go@v0.4.20`
     - `pxpipe claude --model opus`
     - `pxpipe Claude.app`
     - `PXPIPE_MODELS=gpt-5.6-sol pxpipe opencode --model openai/gpt-5.6-sol`
     - `PXPIPE_MODELS=gpt-5.6-sol pxpipe codex --model gpt-5.6-sol`
     - `pxpipe serve` and `pxpipe serve --port 8080`
     - `ANTHROPIC_BASE_URL=http://localhost:47821 claude`
     - Library: `pxpipe.NewHandler(pxpipe.HandlerOptions{})` served on 127.0.0.1:47821.
   - OmniGlyph:
     - `npx omniglyph` (proxy on 127.0.0.1:47821), then `ANTHROPIC_BASE_URL=http://127.0.0.1:47821 claude`
     - PowerShell: `$env:ANTHROPIC_BASE_URL = "http://127.0.0.1:47821"; claude`
     - Library: `renderTextToImages(text, { reflow: true })` and
       `transformAnthropicMessages({ body, model: "claude-fable-5" })`
     - `npx omniglyph export --include "*.ts" src/` and `cat big.log | npx omniglyph export --stdin`
     - Export output: `OmniGlyph-export-<hash>/` holding page-NNN.png, factsheet.txt, prompt.txt, manifest.json
     - `pnpm install && pnpm test`
     - `node benchmarks/billing-sweep/run.mjs --dry-run`
     - `pnpm exec tsx benchmarks/density-frontier/run.ts --dry-run`
     - Live runs need ANTHROPIC_API_KEY, OPENAI_API_KEY or GEMINI_API_KEY, or `--via-cli`.
       Ask Ben before any paid run.
3. Finish the native Go port in the folder Ben pointed to, continuing Codex's work:
   - Use /reverse-engineer-anything, /refactor-chain and /refactor-board.
   - Check both upstream licenses before copying code.
   - Features, each matching the TS version:
     - a. Proxy on 127.0.0.1:47821 with a port flag
     - b. Launchers for claude, Claude.app, opencode and codex, with model routing
     - c. 1-bit PNG text renderer with reflow
     - d. Request transform with gate, billing math and applied/reason
     - e. Export CLI with --include, --stdin and the 4-file output folder
     - f. Embeddable Go library
     - g. Support for macOS, Linux, Windows and PowerShell
     - h. Benchmark dry runs
   - One feature per commit, with a backup first and a Go test on OmniGlyph fixtures.
4. Gates:
   - `go vet ./...` and `go test ./...` green.
   - `pnpm test` green.
   - Export page count and token report match TS.
   - Benchmark tables match TS within a stated tolerance.
   - Proxy smoke test passes.
   - Self-audit per rule 6.
5. Release:
   - Push to github.com/ahmedbenaw/ahmedbenaw on a feature branch.
   - Tag a release candidate and open a draft PR. Ben approves and merges.
6. Weekly worker:
   - Toolchain Operator runs weekly on the Mac and reads `toolchain.lock`.
   - `toolchain.lock` lists every tool, skill, plugin and library, each with its original source repo.
   - For each entry: check upstream, back up, update the local copy, run the gates, then write a report.
   - The worker never removes a feature and never approves anything for Ben.
