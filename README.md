# php-builds

Static PHP binaries built with [static-php-cli](https://github.com/crazywhalecc/static-php-cli), published as GitHub releases for use with [mise](https://mise.jdx.dev/).

Useful for PHP versions not published by [adwinying/php](https://github.com/adwinying/php) (e.g. **8.3.15**, 8.3.16).

## How to build a version

1. Go to **Actions** → **Build PHP** → **Run workflow**.
2. Enter the PHP version (e.g. `8.3.15`) and run.
3. Wait for the workflow to finish (builds can take 20–60 minutes per platform).
4. The release appears under **Releases** with tag `8.3.15` and assets per platform.

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

- **Tag:** `{version}` (e.g. `8.3.15`, no `v` prefix so mise finds it).
- **Assets:** `php-{version}-linux-x86_64.tar.gz`, `php-{version}-linux-aarch64.tar.gz`, `php-{version}-macos-aarch64.tar.gz` (macos-x86_64 not built; GitHub no longer provides macos-13 runners).

Same layout as adwinying/php so the mise github/ubi backend picks the right asset for your OS and arch.

## Version compatibility

Build success depends on [static-php-cli](https://github.com/crazywhalecc/static-php-cli) and its patches; not every PHP version builds.

- **Known to build:** `8.1.31`, `8.3.15` (all three platforms).
- **Often fail:** `7.4.33` (7.4 may be unsupported or require older tooling), `8.2.27`, `8.3.14`, `8.4.2` (patch/source issues). Prefer nearby versions that match [adwinying/php](https://github.com/adwinying/php) (e.g. 8.2.30, 8.3.30) or stick to versions that have built successfully for you.

## Known limitations

- **PHP 8.4.x on Linux:** The workflow skips both Linux jobs for PHP 8.4.x because a static-php-cli patch (`ffi_centos7_fix_O3_strncmp.patch`) fails to apply. You only get `macos-aarch64` for 8.4.x. Use **8.3.x** for full platform coverage (linux-x86_64, linux-aarch64, macos-aarch64).
