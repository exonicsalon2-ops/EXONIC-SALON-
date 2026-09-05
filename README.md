name: Build Desktop App

on:
  push:
    branches: [ "main" ]

jobs:
  build:
    runs-on: windows-2019

    steps:
    - uses: actions/checkout@v3

    - name: Setup MSBuild
      uses: microsoft/setup-msbuild@v1.3.1

    - name: Setup NuGet
      uses: NuGet/setup-nuget@v1.2.0

    - name: Restore NuGet packages
      run: nuget restore ClientVisitManager.csproj

    - name: Build Application
      run: msbuild ClientVisitManager.csproj /p:Configuration=Release /p:OutputPath=bin\Release\

    - name: Upload Executable
      uses: actions/upload-artifact@v3
      with:
        name: ExonicSalonApp
        path: bin/Release/
