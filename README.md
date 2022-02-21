# LRU cache

The standard implemenation of LRU cache (hash table + doubly-linked list). 
All operations are in time complexity of O(1).
This implementation is *not* thread-safe.

## Installation

```
$ nimble install lrucache
```

## API

See [api docs](https://status-im.github.io/lrucache.nim)

## Usage

```nim
# create a new LRU cache with initial capacity of 1 items
let cache = newLRUCache[int, string](1) 

cache[1] = "a"
cache[2] = "b"

# key 1 is not in cache, because key 1 is eldest and capacity is only 1
assert: 1 notin cache 
assert: 2 in cache

# increase capacity and add key 1 
cache.capacity = 2 
cache[1] = "a"
assert: 1 in cache
assert: 2 in cache

# update recentness of key 2 and add key 3, then key 1 will be discarded.
echo cache[2]
cache[3] = "c"
assert: 1 notin cache
assert: 2 in cache
assert: 3 in cache
```

## lrucache devs - create a release
Put a personal access token named `GITHUB_TOKEN` in your environment [with `repo` access](https://github.com/settings/tokens/new?scopes=repo&description=release-it). You can then release interactively using `nimble release`. This will provide options for creating a release commit, a tag, and a github release, and handle the push for you. You can also achieve this non-interactively with `nimble release_patch`, `nimble release_minor`, or `nimble release_major`.
NOTE: if a `GITHUB_TOKEN` is not in your environment, but you have a git user configured for the current working directory with enough permissions for the repository, then likely the commit and tag push will work, but the release creation will fail.
```bash
# Launch interactive release process
nimble release
# Launch non-interactive release process for patch release
nimble release_patch
# Launch non-interactive release process for minor release
nimble release_minor
# Launch non-interactive release process for major release
nimble release_major
```
