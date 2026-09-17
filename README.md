# Public Neural Pleiotropy Figure Gallery

Static GitHub Pages gallery for the neural pleiotropy project's `figures/` tree.

## Directory model

```text
$ROOT/
├── figures/                    # analysis output; source of truth
├── codes/figure_gallery/       # gallery builder and update scripts
└── public_figure_gallery/      # generated website and Git repository
    ├── .git/
    ├── .nojekyll
    ├── index.html
    ├── gallery_index.json
    ├── static/
    └── images/
```

The builder copies the image files from `figures/` into
`public_figure_gallery/images/`, preserving the original directory tree. GitHub
Pages therefore serves the figures directly from the public repository.

## Browser features

- hierarchical folder navigation;
- breadcrumb and level-by-level folder selectors;
- child-folder cards;
- search and inferred tag filtering;
- current folder / subtree / whole-gallery search scope;
- pagination;
- click-to-enlarge and previous/next navigation.

## Update locally

```bash
export NEURAL_PLEIOTROPY_ROOT=/nfs/visu/workplace/yuhdua/projects/neural_pleiotropy
bash "$NEURAL_PLEIOTROPY_ROOT/codes/figure_gallery/run.sh"
```

This scans `figures/`, copies new or changed images, and rebuilds the static
website and `gallery_index.json`. Existing gallery-only images are preserved by
default.

## Update and publish

```bash
bash "$NEURAL_PLEIOTROPY_ROOT/codes/figure_gallery/run.sh" --publish
```

This also runs `git add -A`, creates a commit when files changed, and pushes the
current branch to the configured `origin` repository.

## Mirror deletions deliberately

```bash
bash "$NEURAL_PLEIOTROPY_ROOT/codes/figure_gallery/run.sh" --sync-delete
bash "$NEURAL_PLEIOTROPY_ROOT/codes/figure_gallery/run.sh" --sync-delete --publish
```

`--sync-delete` removes website image copies that no longer exist in the source
`figures/` tree. Without it, historical gallery images remain available.

## Local preview

```bash
cd "$NEURAL_PLEIOTROPY_ROOT/public_figure_gallery"
python -m http.server 8050
```

## Public repository

<https://github.com/sonia1maslova/neural-pleiotropy-figure-gallery>

## Safety

Before publishing, verify that figures, filenames, and annotations contain no
participant identifiers, protected information, credentials, or other material
that should not be public.
