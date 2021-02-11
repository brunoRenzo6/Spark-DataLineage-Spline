# Persistências do SPLINE 

Inicialmente o SPLINE tinha três alternativas para fazer o registro da linhagem de dados, MONGODB, HDFS e ATLAS.


## MONGODB:

#### Executar script PySpark com SPLINE persistindo no MongoDB
```
spark-submit --conf "spark.driver.extraJavaOptions=-Dspline.mode=BEST_EFFORT -Dspline.persistence.factory=za.co.absa.spline.persistence.mongo.MongoPersistenceFactory -Dspline.mongodb.url=mongodb://caminho_do_banco:porta_do_banco -Dspline.mongodb.name=nome_do_banco" --jars nome_do_jar_completo.jar script_pyspark.py
```
ou

```
spark-submit --driver-java-options "-Dspline.mode=BEST_EFFORT -Dspline.persistence.factory=za.co.absa.spline.persistence.mongo.MongoPersistenceFactory -Dspline.mongodb.url=mongodb://caminho_do_banco:porta_do_banco -Dspline.mongodb.name=nome_do_banco" --jars nome_do_jar_completo.jar script_pyspark.py
```

> Utilizado: -Dspline.mongodb.url=mongodb://127.0.0.1:27017 -Dspline.mongodb.name=db_spline

## HDFS:

#### Executar script PySpark com SPLINE persistindo no HDFS:

```
spark-submit --conf "spark.driver.extraJavaOptions=-Dspline.mode=BEST_EFFORT -Dspline.persistence.factory=za.co.absa.spline.persistence.hdfs.HdfsPersistenceFactory" --jars nome_do_jar_completo.jar script_pyspark.py
```

por exemplo:

```
spark-submit --driver-java-options "-Dspline.mode=BEST_EFFORT -Dspline.persistence.factory=za.co.absa.spline.persistence.hdfs.HdfsPersistenceFactory" --jars nome_do_jar_completo.jar script_pyspark.py
```

## PERSISTÊNCIA PARALELA:

#### Executar script PySpark com SPLINE persistindo no MongoDB e HDFS:

```
spark-submit --conf "spark.driver.extraJavaOptions=-Dspline.mode=BEST_EFFORT -Dspline.persistence.factory=za.co.absa.spline.persistence.api.composition.ParallelCompositeFactory -Dspline.mongodb.url=mongodb://caminho_do_banco:porta_do_banco -Dspline.mongodb.name=nome_do_banco -Dspline.persistence.composition.factories=za.co.absa.spline.persistence.mongo.MongoPersistenceFactory,za.co.absa.spline.persistence.hdfs.HdfsPersistenceFactory" --jars nome_do_jar_completo.jar script_pyspark.py
```

ou

```
spark-submit --driver-java-options "-Dspline.mode=BEST_EFFORT -Dspline.persistence.factory=za.co.absa.spline.persistence.api.composition.ParallelCompositeFactory -Dspline.mongodb.url=mongodb://caminho_do_banco:porta_do_banco -Dspline.mongodb.name=nome_do_banco -Dspline.persistence.composition.factories=za.co.absa.spline.persistence.mongo.MongoPersistenceFactory,za.co.absa.spline.persistence.hdfs.HdfsPersistenceFactory" --jars nome_do_jar_completo.jar script_pyspark.py
```

#### Executar script PySpark com SPLINE persistindo no Atlas e HDFS:

```
spark-submit --conf "spark.driver.extraJavaOptions=-Dspline.mode=BEST_EFFORT -Dspline.persistence.factory=za.co.absa.spline.persistence.api.composition.ParallelCompositeFactory -Dspline.persistence.composition.factories=za.co.absa.spline.persistence.atlas.AtlasPersistenceFactory,za.co.absa.spline.persistence.hdfs.HdfsPersistenceFactory -Datlas.kafka.bootstrap.servers=caminho_do_bootstrap_server:porta_do_bootstrap_server" --jars nome_do_jar_completo.jar script_pyspark.py
```

ou

```
spark-submit --driver-java-options "-Dspline.mode=BEST_EFFORT -Dspline.persistence.factory=za.co.absa.spline.persistence.api.composition.ParallelCompositeFactory -Dspline.persistence.composition.factories=za.co.absa.spline.persistence.atlas.AtlasPersistenceFactory,za.co.absa.spline.persistence.hdfs.HdfsPersistenceFactory -Datlas.kafka.bootstrap.servers=caminho_do_bootstrap_server:porta_do_bootstrap_server" --jars nome_do_jar_completo.jar script_pyspark.py
```

