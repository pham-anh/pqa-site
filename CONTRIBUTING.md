# CONTRIBUTING

## Set up integrated content

The content of this site can be pulled from another repository. That repository must contain a `go.mod` file.

Add configuration similar to the following into `config/_default/module.toml`

```
  [[module.imports]]
    disable = false
    ignoreConfig = false
    ignoreImports = false
    path = "github.com/pham-anh/learn-lpic"
  [[module.imports.mounts]]
    source = "LPIC-1"
    target = "content/posts/lpic-1"
```

After that, run

```
hugo mod get -U
```

Then hugo will clone `github.com/pham-anh/learn-lpic`, which contains a directory named `LPIC-1`, and mount the `LPIC-1` into `content/posts/lpic-1`.

This means, when we go to the URI `posts/lpic-1/xxx`, we can see the content of the files `LPIC-1/xxx`. 


## Troubleshooting

### Cannot download integrated repository

```
$ hugo mod get -u github.com/pham-anh/learn-lpic
$ hugo server -p 1234
Error: module "github.com/pham-anh/learn-lpic" not found; either add it as a Hugo Module or store it in "/Users/quynhanhpham/github.com/pqa-site/themes".: module does not exist
```

This is because the current repo is not a hugo module. Let's make it hugo module

```
$ hugo mod init github.com/pham-anh/pqa-site
go: creating new go.mod: module github.com/pham-anh/pqa-site
go: to add module requirements and sums:
        go mod tidy
```

After that we can download the integrated repository

```
$ hugo mod get -u
go get: added github.com/pham-anh/learn-lpic v0.0.0-20210605215540-0a4a31c52ab8
hugo: collected modules in 670 ms
```