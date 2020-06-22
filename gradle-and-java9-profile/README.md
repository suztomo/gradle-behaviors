# Gradle's Maven Profile handling

Gradle ignores Maven profiles.

In this experiment, I use `com.google.cloud:google-cloud-firestore:1.32.0`.
The `com.google.cloud:google-cloud-firestore:1.32.0`'s pom.xml defines a profile to add
`javax.annotation:javax.annotation-api:jar:1.3.2` dependency only if JDK version
is Java 9 or higher:

```
  <profiles>
    <profile>
      <id>java9</id>
      <activation>
        <jdk>[9,)</jdk>
      </activation>
      <dependencies>
        <dependency>
          <groupId>javax.annotation</groupId>
          <artifactId>javax.annotation-api</artifactId>
          <version>${javax.annotations.version}</version>
        </dependency>
      </dependencies>
    </profile>
  </profiles>
```

## Gradle With Java 11

Set the java version to Java 11.

```
suztomo-macbookpro44% which java
/Library/Java/JavaVirtualMachines/jdk-11-latest/Contents/Home/bin/java
suztomo-macbookpro44% java -version
java version "11.0.4" 2019-07-16 LTS
Java(TM) SE Runtime Environment 18.9 (build 11.0.4+10-LTS)
Java HotSpot(TM) 64-Bit Server VM 18.9 (build 11.0.4+10-LTS, mixed mode)
```

The tree does not have javax.annotation-api dependency directly below
`com.google.cloud:google-cloud-firestore:1.32.0`.

