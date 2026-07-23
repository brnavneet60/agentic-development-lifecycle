---
name: deliver-output
description: >
  Render the harness output template and publish via configured deliverers
  (local markdown file, remote git path, or file server). Use when producing
  the final artifact or when the user asks to save/publish output.
---

# Deliver output

1. Read `config/harness.config.yaml` → `outputs`.
2. If `standards_path` is set, read and obey it before rendering.
3. Render `outputs.template` (or `outputs/templates/default.md`) with task data.
4. For each deliverer:
   - `local_file`: write to expanded `path`; create parent dirs.
   - `git_remote`: write file into a clone of `repo` at `path_in_repo`, commit with `commit_message` **only if the user explicitly asked to commit/push**.
   - `file_server`: HTTP `method` to `url` using header from env `auth_env` if set.
5. Print delivered paths/URLs. Never inline tokens in logs.
