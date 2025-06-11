# Kafka Spring Boot Project

## Description

Ce projet est une application Spring Boot qui démontre l'intégration avec Apache Kafka pour la gestion des messages. L'application inclut des fonctionnalités de producteur et consommateur Kafka, ainsi qu'un système de récupération et publication de taux de change.

## Technologies utilisées

- **Java 17**
- **Spring Boot 3.4.2**
- **Spring Kafka**
- **Spring Web**
- **Spring Boot Actuator**
- **Lombok**
- **Maven**

## Architecture du projet

```
src/main/java/com/learn/kafka/
├── controller/
│   └── ExchangeRateController.java     # Contrôleur REST pour les taux de change
├── producer/
│   ├── KafkaProducerConfig.java        # Configuration du producteur Kafka
│   └── MessageProducer.java            # Service de production de messages
├── consumer/
│   ├── KafkaConsumerConfig.java        # Configuration du consommateur Kafka
│   └── MessageConsumer.java            # Service de consommation de messages
├── service/
│   └── ExchangeRatePublisher.java      # Service de publication des taux de change
└── model/
    └── ExchangeRateResponse.java       # Modèle de données pour les taux de change
```

## Configuration

### 1. Configuration Kafka dans `application.properties`

```properties
spring.application.name=kafka
spring.kafka.bootstrap-servers=localhost:9092
spring.kafka.consumer.group-id=tp-kafka-step1
server.port=8081
management.endpoints.web.exposure.include=*
```

Pour un environnement différent, modifiez l'adresse du serveur Kafka :
```properties
spring.kafka.bootstrap-servers=ip_de_votre_server_kafka:9092
```

### 2. Configuration des topics

Le projet utilise plusieurs topics Kafka :
- `mon-tunnel-topic` : Topic principal pour les messages génériques
- `exchange-rates-topic` : Topic dédié aux taux de change

## Fonctionnalités

### Producteur Kafka
- Configuration automatique du producteur avec sérialisation String
- Service `MessageProducer` pour l'envoi de messages vers différents topics
- Support de l'injection de dépendances Spring

### Consommateur Kafka
- Configuration automatique du consommateur avec désérialisation String
- Listener `@KafkaListener` pour la réception de messages
- Gestion des groupes de consommateurs

### API REST - Taux de change
- **POST** `/api/exchange-rates/fetch` : Déclenche la récupération des taux de change
- **POST** `/api/exchange-rates/simulate` : Simule l'envoi de taux de change factices

### Monitoring
- Spring Boot Actuator activé pour le monitoring
- Endpoints de santé et métriques disponibles

## Installation et démarrage

### Prérequis
- Java 17 ou supérieur
- Maven 3.6 ou supérieur
- Apache Kafka en fonctionnement (local ou distant)

### 1. Cloner le projet
```bash
git clone <url-du-repository>
cd kafka-project
```

### 2. Compiler le projet
```bash
./mvnw clean compile
```

### 3. Démarrer Kafka (si local)
```bash
# Démarrer Zookeeper
bin/zookeeper-server-start.sh config/zookeeper.properties

# Démarrer Kafka
bin/kafka-server-start.sh config/server.properties
```

### 4. Lancer l'application
```bash
./mvnw spring-boot:run
```

L'application sera accessible sur `http://localhost:8081`

## Utilisation

### Test du producteur
Pour tester l'envoi de messages, utilisez l'endpoint de production :

```bash
curl --location --request POST 'http://localhost:8081/produce?content=message_content_here'
```

### Test des taux de change
Pour déclencher la récupération des taux de change :

```bash
curl --location --request POST 'http://localhost:8081/api/exchange-rates/fetch'
```

Pour simuler des taux de change :

```bash
curl --location --request POST 'http://localhost:8081/api/exchange-rates/simulate'
```

### Monitoring
Accédez aux endpoints d'actuator :
- Santé : `http://localhost:8081/actuator/health`
- Métriques : `http://localhost:8081/actuator/metrics`
- Informations : `http://localhost:8081/actuator/info`

## Structure des messages

### Messages génériques
Les messages envoyés sur `mon-tunnel-topic` sont des chaînes de caractères simples.

### Taux de change
Les messages de taux de change suivent cette structure JSON :
```json
{
  "baseCurrency": "USD",
  "date": "2025-06-04",
  "rates": {
    "EUR": 0.85,
    "GBP": 0.73,
    "JPY": 150.0,
    "CHF": 0.82
  }
}
```

## Développement

### Étapes de développement (Kata)

Ce projet suit une approche de kata avec plusieurs étapes :

1. **Step 1** : Configuration de base Kafka avec producteur et consommateur
2. **Step 2** : Implémentation des taux de change et API REST
3. **Step 3** : (À venir) Gestion avancée des erreurs et retry

### Prochaines fonctionnalités
- Gestion des erreurs et retry automatique
- Monitoring avancé avec Micrometer
- Tests d'intégration avec Kafka embedded
- Sérialisation/désérialisation JSON native
- Partitioning et scaling

## Dépannage

### Problèmes courants
1. **Connexion Kafka échoue** : Vérifiez que Kafka est démarré et accessible sur le port configuré
2. **Messages non reçus** : Vérifiez la configuration du group-id et des topics
3. **Port 8081 occupé** : Modifiez `server.port` dans `application.properties`

### Logs utiles
Les logs de l'application incluent :
- Réception de messages par le consommateur
- Publication de messages par le producteur
- Erreurs de connexion Kafka
- Métriques de performance

## Contribution

Pour contribuer au projet :
1. Forkez le repository
2. Créez une branche feature (`git checkout -b feature/nouvelle-fonctionnalite`)
3. Committez vos changements (`git commit -am 'Ajout nouvelle fonctionnalité'`)
4. Pushez vers la branche (`git push origin feature/nouvelle-fonctionnalite`)
5. Créez une Pull Request

## Licence

Ce projet est à des fins d'apprentissage et de démonstration.