# ASP.NET Core sandbox by docker

## start

`docker-compose up -d`

## simple web sample

### attach code

```
$ cat <<EOF > app/NetCoreDocker.csproj
<Project Sdk="Microsoft.NET.Sdk.Web">
  <PropertyGroup>
    <TargetFramework>netcoreapp2.1</TargetFramework>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.App" />
  </ItemGroup>
</Project>
EOF

$ cat <<EOF > app/Program.cs
using Microsoft.AspNetCore;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Hosting;
using Microsoft.AspNetCore.Http;

class Program {
  static void Main(string[] args) {
    CreateWebHostBuilder(args).Build().Run();
  }

  public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
    WebHost.CreateDefaultBuilder(args).Configure(app => {
      app.Run(async (HttpContext c) => {
        await c.Response.WriteAsync("Hello ASP.NET Core!\n");
      });
    });
}
EOF
```

### restore project

`docker exec dotnet-build dotnet restore`

### build

`docker exec dotnet-build dotnet publish -c Release -o out`

### deploy

`docker exec asp-net dotnet NetCoreDocker.dll`

### reset

`git clean -fdx`

## start empty vs web project

### create project

`docker exec dotnet-build dotnet new webapp`

### open visual studio

`open app/app.csproj`

### build

`docker exec dotnet-build dotnet publish -c Release -o out`

### run

`docker exec asp-net dotnet app.dll`

### reset

`git clean -fdx`
