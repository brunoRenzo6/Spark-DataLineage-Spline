# Scala Build Tools e Fat JARs

Para rodar projetos e scripts em um cluster, é necessário que todas as dependências estejam acessíveis, Fat JARs são uma alternativa. Uber-JAR ou Fat-JAR, é um JAR file que além de conter o programa Java, inclui também todas as dependências do projeto.

Uma boa ferramenta para gerar Fat Jars é o SBT, uma ferramenta de construção de código aberto para projetos Scala e Java, semelhante ao Maven e Ant do Java.


### Crie um projeto SBT [sbt-by-example](https://www.scala-sbt.org/1.x/docs/sbt-by-example.html)

* Lembre-se de definir a versão do scala 

### Adicione o plugin sbt-assembly

* Crie um arquivo assembly.sbt dentro da pasta project/, desta forma:



	```
	├── src/
	└── project/
	    └── assembly.sbt
  	```
        
* Adicione essa linha ao arquivo assembly.sbt
	```
	resolvers += Resolver.bintrayIvyRepo("com.eed3si9n", "sbt-plugins")
	addSbtPlugin("com.eed3si9n" % "sbt-assembly" % "0.14.2")
	```
	
* Defina as dependências a serem adicionadas no arquivo build.sbt
	```
	libraryDependencies += "za.co.absa.spline" % "spline-core" % "0.3.1"
	libraryDependencies += "za.co.absa.spline" % "spline-persistence-mongo" % "0.3.1"
	libraryDependencies += "za.co.absa.spline" % "spline-core-spark-adapter-2.3" % "0.3.1"
	libraryDependencies += "za.co.absa.spline" % "spline-persistence-atlas" % "0.3.1"
	```
    
* Depois disso você pode rodar o comando  `$ sbt assembly` e um JAR com todas as dependências (O famoso Fat JAR) vai ser gerado para você.
    
* <strong>Throubleshooting</strong>: "deduplicate: different file contents found in the following:"

	Esse é um erro muito comum quando estamos incluindo as dependências do projeto, temos que passar uma denifinição para o sbt-assembly de como resolver esse erro (configurar o build.sbt).
    
    `assemblyMergeStrategy Python2.0 :`
    
```python
  assemblyMergeStrategy in assembly := {
  case PathList(ps @ _*) if ps.last contains "git.properties" => MergeStrategy.first
  case PathList("org","aopalliance", xs @ _*) => MergeStrategy.last
  case PathList("javax", "inject", xs @ _*) => MergeStrategy.last
  case PathList("javax", "servlet", xs @ _*) => MergeStrategy.last
  case PathList("javax", "activation", xs @ _*) => MergeStrategy.last
  case PathList("org", "apache", xs @ _*) => MergeStrategy.last
  case PathList("com", "google", xs @ _*) => MergeStrategy.last
  case PathList("com", "esotericsoftware", xs @ _*) => MergeStrategy.last
  case PathList("com", "codahale", xs @ _*) => MergeStrategy.last
  case PathList("com", "yammer", xs @ _*) => MergeStrategy.last
  case "about.html" => MergeStrategy.rename
  case "META-INF/ECLIPSEF.RSA" => MergeStrategy.last
  case "META-INF/mailcap" => MergeStrategy.last
  case "META-INF/mimetypes.default" => MergeStrategy.last
  case "plugin.properties" => MergeStrategy.last
  case "log4j.properties" => MergeStrategy.last
  case x =>
    val oldStrategy = (assemblyMergeStrategy in assembly).value
    oldStrategy(x)
}
```

#### Referências

[SBT by Example](https://www.scala-sbt.org/1.0/docs/sbt-by-example.html "SBT by Example")
