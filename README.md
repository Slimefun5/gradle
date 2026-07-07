# gradle

Shared Gradle build conventions for the [Slimefun5](https://github.com/Slimefun5) fork's addons — the
build-logic counterpart to [`Slimefun5/workflows`](https://github.com/Slimefun5/workflows).

## Usage

In an addon's `build.gradle.kts`, after the `plugins { }` block (which must apply `java`,
`com.gradleup.shadow`, and `io.github.intisy.github-gradle`):

```kotlin
group = "…"
description = "…"

apply(from = "https://raw.githubusercontent.com/Slimefun5/gradle/stable/slimefun-addon.gradle")
```

`slimefun-addon.gradle` provides the version scheme (+ `-UNOFFICIAL`/`-EXPERIMENTAL`/`artifact_version`
suffix), the `github { publish }` block, the Java-8 toolchain, the common repositories (incl. JitPack),
the common dependencies (`spigot-api:1.16.5`, `jsr305`, `githubCompileOnly` core), the common tasks
(`shadowJar` naming + `META-INF` exclude, disabled `jar`, `build` → `shadowJar`), and disables the test
tasks (the fork does not run addon test suites).

The addon adds only its extras afterwards: `SlimefunMetrics`, bStats + its relocation, extra library
dependencies, and any extra repositories. Overridable via `-PsfCoreVersion`, `-PsfSpigotApi`,
`-PsfDefaultVersion`.
