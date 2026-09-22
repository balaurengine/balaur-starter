# balaur-starter

A minimal [Balaur](https://balaurengine.org) project: a character, a floor, a
camera that follows. Three files and no assets.

It exists to be **built by something else**. It is the repository
[Forge](https://forge.balaurengine.org) points at for its first real build, and
the one to reach for when you want to know whether a toolchain works rather
than whether a game is fun. A starter that needed art or a plugin would answer
a different question.

```
project.toml        name, input actions, export settings
scenes/main.toml    the scene: ground, player, camera
scripts/player.rn   left, right, jump
```

## Run it

```sh
balaur run .
```

`A` and `D` move, `Space` jumps. A gamepad works too — the actions in
`project.toml` bind both.

## Export it

A pack, which is the project compiled but not yet wrapped in a runtime:

```sh
balaur export . --output game.balaur
```

A standalone game for one platform, which needs that platform's runtime
template:

```sh
balaur export . --target linux-x64 --output game
```

`--target` takes `linux-x64`, `linux-arm64`, `macos-universal`, `windows-x64`,
`windows-arm64`, `ios`, `android` or `web`. The desktop targets produce a
single executable; `ios`, `android` and `web` produce a directory.

## Build it on Forge

Register the repository, then start a build:

```sh
curl -X POST https://forge.balaurengine.org/api/v1/forge/projects \
  -H "Authorization: Bearer $FORGE_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
        "name": "balaur-starter",
        "repo_url": "https://github.com/balaurengine/balaur-starter",
        "targets": ["linux-x64", "windows-x64"]
      }'
```

Forge clones this repository on its runner and mounts the checkout read-only
into a sandbox that has no network, so nothing here is fetched at build time —
which is also why the project has no dependencies to fetch.

## Licence

MIT. Copy it, rename it, delete the parts you do not want.
