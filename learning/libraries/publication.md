# Публикация

:::danger
Данная статья находится в разработке!
:::

:::caution
Набор целевых платформ определяется автором мультиплатформенной библиотеки, и они должны предоставлять все реализации конкретной платформы для данной библиотеки. 

Добавление новых целей для мультиплатформенной библиотеки со стороны потребителя не поддерживается.
:::

## Maven

Библиотека, созданная из многоплатформенного проекта, может быть опубликована в репозитории Maven с плагином Gradle `maven-publish`, который может применяться следующим образом:

```kotlin
plugins {
    // ...
    id 'maven-publish'
}
```

При применении данного плагина публикации по умолчанию создаются для каждой из целей, которая может быть создана на текущем хосте. Увидеть это можно, заглянув в [IceRock Moko Maven репозиторий](https://repo1.maven.org/maven2/dev/icerock/moko/):

![moko-maven-rep](publication/publication-moko-rep.png)

Это требует задания в проекте `group` и `version`:

```kotlin
//  build.gradle.kts
group = "dev.icerock.moko"
version = libs.versions.mokoUnitsVersion.get()
```

```bash
#   libs.versions.toml
# ...
mokoUnitsVersion = "0.6.2"
```

Идентификаторы артефакта по умолчанию следуют шаблону `<projName>-<targetName>`, например, `units-iosx64` для цели, названной `iosx64` в проекте `units`.

Кроме того, по умолчанию добавляется дополнительная публикация, содержащая сериализованные объявления Kotlin и используемая IDE для анализа мультиплатформенных библиотек.

По умолчанию в каждую публикацию добавляется исходный код JAR, а также его главный артефакт. Исходные коды JAR содержат исходные коды, используемые при компиляции цели main:

![units-main](publication/publication-units-main.png)

## Материалы

- [Документация - Gradle Maven Publishig](https://docs.gradle.org/current/userguide/publishing_maven.html)
- [Документация Kotlin Lang - Publish a multiplatform library](https://kotlinlang.org/docs/mpp-publish-lib.html)