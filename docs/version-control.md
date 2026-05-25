# Version Control

Unreal projects need careful source control because they mix text files with large binary assets, generated folders, and engine-specific workflows.

## Why Unreal Projects Need Careful Source Control

Compared with many small Unity code-only projects, Unreal projects more quickly involve:

- binary assets such as `.uasset` and `.umap`
- large art files
- generated build outputs
- editor-only caches
- teams that need file locking for content work

That does not make Git wrong for Unreal. It just means you need to configure it properly.

## Git for Unreal Projects

Git works well for:

- solo development
- small teams
- open source repositories
- code-heavy projects

Git needs extra help for large binary assets, usually through Git LFS.

### What Should Be Committed

- `Config/`
- `Content/`
- `Source/`
- `.uproject`
- plugin source and content that belong to the project
- documentation and setup files

### What Should Not Be Committed

- `Binaries/`
- `DerivedDataCache/`
- `Intermediate/`
- `Saved/`
- IDE user files
- generated solution and cache files when they are not part of the chosen workflow

## Recommended `.gitignore`

Use a project-level `.gitignore` similar to this:

```gitignore
Binaries/
DerivedDataCache/
Intermediate/
Saved/
.vs/
*.sln
*.suo
*.user
*.opensdf
*.VC.db
```

You may also ignore editor-specific folders such as `.vscode/` depending on team preference.

## Recommended `.gitattributes`

Use Git LFS for Unreal binary assets and common large source art files:

```gitattributes
*.uasset filter=lfs diff=lfs merge=lfs -text
*.umap filter=lfs diff=lfs merge=lfs -text
*.fbx filter=lfs diff=lfs merge=lfs -text
*.wav filter=lfs diff=lfs merge=lfs -text
*.png filter=lfs diff=lfs merge=lfs -text
*.tga filter=lfs diff=lfs merge=lfs -text
```

Adjust this list to fit your content pipeline. Some teams keep all source art in LFS. Others only track the formats that grow quickly or need locking.

## Git LFS Setup

Install Git LFS, then track the file types you care about.

```text
git lfs install
git lfs track "*.uasset"
git lfs track "*.umap"
git lfs track "*.fbx"
git add .gitattributes
git commit -m "Configure Git LFS for Unreal assets"
```

If your team uses locking:

```text
git lfs lock Content/Maps/MainMenu.umap
git lfs unlock Content/Maps/MainMenu.umap
```

### Solo Developer Workflow

For solo work, Git plus LFS is usually enough if:

- the repository size stays manageable
- you are disciplined about ignores
- you keep binary churn under control

### Team Workflow

For teams, Git can still work well when:

- code reviews happen in GitHub or GitLab
- binary-heavy assets are in LFS
- artists lock files that cannot merge safely
- the team agrees on branching and asset ownership

## Perforce for Unreal Projects

Perforce is common in larger Unreal teams because it handles large binary assets and exclusive locks well.

It is especially attractive when:

- many people work on the same content depot
- binary assets change often
- large file storage is a constant concern
- the studio already has Perforce experience

## Example Perforce Typemap

Perforce typemaps help mark Unreal asset files as binary and lockable.

```text
binary+l //depot/Project/.../*.uasset
binary+l //depot/Project/.../*.umap
binary   //depot/Project/.../*.fbx
binary   //depot/Project/.../*.wav
text     //depot/Project/.../*.ini
text     //depot/Project/.../*.uproject
text     //depot/Project/.../*.uplugin
```

The `+l` flag means exclusive checkout locking.

## Git vs Perforce Comparison

| Feature | Git | Perforce |
|---|---|---|
| Best for code | Excellent | Excellent |
| Best for large binary assets | Requires Git LFS | Strong built-in support |
| File locking | Git LFS locking | Native locking |
| Common Unreal team usage | Small teams / open source | Larger studios |
| Offline local branching | Excellent | More limited |
| Centralised asset workflow | Possible, but less native | Strong |

## Unreal-Specific Source-Control Practices

- keep generated folders ignored
- decide early whether binary assets should require locking
- avoid renaming large sets of assets casually, because redirects and references can create churn
- submit or commit redirected asset cleanups intentionally
- keep `.ini` changes reviewed because they affect team-wide behavior
- coordinate map ownership on busy teams because `.umap` files do not merge well

## Common Mistakes

- committing `Intermediate/` or `Saved/`
- using Git without LFS on a binary-heavy project
- expecting `.uasset` files to merge like text files
- storing shared gameplay truth only in local unversioned config
- letting each team member invent different ignore rules
- forgetting that Unreal asset redirects should be cleaned up and committed deliberately

## Practical Recommendation

For most solo developers and small teams:

- use Git
- add a solid `.gitignore`
- use Git LFS for `.uasset`, `.umap`, and large source assets
- use locks for maps and other non-mergeable binary files

For larger content-heavy teams:

- evaluate Perforce early
- especially if many people touch the same maps, Blueprints, and art assets every day

## Related Pages

- [Assets and References](assets-and-references.md)
- [Editor Tools](editor-tools.md)
- [Glossary](glossary.md)
