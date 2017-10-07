---
title: "événements d’aaaCustom pour la grille d’événement Azure | Documents Microsoft"
description: "Utilisez la grille d’événement Azure toopublish une rubrique et inscription de l’événement de toothat."
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 08/15/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 5055df1c970b043cadf06978a076f7f5c83501cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-route-custom-events-with-azure-event-grid"></a>Créer et acheminer des événements personnalisés avec Azure Event Grid

Grille d’événement Azure est un service de gestion des événements pour le cloud de hello. Dans cet article, vous utilisez hello CLI d’Azure toocreate une rubrique personnalisée s’abonner toohello rubrique et déclencher hello événement tooview hello de résultats. En règle générale, vous envoyer des événements tooan point de terminaison qui répond événement toohello, par exemple, un webhook ou d’une fonction d’Azure. Toutefois, toosimplify cet article, vous envoyez hello événements tooa URL qui collecte simplement des messages de type hello. Vous créez cette URL à l’aide d’un outil tiers en open-source nommé [RequestBin](https://requestb.in/).

>[!NOTE]
>**RequestBin** est un outil open source qui n’est pas destiné à une utilisation à haut débit. Hello outil hello ici est purement le tarif. Si vous effectuez un push plusieurs événements à la fois, vous verrez ne peut-être pas tous les événements dans l’outil de hello.

Lorsque vous avez terminé, vous voyez que les données d’événement hello a été envoyées tooan le point de terminaison.

![Données d’événement](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cet article suppose que vous exécutez la version la plus récente de Azure CLI hello (2.0.14 ou version ultérieure). version de hello toofind, exécutez `az --version`. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0](/cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Créer un groupe de ressources

Les rubriques Event Grid sont des ressources Azure et doivent être placées dans un groupe de ressources Azure. groupe de ressources Hello est une collection logique dans le Azure les ressources sont déployées et gérées.

Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande. 

Hello exemple suivant crée un groupe de ressources nommé *gridResourceGroup* Bonjour *westus2* emplacement.

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a>Créer une rubrique personnalisée

Une rubrique fournit un point de terminaison défini par l’utilisateur vers lequel vous envoyez vos événements. Hello exemple suivant crée les rubrique hello dans votre groupe de ressources. Remplacez `<topic_name>` par un nom unique pour votre rubrique. nom de la rubrique Hello doit être unique, car il est représenté par une entrée DNS. Pour la version préliminaire de hello, prend en charge la grille d’événement **westus2** et **westcentralus** emplacements.

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a>Créer un point de terminaison de message

Avant de s’abonner toohello rubrique, nous allons créer le point de terminaison hello pour le message d’événement hello. Plutôt que d’écrire un événement de code toorespond toohello, nous allons créer un point de terminaison qui collecte les messages de type hello afin que vous puissiez les afficher. RequestBin est une open source, un outil tiers qui vous permet de toocreate un point de terminaison et afficher les demandes qui sont envoyées à tooit. Accédez trop[RequestBin](https://requestb.in/), puis cliquez sur **créer un RequestBin**.  Copier l’URL d’emplacement de hello, car vous en avez besoin lors de l’abonnement toohello rubrique.

## <a name="subscribe-tooa-topic"></a>S’abonner tooa rubrique

Vous vous abonnez tooa rubrique tootell grille d’événement quels événements vous souhaitez tootrack. Hello exemple suivant s’abonne toohello rubrique que vous avez créé et transmet les URL de hello de RequestBin en tant que point de terminaison hello pour la notification d’événement. Remplacez `<event_subscription_name>` avec un nom unique pour votre abonnement, et `<URL_from_RequestBin>` avec la valeur hello à partir de la précédente section de hello. En spécifiant un point de terminaison lors de l’abonnement, grille d’événement gère le routage de point de terminaison toothat événements hello. Pour `<topic_name>`, utilisez la valeur hello vous avez créé précédemment. 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-tooyour-topic"></a>Envoyer une rubrique tooyour d’événement

Maintenant, nous allons déclencher un événement toosee comment grille d’événement distribue le point de terminaison tooyour de message hello. Tout d’abord, nous allons obtenir l’URL de hello et la clé pour la rubrique de hello. Utilisez de nouveau le nom de votre rubrique pour `<topic_name>`.

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

toosimplify cet article, nous avons configuré exemple événement données toosend toohello de rubrique. En règle générale, une application ou un service Azure envoie les données d’événement hello. Hello, l’exemple suivant obtient les données d’événement hello :

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

Si vous `echo "$body"` vous pouvez voir les événements complète hello. Hello `data` élément Hello JSON est la charge utile de hello de votre événement. N’importe quel fichier JSON bien construit peut être placé dans ce champ. Vous pouvez également utiliser le champ de l’objet hello pour le routage et le filtrage avancés.

CURL est un utilitaire qui effectue des requêtes HTTP. Dans cet article, nous utilisons le rubrique tooour événement CURL toosend hello. 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

Vous avez avoir déclenché des événements de hello et grille d’événement envoyé le point de terminaison toohello de message hello que vous avez configuré lors de l’abonnement. Parcourir toohello RequestBin URL que vous avez créé précédemment. Ou cliquez sur Actualiser dans le navigateur RequestBin ouvert. Vous consultez les événements hello que vous venez d’envoyer. 

```json
[{
  "id": "1807",
  "eventType": "recordInserted",
  "subject": "myapp/vehicles/motorcycles",
  "eventTime": "2017-08-10T21:03:07+00:00",
  "data": {
    "make": "Ducati",
    "model": "Monster"
  },
  "topic": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/topics/{topic}"
}]
```

## <a name="clean-up-resources"></a>Supprimer des ressources
Si vous prévoyez toocontinue utilisation de cet événement, procédez de nettoyer les ressources hello créées dans cet article. Si vous n’envisagez pas de toocontinue, utilisez hello suivant ressources hello toodelete de la commande que vous avez créé dans cet article.

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous savez comment toocreate rubriques et abonnements aux événements, en savoir plus sur la grille d’événement peut vous aider à effectuer :

- [Event Grid](overview.md)
- [Surveiller les modifications d’une machine virtuelle avec Azure Event Grid et Azure Logic Apps](monitor-virtual-machine-changes-event-grid-logic-app.md)
