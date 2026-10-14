# zeroclaw-slack-image

[ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw) Debian image with the Slack channel compiled in,
plus small local patches (`patches/`).

The official images are built from the generated `dist` feature list in `Dockerfile.debian`, which does not
include `channel-slack`. This repo builds the same Dockerfile from the upstream release tag with that exact
feature list plus `channel-slack`, after applying `patches/*.patch`.

## Patches

| Patch | Effect |
|---|---|
| `0001-ack-reactions-like-openclaw.patch` | In-progress ack is ⏳ on Slack (`hourglass_flowing_sand`) and a fixed 👀 on Telegram; the ack is withdrawn when the reply is done instead of being swapped for ✅ (failures still get ⚠️ where the channel supports it). Adds the missing Telegram `remove_reaction`. |

## Builds

- Daily check; builds when upstream publishes a new release or the patch set changes (tag includes a hash of
  `patches/`). Also on push to `patches/`, or manually with a tag / `force`.
- Fails instead of pushing if a patch no longer applies, the binary requires x86-64-v3+, Slack support or the
  patch is missing.

```
ghcr.io/wray-lee/zeroclaw:debian-slack                       # latest build
ghcr.io/wray-lee/zeroclaw:<tag>-debian-slack-<patchhash>     # pinned
```

Update on the host:

```bash
docker compose pull && docker compose up -d
```

Note: GitHub disables scheduled workflows after 60 days without repository activity; re-enable it in the
Actions tab or run it manually.
