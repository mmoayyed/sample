CAS Overlay Template 
=======================

CAS WAR overlay.

# Versions

- CAS `6.2.x`
- JDK `11`

# Overview

To build the project, use:

```bash
./gradlew[.bat] clean build
```

To run the project:

```bash
java -jar build/libs/cas.war
```

# Services

- The `build.gradle` file includes the JSON service registry to load services from JSON files:

```groovy
 implementation "org.apereo.cas:cas-server-support-json-service-registry:${casServerVersion}"
```

- Create directory: `mkdir -p /etc/cas/config/services`

- Create `/etc/cas/config/services/Sample-100.json`:

```json
{
    "@class": "org.apereo.cas.services.RegexRegisteredService",
    "serviceId": "https://www.google.com.*",
    "name": "Sample",
    "id": 100,
    "description": "Sample CASified application",
    "evaluationOrder": 10
}
```

- Specify the path to the directory in your `cas.properties` file:

```
cas.service-registry.json.location=file:/etc/cas/config/services
```

Note that by default, `cas.properties` is expected at `/etc/cas/config/cas.properties`.

When you run the system, you should see similar statements in the logs:

```
<Configuration files found at [/etc/cas/config] are [[file [/etc/cas/config/application.yml], file [/etc/cas/config/cas.properties]...
...
<Watching directory path at [/private/etc/cas/config/services]>
...
<Loaded [1] service(s) from [JsonServiceRegistry].>
```