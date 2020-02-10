# golang + js + wasm

**glowasm** -- strictly typed `syscall/js`. Like [flow](https://github.com/facebook/flow) but for Go.

## Features

+ **Strictly typed**. It's a wrapper around `syscall/js` that helps you to avoid runtime errors (you'll get them a lot with a raw `syscall/js`).
+ **Backward compatible**. Almost every type is a wrapper around `js.Value`. So, if something missed, you always can fallback to the classic `syscall/js` calls.
+ **Hand crafted**. It's hard to make usable autogeneration of WebAPI since Go is strictly typed language without union types. So we carefully transalted everything with applying Go best practices.
+ **Cleaned up**. The library provides only useful methods and attributes from WebAPI. No obsolete and deprecated methods, no experimental API that supported only by a few engines. Only what we really need right now.
+ **Almost the same API as in JS**. If you have a experience with [vanilla JS](https://stackoverflow.com/a/20435744), you almost learnt everything about the libray.
+ **But better**. WebAPI has a long history with incremental changes and spaces for unimplemented dreams. However, we can see the full picture to provide better experience and more namespaces.
+ **Documented**. Every method is documented to save your time and reduce googling.

## Installation

```bash
GOOS=js GOARCH=wasm go get github.com/life4/glowasm
```

If you're using VSCode, it's recommend to create in your project `.vscode/settings.json` file with the following content:

```json
{
    "go.toolsEnvVars": {
        "GOARCH": "wasm",
        "GOOS": "js",
    },
    "go.testEnvVars": {
        "GOARCH": "wasm",
        "GOOS": "js",
    },
}
```

## Examples

...

## Error handling

In the beautiful JS world anything at any time can be `null` or `undefined`. Check it when you're not sure:

```go
doc := glowasm.GetWindow().Document()
el := doc.Element("some-element-id")
if el.Type() == js.TypeNull {
    // handle error
}
```

## Missed API

If something is missed, use `syscall/js`-like methods (`Get`, `Set`, `Call` etc):

```go
doc := glowasm.GetWindow().Document()
el := doc.Element("some-element-id")
name = el.Get("name").String()
```
