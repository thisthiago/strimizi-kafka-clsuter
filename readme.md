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


