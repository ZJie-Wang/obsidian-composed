# Publishing Paperpress

This guide covers the one-time GitHub setup, the first `1.0.0` release, and submission to the Obsidian community directory.

## Before publishing

The repository should contain these files at its root:

- `README.md`
- `LICENSE`
- `manifest.json`
- `theme.css`
- `screenshot.png`

The theme name is permanent after community submission. Confirm that `Paperpress` is the intended name before submitting.

## 1. Create the GitHub repository

On GitHub:

1. Select **New repository**.
2. Use `paperpress` as the repository name.
3. Set visibility to **Public**.
4. Do not initialize it with a README, license, or `.gitignore`; those files already exist locally.
5. Select **Create repository**.

From this repository’s local folder, connect and push it. Choose either SSH:

```sh
git remote add origin git@github.com:ZJie-Wang/paperpress.git
git push -u origin main
git push origin 1.0.0
```

or HTTPS:

```sh
git remote add origin https://github.com/ZJie-Wang/paperpress.git
git push -u origin main
git push origin 1.0.0
```

Confirm that GitHub shows the files on `main` and the `1.0.0` tag.

## 2. Create the 1.0.0 release

1. Open the repository on GitHub.
2. Select **Releases → Draft a new release**.
3. Choose the existing tag `1.0.0`.
4. Use `Paperpress 1.0.0` as the release title.
5. Add a short description, such as “Initial public release.”
6. Attach the root `manifest.json` and `theme.css` files as release assets.
7. Select **Publish release**.

The release tag must exactly match the version in `manifest.json`. The two attached files are required because Obsidian installs themes from GitHub release assets, not directly from the repository branch.

## 3. Submit to the Obsidian community directory

1. Sign in at [community.obsidian.md](https://community.obsidian.md/).
2. Link the GitHub account that owns the repository.
3. Select **Themes → New theme**.
4. Enter `https://github.com/ZJie-Wang/paperpress`.
5. Review and accept the developer policies.
6. Submit the theme and address any automated review feedback.

The directory reads `manifest.json` from the default branch. Keep `main` public and ensure its manifest matches the latest release.

## Optional: publish with GitHub CLI

If the `gh` command is installed and authenticated, the repository and release can instead be created from this folder with:

```sh
gh repo create ZJie-Wang/paperpress --public --source=. --remote=origin --push
git push origin 1.0.0
gh release create 1.0.0 manifest.json theme.css \
  --title "Paperpress 1.0.0" \
  --notes "Initial public release."
```

These commands create public resources, so inspect the repository state before running them.

## Future releases

For each update:

1. Increment `version` in `manifest.json` using semantic versioning.
2. Add the version and minimum supported Obsidian version to `versions.json`.
3. Update the version comment in `theme.css`.
4. Commit the changes and create a matching tag.
5. Push `main` and the tag.
6. Create a GitHub release and attach the updated `manifest.json` and `theme.css`.
