# bingenovel-sources

Personal, unofficial [BingeNovel](https://github.com/JamesVictorAlvarez/BingeNovel) Extension Repository. **Not affiliated with, endorsed by, reviewed by, or bundled with BingeNovel.** BingeNovel ships no default or recommended repository ([ADR-0007](https://github.com/JamesVictorAlvarez/BingeNovel/blob/main/docs/adr/0007-use-user-supplied-repositories-without-authorization-vetting.md)) — this repository exists purely so it can be added manually, the same way any third-party repository can.

No automated access to a Target Service in this repository has been authorized by that service. Adding a source here is a personal choice made at your own risk under each Target Service's own terms.

## Contents

- `repo/` — the signed, served repository (`index.min.json`, `repo.json`, `definitions/`). This is what a BingeNovel client fetches, from the `repo` branch.
- `test/fixtures/` — offline fixtures (real HTML captured from each Target Service) used to verify extraction with `bingenovel-repo test`, without hitting the network.

## Sources

| Source | Domain | Capabilities |
| --- | --- | --- |
| ReadNovelFull | readnovelfull.com | search, popular, latest, details |
| Novel Fire | novelfire.net | popular, details, chapters, chapter |

ReadNovelFull's novel-details page only embeds a partial (~30-chapter) static snapshot of its chapter list — the complete archive is served from an ajax endpoint keyed by a numeric novel ID that isn't obtainable through this engine's single-identifier calling convention. So `chapters`/`chapter` are intentionally left out of that definition rather than shipped half-working.

## Using this repository

Add it in BingeNovel as a third-party repository using this GitHub URL:

```
https://github.com/JamesVictorAlvarez/bingenovel-sources
```

## Maintaining

```sh
bingenovel-repo validate repo
bingenovel-repo verify repo
bingenovel-repo test --definition repo/definitions/<hash>.json --fixtures test/fixtures/<source>
bingenovel-repo sign --key <path-to-publisher.key> repo
```

`publisher.key` is not in this repository — keep it outside of source control, per `docs/extensions/authoring.md` in the BingeNovel repo.
