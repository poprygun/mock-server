# Static Mock Server

**All Map data is mocked and limited to few tiles.**

Create or modify stubbed responses in `/mappings` diretory.

## Download latest copy of wiremock standalone

```bash
wget http://repo1.maven.org/maven2/com/github/tomakehurst/wiremock-standalone/2.24.1/wiremock-standalone-2.24.1.jar -O lib/wiremock-standalone.jar
```

## To create a new stub

Post json to `http://mock-server.cfapps.io/__admin/mappings/new`

```bash
echo '{"request":{"method":"GET","url":"/some/comrade"},"response":{"status":200,"body":"{\"name\": \"John Doe\", \"last name\":\"Doe the 2nd\"}","headers":{"Content-Type":"application/json"}}}' | http post http://mock-server.cfapps.io/__admin/mappings/new
```

## To test locally

```bash
java -jar lib/wiremock-standalone.jar --port 8081

http GET  http://localhost:8081/anything Cache-Control:no-cache
```

## Package and push to PCF

```bash
zip -r -X wiremock-standalone.zip bin lib mappings
cf push
```

## Test deployed server

```bash
http get http://mock-server.cfapps.io/anything Cache-Control:no-cache
```