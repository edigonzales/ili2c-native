# ili2c-native

## TODO / Fragen

- Besser aus einem Release herstellen. Bestehende resource-config.json? Wir auch mit dem Agent hergestellt, oder?

## Ablauf
Java: Liberica NIK 22.2.r11-nik

```
./gradlew bindist -x test -x usrdoc
```

Zipfile entpacken.


Zusätzliche Config für Native-Image mittels Agent erzeugen:

```
java -agentlib:native-image-agent=config-output-dir=conf-dir -jar dist/ili2c-tool-5.3.1-SNAPSHOT/ili2c.jar

java -agentlib:native-image-agent=config-output-dir=conf-dir -jar /Users/stefan/Downloads/ili2c-5.3.0/ili2c.jar
```

```
native-image -Djava.awt.headless=false --enable-url-protocols=http,https --no-fallback -H:ReflectionConfigurationFiles=conf-dir/reflect-config.json -H:ResourceConfigurationFiles=conf-dir/resource-config.json -jar dist/ili2c-tool-5.3.1-SNAPSHOT/ili2c.jar ili2c

native-image -Djava.awt.headless=false --enable-url-protocols=http,https --no-fallback -H:ReflectionConfigurationFiles=conf-dir/reflect-config.json -H:ResourceConfigurationFiles=conf-dir/resource-config.json -jar /Users/stefan/Downloads/ili2c-5.3.0/ili2c.jar ili2c
```