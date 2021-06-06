Example to setup a monorepo

Notes:
- https://github.com/actions/cache/
- https://github.com/actions/setup-go/
- https://github.com/actions/setup-node/
- https://docs.github.com/en/actions/guides/caching-dependencies-to-speed-up-workflows

Thoughts:
- There is a bit of duplicated settings because of configuring the cache
- `test` and `build` should be two different jobs.
  - Because something fails to pass the `tests` doesn't mean it fails to `build`.
  - They should both be dependant on the same cache.
  - This means they should have a dependant job that restores the cache or installs the dependencies.
  - If there is no dependant job, the `test` and `build` job will have a cache conflict, and return a `warning`. See Footnote #1.
  - This also means that `test` and `build` are both downloading dependencies at the same time.
- Nice to have: see if the failures happen during download.
  - Though this could be figured out if examining the steps.
- You decide what trade off you want.

Footnotes:

1.

> Unable to reserve cache with key Linux-yarn-d74ae37f06deec8f74b51f87387993c4d4b3d704e1c108f120805b6e6624dae8, another job may be creating this cache.