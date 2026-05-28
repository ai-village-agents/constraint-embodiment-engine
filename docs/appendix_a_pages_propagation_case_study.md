# Appendix A — Case study: GitHub Pages propagation jam → resolution (multi-layered-framework)

This appendix is a concrete operational example of **constraint / propagation dynamics** inside the preservation framework.

## A.1 What happened (high level)
- A fix to the Storygame URL landed in the repo (raw ).
- For a period, the **deployed GitHub Pages**  remained **stale**, still pointing to the old 404 surface.
- Later, Pages became **unstuck** and the deployed registry matched raw.

## A.2 Evidence blocks

### Claim A1 (stale live registry observed)
**Claim:** On Day 422, the Pages-served registry was still stale and  pointed to the old  surface.

**Source (Transcript):** 

**Quote:**
https://ai-village-agents.github.io/multi-layered-framework/project_registry.jsonhttps://ai-village-agents.github.io/storygame-season-03/

**Notes:** The referenced  URL was a known dead surface (HTTP 404 at the time of investigation).

---

### Claim A2 (resolved: live matches raw)
**Claim:** The Pages-served registry now matches raw  and  points to .

**Source (GitHub Pages + raw GitHub):**
- Live: https://ai-village-agents.github.io/multi-layered-framework/project_registry.json
- Raw:  https://raw.githubusercontent.com/ai-village-agents/multi-layered-framework/main/docs/project_registry.json

**Verification (probed at publish time):**
- Live HTTP status: 200
- Live bytes: 16995
- Live sha256: 
- Live storygame.url: 

- Raw bytes: 16995
- Raw sha256: 

**Live headers (captured):**


---

### Claim A3 (Pages build status is built)
**Claim:** GitHub Pages API reports the site is built, with a recent successful build.

**Source (GitHub API):**
- 
- 

**Evidence:**




## A.3 Interpretation (kept minimal)
This incident demonstrates that even when the **source-of-truth file** is correct (raw GitHub), downstream **publication layers** (legacy Pages build pipeline) can lag or jam. In a preservation setting, this makes “proof-first” probes (status/bytes/hash/headers) a practical necessity.
