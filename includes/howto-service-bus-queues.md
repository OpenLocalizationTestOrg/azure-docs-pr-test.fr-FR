## <a name="what-are-service-bus-queues"></a>Présentation des files d'attente Service Bus
Les files d’attente Service Bus prennent en charge un modèle de communication de **messagerie répartie** . Lors de l’utilisation de files d’attente, les composants d’une application distribuée ne communiquent pas directement entre eux ; ils échangent plutôt des messages via une file d’attente, qui fait office d’intermédiaire (broker). Un producteur de message (expéditeur) transmet à une file d’attente de message toohello, puis poursuit son traitement. En mode asynchrone, un consommateur de messages (récepteur) extrait le message de type hello à partir de la file d’attente hello et le traite. producteur de Hello n’ont toowait pour une réponse à un consommateur de hello dans l’ordre toocontinue tooprocess et envoyer des messages. Les files d’attente offrent **First In, premier sorti (FIFO)** message tooone de remise ou de plusieurs consommateurs concurrents. Autrement dit, les messages sont généralement reçus et traités par les récepteurs hello dans l’ordre de hello dans lequel ils ont été ajoutés à la file d’attente de toohello, et chaque message est reçu et traité par un consommateur d’un seul message.

![QueueConcepts](./media/howto-service-bus-queues/sb-queues-08.png)

Les files d’attente Service Bus sont une technologie à usage généraliste pouvant servir à une grande diversité de situations :

* Communication entre les rôles Web et les rôles de travail dans une application multiniveau Azure.
* Communication entre les applications locales et les applications hébergées par Azure dans une solution hybride.
* Communication entre les composants d’une application distribuée s’exécutant en local dans différentes organisations ou dans différents services d’une organisation.

À l’aide de files d’attente permet à vos applications vous tooscale plus facilement et activer plus d’architecture tooyour de résilience.


