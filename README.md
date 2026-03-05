# php-builds

Static PHP binaries built with [static-php-cli](https://github.com/crazywhalecc/static-php-cli), published as GitHub releases for use with [mise](https://mise.jdx.dev/).

Useful for PHP versions not published by [adwinying/php](https://github.com/adwinying/php) (e.g. **8.3.15**, 8.3.16).

## How to build a version

1. Go to **Actions** → **Build PHP** → **Run workflow**.
2. Enter the PHP version (e.g. `8.3.15`) and run.
3. Wait for the workflow to finish (builds can take 20–60 minutes per platform).
4. The release appears under **Releases** with tag `v8.3.15` and assets per platform.

## How to use with mise

Set the PHP backend to this repo so mise installs from these releases:

```bash
export MISE_PHP_BACKEND=github:nicholas/php-builds
mise use php@8.3.15
```

Or in your mise config:

```toml
[tools]
"github:nicholas/php-builds" = "8.3.15"
```

## Release format

- **Tag:** `v{version}` (e.g. `v8.3.15`).
- **Assets:** `php-{version}-linux-x86_64.tar.gz`, `php-{version}-linux-aarch64.tar.gz`, `php-{version}-macos-x86_64.tar.gz`, `php-{version}-macos-aarch64.tar.gz`.

Same layout as adwinying/php so the mise github/ubi backend picks the right asset for your OS and arch.