```
suztomo-macbookpro44% ./gradlew dependencies
compileClasspath - Compile classpath for source set 'main'.
\--- com.google.cloud:google-cloud-firestore:1.32.0
     +--- com.google.cloud:google-cloud-core-grpc:1.91.3
     |    +--- com.google.auth:google-auth-library-credentials:0.18.0
     |    +--- com.google.cloud:google-cloud-core:1.91.3
     |    |    +--- com.google.api:gax:1.49.1 -> 1.51.0
     |    |    |    +--- com.google.guava:guava:28.1-android
     |    |    |    |    +--- com.google.guava:failureaccess:1.0.1
     |    |    |    |    +--- com.google.guava:listenablefuture:9999.0-empty-to-avoid-conflict-with-guava
     |    |    |    |    +--- com.google.code.findbugs:jsr305:3.0.2
     |    |    |    |    +--- org.checkerframework:checker-compat-qual:2.5.5
     |    |    |    |    +--- com.google.errorprone:error_prone_annotations:2.3.2 -> 2.3.3
     |    |    |    |    +--- com.google.j2objc:j2objc-annotations:1.3
     |    |    |    |    \--- org.codehaus.mojo:animal-sniffer-annotations:1.18
     |    |    |    +--- com.google.code.findbugs:jsr305:3.0.2
     |    |    |    +--- org.threeten:threetenbp:1.3.3 -> 1.4.0
     |    |    |    +--- com.google.auth:google-auth-library-oauth2-http:0.18.0
     |    |    |    |    +--- com.google.auto.value:auto-value-annotations:1.6.6
     |    |    |    |    +--- com.google.code.findbugs:jsr305:3.0.2
     |    |    |    |    +--- com.google.auth:google-auth-library-credentials:0.18.0
     |    |    |    |    +--- com.google.http-client:google-http-client:1.32.1
     |    |    |    |    |    +--- org.apache.httpcomponents:httpclient:4.5.10
     |    |    |    |    |    |    +--- org.apache.httpcomponents:httpcore:4.4.12
     |    |    |    |    |    |    +--- commons-logging:commons-logging:1.2
     |    |    |    |    |    |    \--- commons-codec:commons-codec:1.11
     |    |    |    |    |    +--- org.apache.httpcomponents:httpcore:4.4.12
     |    |    |    |    |    +--- com.google.code.findbugs:jsr305:3.0.2
     |    |    |    |    |    +--- com.google.guava:guava:28.1-android (*)
     |    |    |    |    |    +--- com.google.j2objc:j2objc-annotations:1.3
     |    |    |    |    |    +--- io.opencensus:opencensus-api:0.24.0
     |    |    |    |    |    |    \--- io.grpc:grpc-context:1.22.1 -> 1.25.0
     |    |    |    |    |    \--- io.opencensus:opencensus-contrib-http-util:0.24.0
     |    |    |    |    |         +--- io.opencensus:opencensus-api:0.24.0 (*)
     |    |    |    |    |         \--- com.google.guava:guava:26.0-android -> 28.1-android (*)
     |    |    |    |    +--- com.google.http-client:google-http-client-jackson2:1.32.1
     |    |    |    |    |    +--- com.google.http-client:google-http-client:1.32.1 (*)
     |    |    |    |    |    \--- com.fasterxml.jackson.core:jackson-core:2.9.9 -> 2.10.1
     |    |    |    |    \--- com.google.guava:guava:28.1-android (*)
     |    |    |    +--- com.google.api:api-common:1.8.1
     |    |    |    |    +--- com.google.code.findbugs:jsr305:3.0.2
     |    |    |    |    +--- com.google.guava:guava:26.0-android -> 28.1-android (*)
     |    |    |    |    \--- javax.annotation:javax.annotation-api:1.3.2
     |    |    |    \--- io.opencensus:opencensus-api:0.24.0 (*)
     |    |    +--- com.google.protobuf:protobuf-java-util:3.10.0 -> 3.11.1
     |    |    |    +--- com.google.protobuf:protobuf-java:3.11.1
     |    |    |    +--- com.google.guava:guava:28.1-android (*)
     |    |    |    +--- com.google.errorprone:error_prone_annotations:2.3.3
     |    |    |    \--- com.google.code.gson:gson:2.8.6
     |    |    +--- com.google.api.grpc:proto-google-common-protos:1.17.0
     |    |    |    \--- com.google.protobuf:protobuf-java:3.7.1 -> 3.11.1
     |    |    +--- com.google.api.grpc:proto-google-iam-v1:0.13.0
     |    |    |    +--- com.google.protobuf:protobuf-java:3.7.1 -> 3.11.1
     |    |    |    +--- com.google.api:api-common:1.8.1 (*)
     |    |    |    \--- com.google.api.grpc:proto-google-common-protos:1.16.0 -> 1.17.0 (*)
     |    |    +--- org.threeten:threetenbp:1.3.3 -> 1.4.0
     |    |    +--- com.google.api:api-common:1.8.1 (*)
     |    |    +--- com.google.auth:google-auth-library-credentials:0.18.0
     |    |    +--- com.google.auth:google-auth-library-oauth2-http:0.18.0 (*)
     |    |    +--- com.google.http-client:google-http-client:1.32.1 (*)
     |    |    +--- com.google.http-client:google-http-client-jackson2:1.32.1 (*)
     |    |    +--- com.google.protobuf:protobuf-java:3.10.0 -> 3.11.1
     |    |    \--- com.google.guava:guava:28.1-android (*)
     |    +--- com.google.guava:guava:28.1-android (*)
     |    +--- com.google.api:gax:1.49.1 -> 1.51.0 (*)
     |    +--- com.google.api:gax-grpc:1.49.1 -> 1.51.0
     |    |    +--- com.google.api:gax:1.51.0 (*)
     |    |    +--- io.grpc:grpc-stub:1.25.0
     |    |    |    \--- io.grpc:grpc-api:1.25.0
     |    |    |         +--- io.grpc:grpc-context:1.25.0
     |    |    |         +--- com.google.errorprone:error_prone_annotations:2.3.3
     |    |    |         +--- com.google.code.findbugs:jsr305:3.0.2
     |    |    |         +--- org.codehaus.mojo:animal-sniffer-annotations:1.17 -> 1.18
     |    |    |         \--- com.google.guava:guava:28.1-android (*)
     |    |    +--- io.grpc:grpc-auth:1.25.0
     |    |    |    +--- io.grpc:grpc-api:1.25.0 (*)
     |    |    |    \--- com.google.auth:google-auth-library-credentials:0.17.1 -> 0.18.0
     |    |    +--- io.grpc:grpc-protobuf:1.25.0
     |    |    |    +--- io.grpc:grpc-api:1.25.0 (*)
     |    |    |    +--- com.google.protobuf:protobuf-java:3.10.0 -> 3.11.1
     |    |    |    +--- com.google.guava:guava:28.1-android (*)
     |    |    |    +--- com.google.api.grpc:proto-google-common-protos:1.12.0 -> 1.17.0 (*)
     |    |    |    \--- io.grpc:grpc-protobuf-lite:1.25.0
     |    |    |         +--- io.grpc:grpc-api:1.25.0 (*)
     |    |    |         \--- com.google.guava:guava:28.1-android (*)
     |    |    +--- com.google.guava:guava:28.1-android (*)
     |    |    +--- com.google.code.findbugs:jsr305:3.0.2
     |    |    +--- org.threeten:threetenbp:1.3.3 -> 1.4.0
     |    |    +--- com.google.auth:google-auth-library-oauth2-http:0.18.0 (*)
     |    |    +--- com.google.auth:google-auth-library-credentials:0.18.0
     |    |    +--- com.google.api.grpc:proto-google-common-protos:1.15.0 -> 1.17.0 (*)
     |    |    +--- com.google.api:api-common:1.8.1 (*)
     |    |    +--- io.grpc:grpc-netty-shaded:1.25.0
     |    |    |    \--- io.grpc:grpc-core:1.25.0
     |    |    |         +--- io.grpc:grpc-api:1.25.0 (*)
     |    |    |         +--- com.google.code.gson:gson:2.8.5 -> 2.8.6
     |    |    |         +--- com.google.android:annotations:4.1.1.4
     |    |    |         +--- io.perfmark:perfmark-api:0.19.0
     |    |    |         |    +--- com.google.code.findbugs:jsr305:3.0.2
     |    |    |         |    \--- com.google.errorprone:error_prone_annotations:2.3.3
     |    |    |         +--- io.opencensus:opencensus-api:0.21.0 -> 0.24.0 (*)
     |    |    |         \--- io.opencensus:opencensus-contrib-grpc-metrics:0.21.0
     |    |    |              \--- io.opencensus:opencensus-api:0.21.0 -> 0.24.0 (*)
     |    |    \--- io.grpc:grpc-alts:1.25.0
     |    |         +--- io.grpc:grpc-grpclb:1.25.0
     |    |         |    +--- io.grpc:grpc-core:1.25.0 (*)
     |    |         |    +--- io.grpc:grpc-protobuf:1.25.0 (*)
     |    |         |    +--- io.grpc:grpc-stub:1.25.0 (*)
     |    |         |    +--- com.google.protobuf:protobuf-java:3.10.0 -> 3.11.1
     |    |         |    \--- com.google.protobuf:protobuf-java-util:3.10.0 -> 3.11.1 (*)
     |    |         +--- io.grpc:grpc-auth:1.25.0 (*)
     |    |         +--- io.grpc:grpc-core:1.25.0 (*)
     |    |         +--- io.grpc:grpc-netty-shaded:1.25.0 (*)
     |    |         +--- io.grpc:grpc-protobuf:1.25.0 (*)
     |    |         +--- io.grpc:grpc-stub:1.25.0 (*)
     |    |         +--- org.apache.commons:commons-lang3:3.5
     |    |         +--- com.google.protobuf:protobuf-java:3.10.0 -> 3.11.1
     |    |         +--- org.conscrypt:conscrypt-openjdk-uber:2.2.1
     |    |         \--- com.google.auth:google-auth-library-oauth2-http:0.17.1 -> 0.18.0 (*)
     |    +--- com.google.api:api-common:1.8.1 (*)
     |    +--- io.grpc:grpc-api:1.24.1 -> 1.25.0 (*)
     |    +--- io.grpc:grpc-core:1.24.1 -> 1.25.0 (*)
     |    \--- com.google.http-client:google-http-client:1.32.1 (*)
     +--- com.google.api.grpc:proto-google-cloud-firestore-admin-v1:1.32.0
     |    +--- com.google.protobuf:protobuf-java:3.11.1
     |    +--- com.google.api:api-common:1.8.1 (*)
     |    +--- com.google.api.grpc:proto-google-common-protos:1.17.0 (*)
     |    \--- com.google.guava:guava:28.1-android (*)
     +--- com.google.api.grpc:proto-google-cloud-firestore-v1:1.32.0
     |    +--- com.google.protobuf:protobuf-java:3.11.1
     |    +--- com.google.api:api-common:1.8.1 (*)
     |    +--- com.google.api.grpc:proto-google-common-protos:1.17.0 (*)
     |    \--- com.google.guava:guava:28.1-android (*)
     +--- com.google.api.grpc:proto-google-cloud-firestore-v1beta1:0.85.0
     |    +--- com.google.protobuf:protobuf-java:3.11.1
     |    +--- com.google.api:api-common:1.8.1 (*)
     |    +--- com.google.api.grpc:proto-google-common-protos:1.17.0 (*)
     |    \--- com.google.guava:guava:28.1-android (*)
     +--- com.google.auto.value:auto-value-annotations:${auto-value-annotation.version} -> 1.6.6
     +--- io.opencensus:opencensus-contrib-grpc-util:0.24.0
     |    +--- io.opencensus:opencensus-api:0.24.0 (*)
     |    \--- io.grpc:grpc-core:1.22.1 -> 1.25.0 (*)
     +--- com.google.code.findbugs:jsr305:3.0.2
     +--- com.google.api:api-common:1.8.1 (*)
     +--- io.grpc:grpc-protobuf:1.25.0 (*)
     +--- io.grpc:grpc-context:1.25.0
     +--- com.google.protobuf:protobuf-java:3.11.1
     +--- com.google.api.grpc:proto-google-common-protos:1.17.0 (*)
     +--- com.google.api:gax:1.51.0 (*)
     +--- io.grpc:grpc-api:1.25.0 (*)
     +--- com.google.api:gax-grpc:1.51.0 (*)
     +--- com.google.guava:guava:28.1-android (*)
     +--- org.threeten:threetenbp:1.4.0
     +--- io.grpc:grpc-stub:1.25.0 (*)
     +--- io.opencensus:opencensus-api:0.24.0 (*)
     +--- com.google.auth:google-auth-library-credentials:0.18.0
     +--- com.google.cloud:google-cloud-core:1.91.3 (*)
     +--- com.google.code.gson:gson:2.8.6
     +--- com.fasterxml.jackson.core:jackson-core:2.10.1
     +--- com.google.protobuf:protobuf-java-util:3.11.1 (*)
     \--- com.google.cloud:google-cloud-conformance-tests:0.0.1
          +--- com.google.protobuf:protobuf-java:3.10.0 -> 3.11.1
          +--- com.google.api.grpc:proto-google-cloud-firestore-v1:1.27.0 -> 1.32.0 (*)
          \--- com.google.api.grpc:proto-google-cloud-bigtable-v2:0.80.0
               +--- com.google.protobuf:protobuf-java:3.10.0 -> 3.11.1
               +--- com.google.api:api-common:1.8.1 (*)
               +--- com.google.api.grpc:proto-google-common-protos:1.17.0 (*)
               \--- javax.annotation:javax.annotation-api:1.3.2


```


