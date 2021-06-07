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
