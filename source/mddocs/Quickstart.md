# Quickstart

## Installation

### Gradle Setting

Add repo setting:

```groovy
repositories {
    maven {
        url  "https://dl.bintray.com/ki5fpl/tronj"
    }
}
```

Then add `abi` as dependency.

```groovy
dependencies {
    ....

    implementation 'com.github.ki5fpl.tronj:abi:0.4.0'
    implementation 'com.github.ki5fpl.tronj:client:0.4.0'

    ....
}
```

###Maven Settings

Use maven repo setting from Bintray.

```xml
<dependency>
  <groupId>com.github.ki5fpl.tronj</groupId>
  <artifactId>abi</artifactId>
  <version>0.4.0</version>
  <type>pom</type>
</dependency>
```

## Using Tronj

### Choose net from **main net**, **shasta** or **nile**

```java
TronClient client = ofMainnet("your private key");
// TronClient client = ofShasta("your private key");
// TronClient client = ofNile("your private key");
```

Aftre binding your private key with the `TronClient` object, your are ready to build, sign and broadcast your transactions.