```
suztomo-macbookpro44% ../gradlew -v

------------------------------------------------------------
Gradle 6.5
------------------------------------------------------------

Build time:   2020-06-02 20:46:21 UTC
Revision:     a27f41e4ae5e8a41ab9b19f8dd6d86d7b384dad4

Kotlin:       1.3.72
Groovy:       2.5.11
Ant:          Apache Ant(TM) version 1.10.7 compiled on September 1 2019
JVM:          11.0.4 (Oracle Corporation 11.0.4+10-LTS)
OS:           Mac OS X 10.15.5 x86_64
```

## Gradle With Java 8

```
suztomo-macbookpro44% which java
/Library/Java/JavaVirtualMachines/jdk-8-latest/Contents/Home/bin/java
suztomo-macbookpro44% ../gradlew dependencies
```

The result remains the same. The tree does not have javax.annotation-api dependency directly below
`com.google.cloud:google-cloud-firestore:1.32.0`.


```
compileClasspath - Compile classpath for source set 'main'.
\--- com.google.cloud:google-cloud-firestore:1.32.0
     +--- com.google.cloud:google-cloud-core-grpc:1.91.3
     |    +--- com.google.auth:google-auth-library-credentials:0.18.0
     |    +--- com.google.cloud:google-cloud-core:1.91.3
     |    |    +--- com.google.api:gax:1.49.1 -> 1.51.0
     |    |    |    +--- com.google.guava:guava:28.1-android
     |    |    |    |    +--- com.google.guava:failureaccess:1.0.1
     |    |    |    |    +--- com.google.guava:listenablefuture:9999.0-empty-to-avoid-conflict-with-guava
     |    |    |    |    +--- com.google.code.findbugs:jsr305:3.0.2
     |    |    |    |    +--- org.checkerframework:checker-compat-qual:2.5.5
     |    |    |    |    +--- com.google.errorprone:error_prone_annotations:2.3.2 -> 2.3.3
     |    |    |    |    +--- com.google.j2objc:j2objc-annotations:1.3
     |    |    |    |    \--- org.codehaus.mojo:animal-sniffer-annotations:1.18
     |    |    |    +--- com.google.code.findbugs:jsr305:3.0.2
     |    |    |    +--- org.threeten:threetenbp:1.3.3 -> 1.4.0
     |    |    |    +--- com.google.auth:google-auth-library-oauth2-http:0.18.0
     |    |    |    |    +--- com.google.auto.value:auto-value-annotations:1.6.6
     |    |    |    |    +--- com.google.code.findbugs:jsr305:3.0.2
     |    |    |    |    +--- com.google.auth:google-auth-library-credentials:0.18.0
     |    |    |    |    +--- com.google.http-client:google-http-client:1.32.1
     |    |    |    |    |    +--- org.apache.httpcomponents:httpclient:4.5.10
     |    |    |    |    |    |    +--- org.apache.httpcomponents:httpcore:4.4.12
     |    |    |    |    |    |    +--- commons-logging:commons-logging:1.2
     |    |    |    |    |    |    \--- commons-codec:commons-codec:1.11
     |    |    |    |    |    +--- org.apache.httpcomponents:httpcore:4.4.12
     |    |    |    |    |    +--- com.google.code.findbugs:jsr305:3.0.2
     |    |    |    |    |    +--- com.google.guava:guava:28.1-android (*)
     |    |    |    |    |    +--- com.google.j2objc:j2objc-annotations:1.3
     |    |    |    |    |    +--- io.opencensus:opencensus-api:0.24.0
     |    |    |    |    |    |    \--- io.grpc:grpc-context:1.22.1 -> 1.25.0
     |    |    |    |    |    \--- io.opencensus:opencensus-contrib-http-util:0.24.0
     |    |    |    |    |         +--- io.opencensus:opencensus-api:0.24.0 (*)
     |    |    |    |    |         \--- com.google.guava:guava:26.0-android -> 28.1-android (*)
     |    |    |    |    +--- com.google.http-client:google-http-client-jackson2:1.32.1
     |    |    |    |    |    +--- com.google.http-client:google-http-client:1.32.1 (*)
     |    |    |    |    |    \--- com.fasterxml.jackson.core:jackson-core:2.9.9 -> 2.10.1
     |    |    |    |    \--- com.google.guava:guava:28.1-android (*)
     |    |    |    +--- com.google.api:api-common:1.8.1
     |    |    |    |    +--- com.google.code.findbugs:jsr305:3.0.2
     |    |    |    |    +--- com.google.guava:guava:26.0-android -> 28.1-android (*)
     |    |    |    |    \--- javax.annotation:javax.annotation-api:1.3.2
     |    |    |    \--- io.opencensus:opencensus-api:0.24.0 (*)
     |    |    +--- com.google.protobuf:protobuf-java-util:3.10.0 -> 3.11.1
     |    |    |    +--- com.google.protobuf:protobuf-java:3.11.1
     |    |    |    +--- com.google.guava:guava:28.1-android (*)
     |    |    |    +--- com.google.errorprone:error_prone_annotations:2.3.3
     |    |    |    \--- com.google.code.gson:gson:2.8.6
     |    |    +--- com.google.api.grpc:proto-google-common-protos:1.17.0
     |    |    |    \--- com.google.protobuf:protobuf-java:3.7.1 -> 3.11.1
     |    |    +--- com.google.api.grpc:proto-google-iam-v1:0.13.0
     |    |    |    +--- com.google.protobuf:protobuf-java:3.7.1 -> 3.11.1
     |    |    |    +--- com.google.api:api-common:1.8.1 (*)
     |    |    |    \--- com.google.api.grpc:proto-google-common-protos:1.16.0 -> 1.17.0 (*)
     |    |    +--- org.threeten:threetenbp:1.3.3 -> 1.4.0
     |    |    +--- com.google.api:api-common:1.8.1 (*)
     |    |    +--- com.google.auth:google-auth-library-credentials:0.18.0
     |    |    +--- com.google.auth:google-auth-library-oauth2-http:0.18.0 (*)
     |    |    +--- com.google.http-client:google-http-client:1.32.1 (*)
     |    |    +--- com.google.http-client:google-http-client-jackson2:1.32.1 (*)
     |    |    +--- com.google.protobuf:protobuf-java:3.10.0 -> 3.11.1
     |    |    \--- com.google.guava:guava:28.1-android (*)
     |    +--- com.google.guava:guava:28.1-android (*)
     |    +--- com.google.api:gax:1.49.1 -> 1.51.0 (*)
     |    +--- com.google.api:gax-grpc:1.49.1 -> 1.51.0
     |    |    +--- com.google.api:gax:1.51.0 (*)
     |    |    +--- io.grpc:grpc-stub:1.25.0
     |    |    |    \--- io.grpc:grpc-api:1.25.0
     |    |    |         +--- io.grpc:grpc-context:1.25.0
     |    |    |         +--- com.google.errorprone:error_prone_annotations:2.3.3
     |    |    |         +--- com.google.code.findbugs:jsr305:3.0.2
     |    |    |         +--- org.codehaus.mojo:animal-sniffer-annotations:1.17 -> 1.18
     |    |    |         \--- com.google.guava:guava:28.1-android (*)
     |    |    +--- io.grpc:grpc-auth:1.25.0
     |    |    |    +--- io.grpc:grpc-api:1.25.0 (*)
     |    |    |    \--- com.google.auth:google-auth-library-credentials:0.17.1 -> 0.18.0
     |    |    +--- io.grpc:grpc-protobuf:1.25.0
     |    |    |    +--- io.grpc:grpc-api:1.25.0 (*)
     |    |    |    +--- com.google.protobuf:protobuf-java:3.10.0 -> 3.11.1
     |    |    |    +--- com.google.guava:guava:28.1-android (*)
     |    |    |    +--- com.google.api.grpc:proto-google-common-protos:1.12.0 -> 1.17.0 (*)
     |    |    |    \--- io.grpc:grpc-protobuf-lite:1.25.0
     |    |    |         +--- io.grpc:grpc-api:1.25.0 (*)
     |    |    |         \--- com.google.guava:guava:28.1-android (*)
     |    |    +--- com.google.guava:guava:28.1-android (*)
     |    |    +--- com.google.code.findbugs:jsr305:3.0.2
     |    |    +--- org.threeten:threetenbp:1.3.3 -> 1.4.0
     |    |    +--- com.google.auth:google-auth-library-oauth2-http:0.18.0 (*)
     |    |    +--- com.google.auth:google-auth-library-credentials:0.18.0
     |    |    +--- com.google.api.grpc:proto-google-common-protos:1.15.0 -> 1.17.0 (*)
     |    |    +--- com.google.api:api-common:1.8.1 (*)
     |    |    +--- io.grpc:grpc-netty-shaded:1.25.0
     |    |    |    \--- io.grpc:grpc-core:1.25.0
     |    |    |         +--- io.grpc:grpc-api:1.25.0 (*)
     |    |    |         +--- com.google.code.gson:gson:2.8.5 -> 2.8.6
     |    |    |         +--- com.google.android:annotations:4.1.1.4
     |    |    |         +--- io.perfmark:perfmark-api:0.19.0
     |    |    |         |    +--- com.google.code.findbugs:jsr305:3.0.2
     |    |    |         |    \--- com.google.errorprone:error_prone_annotations:2.3.3
     |    |    |         +--- io.opencensus:opencensus-api:0.21.0 -> 0.24.0 (*)
     |    |    |         \--- io.opencensus:opencensus-contrib-grpc-metrics:0.21.0
     |    |    |              \--- io.opencensus:opencensus-api:0.21.0 -> 0.24.0 (*)
     |    |    \--- io.grpc:grpc-alts:1.25.0
     |    |         +--- io.grpc:grpc-grpclb:1.25.0
     |    |         |    +--- io.grpc:grpc-core:1.25.0 (*)
     |    |         |    +--- io.grpc:grpc-protobuf:1.25.0 (*)
     |    |         |    +--- io.grpc:grpc-stub:1.25.0 (*)
     |    |         |    +--- com.google.protobuf:protobuf-java:3.10.0 -> 3.11.1
     |    |         |    \--- com.google.protobuf:protobuf-java-util:3.10.0 -> 3.11.1 (*)
     |    |         +--- io.grpc:grpc-auth:1.25.0 (*)
     |    |         +--- io.grpc:grpc-core:1.25.0 (*)
     |    |         +--- io.grpc:grpc-netty-shaded:1.25.0 (*)
     |    |         +--- io.grpc:grpc-protobuf:1.25.0 (*)
     |    |         +--- io.grpc:grpc-stub:1.25.0 (*)
     |    |         +--- org.apache.commons:commons-lang3:3.5
     |    |         +--- com.google.protobuf:protobuf-java:3.10.0 -> 3.11.1
     |    |         +--- org.conscrypt:conscrypt-openjdk-uber:2.2.1
     |    |         \--- com.google.auth:google-auth-library-oauth2-http:0.17.1 -> 0.18.0 (*)
     |    +--- com.google.api:api-common:1.8.1 (*)
     |    +--- io.grpc:grpc-api:1.24.1 -> 1.25.0 (*)
     |    +--- io.grpc:grpc-core:1.24.1 -> 1.25.0 (*)
     |    \--- com.google.http-client:google-http-client:1.32.1 (*)
     +--- com.google.api.grpc:proto-google-cloud-firestore-admin-v1:1.32.0
     |    +--- com.google.protobuf:protobuf-java:3.11.1
     |    +--- com.google.api:api-common:1.8.1 (*)
     |    +--- com.google.api.grpc:proto-google-common-protos:1.17.0 (*)
     |    \--- com.google.guava:guava:28.1-android (*)
     +--- com.google.api.grpc:proto-google-cloud-firestore-v1:1.32.0
     |    +--- com.google.protobuf:protobuf-java:3.11.1
     |    +--- com.google.api:api-common:1.8.1 (*)
     |    +--- com.google.api.grpc:proto-google-common-protos:1.17.0 (*)
     |    \--- com.google.guava:guava:28.1-android (*)
     +--- com.google.api.grpc:proto-google-cloud-firestore-v1beta1:0.85.0
     |    +--- com.google.protobuf:protobuf-java:3.11.1
     |    +--- com.google.api:api-common:1.8.1 (*)
     |    +--- com.google.api.grpc:proto-google-common-protos:1.17.0 (*)
     |    \--- com.google.guava:guava:28.1-android (*)
     +--- com.google.auto.value:auto-value-annotations:${auto-value-annotation.version} -> 1.6.6
     +--- io.opencensus:opencensus-contrib-grpc-util:0.24.0
     |    +--- io.opencensus:opencensus-api:0.24.0 (*)
     |    \--- io.grpc:grpc-core:1.22.1 -> 1.25.0 (*)
     +--- com.google.code.findbugs:jsr305:3.0.2
     +--- com.google.api:api-common:1.8.1 (*)
     +--- io.grpc:grpc-protobuf:1.25.0 (*)
     +--- io.grpc:grpc-context:1.25.0
     +--- com.google.protobuf:protobuf-java:3.11.1
     +--- com.google.api.grpc:proto-google-common-protos:1.17.0 (*)
     +--- com.google.api:gax:1.51.0 (*)
     +--- io.grpc:grpc-api:1.25.0 (*)
     +--- com.google.api:gax-grpc:1.51.0 (*)
     +--- com.google.guava:guava:28.1-android (*)
     +--- org.threeten:threetenbp:1.4.0
     +--- io.grpc:grpc-stub:1.25.0 (*)
     +--- io.opencensus:opencensus-api:0.24.0 (*)
     +--- com.google.auth:google-auth-library-credentials:0.18.0
     +--- com.google.cloud:google-cloud-core:1.91.3 (*)
     +--- com.google.code.gson:gson:2.8.6
     +--- com.fasterxml.jackson.core:jackson-core:2.10.1
     +--- com.google.protobuf:protobuf-java-util:3.11.1 (*)
     \--- com.google.cloud:google-cloud-conformance-tests:0.0.1
          +--- com.google.protobuf:protobuf-java:3.10.0 -> 3.11.1
          +--- com.google.api.grpc:proto-google-cloud-firestore-v1:1.27.0 -> 1.32.0 (*)
          \--- com.google.api.grpc:proto-google-cloud-bigtable-v2:0.80.0
               +--- com.google.protobuf:protobuf-java:3.10.0 -> 3.11.1
               +--- com.google.api:api-common:1.8.1 (*)
               +--- com.google.api.grpc:proto-google-common-protos:1.17.0 (*)
               \--- javax.annotation:javax.annotation-api:1.3.2

```


