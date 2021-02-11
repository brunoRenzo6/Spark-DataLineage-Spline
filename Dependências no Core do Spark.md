# Dependências no Core do Spark

O JAR completo nada mais é que um JAR criado a partir do código Scala conforme [apresentado aqui](https://github.com/WilliamPorto/keyruslab-spline/blob/master/FatJAR.md "apresentado aqui") com todas as dependências necessárias.

A novidade é que é possível gerar um JAR sem dependências, a pergunta é: É possível gerar o JAR do SPLINE sem dependência?
Resposta: Não.

O código que é feito em Scala utiliza o SPLINE, uma biblioteca externa, por ser uma biblioteca externa é preciso que sua dependência seja baixada: Então como é possível gerar o JAR sem as dependências?

Na verdade, você gerará um JAR pequeno, que contenha apenas o código feito em Scala, mas como as dependências são necessárias para o Spark entender o que seu código está utilizando, é preciso baixar todas as dependências do SPLINE que será utilizado e mais as dependências das dependências do SPLINE, tudo isso manualmente.

__Desvantagem__: Será preciso fazer tudo manualmente, desnecessário já que o Maven serve para isso.

__Vantagem__: Apenas as dependências necessárias serão utilizadas, evitando dependências desnecessárias conforme os imports utilizados no Scala. Preparação do ambiente definitivo, já que as dependências ficarão diretamente no core do Spark. Tudo está prontinho abaixo apenas para baixar e copiar para a pasta específica.

* [spline-commons-0.3.1.jar](https://search.maven.org/remotecontent?filepath=za/co/absa/spline/spline-commons/0.3.1/spline-commons-0.3.1.jar "Baixar Agora")
* [spline-core-0.3.1.jar](https://search.maven.org/remotecontent?filepath=za/co/absa/spline/spline-core/0.3.1/spline-core-0.3.1.jar "Baixar Agora")
* [spline-core-spark-adapter-api-0.3.1.jar](https://search.maven.org/remotecontent?filepath=za/co/absa/spline/spline-core-spark-adapter-api/0.3.1/spline-core-spark-adapter-api-0.3.1.jar "Baixar Agora")
* [spline-core-spark-adapter-2.2-0.3.1.jar](https://search.maven.org/remotecontent?filepath=za/co/absa/spline/spline-core-spark-adapter-2.2/0.3.1/spline-core-spark-adapter-2.2-0.3.1.jar "Baixar Agora") ou [spline-core-spark-adapter-2.3-0.3.1.jar](https://search.maven.org/remotecontent?filepath=za/co/absa/spline/spline-core-spark-adapter-2.3/0.3.1/spline-core-spark-adapter-2.3-0.3.1.jar "Baixar Agora") (De acordo com a versão do Spark)
* [spline-model-0.3.1.jar](https://search.maven.org/remotecontent?filepath=za/co/absa/spline/spline-model/0.3.1/spline-model-0.3.1.jar "Baixar Agora")
* [spline-persistence-api-0.3.1.jar](https://search.maven.org/remotecontent?filepath=za/co/absa/spline/spline-persistence-api/0.3.1/spline-persistence-api-0.3.1.jar "Baixar Agora")
* [spline-persistence-hdfs-0.3.1.jar](https://search.maven.org/remotecontent?filepath=za/co/absa/spline/spline-persistence-hdfs/0.3.1/spline-persistence-hdfs-0.3.1.jar "Baixar Agora")
* [spline-persistence-mongo-0.3.1.jar](https://search.maven.org/remotecontent?filepath=za/co/absa/spline/spline-persistence-mongo/0.3.1/spline-persistence-mongo-0.3.1.jar "Baixar Agora")
* [spline-persistence-atlas-0.3.1.jar](https://search.maven.org/remotecontent?filepath=za/co/absa/spline/spline-persistence-atlas/0.3.1/spline-persistence-atlas-0.3.1.jar "Baixar Agora")
* [atlas-notification-0.8.2.jar](https://search.maven.org/remotecontent?filepath=org/apache/atlas/atlas-notification/0.8.2/atlas-notification-0.8.2.jar "Baixar Agora")
* [atlas-typesystem-0.8.2.jar](https://search.maven.org/remotecontent?filepath=org/apache/atlas/atlas-typesystem/0.8.2/atlas-typesystem-0.8.2.jar "Baixar Agora")
* [atlas-common-0.8.2.jar](https://search.maven.org/remotecontent?filepath=org/apache/atlas/atlas-common/0.8.2/atlas-common-0.8.2.jar "Baixar Agora")
* [atlas-intg-0.8.2.jar](https://search.maven.org/remotecontent?filepath=org/apache/atlas/atlas-intg/0.8.2/atlas-intg-0.8.2.jar "Baixar Agora")
* [json4s-native_2.11-3.2.11.jar](https://search.maven.org/remotecontent?filepath=org/json4s/json4s-native_2.11/3.2.11/json4s-native_2.11-3.2.11.jar "Baixar Agora")
* [slf4s-api_2.11-1.7.25.jar](https://search.maven.org/remotecontent?filepath=org/slf4s/slf4s-api_2.11/1.7.25/slf4s-api_2.11-1.7.25.jar "Baixar Agora")
* [jettison-1.3.7.jar](https://search.maven.org/remotecontent?filepath=org/codehaus/jettison/jettison/1.3.7/jettison-1.3.7.jar "Baixar Agora")
* [mongo-java-driver-3.2.2.jar](https://search.maven.org/remotecontent?filepath=org/mongodb/mongo-java-driver/3.2.2/mongo-java-driver-3.2.2.jar "Baixar Agora")
* [casbah-commons_2.11-3.1.1.jar](https://search.maven.org/remotecontent?filepath=org/mongodb/casbah-commons_2.11/3.1.1/casbah-commons_2.11-3.1.1.jar "Baixar Agora")
* [casbah-core_2.11-3.1.1.jar](https://search.maven.org/remotecontent?filepath=org/mongodb/casbah-core_2.11/3.1.1/casbah-core_2.11-3.1.1.jar "Baixar Agora")
* [casbah-query_2.11-3.1.1.jar](https://search.maven.org/remotecontent?filepath=org/mongodb/casbah-query_2.11/3.1.1/casbah-query_2.11-3.1.1.jar "Baixar Agora")
* [salat-core_2.11-1.11.2.jar](https://search.maven.org/remotecontent?filepath=com/github/salat/salat-core_2.11/1.11.2/salat-core_2.11-1.11.2.jar "Baixar Agora")
* [salat-util_2.11-1.11.2.jar](https://search.maven.org/remotecontent?filepath=com/github/salat/salat-util_2.11/1.11.2/salat-util_2.11-1.11.2.jar "Baixar Agora")
* [joda-time-2.3.jar](https://search.maven.org/remotecontent?filepath=joda-time/joda-time/2.3/joda-time-2.3.jar "Baixar Agora")
* [json4s-ext_2.11-3.2.11.jar](https://search.maven.org/remotecontent?filepath=org/json4s/json4s-ext_2.11/3.2.11/json4s-ext_2.11-3.2.11.jar "Baixar Agora")
* [kafka-clients-1.1.0.jar](https://search.maven.org/remotecontent?filepath=org/apache/kafka/kafka-clients/1.1.0/kafka-clients-1.1.0.jar "Baixar Agora")
* [spline-sample-0.3.1.jar](https://search.maven.org/remotecontent?filepath=za/co/absa/spline/spline-sample/0.3.1/spline-sample-0.3.1.jar "Baixar Agora")

Com essas dependências mais o JAR feito em Scala, copiado dentro do core do Spark, tudo funcionará, qualquer tipo de persistência, bastando apenas que você envie as propriedades necessárias no ```spark-submit``` de acordo com [esse documento](https://github.com/WilliamPorto/keyruslab-spline/blob/master/Persist%C3%AAncia.md "esse documento"), mas um detalhe, agora não é preciso colocar a parte ```--jars nome_do_jar_completo.jar``` pois seus JARs já estarão dentro do core do Spark e serão compilados tudo dentro do Spark Context ao executar o ```spark-submit```.

Desfrute do seu SPLINE apenas enviando o Script em Python, lembrando que seu Script em Python precisa chamar o método do Scala para habilitar o SPLINE. Observe uma chamada para persistir os dados no MongoDB depois desse processo:

```
spark-submit --conf "spark.driver.extraJavaOptions=-Dspline.mode=BEST_EFFORT -Dspline.persistence.factory=za.co.absa.spline.persistence.mongo.MongoPersistenceFactory -Dspline.mongodb.url=mongodb://caminho_do_banco:porta_do_banco -Dspline.mongodb.name=nome_do_banco" script_pyspark.py
```

ou

```
spark-submit --driver-java-options "-Dspline.mode=BEST_EFFORT -Dspline.persistence.factory=za.co.absa.spline.persistence.mongo.MongoPersistenceFactory -Dspline.mongodb.url=mongodb://caminho_do_banco:porta_do_banco -Dspline.mongodb.name=nome_do_banco" script_pyspark.py
```

> Utilizado: -Dspline.mongodb.url=mongodb://127.0.0.1:27017 -Dspline.mongodb.name=db_spline

Provavelmente você teria 3 perguntas básicas, pois eu teria:

1. Se algum link não funcionar, como eu poderei buscar por conta própria as dependências? Resposta: Acesse o [Search Maven](https://search.maven.org/ "Search Maven") e busque qualquer dependência, lembrando que as do SPLINE são específicas, então, não fugirá do que está a cima, ao encontrar a dependência o site disponibilizará várias formas de download, incluindo o JAR. Pensando em possíveis problemas, [guardamos no repositório](https://github.com/WilliamPorto/keyruslab-spline/tree/master/Downloads "guardamos no repositório") para você.

2. Porque todas as dependências do SPLINE foram utilizadas na versão 0.3.1? Resposta: Isso [foi explicado aqui](https://github.com/WilliamPorto/keyruslab-spline/blob/master/Persist%C3%AAncia.md "foi explicado aqui").

3. Aonde eu coloco todos esses JARs baixados? Resposta: Talvez a pergunta mais importante, é claro, precisamos colocar em algum local, esse local deve ser o core do Spark, é necessário que você encontre a pasta de JARs que fica dentro da instalação do seu Spark e colar lá junto com os vários outros JARs que já estão lá, abaixo será mostrado o meu caso, talvez sirva para você:

```
cp /root/JARs/spline-commons-0.3.1.jar /usr/hdp/current/spark2-client/jars/spline-commons-0.3.1.jar
cp /root/JARs/spline-core-0.3.1.jar /usr/hdp/current/spark2-client/jars/spline-core-0.3.1.jar
cp /root/JARs/spline-core-spark-adapter-api-0.3.1.jar /usr/hdp/current/spark2-client/jars/spline-core-spark-adapter-api-0.3.1.jar
cp /root/JARs/spline-core-spark-adapter-2.3-0.3.1.jar /usr/hdp/current/spark2-client/jars/spline-core-spark-adapter-2.3-0.3.1.jar
cp /root/JARs/spline-model-0.3.1.jar /usr/hdp/current/spark2-client/jars/spline-model-0.3.1.jar
cp /root/JARs/spline-persistence-api-0.3.1.jar /usr/hdp/current/spark2-client/jars/spline-persistence-api-0.3.1.jar
cp /root/JARs/spline-persistence-hdfs-0.3.1.jar /usr/hdp/current/spark2-client/jars/spline-persistence-hdfs-0.3.1.jar
cp /root/JARs/spline-persistence-mongo-0.3.1.jar /usr/hdp/current/spark2-client/jars/spline-persistence-mongo-0.3.1.jar
cp /root/JARs/spline-persistence-atlas-0.3.1.jar /usr/hdp/current/spark2-client/jars/spline-persistence-atlas-0.3.1.jar
cp /root/JARs/atlas-notification-0.8.2.jar /usr/hdp/current/spark2-client/jars/atlas-notification-0.8.2.jar
cp /root/JARs/atlas-typesystem-0.8.2.jar /usr/hdp/current/spark2-client/jars/atlas-typesystem-0.8.2.jar
cp /root/JARs/atlas-common-0.8.2.jar /usr/hdp/current/spark2-client/jars/atlas-common-0.8.2.jar
cp /root/JARs/atlas-intg-0.8.2.jar /usr/hdp/current/spark2-client/jars/atlas-intg-0.8.2.jar
cp /root/JARs/json4s-native_2.11-3.2.11.jar /usr/hdp/current/spark2-client/jars/json4s-native_2.11-3.2.11.jar
cp /root/JARs/slf4s-api_2.11-1.7.25.jar /usr/hdp/current/spark2-client/jars/slf4s-api_2.11-1.7.25.jar
cp /root/JARs/jettison-1.3.7.jar /usr/hdp/current/spark2-client/jars/jettison-1.3.7.jar
cp /root/JARs/mongo-java-driver-3.2.2.jar /usr/hdp/current/spark2-client/jars/mongo-java-driver-3.2.2.jar
cp /root/JARs/casbah-commons_2.11-3.1.1.jar /usr/hdp/current/spark2-client/jars/casbah-commons_2.11-3.1.1.jar
cp /root/JARs/casbah-core_2.11-3.1.1.jar /usr/hdp/current/spark2-client/jars/casbah-core_2.11-3.1.1.jar
cp /root/JARs/casbah-query_2.11-3.1.1.jar /usr/hdp/current/spark2-client/jars/casbah-query_2.11-3.1.1.jar
cp /root/JARs/salat-core_2.11-1.11.2.jar /usr/hdp/current/spark2-client/jars/salat-core_2.11-1.11.2.jar
cp /root/JARs/salat-util_2.11-1.11.2.jar /usr/hdp/current/spark2-client/jars/salat-util_2.11-1.11.2.jar
cp /root/JARs/joda-time-2.3.jar /usr/hdp/current/spark2-client/jars/joda-time-2.3.jar
cp /root/JARs/json4s-ext_2.11-3.2.11.jar /usr/hdp/current/spark2-client/jars/json4s-ext_2.11-3.2.11.jar
cp /root/JARs/kafka-clients-1.1.0.jar /usr/hdp/current/spark2-client/jars/kafka-clients-1.1.0.jar
cp /root/JARs/spline-sample-0.3.1.jar /usr/hdp/current/spark2-client/jars/spline-sample-0.3.1.jar
```

Caso queira, poderá continuar enviando seu JAR na chamada do ```spark-submit```, mas seu JAR pequeno dessa vez, ou seja, apenas com o código feito em Scala sem dependências, pois as dependências já estão no core do Spark, mas eu acredito que seria mais interessante já colocar o seu JAR pequeno dentro do core do Spark, assim você realmente não precisará enviar nada para o ```spark-submit```.

Então, gere seu JAR e copie no mesmo lugar:

```
cp /root/JARs/meu_jar_pequeno.jar /usr/hdp/current/spark2-client/jars/meu_jar_pequeno.jar
```

#### Referências

[Issue: Sample / Documentation to integrate with Apache Atlas #31](https://github.com/AbsaOSS/spline/issues/31 "Issue: Sample / Documentation to integrate with Apache Atlas #31")

[Search Maven: za.co.absa.spline](https://search.maven.org/search?q=g:za.co.absa.spline "Search Maven: za.co.absa.spline")
