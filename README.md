# ili2c-native

## TODO / Fragen

- Besser aus einem Release herstellen. Bestehende resource-config.json? Wir auch mit dem Agent hergestellt, oder?
- ...

## Ablauf
Java: Liberica NIK 22.2.r11-nik

```
./gradlew bindist -x test -x usrdoc
```

Zipfile entpacken.


Zusätzliche Config für Native-Image mittels Agent erzeugen:

```
java -agentlib:native-image-agent=config-output-dir=conf-dir -jar dist/ili2c-tool-5.3.1-SNAPSHOT/ili2c.jar

java -agentlib:native-image-agent=config-output-dir=conf-dir-macos -jar /Users/stefan/Downloads/ili2c-5.3.0/ili2c.jar
```

```
native-image -Djava.awt.headless=false --enable-url-protocols=http,https --no-fallback -H:ReflectionConfigurationFiles=conf-dir/reflect-config.json -H:ResourceConfigurationFiles=conf-dir/resource-config.json -jar dist/ili2c-tool-5.3.1-SNAPSHOT/ili2c.jar ili2c

native-image -Djava.awt.headless=false --enable-url-protocols=http,https --no-fallback -H:ReflectionConfigurationFiles=conf-dir/reflect-config.json -H:ResourceConfigurationFiles=conf-dir/resource-config.json -jar /Users/stefan/Downloads/ili2c-5.3.0/ili2c.jar ili2c
```



Vgl ilivalidator:

native-image -Djava.awt.headless=false --enable-url-protocols=http,https --no-fallback -H:Class=org.interlis2.validator.Main -H:CLibraryPath=/Users/stefan/.sdkman/candidates/java/22.2.r11-nik/lib/svm/clibraries/darwin-aarch64 -H:ReflectionConfigurationFiles=conf-dir/reflect-config.json -H:ResourceConfigurationFiles=/Users/stefan/sources/ilivalidator-native/build/native/generated/generateResourcesConfigFile,/Users/stefan/sources/ilivalidator-native/resources/META-INF/native-image,/Users/stefan/sources/ilivalidator-native/conf-dir -cp /Users/stefan/Downloads/ilivalidator-1.12.0/antlr-2.7.7.jar:/Users/stefan/Downloads/ilivalidator-1.12.0/base64-2.3.9.jar:/Users/stefan/Downloads/ilivalidator-1.12.0/ehibasics-1.4.1.jar:/Users/stefan/Downloads/ilivalidator-1.12.0/ili2c-core-5.2.8.jar:/Users/stefan/Downloads/ilivalidator-1.12.0/ili2c-tool-5.2.8.jar:/Users/stefan/Downloads/ilivalidator-1.12.0/iox-api-1.0.4.jar:/Users/stefan/Downloads/ilivalidator-1.12.0/iox-ili-1.21.12.jar:/Users/stefan/Downloads/ilivalidator-1.12.0/jts-core-1.14.0.jar -jar /Users/stefan/Downloads/ilivalidator-1.12.0/ilivalidator-1.12.0.jar --verbose ilivalidator