# Maven's profile handling

Maven handles the profile as expected.

## Maven With Java 11

The tree does have the javax.annotation-api dependency directly below
`com.google.cloud:google-cloud-firestore:1.32.0`. This is because Maven respects
the profile that is activated for Java 9 and higher.


```
[INFO] --- maven-dependency-plugin:2.8:tree (default-cli) @ maven-profile-test ---
[INFO] suztomo:maven-profile-test:jar:0.1.0-SNAPSHOT
[INFO] \- com.google.cloud:google-cloud-firestore:jar:1.32.0:compile
[INFO]    +- com.google.cloud:google-cloud-core-grpc:jar:1.91.3:compile
[INFO]    |  \- com.google.http-client:google-http-client:jar:1.32.1:compile
[INFO]    |     +- org.apache.httpcomponents:httpclient:jar:4.5.10:compile
[INFO]    |     |  +- commons-logging:commons-logging:jar:1.2:compile
[INFO]    |     |  \- commons-codec:commons-codec:jar:1.11:compile
[INFO]    |     +- org.apache.httpcomponents:httpcore:jar:4.4.12:compile
[INFO]    |     \- io.opencensus:opencensus-contrib-http-util:jar:0.24.0:compile
[INFO]    +- com.google.api.grpc:proto-google-cloud-firestore-admin-v1:jar:1.32.0:compile
[INFO]    +- com.google.api.grpc:proto-google-cloud-firestore-v1:jar:1.32.0:compile
[INFO]    +- com.google.api.grpc:proto-google-cloud-firestore-v1beta1:jar:0.85.0:compile
[INFO]    +- com.google.auto.value:auto-value-annotations:jar:1.6.6:compile
[INFO]    +- io.opencensus:opencensus-contrib-grpc-util:jar:0.24.0:compile
[INFO]    +- com.google.code.findbugs:jsr305:jar:3.0.2:compile
[INFO]    +- com.google.api:api-common:jar:1.8.1:compile
[INFO]    +- io.grpc:grpc-protobuf:jar:1.25.0:compile
[INFO]    |  \- io.grpc:grpc-protobuf-lite:jar:1.25.0:compile
[INFO]    +- io.grpc:grpc-context:jar:1.25.0:compile
[INFO]    +- com.google.protobuf:protobuf-java:jar:3.11.1:compile
[INFO]    +- com.google.api.grpc:proto-google-common-protos:jar:1.17.0:compile
[INFO]    +- com.google.api:gax:jar:1.51.0:compile
[INFO]    |  \- com.google.auth:google-auth-library-oauth2-http:jar:0.18.0:compile
[INFO]    +- io.grpc:grpc-api:jar:1.25.0:compile
[INFO]    |  \- com.google.errorprone:error_prone_annotations:jar:2.3.3:compile
[INFO]    +- com.google.api:gax-grpc:jar:1.51.0:compile
[INFO]    |  +- io.grpc:grpc-auth:jar:1.25.0:compile
[INFO]    |  +- io.grpc:grpc-netty-shaded:jar:1.25.0:compile
[INFO]    |  |  \- io.grpc:grpc-core:jar:1.25.0:compile (version selected from constraint [1.25.0,1.25.0])
[INFO]    |  |     +- com.google.android:annotations:jar:4.1.1.4:compile
[INFO]    |  |     +- io.perfmark:perfmark-api:jar:0.19.0:compile
[INFO]    |  |     \- io.opencensus:opencensus-contrib-grpc-metrics:jar:0.21.0:compile
[INFO]    |  \- io.grpc:grpc-alts:jar:1.25.0:compile
[INFO]    |     +- io.grpc:grpc-grpclb:jar:1.25.0:compile
[INFO]    |     +- org.apache.commons:commons-lang3:jar:3.5:compile
[INFO]    |     \- org.conscrypt:conscrypt-openjdk-uber:jar:2.2.1:compile
[INFO]    +- com.google.guava:guava:jar:28.1-android:compile
[INFO]    |  +- com.google.guava:failureaccess:jar:1.0.1:compile
[INFO]    |  +- com.google.guava:listenablefuture:jar:9999.0-empty-to-avoid-conflict-with-guava:compile
[INFO]    |  +- org.checkerframework:checker-compat-qual:jar:2.5.5:compile
[INFO]    |  +- com.google.j2objc:j2objc-annotations:jar:1.3:compile
[INFO]    |  \- org.codehaus.mojo:animal-sniffer-annotations:jar:1.18:compile
[INFO]    +- org.threeten:threetenbp:jar:1.4.0:compile
[INFO]    +- io.grpc:grpc-stub:jar:1.25.0:compile
[INFO]    +- io.opencensus:opencensus-api:jar:0.24.0:compile
[INFO]    +- com.google.auth:google-auth-library-credentials:jar:0.18.0:compile
[INFO]    +- com.google.cloud:google-cloud-core:jar:1.91.3:compile
[INFO]    |  +- com.google.api.grpc:proto-google-iam-v1:jar:0.13.0:compile
[INFO]    |  \- com.google.http-client:google-http-client-jackson2:jar:1.32.1:compile
[INFO]    +- com.google.code.gson:gson:jar:2.8.6:compile
[INFO]    +- com.fasterxml.jackson.core:jackson-core:jar:2.10.1:compile
[INFO]    +- com.google.protobuf:protobuf-java-util:jar:3.11.1:compile
[INFO]    +- com.google.cloud:google-cloud-conformance-tests:jar:0.0.1:compile
[INFO]    |  \- com.google.api.grpc:proto-google-cloud-bigtable-v2:jar:0.80.0:compile
[INFO]    \- javax.annotation:javax.annotation-api:jar:1.3.2:compile
```

