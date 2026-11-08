# Verificación local Android — AV2

Revisión del 08/11/2026 sobre la base `922361d`. El cliente declara `minSdk = 24` y utiliza `java.time`, pero no habilitaba core library desugaring. Android Lint detectó 55 errores `NewApi`.

Se habilita desugaring en `compileOptions` y se añade `desugar_jdk_libs:2.1.5` mediante el catálogo de versiones. La corrección mantiene el mínimo Android declarado; no oculta errores con una baseline ni desactiva comprobaciones.

## Repetir la verificación

Con JDK 21, SDK Android instalado y `ANDROID_HOME` configurado:

```text
./gradlew --no-daemon lintDebug testDebugUnitTest assembleDebug
```

En Windows se utiliza `gradlew.bat`. El wrapper fija Gradle 9.4.1 y el módulo utiliza compile SDK 36.1.

El workflow `Android verification` repite esos comandos en PR y push a `develop`/`main` y conserva los informes y el APK debug como artifacts.

Los reportes locales y el conteo de advertencias se incorporan al informe AV2. La prueba unitaria existente es una prueba de ejemplo; su aprobación no acredita los flujos de paciente. El APK generado tampoco sustituye la instalación, el recorrido integrado ni la validación con usuarios.

Referencia de implementación: [Android Developers — library desugaring](https://developer.android.com/studio/write/java8-support#library-desugaring) y [changelog oficial de desugar_jdk_libs](https://github.com/google/desugar_jdk_libs/blob/master/CHANGELOG.md).
