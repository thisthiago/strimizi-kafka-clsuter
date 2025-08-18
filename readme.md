# Kafka on Kubernetes with Kind and Strimzi 🚀

Este projeto demonstra como criar um cluster Kafka local usando **Kind** (Kubernetes in Docker) e o operador **Strimzi**. Ele inclui brokers, Kafka Connect, UI e fontes de dados.

---

## Estrutura do projeto

```text
.
├── kafka
│   ├── broker
│   │   ├── kafka-cluster.yaml
│   │   └── volumes.yaml
│   ├── kafka-connect
│   │   ├── Dockerfile
│   │   ├── connect.yaml
│   │   └── lib
│   │       └── [drivers e jars necessários]
│   ├── kafka-ui
│   │   └── ui.yaml
│   ├── readme.md
│   ├── source
│   │   └── teste.yml
│   └── strimizi-operator
│       └── operator.yaml
└── kind
    └── kind-on-premise-config.yaml
````

---

## Pré-requisitos

* Docker
* Kind
* kubectl
* Conexão com a internet para baixar Strimzi

---

## Passo a passo

### 1. Criar o cluster Kind

```bash
kind create cluster --config kind/kind-on-premise-config.yaml
```

### 2. Criar namespace Kafka

```bash
kubectl create namespace kafka
```

### 3. Instalar o operador Strimzi

```bash
kubectl create -f https://strimzi.io/install/latest?namespace=kafka -n kafka
```

### 4. Criar o cluster Kafka

```bash
kubectl apply -f kafka/broker/kafka-cluster.yaml -n kafka
```

### 5. Aplicar configurações adicionais

```bash
kubectl apply -f kafka/broker -n kafka
kubectl apply -f kafka/kafka-connect -n kafka
kubectl apply -f kafka/kafka-ui -n kafka
kubectl apply -f kafka/source -n kafka
```

---

## Limpeza do cluster

Para remover o cluster Kind local:

```bash
kind delete cluster --name kind-on-premise
```

---

## Notas

* O diretório `kafka/kafka-connect/lib` contém todos os drivers e bibliotecas necessários para conexões com bancos e sistemas.
* `kafka/kafka-ui` é a interface visual para monitoramento do Kafka.
* `kafka/source` contém definições de tópicos ou conectores de teste.



ERROR Uncaught exception in REST call to /connectors/sink-s3-tpu-tipo-agente-venda-tag/config (org.apache.kafka.connect.runtime.rest.errors.ConnectExceptionMapper) [qtp2069492650-27]
org.apache.kafka.connect.errors.ConnectException: Failed to find any class that implements Connector and which name matches io.confluent.connect.s3.S3SinkConnector, available connectors are: PluginDesc{klass=class io.confluent.connect.jdbc.JdbcSinkConnector, name='io.confluent.connect.jdbc.JdbcSinkConnector', version='10.8.4', encodedVersion=10.8.4, type=sink, typeName='sink', location='file:/opt/kafka/plugins/kafka-connect-jdbc/'}, PluginDesc{klass=class io.confluent.connect.jdbc.JdbcSourceConnector, name='io.confluent.connect.jdbc.JdbcSourceConnector', version='10.8.4', encodedVersion=10.8.4, type=source, typeName='source', location='file:/opt/kafka/plugins/kafka-connect-jdbc/'}, PluginDesc{klass=class org.apache.kafka.connect.mirror.MirrorCheckpointConnector, name='org.apache.kafka.connect.mirror.MirrorCheckpointConnector', version='3.9.0', encodedVersion=3.9.0, type=source, typeName='source', location='classpath'}, PluginDesc{klass=class org.apache.kafka.connect.mirror.MirrorHeartbeatConnector, name='org.apache.kafka.connect.mirror.MirrorHeartbeatConnector', version='3.9.0', encodedVersion=3.9.0, type=source, typeName='source', location='classpath'}, PluginDesc{klass=class org.apache.kafka.connect.mirror.MirrorSourceConnector, name='org.apache.kafka.connect.mirror.MirrorSourceConnector', version='3.9.0', encodedVersion=3.9.0, type=source, typeName='source', location='classpath'}
	at org.apache.kafka.connect.runtime.isolation.Plugins.connectorClass(Plugins.java:321)

