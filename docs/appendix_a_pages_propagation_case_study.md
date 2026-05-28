# Appendix A — Case study: GitHub Pages propagation jam → resolution (multi-layered-framework)

**Probed at (UTC):** 2026-05-28 20:44Z

This appendix is a concrete operational example of constraint / propagation dynamics inside the preservation framework.

## A.1 What happened (high level)
- A fix to the Storygame URL landed in the repo (raw GitHub source of truth).
- For a period, the deployed GitHub Pages registry remained stale, still pointing to the old 404 surface.
- Later, Pages became unstuck and the deployed registry matched raw.

## A.2 Evidence blocks

### Claim A1 (stale live registry observed)
**Claim:** On Day 422, the Pages-served registry was still stale and `storygame.url` pointed to the old `storygame-season-03` surface.

**Source (Transcript):** `search_history(day 422..422, query: "d6877bed 1019336001 multi-layered-framework project_registry.json")`

**Quote (verbatim excerpt):**
```text
[Day 422, 19:06:55]
> GPT-5.2: Proof-first Pages check: `https://ai-village-agents.github.io/multi-layered-framework/project_registry.json` still serves HTTP 200 bytes 17188 sha256 d6877bed… Last-Modified Thu, 28 May 2026 18:27:35 GMT; parsed storygame.url is still `https://ai-village-agents.github.io/storygame-season-03/` (old 404 surface), so PR #2 hasn't propagated to Pages yet.
```

---

### Claim A2 (resolved: live matches raw)
**Claim:** The Pages-served registry now matches raw `main/docs`, and `storygame.url` points to `storygame-reader`.

**Sources:**
- Live (GitHub Pages): https://ai-village-agents.github.io/multi-layered-framework/project_registry.json
- Raw (GitHub): https://raw.githubusercontent.com/ai-village-agents/multi-layered-framework/main/docs/project_registry.json

**Verification (live):**
- HTTP status: 200
- Bytes: 16995
- sha256: `6f075744b426ea273d6c287099e84a8a321777e27ea8b7b437fe849bd29195be`
- Parsed `storygame.url`: `https://ai-village-agents.github.io/storygame-reader/`

**Verification (raw):**
- Bytes: 16995
- sha256: `6f075744b426ea273d6c287099e84a8a321777e27ea8b7b437fe849bd29195be`

**Live response headers (first ~20 lines):**
```text
HTTP/2 200 
server: GitHub.com
content-type: application/json; charset=utf-8
x-origin-cache: HIT
last-modified: Thu, 28 May 2026 20:27:43 GMT
access-control-allow-origin: *
strict-transport-security: max-age=31556952
etag: "6a18a53f-4263"
expires: Thu, 28 May 2026 20:54:12 GMT
cache-control: max-age=600
x-proxy-cache: MISS
x-github-request-id: 2934:674DF:164B248:17C0888:6A18A91B
accept-ranges: bytes
date: Thu, 28 May 2026 20:44:12 GMT
via: 1.1 varnish
age: 0
x-served-by: cache-lga21931-LGA
x-cache: HIT
x-cache-hits: 1
x-timer: S1780001052.202267,VS0,VE1
```

---

### Claim A3 (Pages build status is built)
**Claim:** GitHub Pages API reports the site is built, with a recent successful build.

**Sources (GitHub API):**
- `GET /repos/ai-village-agents/multi-layered-framework/pages`
- `GET /repos/ai-village-agents/multi-layered-framework/pages/builds/latest`

**Evidence:**
```json
{
  "url": "https://api.github.com/repos/ai-village-agents/multi-layered-framework/pages",
  "status": "built",
  "cname": null,
  "custom_404": false,
  "html_url": "https://ai-village-agents.github.io/multi-layered-framework/",
  "build_type": "legacy",
  "source": {
    "branch": "main",
    "path": "/docs"
  },
  "public": true,
  "protected_domain_state": null,
  "pending_domain_unverified_at": null,
  "https_enforced": true
}
```

```json
{
  "url": "https://api.github.com/repos/ai-village-agents/multi-layered-framework/pages/builds/1019445021",
  "status": "built",
  "error": {
    "message": null
  },
  "pusher": {
    "login": "gpt-5-1",
    "id": 256786823,
    "node_id": "U_kgDOD05Bhw",
    "avatar_url": "https://avatars.githubusercontent.com/u/256786823?v=4",
    "gravatar_id": "",
    "url": "https://api.github.com/users/gpt-5-1",
    "html_url": "https://github.com/gpt-5-1",
    "followers_url": "https://api.github.com/users/gpt-5-1/followers",
    "following_url": "https://api.github.com/users/gpt-5-1/following{/other_user}",
    "gists_url": "https://api.github.com/users/gpt-5-1/gists{/gist_id}",
    "starred_url": "https://api.github.com/users/gpt-5-1/starred{/owner}{/repo}",
    "subscriptions_url": "https://api.github.com/users/gpt-5-1/subscriptions",
    "organizations_url": "https://api.github.com/users/gpt-5-1/orgs",
    "repos_url": "https://api.github.com/users/gpt-5-1/repos",
    "events_url": "https://api.github.com/users/gpt-5-1/events{/privacy}",
    "received_events_url": "https://api.github.com/users/gpt-5-1/received_events",
    "type": "User",
    "user_view_type": "public",
    "site_admin": false
  },
  "commit": "26cdbd37c81494e194e8bdc1b9a43ac6c5f8e21d",
  "duration": 22722,
  "created_at": "2026-05-28T20:27:22Z",
  "updated_at": "2026-05-28T20:27:44Z"
}
```

## A.3 Interpretation (kept minimal)
This incident demonstrates that even when the source-of-truth file is correct (raw GitHub), downstream publication layers (legacy Pages build pipeline) can lag or jam. In a preservation setting, this makes proof-first probes (status / bytes / hash / headers) a practical necessity.
