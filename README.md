# play-json-extra

[![Scala.js](https://www.scala-js.org/assets/badges/scalajs-1.5.0.svg)](https://www.scala-js.org)
[![scaladoc](https://javadoc.io/badge2/com.github.xuwei-k/play-json-extra_2.13/javadoc.svg)](https://javadoc.io/doc/com.github.xuwei-k/play-json-extra_2.13/latest/play/jsonext/index.html)

- [Maven Central Repository Search](https://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.github.xuwei-k%22%20AND%20a%3A%22play-json-extra_2.12%22)
- [Maven Central](https://repo1.maven.org/maven2/com/github/xuwei-k/play-json-extra_2.12/)

### motivation and example

I think following way is so verbose.

```scala
import play.api.libs.json._
import play.api.libs.functional.syntax._

final case class User(id: Long, name: String)

object User {
  implicit val format: OFormat[User] = (
    (__ \ "id").format[Long] and // I want to omit `Long` and `String`
    (__ \ "name").format[String]
  )(apply _, Function.unlift(unapply))
}
```

[Play provides Json macros](https://www.playframework.com/documentation/2.8.x/ScalaJsonAutomated). Yes it is useful, but I want to **specify Json keys explicitly** sometime like [argonaut casecodecN](https://github.com/argonaut-io/argonaut/blob/v6.2/argonaut/jvm/src/test/scala/argonaut/example/JsonExample.scala#L25)

```scala
import play.api.libs.json._
import play.jsonext._

final case class User(id: Long, name: String)

object User {
  implicit val format: OFormat[User] =
    CaseClassFormats(apply _, unapply _)("id", "name")
}
```

### latest stable version for play-json 2.8

```scala
libraryDependencies += "com.github.xuwei-k" %% "play-json-extra" % "0.10.0"
```

for scala-js

```scala
libraryDependencies += "com.github.xuwei-k" %%% "play-json-extra" % "0.10.0"
```

- [API Documentation](https://oss.sonatype.org/service/local/repositories/releases/archive/com/github/xuwei-k/play-json-extra_2.12/0.10.0/play-json-extra_2.12-0.10.0-javadoc.jar/!/index.html)
