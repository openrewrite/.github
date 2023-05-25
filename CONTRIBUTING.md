# Welcome 👋

Thank you for taking the time to contribute to OpenRewrite! All types of contributions are encouraged and valued. 

Please make sure to read the relevant section before making your contribution. It will make it a lot easier for us maintainers and smooth out the experience for all involved. The community looks forward to your contributions. 😁

In this guide, you will find instructions for the [different ways you can contribute to the project](#ways-to-contribute) as well as [useful context for setting up your development environment](#building--developing).

## Ways to contribute

There are various ways to contribute, each of which we will cover in more detail below.

1. [Asking questions & reporting issues](#asking-questions--reporting-issues)
2. [Answering community questions](#answering-community-questions)
3. [Improving the documentation](#improving-the-documentation)
4. [Contributing fixes](#contributing-fixes)
5. [Adding new recipes](#adding-new-recipes)
6. [New features](#new-features)

### Asking questions & reporting issues

When starting out, you will likely have questions about OpenRewrite; we have multiple channels where you can ask questions:

* [Slack](https://join.slack.com/t/rewriteoss/shared_invite/zt-nj42n3ea-b~62rIHzb3Vo0E1APKCXEA)
* [Discord](https://discord.gg/xk3ZKrhWAb)
* [https://github.com/openrewrite/rewrite/discussions](https://github.com/openrewrite/rewrite/discussions)
* [https://github.com/openrewrite/rewrite/issues](https://github.com/openrewrite/rewrite/issues)
* [Stack Overflow](https://stackoverflow.com/questions/tagged/openrewrite)

We monitor all of these channels and try to respond in a timely manner. Please only post your question in a **single channel** so that we don't spend time looking into questions that may have already been answered elsewhere.

Furthermore, when asking a question or reporting an issue, please be as specific as possible and include details that will help us immediately dive in. For instance:

1. Share what you have read and tried already so that we don't end up sending you to places you've already been.
2. Explain how you are running OpenRewrite. Are you using Maven? Gradle? [Moderne.io](https://app.moderne.io)? Something else?
3. Provide the version numbers of the Maven or Gradle plugin, OpenRewrite itself, and any rewrite modules you may be using.
4. Add as much of your OpenRewrite configuration as you're able to share so that we can rule out configuration issues.
5. Let us know what recipe you are running, especially when using a `rewrite.yml` file.
6. Include a before and after. Also, what did you expect the after to be?
7. When errors occur, please include the output of `--stacktrace` for Gradle or `--debug` for Maven.
8. Ensure that you are asking questions or reporting issues on the respective OpenRewrite module if at all possible.

By doing all of these things, you will not only help us get you answers more quickly, but you will help out the community who may search for these details in the future.

### Answering community questions

Once you get more familiar with OpenRewrite, you might spot questions from within the community that you already know the answer to. Helping answer these questions is a great way to reduce the load on contributors, and very much appreciated.

If you are unsure whether your answer is the best approach, then responding to a question will help you further your own understanding as well. Please feel free to answer questions in any of the [channels](#asking-questions--reporting-issues). By doing so, we can help everyone learn and grow.

### Improving the documentation

As you increase your knowledge of OpenRewrite, you might find mistakes in our documentation, areas where we could be more clear, or topics that are missing. If you have suggestions for any of those, please consider contributing to [rewrite-docs](https://github.com/openrewrite/rewrite-docs). There are further instructions in that project's [README](https://github.com/openrewrite/rewrite-docs#readme). All changes made to that repository are deployed to [https://docs.openrewrite.org](https://docs.openrewrite.org).

### Contributing fixes

The best way to work towards a fix is to first replicate the issue with a minimal unit test. Nearly every recipe has a dedicated unit test that shows a before and after situation. Usually, you can copy the first unit test for any specific recipe, and adjust that to match the problem case. 

Once replicated, you can already open a draft pull request, even if you are unsure whether you will be able to contribute a fix. That allows us to also have a look at the specifics of the issue in our IDE, if necessary. From there, we generally recommend that people step through the recipe execution using the debugger while running the new unit test. As you make changes to the recipe, you should see the test go from failing to passing. If you get stuck at any point, we’re happy to help.

Are you looking for a good place to start contributing? We have added the ["Good first issue"](https://github.com/orgs/openrewrite/projects/4/views/10?filterQuery=label%3A%22good+first+issue%22) label to a few of our backlog items, and added hints on the possible implementation.

### Adding new recipes

Before you add a new recipe, we suggest you first open an issue to discuss the specifics of what you're wanting to achieve. Please include a before and after example so that we're able to judge whether or not the recipe is feasible or desirable. By reaching out before you start implementing, we can also help guide you to similar existing recipes that you might want to borrow parts of or compare your solution to.

Once you start implementing the new recipe, we recommend you start by writing unit tests similar to those discussed in the [contributing fixes](#contributing-fixes) section. This way you'll be able to step through them with a debugger or the [TreeVisitingPrinter](https://docs.openrewrite.org/concepts-explanations/tree-visiting-printer) to explore what tree elements are available.

An early draft pull request at this stage makes it easier for us to provide you with feedback to improve your implementation – which will result in less work for you in the long run. 

Once you mark your implementation as ready for review, we will go through it in detail to get it in shape to merge into OpenRewrite.

### New features

If you want to add a new major feature, please reach out to us via [Slack](https://join.slack.com/t/rewriteoss/shared_invite/zt-nj42n3ea-b~62rIHzb3Vo0E1APKCXEA) to discuss the specifics. By doing so, we can help guide you and ensure that it's feasible before you spend a considerable amount of time.

## Building & developing

We recommend that you use [IntelliJ](https://www.jetbrains.com/idea/) for development, as some of the Gradle specifics in `openrewrite/rewrite` are not supported as well in other IDEs. 

All projects use Java 17 for their tests, to take advantage of text blocks. For `src/main`, we use Java 8 exclusively so that our users only need Java 8 to run OpenRewrite migration recipes. We use [Gradle](https://gradle.org/) as our build tool.

**Note**: The Gradle wrapper requires a preexisting JDK 8 installation. If not present, the build will fail to download the toolchain in the `:write-gradle:compilyGroovy` task. You will need to install JDK 8 manually. For Unix systems, we strongly recommend using [SDKMAN!](https://sdkman.io/) to install and switch between Java versions. 

### IntelliJ changes

By default, IntelliJ uses Gradle to build and run tests with. While that ensures compatibility, it is very slow. To help speed up compilation and testing, we recommend that you change this to use `IntelliJ IDEA` instead:

![](/resources/gradle-select.png)

As part of doing that, you'll also need to update the `Java Compiler` to set the `-parameters` compiler flag. If your system does not have `UTF-8` as its default character encoding (e.g., Windows), you must also add `-encoding utf8`.

![](/resources/parameters.png)

You will also need to add an override to the compiler parameters for the `rewrite.rewrite-java-17.main` module to have the compilation options of: 

```
-parameters --add-exports jdk.compiler/com.sun.tools.javac.comp=ALL-UNNAMED --add-exports jdk.compiler/com.sun.tools.javac.file=ALL-UNNAMED --add-exports jdk.compiler/com.sun.tools.javac.main=ALL-UNNAMED --add-exports jdk.compiler/com.sun.tools.javac.tree=ALL-UNNAMED --add-exports jdk.compiler/com.sun.tools.javac.util=ALL-UNNAMED --add-exports jdk.compiler/com.sun.tools.javac.code=ALL-UNNAMED
```

![](/resources/compilation-options.png)

#### Optimizing your IDE for only modules you want to work on

If you are only working on a subset of the modules in [openrewrite/rewrite](https://github.com/openrewrite/rewrite), you can optimize your IDE to only load those modules. Create a new `IDE.properties` file if one doesn't exist in the base directory of the project and then copy the contents of [IDE.properties.tmp](https://github.com/openrewrite/rewrite/blob/main/IDE.properties.tmp) file to it. Next, comment out any lines that correspond to modules that you do not want to work on. This will cause Gradle to swap those project dependencies for binary dependencies resolved from either Maven local or the OSS snapshots repository – which will speed up your IDE.

### Windows caveats

If you are contributing to OpenRewrite on Windows, please ensure that you set `core.autocrlf = false` as [Rewrite](https://github.com/openrewrite/rewrite) requires unix-style line endings. This can be done when you clone the repository:

```shell
git clone -c core.autocrlf=false https://github.com/openrewrite/rewrite.git
```

Also, as mentioned in the [IntelliJ section](#intellij-changes) above, please ensure that your system uses `UTF-8` for character encoding.
