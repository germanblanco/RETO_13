# RETO_13

Esta actividad consiste en realizar una operación *sencilla* en un Dataframe usando Spark y Scala. La operación propuesta es dividir una columna con fechas en tres columnas (año, mes y día).

## Entorno de trabajo

Para realizar la actividad se propone montar un entorno de trabajo similar al que hay en el banco. Se propone crear una máquina virtual e instalar en ella Oracle Java 7, Scala 2.10 y Spark 1.6.3.

Ejemplo de instrucciones para instalar el entorno en un ubuntu 14.04:
<pre><code>
sudo apt-get update
sudo apt-get upgrade
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java7-installer
sudo wget www.scala-lang.org/files/archive/scala-2.10.4.deb
sudo dpkg -i scala-2.10.4.deb
sudo apt-get update
sudo apt-get install scala
sudo apt-get -f install
sudo apt-get autoremove
wget http://d3kbcqa49mib13.cloudfront.net/spark-1.6.3-bin-hadoop2.6.tgz
tar xvf spark-1.6.3-bin-hadoop2.6.tgz
sudo mv spark-1.6.3-bin-hadoop2.6 /usr/local/spark
echo "export PATH=$PATH:/usr/local/spark/bin" >> .bashrc
source .bashrc
</code></pre>
La dirección de descarga de Spark se obtiene de https://spark.apache.org/downloads.html

## Creación de datos de prueba

Ejemplo de instrucciones para crear datos de prueba:
<pre><code>
import org.apache.spark.sql.types.{StructType, StructField, StringType, IntegerType}
import org.apache.spark.sql.Row
val mydata = List(Row(1, "2019-07-09"), Row(2, "2019-07-08"))
val myrdd = sc.parallelize(mydata)
val myschema =  StructType(StructField("k", IntegerType, true) :: StructField("v", StringType, false) :: Nil)
val mydf = sqlContext.createDataFrame(myrdd, myschema)
</code></pre>
Se puede ver el contenido de mydf con:
<pre><code>
mydf.foreach(x => println("col 1: " + x.get(0) + " col 2: " + x.get(1)))
</code></pre>

