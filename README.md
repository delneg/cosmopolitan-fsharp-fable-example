# Universal F# Fable JS executable

This repository shows how you can create F# Fable JS actually portable executables
using [cosmopolitan](https://github.com/jart/cosmopolitan) and the [QuickJS Javascript Engine](https://bellard.org/quickjs/), and [Fable itself](https://fable.io/).
[αcτµαlly pδrταblε εxεcµταblε](https://justine.lol/ape.html) is a binary can run natively
in many operative systems.

# For the impatient

Just run these commands to enjoy a portable F# Fable JS binary:

```
dotnet tool restore
dotnet fable
zip qjs.com Main.fs.js .args
./qjs.com
```


# Pre-requisite

You'll need **dotnet** version 6 or above installed.
You can [download it here](https://dotnet.microsoft.com/en-us/download)


# Getting Started

You need the quickjs universal binary `qjs.com`.
I included it in the repo but you can build it yourself with:

```bash
git clone https://github.com/jart/cosmopolitan
cd cosmopolitan
make -j8 o//third_party/quickjs/qjs.com
cp o//third_party/quickjs/qjs.com ..
```

Now you can build your Javascript file with your favorite Fable toolchain.
For example with `dotnet fable`:
```
dotnet fable
```

Now you need to add the Fable JS produced `Main.fs.js` to the `qjs.com` binary.
APE binaries are also zip archives and can access the files contained in theirselves.

You also need to add a `.args` file to set some command line arguments to pass
to quickjs. In our case we will pass the file name in the `/zip` directory,
which is a special path containing the files in the zip archive.

```
zip qjs.com Main.fs.js .args
```

Now you created your universal F# Fable JS binary, you can run in every major
operating system with no dependencies.

# Fast compile run loop

You don't need to zip a Javascript file to run it with quickjs.
You can just use `qjs.com` as a standalone Javascript runtime.

```
dotnet fable && ./qjs.com Main.fs.js
```
