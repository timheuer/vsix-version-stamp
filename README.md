# vsix-version-stamp
This is meant to be used as a composite action step when developing Visual Studio Extensions using the pattern in the [VSIX Community](https://github.com/VsixCommunity/) cookbooks/samples.

## Usage
When you have your GitHub Action workflow for your VSIX extension you can add this composite action:

```yml
on: [push]
      
jobs:
  build:
    name: Build 
    runs-on: windows-2022
      
    steps:
    - uses: actions/checkout@v3

    - name: Setup .NET build dependencies
      uses: timheuer/bootstrap-dotnet@v1

    - name: Increment VSIX version
      id: vsix_version
      uses: ./.github/workflows/composite/vsixversion
      with:
        manifest-file: src\YourProjectLocation\source.extension.vsixmanifest
        vsix-token-source-file: src\YourProjectLocation\source.extension.cs
```

This will automatically increment the build portion (Major.Minor.Build) with the GitHub Actions run number.