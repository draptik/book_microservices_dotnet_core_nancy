# Chapter 1

This folder contains a Hello-World app for .NET Core on linux. It took me a few tries to get everything up and running.

**IMPORTANT:**

Since the book was published the .NET Core project setup has changed (again).

The book uses `project.json` to configure projects. Microsoft recently changed the project configuration to `msbuild/csproj` files (2017-03-07).

A detailed description (including migration concepts) can be found here:

- [Scott Hanselmann's blog: Working with Multiple .NET Core SDKs](https://www.hanselman.com/blog/WorkingWithMultipleNETCoreSDKsBothProjectjsonAndMsbuildcsproj.aspx)
- [Nate McMaster's blog: Project.json to MSBuild conversion guide](http://www.natemcmaster.com/blog/2017/01/19/project-json-to-csproj/)

## Installation

### Trial 1 (fail)

My first approach will be to downgrade some libs so I can work with the older `project.json`...

#### Downgrading Yeoman's generator-aspnet

The current (2017-03-07) `generator-aspnet` has version `0.3.x`. This version only supports the new format (`csproj`). To donwgrade `generator-aspnet` to version `0.2.6` (see [this github issue for details](https://github.com/OmniSharp/generator-aspnet/issues/927)):

```sh
npm install -g generator-aspnet@0.2.6
```

#### Installation

From the book (after downgrading `generator-aspnet` to version `0.2.6`):

- `yo aspnet`
- choose `Empty Web Application`
- name of application: `Hellomicroservices`

The result should look similar to:

```sh
$ npm install -g generator-aspnet@0.2.6
$ npm list -g generator-aspnet
/home/patrick/.nvm/versions/node/v6.9.4/lib
└── generator-aspnet@0.2.6

$ yo aspnet

     _-----_     ╭──────────────────────────╮
    |       |    │      Welcome to the      │
    |--(o)--|    │  marvellous ASP.NET Core │
   `---------´   │        generator!        │
    ( _´U`_ )    ╰──────────────────────────╯
    /___A___\   /
     |  ~  |
   __'.___.'__
 ´   `  |° ´ Y `

? What type of application do you want to create? Empty Web Application
? What's the name of your ASP.NET application? Hellomicroservices
   create Hellomicroservices/.gitignore
   create Hellomicroservices/Program.cs
   create Hellomicroservices/Startup.cs
   create Hellomicroservices/project.json
   create Hellomicroservices/web.config
   create Hellomicroservices/Dockerfile
   create Hellomicroservices/Dockerfile.nano
   create Hellomicroservices/Properties/launchSettings.json
   create Hellomicroservices/README.md
   create Hellomicroservices/global.json


Your project is now created, you can use the following commands to get going
    cd "Hellomicroservices"
    dotnet restore
    dotnet build (optional, build will also happen when it's run)
    dotnet run
```

Following the instructions...

```sh
$ cd Hellomicroservices
$ dotnet restore
MSBUILD : error MSB1003: Specify a project or solution file. The current working directory does not contain a project or solution file.
```

For this to work I probably also have to also downgrade the .NET Core SDK. Since Arch Linux currently only has the most up-to-date version in it's AUR repository I will skip this option for now.


### Trial 2: Plain dotnet templating (works)

Create project template **without Yeoman**.

Pure `dotnet new` templating:

```sh
mkdir aspnetcore
cd aspnetcore
dotnet new web
dotnet restore
dotnet run
```

and open browser at `http://localhost:5000`

### Trial 3: Yeoman's aspnet generator with Nancy (works)

From the book (using the current version of `generator-aspnet` `0.3.x`):

- `yo aspnet`
- choose `Nancy ASP.NET Application`
- name of application: `NancyApplication`

The result should look similar to:

```sh
$ npm install -g generator-aspnet
$ npm list -g generator-aspnet
/home/patrick/.nvm/versions/node/v6.9.4/lib
└── generator-aspnet@0.3.2
$ yo aspnet

     _-----_     ╭──────────────────────────╮
    |       |    │      Welcome to the      │
    |--(o)--|    │  marvellous ASP.NET Core │
   `---------´   │        generator!        │
    ( _´U`_ )    ╰──────────────────────────╯
    /___A___\   /
     |  ~  |
   __'.___.'__
 ´   `  |° ´ Y `

? What type of application do you want to create? Nancy ASP.NET Application
? What's the name of your ASP.NET application? NancyApplication
   create NancyApplication/.gitignore
   create NancyApplication/Startup.cs
   create NancyApplication/NancyApplication.csproj
   create NancyApplication/HomeModule.cs
   create NancyApplication/Program.cs
   create NancyApplication/global.json


Your project is now created, you can use the following commands to get going
    cd "NancyApplication"
    dotnet restore
    dotnet build (optional, build will also happen when it's run)
    dotnet run
```

Follow the instructions:

```sh
cd "NancyApplication"
dotnet restore
dotnet run
```

and open browser at `http://localhost:5000`

## Summary

I'll try to use **Trial 3**: A simple Nancy project generated using `yo aspnet`.








# Current versions

## Arch linux

```sh
 $ nvm --version
0.31.2
 $ node --version
v6.9.4
 $ npm --version
3.10.10
 $ yo --version
1.8.5
 $ dotnet --version
1.0.0-rc4-004771
```

## Ubuntu linux

```sh
 $ nvm --version
TODO
 $ node --version
TODO
 $ npm --version
TODO
 $ yo --version
TODO 
 $ dotnet --version
TODO
```
