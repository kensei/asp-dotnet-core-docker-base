# asp dotnet.core docker base

## start

`docker-compose up -d`

## simple web sample

```
cat <<EOF > app/NetCoreDocker.csproj
<Project Sdk="Microsoft.NET.Sdk.Web">
  <PropertyGroup>
    <TargetFramework>netcoreapp2.1</TargetFramework>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.App" />
  </ItemGroup>
</Project>
EOF
```
