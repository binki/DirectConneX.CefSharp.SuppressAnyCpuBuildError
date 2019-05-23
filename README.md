CefSharp will purposefully error the build if you target AnyCPU unless if an MSBuild property is set on the project.

However, `<PackageReference/>` dependencies are transitive.
That is, when Project A has a `<ProjectReference/>` to Project B which has a `<PackageReference/>` to NuGet Package C, Project A acts as if it has a direct dependency on Nuget Package C.
This applies even if, due to encapsulation, Project A has no need to know that Project B has a reference to Nuget Package C.
In this case, the result of CefSharp’s [buildsystem design decisions](https://github.com/cefsharp/CefSharp/issues/1714) might force you to make an executable project aware that its dependency project uses CefSharp.

To fix this, this package simply provides a props file which suppresses the CefSharp error.
You can reference this package from the project which references CefSharp to prevent any dependency on your project from failing the build.
