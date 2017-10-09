## <a name="what-is-queue-storage"></a>Présentation du stockage de files d'attente
Stockage de file d’attente Azure est un service pour stocker un grand nombre de messages qui sont accessibles à partir de n’importe où dans le monde hello via des appels authentifiés à l’aide de HTTP ou HTTPS. Un message de la file d’attente unique peut être de taille too64 Ko, et une file d’attente peut contenir des millions de messages, des limites de capacité totale de toohello d’un compte de stockage.

Voici quelques utilisations courantes des files d’attente de stockage :

* Création d’une file d’attente de travail tooprocess asynchrone
* Transmission de messages à partir d’un rôle de travail Azure tooan rôle web Azure

## <a name="queue-service-concepts"></a>Concepts du service de File d’attente
Hello service file d’attente contient hello suivant des composants :

![File d'attente 1](./media/storage-queue-concepts-include/queue1.png)

* **Format d’URL :** files d’attente sont adressables hello suivant le format d’URL :   
    http://`<storage account>`.queue.core.windows.net/`<queue>` 
  
    Hello suivant URL traite une file d’attente dans le diagramme de hello :  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* **Compte de stockage :** tous accéder tooAzure stockage s’effectue via un compte de stockage. Pour plus d’informations sur la capacité du compte de stockage, consultez la page [Objectifs de performance et évolutivité du stockage Azure](../articles/storage/common/storage-scalability-targets.md) .
* **File d’attente :** une file d’attente contient un ensemble de messages. Tous les messages doivent être dans une file d’attente. Notez que ce nom de file d’attente hello doit être en minuscule. Pour plus d'informations sur l’affectation de noms à des files d’attente, consultez [Affectation de noms pour les files d'attente et les métadonnées](https://msdn.microsoft.com/library/azure/dd179349.aspx).
* **Message :** un message, dans n’importe quel format, des too64 Ko. Hello durée maximale pendant laquelle un message peut rester dans la file d’attente hello est de 7 jours.

