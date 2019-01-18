# ANTLRv4 support in IntelliJ IDEs

A library to support the use of ANTLRv4 grammars for custom languages in IntelliJ-based IDEs plug-in development.

This library has adaptors that convert ANTLR-generated parse trees into IntelliJ PSI trees.  Mostly this library is about adapting ANTLR parsers and trees, but there is considerable support to examine PSI trees derived from ANTLR parse trees. For example, if you're building a structure view for your plug-in and you want to get the list of function names you can use XPath-like specs such as `"/script/function/ID"`:

```java
Collection<? extends PsiElement> allfuncs =
    XPath.findAll(SampleLanguage.INSTANCE, tree,
                  "/script/function/ID");
```

I have made a sample plug-in that demonstrates the use of this library: [antlr/jetbrains-plugin-sample](https://github.com/antlr/jetbrains-plugin-sample).

## Using the library in your project

The library is [published on Maven Central](https://search.maven.org/search?q=a:antlr4-intellij-adaptor) which means you can download the JAR and add it to your classpath manually, or pull the dependency automatically if you are using a Gradle build:

```groovy
repositories {
    mavenCentral()
}

dependencies {
    compile "org.antlr:antlr4-intellij-adaptor:0.1"
}
```

## Examples

Here is a list of known plugins that use the adaptor:

* [ANTLRv4 grammar plugin](https://github.com/antlr/intellij-plugin-v4)
* [Pebble plugin](https://plugins.jetbrains.com/plugin/9407-pebble)

Other usages can be [found on GitHub](https://github.com/search?p=1&q=ANTLRParserAdaptor&type=Code)

## Migration from the pre-Maven version

Before 0.1, it was recommended to add this Git repo as a submodule of your own project, or to copy the source files directly.

It is now recommended to use the Maven dependency. The main **breaking change** is that the base package has been renamed from `org.antlr.jetbrains.adaptor` to `org.antlr.intellij.adaptor`
