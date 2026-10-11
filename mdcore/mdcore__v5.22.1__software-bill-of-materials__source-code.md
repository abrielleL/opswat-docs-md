<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/software-bill-of-materials/source-code -->

# Source code

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Since each programming language has its declaration files for the libraries being used, the SBOM engine only analyzes the files with these specific filenames to avoid false positives or performance downgrades.

| Programming language | File to check |
| --- | --- |
| Ruby | Gemfile.lock  library package in tar.gz, gem format |
| Python | Pipfile.lock  poetry.lock  requirements*.txt  setup.py  pyproject.toml  version.py  library package in tar.gz, egg, whl, zip format |
| PHP | composer.lock  composer.json  library package in zip format |
| NodeJS | package.json  package-lock.json  yarn.lock  pnpm-lock.yaml  library package in tgz, jar format |
| TypeScript | package.json |
| CoffeeScript | package.json |
| Java | pom.xml  pom.properties  gradle.lockfile  build.gradle, settings.gradle  build.gradle.kts, settings.gradle.kts  libs.versions.toml  *.jar  library package in zip, src.zip, sources.zip, tar.gz, src.tar.gz, sources.tar.gz format |
| Scala | pom.xml |
| Groovy | pom.xml  build.gradle, build.gradle.kts  settings.gradle, settings.gradle.kts |
| Clojoure | pom.xml |
| Kotlin | build.gradle, build.gradle.kts  settings.gradle, settings.gradle.kts  libs.versions.toml  *.lockfile |
| Go | go.mod |
| Rust | cargo.lock |
| Dart | pubspec.lock |
| .NET | packages.lock.json  packages.config  .deps.json  .nuspec  .csproj  dll  library package in nupkg format |
| Elixir | mix.lock |
| Swift | Podfile.lock  Package.resolved |
| C/C++ package manager | conan.lock dll ,exe, hpp |
| Julia | [Pp]roject.toml, [Mm]anifest.toml |
| R | renv.lock |
