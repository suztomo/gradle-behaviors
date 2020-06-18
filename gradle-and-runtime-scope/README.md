# Runtime Scope

From https://github.com/mesos/mesos-rxjava/blob/master/pom.xml#L141-L151

[`io.reactivex:rxnetty:0.5.1`](https://search.maven.org/artifact/io.reactivex/rxnetty/0.5.1/jar) has
a dependency of `io.reactivex:rxjava:1.0.14` with runtime scope.

```
    <dependency>
      <groupId>io.reactivex</groupId>
      <artifactId>rxjava</artifactId>
      <version>1.0.14</version>
      <scope>runtime</scope>
    </dependency>
```

Gradle's compileClasspath does not include `io.reactivex:rxjava:1.0.14`.

Gradle's runtimeClasspath includes `io.reactivex:rxjava:1.0.14`.

```
compileClasspath - Compile classpath for source set 'main'.
\--- io.reactivex:rxnetty:0.5.1

compileOnly - Compile only dependencies for source set 'main'. (n)
No dependencies

default - Configuration for default artifacts. (n)
No dependencies

implementation - Implementation only dependencies for source set 'main'. (n)
\--- io.reactivex:rxnetty:0.5.1 (n)

runtimeClasspath - Runtime classpath of source set 'main'.
\--- io.reactivex:rxnetty:0.5.1
     +--- io.reactivex:rxjava:1.0.14
     +--- io.netty:netty-codec-http:4.1.0.Beta7
     |    \--- io.netty:netty-codec:4.1.0.Beta7
     |         \--- io.netty:netty-transport:4.1.0.Beta7
     |              +--- io.netty:netty-buffer:4.1.0.Beta7
     |              |    \--- io.netty:netty-common:4.1.0.Beta7
     |              \--- io.netty:netty-resolver:4.1.0.Beta7
     |                   \--- io.netty:netty-common:4.1.0.Beta7
     +--- io.netty:netty-handler:4.1.0.Beta7
     |    +--- io.netty:netty-buffer:4.1.0.Beta7 (*)
     |    +--- io.netty:netty-transport:4.1.0.Beta7 (*)
     |    \--- io.netty:netty-codec:4.1.0.Beta7 (*)
     +--- io.netty:netty-transport-native-epoll:4.1.0.Beta7
     |    +--- io.netty:netty-common:4.1.0.Beta7
     |    +--- io.netty:netty-buffer:4.1.0.Beta7 (*)
     |    \--- io.netty:netty-transport:4.1.0.Beta7 (*)
     \--- org.slf4j:slf4j-api:1.7.6
```

