<!-- source: https://www.opswat.com/docs/mdcore/v5.24.1/software-bill-of-materials/source-code -->

# Source code

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

Since each programming language has its declaration files for the libraries being used, the SBOM engine only analyzes the files with these specific filenames to avoid false positives or performance downgrades.

| Programming language | **Manifest and lock files** | **Package archives and binaries** |
| --- | --- | --- |
| Ruby | Gemfile.lock | .gem, .tar.gz |
| Python | Pipfile.lock, poetry.lock, requirements*.txt, METADATA, PKG-INFO  setup.py, pyproject.toml, version.py | .whl, .tar.gz (metadata read from the archive), .egg, .zip |
| PHP | composer.lock, composer.json | .zip |
| Node.js | package.json, package-lock.json, yarn.lock, pnpm-lock.yaml | .tgz |
| TypeScript / CoffeeScript | package.json, package-lock.json, yarn.lock, pnpm-lock.yaml |  |
| Java | pom.xml, pom.properties, build.gradle(.kts), settings.gradle(.kts), gradle.lockfile, libs.versions.toml | .jar, .zip, .tar.gz, source archives (src.zip, sources.zip, src.tar.gz, sources.tar.gz |
| Kotlin / Groovy | build.gradle(.kts), settings.gradle(.kts), gradle.lockfile, libs.versions.toml, pom.xml | .jar |
| Scala / Clojure | pom.xml | .jar |
| Go | go.mod |  |
| Rust | Cargo.lock |  |
| Dart | pubspec.lock |  |
| .NET | packages.lock.json, packages.config, *.deps.json, *.nuspec, *.csproj | .nupkg, .dll |
| Elixir | mix.lock |  |
| Swift | Podfile.lock, Package.resolved |  |
| C/C++ | vcpkg.json, conan.lock | .exe, .dll |
| Julia | [Pp]roject.toml, [Mm]anifest.toml |  |
| R | renv.lock |  |
