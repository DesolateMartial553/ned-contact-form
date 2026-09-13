---
name: GitHub publishing
description: Project-specific constraint for publishing this Repl through its GitHub connector.
---

Use the authenticated GitHub connector API rather than assuming `git` or `gh` commands receive the connector credential. If Git transport authentication fails, publish tracked files through GitHub's Git Data API using base64-encoded blobs and SHA-only directory trees.

**Why:** The attached GitHub integrations reported healthy and API requests succeeded, but both `git` and `gh` lacked usable CLI authentication. Large inline tree requests also hit payload and content-inspection limits.

**How to apply:** For future source syncs, prefer normal Git only after a quick authentication check. Otherwise upload changed files as encoded blobs, assemble directory-sized trees, create a commit, and update `refs/heads/main`.