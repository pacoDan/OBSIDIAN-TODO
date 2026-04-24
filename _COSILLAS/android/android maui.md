# Install .NET for Android dependencies
```sh
dotnet build -t:InstallAndroidDependencies -f net8.0-android -p:AndroidSdkDirectory=c:\work\android-sdk -p:JavaSdkDirectory=c:\work\jdk -p:AcceptAndroidSdkLicenses=True
```
8 , falla
```sh
dotnet build -t:InstallAndroidDependencies -f net8.0-android -p:AndroidSdkDirectory="/home/daniel/Android/Sdk" -p:JavaSdkDirectory="/home/daniel/.desarrollo/amazon-corretto-17.0.17.10.1-linux-x64" -p:AcceptAndroidSdkLicenses=True
```
10 ok
```sh
dotnet build -t:InstallAndroidDependencies -f net8.0-android -p:AndroidSdkDirectory="/home/daniel/Android/Sdk" -p:JavaSdkDirectory="/home/daniel/.desarrollo/amazon-corretto-17.0.17.10.1-linux-x64" -p:AcceptAndroidSdkLicenses=True
```
para correr ok (notar que deebee haceerde dentro de la carpeta del proyecto, NO DONDE ESTA EL .SLN)
```sh
dotnet run -f net10.0-android \
  -p:AndroidSdkDirectory="/home/daniel/Android/Sdk" \
  -p:JavaSdkDirectory="/home/daniel/.desarrollo/amazon-corretto-17.0.17.10.1-linux-x64"
```
---
sino en Rider configurar en `/home/daniel/.dotnet/packs/Microsoft.Android.Sdk.Linux/36.1.12/tools/Xamarin.Android.Tooling.targets`
cerca de:
```targets
<ResolveSdks  
    ContinueOnError="$(_AndroidAllowMissingSdkTooling)"  
    CommandLineToolsVersion="$(AndroidCommandLineToolsVersion)"  
    AndroidSdkPath="$(AndroidSdkDirectory)"
```
como
```targets
<ResolveSdks  
    ContinueOnError="$(_AndroidAllowMissingSdkTooling)"  
    CommandLineToolsVersion="$(AndroidCommandLineToolsVersion)"  
    AndroidSdkPath="/home/daniel/Android/Sdk"
    AndroidNdkPath="$(AndroidNdkDirectory)"  
	JavaSdkPath="/home/daniel/.desarrollo/amazon-corretto-17.0.17.10.1-linux-x64"
```

## Opción 1 (recomendada): `Directory.Build.props` en la raíz de la solución MAS QUE TODO POR LA SDK Y JDK

Crea un archivo `Directory.Build.props` al lado del `.sln` con:
```xml
<Project>
  <PropertyGroup>
    <AndroidSdkDirectory>/home/daniel/Android/Sdk</AndroidSdkDirectory>
    <JavaSdkDirectory>/home/daniel/.desarrollo/amazon-corretto-17.0.17.10.1-linux-x64</JavaSdkDirectory>

    <!-- Opcional -->
    <AcceptAndroidSdkLicenses>true</AcceptAndroidSdkLicenses>
  </PropertyGroup>
</Project><Project>
  <PropertyGroup>
    <AndroidSdkDirectory>/home/daniel/Android/Sdk</AndroidSdkDirectory>
    <JavaSdkDirectory>/home/daniel/.desarrollo/amazon-corretto-17.0.17.10.1-linux-x64</JavaSdkDirectory>

    <!-- Opcional -->
    <AcceptAndroidSdkLicenses>true</AcceptAndroidSdkLicenses>
  </PropertyGroup>
</Project>
```
**o editando en el mismo  AndroidApp2.csproj**  OK

---
truco ok en dotnet para ahorrase eel namespaces:
`<ImplicitUsings>enable</ImplicitUsings>`

