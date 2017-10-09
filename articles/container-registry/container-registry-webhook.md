---
title: aaaAzure conteneur Registre webhooks | Documents Microsoft
description: Webhooks Azure Container Registry
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acr, azure-container-registry
keywords: Docker, Conteneurs, ACR
ms.assetid: 
ms.service: container-registry
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/06/2017
ms.author: nepeters
ms.openlocfilehash: adc2afec486007e2d54cd689e6f7ef8b1098db06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a>Utilisation des webhooks Azure Container Registry - Portail Azure

Un Registre de conteneur Azure stocke et gère les images de conteneur Docker privés, comme toohello Hub d’ancrage stocke les images Docker publiques. Vous utilisez des webhooks tootrigger événements lorsque certaines actions sont exécutées dans un des référentiels de votre Registre. Webhooks peut répondre tooevents au niveau du Registre hello ou elles peuvent être étendues vers le bas de balise du référentiel spécifique tooa. 

Pour plus d’informations et des concepts, consultez hello [vue d’ensemble](./container-registry-intro.md).

## <a name="prerequisites"></a>Composants requis 

- Registre managé de conteneurs Azure: créez un registre de conteneurs managé dans votre abonnement Azure. Par exemple, utilisez hello portail Azure ou hello Azure CLI 2.0. 
- Docker CLI - tooset de votre ordinateur local en tant qu’un ordinateur hôte et l’accès hello Docker CLI commandes Docker, installez le moteur Docker. 

## <a name="create-webhook-azure-portal"></a>Créer un portail Azure webhook

1. Connectez-vous à toohello portail Azure et accédez de Registre toohello dans lequel vous souhaitez toocreate webhooks. 

2. Dans le panneau de conteneur hello, sélectionnez l’onglet de « Webhooks » de hello. 

3. Sélectionnez « Ajouter » à partir de la barre d’outils du panneau hello webhook. 

4. Hello complète *créer le Webhook* formulaire avec hello informations suivantes :

| Valeur | Description |
|---|---|
| Nom | Hello nom toogive toohello webhook. Il ne peut contenir que des lettres minuscules et des chiffres et avoir de 5 à 50 caractères. |
| URI de service | Hello URI où hello webhook doit envoyer des notifications de publication. |
| En-têtes personnalisés | En-têtes toopass en même temps que la demande POST de hello. Ils doivent être au format « clé : valeur ». |
| Actions de déclencheur | Actions qui déclenchent hello webhook. Actuellement, webhooks peut être déclenchée par push et/ou supprimer actions tooan image. |
| État | état Hello du webhook hello après sa création. Il est activé par défaut. |
| Scope | étendue Hello qui fonctionne de webhook hello. Étendue de hello est par défaut pour tous les événements dans le Registre de hello. Il peut être spécifié pour un référentiel ou d’une balise à l’aide du format de hello « référentiel : balise ». |

Exemple de formulaire webhook :

![Interface utilisateur DC/OS](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a>Créer un webhook avec Azure CLI

un webhook à l’aide de toocreate hello CLI d’Azure, utilisez hello [az acr webhook créer](/cli/azure/acr/webhook#create) commande.

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a>Tester un webhook

### <a name="azure-portal"></a>Portail Azure

Webhook de hello toousing préalable sur le conteneur de l’image par émission de données et supprimer des actions, il peut être testé à l’aide de hello **Ping** bouton. Lorsqu’il est utilisé, hello Ping envoie qu'un toohello de la demande post générique spécifié de point de terminaison et les journaux de réponse hello. Cela s’avère utile tooverify qui hello webhook a été configuré correctement.

1. Sélectionnez webhook hello souhaité tootest. 
2. Dans la barre d’outils supérieure hello, sélectionnez l’action de « Ping » de hello. 
3. Demande de vérification de hello et de réponse.

### <a name="azure-cli"></a>Interface de ligne de commande Azure

tootest un webhook ACR avec hello CLI d’Azure, utilisez hello [ping de webhook az acr](/cli/azure/acr/webhook#ping) commande.

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

résultats de hello toosee, utilisez hello [az acr webhook événements de la liste](/cli/azure/acr/webhook#list-events) commande. 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a>Supprimer un webhook

### <a name="azure-portal"></a>Portail Azure

Chaque webhook peut être supprimé en sélectionnant hello webhook, puis le bouton Supprimer hello hello portail Azure.

### <a name="azure-cli"></a>Interface de ligne de commande Azure

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```