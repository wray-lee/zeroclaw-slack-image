# zeroclaw-slack-image

[ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw) Debian image with the Slack channel compiled in.

The official images are built from the generated `dist` feature list in `Dockerfile.debian`, which does not
include `channel-slack`. This repo builds the same Dockerfile from the upstream release tag with that exact
feature list plus `channel-slack`, nothing else changed.

- Checks daily, builds only when upstream publishes a new release (or run it manually with a tag / `force`).
- Fails instead of pushing if the binary requires x86-64-v3+ or lacks Slack support.

```
ghcr.io/wray-lee/zeroclaw:debian-slack          # latest build
ghcr.io/wray-lee/zeroclaw:<tag>-debian-slack    # pinned, e.g. v0.8.5-debian-slack
```

Update on the host:

```bash
docker compose pull && docker compose up -d
```

Note: GitHub disables scheduled workflows after 60 days without repository activity; re-enable it in the
Actions tab or run it manually.
