[![](https://img.shields.io/github/release/cedrickring/golang-action.svg)](https://github.com/cedrickring/golang-action/releases/latest) [![Actions Status](https://wdp9fww0r9.execute-api.us-west-2.amazonaws.com/production/badge/cedrickring/golang-action)](https://wdp9fww0r9.execute-api.us-west-2.amazonaws.com/production/results/cedrickring/golang-action)
# Golang Action

This Action allows you to run Go commands with your code. It will automatically setup your workspace (`~/go/src/github.com/<your-name>/<repo>`) before the command is run.

## How to use

1. Add an Action
2. Enter "cedrickring/golang-action@1.3.0" (`cedrickring/golang-action/go1.10@1.3.0` for Golang 1.10, 1.11, 1.12, defaults to the latest golang version)
3. If your repo builds with `make` or `go build && go test`, that's all you need.  Otherwise, add a command in the args section like:
    ```bash
    go build -o my_executable main.go
    ```
    or run your `make` targets with
    ```bash
    make test
    ```

If your repository's `import` name is different from the path on GitHub,
provide the `import` name by adding an environment variable
`IMPORT=import/name`.  This may be useful if you have forked an open
source Go project.

If you prefer editing your `main.workflow` files by hand, use an `action`
block like this:

```hcl
action "ci" {
  uses="cedrickring/golang-action@1.3.0"

  # optional build command:
  args="./build.sh"

  # optional import name:
  env={
    IMPORT="root/repo"
  }
}
```

If your project's go is not located at the root of the repo you can also specifiy environment variable `PROJECT_PATH`:
```hcl
action "test_vendored" {
  uses="cedrickring/golang-action@1.3.0"
  # optional relative project path, default is root of repo e.g. "./":
  env={
    PROJECT_PATH = "./tests/projects/go_modules_vendored"
  }
}
```

To use a specific golang version (1.10, 1.11, 1.12):

```hcl
action "ci" {
  uses="cedrickring/golang-action/go1.12@1.3.0"
  ...
}
```
