# APITestFramework

[Purgomalum](https://www.purgomalum.com/) is a simple, free RESTful web service for filtering and removing content of profanity, obscenity and other unwanted text.

This is a test automation framework written against it.

##### Resources

- [SpecFlow Project Template with dotnet new](https://specflow.org/blog/specflow-project-template-with-dotnet-new/)
- [SpecFlow context injection](https://docs.specflow.org/projects/specflow/en/latest/Bindings/Context-Injection.html)
- [RestSharp](https://restsharp.dev/)

### Getting started

- [Install Docker](https://www.docker.com/products/docker-desktop)
- [Install .Net Core SDK](https://dotnet.microsoft.com/download)
- [Clone this repositiry to your machine](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository)

### Run tests

#### Terminal/CMD

- Mac: [Open the Terminal app](https://www.howtogeek.com/682770/how-to-open-the-terminal-on-a-mac/) and [navigate to the repository folder](https://www.macworld.com/article/2042378/master-the-command-line-navigating-files-and-folders.html)
- Windows: [Open command prompt in repository folder](https://helpdeskgeek.com/how-to/open-command-prompt-folder-windows-explorer/)
- Execute the below commands

#### Run the tests on your machine OR...

```bash
cd src/Purgomalum.Test
dotnet test
```

#### ...in [Docker](https://www.docker.com/)

Create image containing compiled test code and run it.

```bash
docker build -t test-complied-box:1.0 .
docker run --rm test-complied-box:1.0
```

Run code from a volume - used in debug.

```bash
docker run --rm -v ${PWD}/src:/src --entrypoint="dotnet" -it mcr.microsoft.com/dotnet/core/sdk:3.1 test /src --filter Category=sweary
```

#### [To run with filters]("https://docs.microsoft.com/en-us/dotnet/core/testing/selective-unit-tests")

- Has tag: ```dotnet test --filter Category=sweary```
- Does not have tag: ```dotnet test --filter Category!=sweary```
- Feature: ```dotnet test --filter FeatureTitle=Find_Profanity```
- Scenario: ```dotnet test --filter Description=Profanity_Found```
- Combinations: ```dotnet test --filter "FeatureTitle=Find_Profanity&Description=Profanity_Found"```

#### Expected output

```bash
-> Using default config
Test run for /APITestFramework/src/bin/Debug/netcoreapp3.1/APITestFramwwork.dll(.NETCoreApp,Version=v3.1)
Microsoft (R) Test Execution Command Line Tool Version 16.6.0
Copyright (c) Microsoft Corporation.  All rights reserved.

Starting test execution, please wait...

A total of 1 test files matched the specified pattern.
-> Loading plugin /APITestFramework/src/bin/Debug/netcoreapp3.1/TechTalk.SpecFlow.xUnit.SpecFlowPlugin.dll
-> Using default config

Test Run Successful.
Total tests: 16
     Passed: 16
 Total time: 4.1265 Seconds
 ```

### [Visual Studio Code](https://code.visualstudio.com/)

Dotnet core tests can be debugged and run from VS code.

Required extensions:

- [.Net Core Test Explorer](https://marketplace.visualstudio.com/items?itemName=formulahendry.dotnet-test-explorer)
- [C#](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)
- [Cucumber (Gherkin) Full Support](https://marketplace.visualstudio.com/items?itemName=alexkrechik.cucumberautocomplete)
- [Specflow Tools](https://marketplace.visualstudio.com/items?itemName=amillard98.specflow-tools)

Include the below setting in .vscode/settings.json

```json
"dotnet-test-explorer.testProjectPath" : "./src"
 ```

### Troubleshooting

###### Mac MSBuild error

- Issue: The below error when building the project

 ```bash
error MSB4018: The "GenerateFeatureFileCodeBehindTask" task failed unexpectedly.
 ```

- Fix: Run the below in Terminal to set environmental variable

 ```bash
export MSBUILDSINGLELOADCONTEXT=1
 ```

- Issue: cannot install dotnet executable on M1 machine
- Fix:

 ```bash
sudo ln -s /usr/local/share/dotnet/x64/dotnet /usr/local/bin
 ```