## ATLAS:

A persistência em Atlas tem dois pequenos diferenciais dos demais.

1. Os desenvolvedores do Spline pararam de oferecer suporte ao Atlas na versão 0.3.1, portanto, caso você queira utilizar o Spline persistindo no Atlas é necessário que você utilize as dependências 0.3.1. A previsão é que uma nova API resolva esses problemas na versão 0.4, enquanto isso, é preciso seguir esse tutorial.

2. Para utilizar o Atlas é preciso colocar um arquivo de modelo de persistência dentro da pasta models do Atlas, é um arquivo JSON que mostra ao Atlas como o Spline enviará as informações para ele persistir em sua linhagem.

A boa notícia é que você pode fazer o download do [Atlas Metal Model](https://search.maven.org/remotecontent?filepath=za/co/absa/spline/spline-persistence-atlas/0.3.1/spline-persistence-atlas-0.3.1-atlas-meta-model.json "Baixar Agora"), caso queira procurar por conta própria, apenas entre no [Search Maven](https://search.maven.org/ "Search Maven") e busque a dependência do __spline-persistence-atlas-0.3.1__, lá terá o modelo para ser baixado.

Veja se serve para você, mas no meu caso, foi copiado o arquivo de modelo para dentro da pasta de instalação do Atlas assim:

```
cp /root/Model/spline-meta-model.json /usr/hdp/current/atlas-client/models/spline-meta-model.json
```

__Um passo muito importante que não deve ser esquecido, após copiar esse arquivo de modelo, reinicie o Atlas, sério, isso não funcionará se não for reiniciado, então sim, você poderá utilizar o Spline persistindo no Atlas.__

Importante dizer que devemos respeitar as versões que funcionaram corretamente conforme apresentados na [introdução desse repositório](https://github.com/WilliamPorto/keyruslab-spline/blob/master/README.md "introdução desse repositório").

#### Executar script PySpark com SPLINE persistindo no Atlas utilizando o JAR Completo:

```
spark-submit --conf "spark.driver.extraJavaOptions=-Dspline.mode=BEST_EFFORT -Dspline.persistence.factory=za.co.absa.spline.persistence.atlas.AtlasPersistenceFactory -Datlas.kafka.bootstrap.servers=caminho_do_bootstrap_server:porta_do_bootstrap_server" --jars nome_do_jar_completo.jar script_pyspark.py
```

ou

```
spark-submit --driver-java-options "-Dspline.mode=BEST_EFFORT -Dspline.persistence.factory=za.co.absa.spline.persistence.atlas.AtlasPersistenceFactory -Datlas.kafka.bootstrap.servers=caminho_do_bootstrap_server:porta_do_bootstrap_server" --jars nome_do_jar_completo.jar script_pyspark.py
```

#### Executar script PySpark com SPLINE persistindo no Atlas sem o JAR Completo:

```
spark-submit --conf "spark.driver.extraJavaOptions=-Dspline.mode=BEST_EFFORT -Dspline.persistence.factory=za.co.absa.spline.persistence.atlas.AtlasPersistenceFactory -Datlas.kafka.bootstrap.servers=caminho_do_bootstrap_server:porta_do_bootstrap_server" script_pyspark.py
```

ou

```
spark-submit --driver-java-options "-Dspline.mode=BEST_EFFORT -Dspline.persistence.factory=za.co.absa.spline.persistence.atlas.AtlasPersistenceFactory -Datlas.kafka.bootstrap.servers=caminho_do_bootstrap_server:porta_do_bootstrap_server" script_pyspark.py
```

> Utilizado: -Datlas.kafka.bootstrap.servers=sandbox-hdp.hortonworks.com:6667

Não é preciso enviar o JAR completo na hora da execução com ```spark-submit```, aliás, quando é executado o SPLINE persistindo no Atlas é aconcelhável que não seja realmente enviado, pois o JAR fica muito grande e pode causar um certo delay de execução, ocasionando possíveis erros, portanto, [veja como é possível](https://github.com/WilliamPorto/keyruslab-spline/blob/master/Depend%C3%AAncias%20no%20Core%20do%20Spark.md "veja como é possível") __executar o SPLINE sem a necessidade de enviar o JAR completo ou algum JAR__.

#### Exemplo do data lineage de um Join   
![Spline_Atlas_Nifi](https://github.com/WilliamPorto/keyruslab-spline/blob/master/Repositorio%20de%20Imagens%20Spline_Atlas/splineAtlas.jpg)

## ATLAS e NiFi (End-to-End Lineage):

Uma representação visual da linhagem de dados(data lineage) é essencial para compreender os diferentes processos envolvidos em um fluxo de dados(data flow) e suas dependências. A gestão de metadados(metadata management) é a chave para capturar dados empresariais e reprensentar essa linhagem de dados de uma ponta a outra do fluxo.

Nesse fluxo, que começa pela ingestão de dados, limpeza/transformação até a etapa de análise(analytics), diversos componentes enstao envolvidos para solucionar os problemas de bigdata empresárias. Falando de Hortonworks temos Kafka, Nifi, Spark, Hive, Hive LLAP etc.

O SPLINE pode ser utilizado é uma peça chave nessa integração entre ferramentas.

Um ótima solução foi descrita na comunidade do Hortonworks [End to End Atlas Lineage with Nifi, Spark, Hive](https://br.hortonworks.com/blog/hdf-3-1-blog-series-part-6-introducing-nifi-atlas-integration/)

Integração entre ferramentas sempre é um processo complicado, especialmente quando estamos modificando uma ferramenta que não previa essa funcionalidade. Por isso vamos disponibilizar a solução para o <strong>Step 2) Spark --> HDFS</strong> do artigo.
</br>
</br>
</br>
#### spline-persistence-atlas-0.3.1
[spline-persistence-atlas-0.3.1](https://github.com/WilliamPorto/keyruslab-spline/tree/master/Downloads/Nifi_ModifiedAtlas) com o `za.co.absa.spline.persistence.atlas.conversion.DatasetConverter` modificado para reconhecer a lineage do Nifi como um input válido.

#### spark-submit com as 2 novas propriedades necessárias
```
spark-submit --driver-java-options "-Dspline.mode=BEST_EFFORT -Datlas.kafka.bootstrap.servers=sandbox-hdp.hortonworks.com:6667 -Dspline.persistence.factory=za.co.absa.spline.persistence.atlas.AtlasPersistenceFactory -Dcluster.name=Sandbox -Dabsolute.base.path=hdfs://sandbox-hdp.hortonworks.com:8020" --jars pHandlerATLASPackage.jar criptomoedasJob.py
```
> Utilizado: -Dcluster.name=Sandbox
> 
> Utilizado: -Dabsolute.base.path=hdfs://sandbox-hdp.hortonworks.com:8020

#### AtlasUI End-to-End lineage (Local-->HDFS-->Spark-->HDFS-->HIVE)
![Spline_Atlas_Nifi](https://github.com/WilliamPorto/keyruslab-spline/blob/master/Repositorio%20de%20Imagens%20Spline_Atlas/endToEnd.png)


#### Referências

[Spline Oficial](https://absaoss.github.io/spline/ "Spline Oficial")

[Issue: HDFS factory not working. #14](https://github.com/AbsaOSS/spline/issues/14 "Issue: HDFS factory not working. #14")

[Issue: Sample / Documentation to integrate with Apache Atlas #31](https://github.com/AbsaOSS/spline/issues/31 "Issue: Sample / Documentation to integrate with Apache Atlas #31")

[Return Atlas support to Spline 0.3 #75](https://github.com/AbsaOSS/spline/issues/75 "Return Atlas support to Spline 0.3 #75")

[How To Install MongoDB on CentOS 7](https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-on-centos-7 "How To Install MongoDB on CentOS 7")

[Apache NiFi Overview](https://nifi.apache.org/docs/nifi-docs/html/overview.html "Apache NiFi Overview")

[Hortonworks DataFlow (HDF) 3.1 blog series part 5: Introducing Apache NiFi-Atlas integration](https://br.hortonworks.com/blog/hdf-3-1-blog-series-part-6-introducing-nifi-atlas-integration/ "Hortonworks DataFlow (HDF) 3.1 blog series part 5: Introducing Apache NiFi-Atlas integration")

[End to End Atlas Lineage with Nifi , Spark , Hive](https://community.hortonworks.com/articles/186772/end-to-end-atlas-lineage-with-nifi-spark-hive.html "End to End Atlas Lineage with Nifi , Spark , Hive")

[Installing and Upgrading NiFi](https://docs.hortonworks.com/HDPDocuments/HDF3/HDF-3.3.1/installing-upgrading-nifi/content/starting_and_stopping_nifi_on_linux.html "Installing and Upgrading NiFi")
