# go-nextver
CLI tool designed to analyze a Go module and opine on the next semantic version:

This is a **PROOF-OF-CONCEPT** and its code will probably be rolled into [**Squire**](https://github.com/mikeschinkel/squire) once it matures, and at that point I may delete this repo.  

Feel free to use it for your own needs in the interim, however.

## Example Output

Running this command _(on my local machine):_

```shell
nextver ~/Projects/go-pkgs/go-dt
```
Produced this output at the time of this writing _(the output will change as the project matures):_

```txt
Nextver Go Module Analysis
Local repo: ~/Projects/go-pkgs/go-dt
Cache: ~/Library/Caches/repos/go-dt-a1acdd1a112c4380
HEAD: f2730697b9915cbca4be0c3f9cb43a15e81e77b8
Working tree: dirty (analysis uses cached checkout of HEAD)

Baseline
- Latest reachable semver tag: v0.4.0

Review Signals (tests; informational)
- Tests added:
  - dir_path_test.go (+954/-0)
  - dtx/slices_test.go (+160/-0)
  - entry_path_test.go (+97/-0)
  - test/fuzz_tilde_dir_path_test.go (+76/-0)
  - tilde_dir_path_test.go (+67/-0)
- Tests removed:
  - segments_test.go (+103/-0)
  - test/dirpath_test.go (+6/-0)
- Summary: 5 added, 2 removed, 0 modified

API Changes
- github.com/mikeschinkel/go-dt
  - Breaking:
    - field DirEntry.Rel: changed from EntryPath to RelPath
    - func NewDirEntry(): changed from func(DirPath, *bool) DirEntry to func(DirPath, io/fs.DirEntry) DirEntry
    - method DirEntry.Filename(): changed from func() Filename to func() Filename (underlying type changed from struct{Root DirPath; Rel EntryPath; Entry io/fs.DirEntry; skipDir *bool} to struct{Root DirPath; Rel RelPath; Entry io/fs.DirEntry; skipDir *bool})
    - method EntryPath.Lstat(): changed from func() (os.FileInfo, error) to func(...io/fs.FS) (os.FileInfo, error)
    - var ErrFileDoesNotExist: removed
    - var ErrNotADirectory: removed
  - Non-breaking:
    - func DirPathRead(): added
    - func NewDirEntryWithSkipDir(): added
    - func ParseTildeDirPath(): added
    - func ParseURLSegment(): added
    - interface Config: added
    - method DirEntry.EntryPath(): added
    - method DirEntry.Ext(): added
    - method DirEntry.Filepath(): added
    - method DirPath.EvalSymlinks(): added
    - method DirPath.Expand(): added
    - method DirPath.Lstat(): added
    - method DirPath.Normalize(): added
    - method DirPath.ToLower(): added
    - method DirPath.ToSlash(): added
    - method DirPath.ToTilde(): added
    - method DirPath.ToUpper(): added
    - method EntryPath.Clean(): added
    - method EntryPath.EvalSymlinks(): added
    - method EntryPath.Expand(): added
    - method EntryPath.IsAbs(): added
    - method EntryPath.IsFile(): added
    - method Filepath.EvalSymlinks(): added
    - method Filepath.Expand(): added
    - method PathSegment.Contains(): added
    - method PathSegment.Exists(): added
    - method PathSegment.HasDotDotPrefix(): added
    - method PathSegment.MkdirAll(): added
    - method PathSegment.Status(): added
    - method PathSegment.TrimPrefix(): added
    - method PathSegment.TrimSuffix(): added
    - method PathSegment.WriteFile(): added
    - method PathSegments.Contains(): added
    - method PathSegments.HasPrefix(): added
    - method PathSegments.HasSuffix(): added
    - method PathSegments.ToLower(): added
    - method PathSegments.ToSlash(): added
    - method PathSegments.ToUpper(): added
    - method PathSegments.TrimPrefix(): added
    - method PathSegments.TrimSuffix(): added
    - type RelPath: added
    - type TildeDirPath: added
    - var ErrAccessingCLIConfigDir: added
    - var ErrAccessingUserCacheDir: added
    - var ErrAccessingUserConfigDir: added
    - var ErrAccessingUserHomeDir: added
    - var ErrAccessingWorkingDir: added
    - var ErrFileNotExists: added
    - var ErrInvalidPathSeparator: added
    - var ErrNotDirectory: added
    - var ErrNotTildePath: added

Verdict
- Opinion: breaking (high confidence)
- Suggested next version:
  - Breaking version: v0.5.0
  - Compatible: n/a (breaking files present)

Notes
- This tool analyzes exported API only; it ignores function bodies and behavioral inference.
- Analysis compares the latest reachable semver tag vs current HEAD (not the working tree) using a cached local checkout.
```
