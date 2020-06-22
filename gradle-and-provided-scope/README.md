# Provided Scope

`com.google.http-client:google-http-client-appengine:1.35.0` has a dependency of
`com.google.appengine:appengine-api-1.0-sdk:1.9.71` with provided scope.

Gradle does not fetch the provided-scope dependency.

```
compileClasspath - Compile classpath for source set 'main'.
\--- com.google.http-client:google-http-client-appengine:1.35.0
     \--- com.google.http-client:google-http-client:1.35.0
          +--- org.apache.httpcomponents:httpclient:4.5.12
          |    +--- org.apache.httpcomponents:httpcore:4.4.13
          |    +--- commons-logging:commons-logging:1.2
          |    \--- commons-codec:commons-codec:1.11
          +--- org.apache.httpcomponents:httpcore:4.4.13
          +--- com.google.code.findbugs:jsr305:3.0.2
          +--- com.google.guava:guava:29.0-android
          |    +--- com.google.guava:failureaccess:1.0.1
          |    +--- com.google.guava:listenablefuture:9999.0-empty-to-avoid-conflict-with-guava
          |    +--- com.google.code.findbugs:jsr305:3.0.2
          |    +--- org.checkerframework:checker-compat-qual:2.5.5
          |    +--- com.google.errorprone:error_prone_annotations:2.3.4
          |    \--- com.google.j2objc:j2objc-annotations:1.3
          +--- com.google.j2objc:j2objc-annotations:1.3
          +--- io.opencensus:opencensus-api:0.24.0
          |    \--- io.grpc:grpc-context:1.22.1
          \--- io.opencensus:opencensus-contrib-http-util:0.24.0
               +--- io.opencensus:opencensus-api:0.24.0 (*)
               \--- com.google.guava:guava:26.0-android -> 29.0-android (*)
```