## Maven With Java 8

The dependency is not there because the profile is activated only if the JDK is
verison 9 or higher.

```
[INFO] --- maven-dependency-plugin:2.8:tree (default-cli) @ maven-profile-test ---
[INFO] suztomo:maven-profile-test:jar:0.1.0-SNAPSHOT
[INFO] \- com.google.cloud:google-cloud-firestore:jar:1.32.0:compile
[INFO]    +- com.google.cloud:google-cloud-core-grpc:jar:1.91.3:compile
[INFO]    |  \- com.google.http-client:google-http-client:jar:1.32.1:compile
[INFO]    |     +- org.apache.httpcomponents:httpclient:jar:4.5.10:compile
[INFO]    |     |  +- commons-logging:commons-logging:jar:1.2:compile
[INFO]    |     |  \- commons-codec:commons-codec:jar:1.11:compile
[INFO]    |     +- org.apache.httpcomponents:httpcore:jar:4.4.12:compile
[INFO]    |     \- io.opencensus:opencensus-contrib-http-util:jar:0.24.0:compile
[INFO]    +- com.google.api.grpc:proto-google-cloud-firestore-admin-v1:jar:1.32.0:compile
[INFO]    +- com.google.api.grpc:proto-google-cloud-firestore-v1:jar:1.32.0:compile
[INFO]    +- com.google.api.grpc:proto-google-cloud-firestore-v1beta1:jar:0.85.0:compile
[INFO]    +- com.google.auto.value:auto-value-annotations:jar:1.6.6:compile
[INFO]    +- io.opencensus:opencensus-contrib-grpc-util:jar:0.24.0:compile
[INFO]    +- com.google.code.findbugs:jsr305:jar:3.0.2:compile
[INFO]    +- com.google.api:api-common:jar:1.8.1:compile
[INFO]    |  \- javax.annotation:javax.annotation-api:jar:1.3.2:compile
[INFO]    +- io.grpc:grpc-protobuf:jar:1.25.0:compile
[INFO]    |  \- io.grpc:grpc-protobuf-lite:jar:1.25.0:compile
[INFO]    +- io.grpc:grpc-context:jar:1.25.0:compile
[INFO]    +- com.google.protobuf:protobuf-java:jar:3.11.1:compile
[INFO]    +- com.google.api.grpc:proto-google-common-protos:jar:1.17.0:compile
[INFO]    +- com.google.api:gax:jar:1.51.0:compile
[INFO]    |  \- com.google.auth:google-auth-library-oauth2-http:jar:0.18.0:compile
[INFO]    +- io.grpc:grpc-api:jar:1.25.0:compile
[INFO]    |  \- com.google.errorprone:error_prone_annotations:jar:2.3.3:compile
[INFO]    +- com.google.api:gax-grpc:jar:1.51.0:compile
[INFO]    |  +- io.grpc:grpc-auth:jar:1.25.0:compile
[INFO]    |  +- io.grpc:grpc-netty-shaded:jar:1.25.0:compile
[INFO]    |  |  \- io.grpc:grpc-core:jar:1.25.0:compile (version selected from constraint [1.25.0,1.25.0])
[INFO]    |  |     +- com.google.android:annotations:jar:4.1.1.4:compile
[INFO]    |  |     +- io.perfmark:perfmark-api:jar:0.19.0:compile
[INFO]    |  |     \- io.opencensus:opencensus-contrib-grpc-metrics:jar:0.21.0:compile
[INFO]    |  \- io.grpc:grpc-alts:jar:1.25.0:compile
[INFO]    |     +- io.grpc:grpc-grpclb:jar:1.25.0:compile
[INFO]    |     +- org.apache.commons:commons-lang3:jar:3.5:compile
[INFO]    |     \- org.conscrypt:conscrypt-openjdk-uber:jar:2.2.1:compile
[INFO]    +- com.google.guava:guava:jar:28.1-android:compile
[INFO]    |  +- com.google.guava:failureaccess:jar:1.0.1:compile
[INFO]    |  +- com.google.guava:listenablefuture:jar:9999.0-empty-to-avoid-conflict-with-guava:compile
[INFO]    |  +- org.checkerframework:checker-compat-qual:jar:2.5.5:compile
[INFO]    |  +- com.google.j2objc:j2objc-annotations:jar:1.3:compile
[INFO]    |  \- org.codehaus.mojo:animal-sniffer-annotations:jar:1.18:compile
[INFO]    +- org.threeten:threetenbp:jar:1.4.0:compile
[INFO]    +- io.grpc:grpc-stub:jar:1.25.0:compile
[INFO]    +- io.opencensus:opencensus-api:jar:0.24.0:compile
[INFO]    +- com.google.auth:google-auth-library-credentials:jar:0.18.0:compile
[INFO]    +- com.google.cloud:google-cloud-core:jar:1.91.3:compile
[INFO]    |  +- com.google.api.grpc:proto-google-iam-v1:jar:0.13.0:compile
[INFO]    |  \- com.google.http-client:google-http-client-jackson2:jar:1.32.1:compile
[INFO]    +- com.google.code.gson:gson:jar:2.8.6:compile
[INFO]    +- com.fasterxml.jackson.core:jackson-core:jar:2.10.1:compile
[INFO]    +- com.google.protobuf:protobuf-java-util:jar:3.11.1:compile
[INFO]    \- com.google.cloud:google-cloud-conformance-tests:jar:0.0.1:compile
[INFO]       \- com.google.api.grpc:proto-google-cloud-bigtable-v2:jar:0.80.0:compile
```
