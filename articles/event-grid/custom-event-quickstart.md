---
title: "Événements personnalisés pour Azure Event Grid | Microsoft Docs"
description: "Utilisez Azure Event Grid pour publier une rubrique et pour vous abonner à cet événement."
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 08/15/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 0290836bebadb20085a3ce84dddc088c3af385da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-route-custom-events-with-azure-event-grid"></a>Créer et acheminer des événements personnalisés avec Azure Event Grid

Azure Event Grid est un service de gestion d’événements pour le cloud. Dans cet article, vous utilisez Azure CLI pour créer une rubrique personnalisée, vous abonner à cette rubrique et déclencher l’événement pour afficher le résultat. En règle générale, vous envoyez des événements à un point de terminaison qui répond à l’événement, comme un webhook ou une fonction Azure. Toutefois, pour simplifier cet article, vous envoyez les événements à une URL qui collecte seulement les messages. Vous créez cette URL à l’aide d’un outil tiers en open-source nommé [RequestBin](https://requestb.in/).

>[!NOTE]
>**RequestBin** est un outil open source qui n’est pas destiné à une utilisation à haut débit. L’utilisation de l’outil ici est uniquement à but démonstratif. Si vous envoyez plusieurs événements par push en simultané, vous pouvez ne pas voir tous les événements dans l’outil.

Une fois terminé, vous voyez que les données d’événement ont été envoyées à un point de terminaison.

![Données d’événement](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, cet article nécessite l’exécution de la version la plus récente d’Azure CLI (2.0.14 ou une version ultérieure). Pour connaître la version de l’interface, exécutez `az --version`. Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0](/cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Créer un groupe de ressources

Les rubriques Event Grid sont des ressources Azure et doivent être placées dans un groupe de ressources Azure. Un groupe de ressources est une collection logique dans laquelle des ressources Azure sont déployées et gérées.

Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create). 

L’exemple suivant crée un groupe de ressources nommé *gridResourceGroup* à l’emplacement *westus2*.

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a>Créer une rubrique personnalisée

Une rubrique fournit un point de terminaison défini par l’utilisateur vers lequel vous envoyez vos événements. L’exemple suivant permet de créer la rubrique dans votre groupe de ressources. Remplacez `<topic_name>` par un nom unique pour votre rubrique. Le nom de la rubrique doit être unique, car elle est représentée par une entrée DNS. Dans sa version préliminaire, Event Grid prend en charge les emplacements **westus2** et **westcentralus**.

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a>Créer un point de terminaison de message

Avant de nous abonner à la rubrique, nous allons créer le point de terminaison pour le message de l’événement. Au lieu d’écrire du code qui réponde à l’événement, nous allons créer un point de terminaison qui collecte les messages, afin que vous puissiez les consulter. RequestBin est un outil tiers en open-source qui vous permet de créer un point de terminaison et d’afficher les requêtes qui lui sont envoyées. Accédez à [RequestBin](https://requestb.in/), puis cliquez sur **Créer un RequestBin**.  Copiez l’URL du fichier bin, dont vous avez besoin pour vous abonner à la rubrique.

## <a name="subscribe-to-a-topic"></a>S’abonner à une rubrique

Vous vous abonnez à une rubrique pour communiquer à Event Grid les événements qui vous intéressent. L’exemple suivant s’abonne à la rubrique que vous avez créée et transmet l’URL à partir de RequestBin en tant que point de terminaison de la notification d’événement. Remplacez `<event_subscription_name>` par un nom unique pour votre abonnement, et `<URL_from_RequestBin>` par la valeur de la section précédente. En spécifiant un point de terminaison lors de l’abonnement, Event Grid gère le routage d’événements vers ce point de terminaison. Pour `<topic_name>`, utilisez la valeur que vous avez créée précédemment. 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-to-your-topic"></a>Envoyer un événement à votre rubrique

Nous allons maintenant déclencher un événement pour voir comment Event Grid distribue le message à votre point de terminaison. Tout d’abord, il nous faut l’URL et la clé de la rubrique. Utilisez de nouveau le nom de votre rubrique pour `<topic_name>`.

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

Pour simplifier cet article, nous avons configuré des exemples de données d’événements à envoyer à la rubrique. En règle générale, une application ou un service Azure envoie les données d’événements. L’exemple suivant obtient les données d’événements :

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

Si vous affichez `echo "$body"`, vous pouvez voir l’événement complet. L’élément `data` du fichier JSON est la charge utile de l’événement. N’importe quel fichier JSON bien construit peut être placé dans ce champ. Vous pouvez aussi utiliser le champ objet pour un routage et un filtrage avancés.

CURL est un utilitaire qui effectue des requêtes HTTP. Dans cet article, nous utilisons CURL pour envoyer l’événement à notre rubrique. 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

Vous avez déclenché l’événement, et Event Grid a envoyé le message au point de terminaison configuré lors de l’abonnement. Accédez à l’URL de RequestBin que vous avez créée précédemment. Ou cliquez sur Actualiser dans le navigateur RequestBin ouvert. L’événement que vous venez d’envoyer apparaît. 

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
Si vous envisagez de continuer à utiliser cet événement, ne supprimez pas les ressources créées dans cet article. Sinon, utilisez la commande suivante pour supprimer les ressources créées avec cet article.

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous savez créer des rubriques et des abonnements d’événements, vous pouvez en apprendre davantage sur Event Grid et ce qu’il peut vous offrir :

- [Event Grid](overview.md)
- [Surveiller les modifications d’une machine virtuelle avec Azure Event Grid et Azure Logic Apps](monitor-virtual-machine-changes-event-grid-logic-app.md)
