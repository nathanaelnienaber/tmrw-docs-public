Here’s **`env-config.md`**—ready to copy-paste:

```markdown
# Environment Configuration

## Who Should Read This
- Anyone running the project locally
- Anyone handling secrets or tokens

## Purpose
- Explain which environment variables are needed
- Keep secrets out of source control
- Make local setup repeatable for every developer

## DO
- Copy `.env.example` to `.env` for local work.
- Keep `.env` out of Git with `.gitignore`.
- Store real secrets in a secure vault or secret manager.
- Use `make` commands for quick service access in development.

## DO NOT
- Do not commit real secrets to the repo.
- Do not share `.env` files in public channels.
- Do not hard-code secret values in code.

### Example `.env`
```

MONGO\_URI=mongodb://localhost:27017/tmrw
MINIO\_ACCESS\_KEY=tmrw
MINIO\_SECRET\_KEY=supersecret

````

### CLI Access
```bash
make mongo   # open MongoDB shell
make minio   # open MinIO console
make gitea   # open Gitea (optional)
````

## Who Maintains This File

The **DevOps Team**. Reviewed whenever environment variables change.
