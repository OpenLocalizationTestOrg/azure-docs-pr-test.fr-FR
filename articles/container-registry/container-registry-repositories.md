---
title: "référentiels de Registre de conteneur aaaAzure | Documents Microsoft"
description: "Comment toouse les référentiels de Registre de conteneur Azure pour les images de Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: cristyg
ms.openlocfilehash: 108622c565e41777fbb1fc9da9a01168abc7a7fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a>Référentiels Azure Container Registry

Registre de conteneur Azure vous permet des images de conteneur toostore dans des référentiels. En stockant les images dans des référentiels, vous pouvez créer des groupes d’images (ou une version de ces images) au sein d’environnements isolés. Vous pouvez spécifier ces référentiels lorsque vous appuyez sur le Registre de tooyour d’images.


## <a name="prerequisites"></a>Composants requis
* **Azure Container Registry** : créez un Registre de conteneur dans votre abonnement Azure. Par exemple, utiliser hello [portail Azure](container-registry-get-started-portal.md) ou hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).
* **Docker CLI** -tooset de votre ordinateur local en tant qu’un ordinateur hôte et l’accès hello Docker CLI commandes Docker, installez [moteur Docker](https://docs.docker.com/engine/installation/).
* **Extraire une image** - extraire une image à partir du Registre du Hub Docker publique hello marquer et poussez-le tooyour Registre. Pour obtenir des conseils sur la façon de push et pull des images, consultez [Registre privé de Push Docker image tooAzure](container-registry-get-started-docker-cli.md).


## <a name="viewing-repositories-in-hello-portal"></a>Affichage des référentiels dans hello portail

Une fois que vous avez envoyée Registre de conteneur tooyour images, vous pouvez voir une liste de référentiels hello images hello Bonjour Azure portal d’hébergement.

Si vous avez suivi les étapes de hello Bonjour [Registre privé de Push de Docker image tooAzure](container-registry-get-started-docker-cli.md) article, vous devez maintenant avoir une image Nginx dans le Registre de conteneur. Dans le cadre d’instructions de hello, vous devez spécifié un espace de noms pour l’image de hello. Dans l’exemple hello ci-dessous, commande hello pousse le référentiel « exemples » toohello hello NGinx image :

```
docker push myregistry.azurecr.io/samples/nginx
```
 Azure Container Registry prend en charge les espaces de noms de référentiel à plusieurs niveaux. Cette fonctionnalité permet de vous toogroup collections d’application spécifique d’images tooa connexes, ou une collection de développement de toospecific d’applications ou les équipes d’exploitation. tooread en savoir plus sur les référentiels dans les registres de conteneur, consultez [registres de conteneur privé Docker dans Azure](container-registry-intro.md).

référentiels de Registre tooview hello conteneur :

1. Ouvrez une session dans toohello portail Azure
2. Sur hello **Registre de conteneur Azure** panneau, Registre de select hello vous souhaitez tooinspect
3. Dans le panneau de Registre hello, cliquez sur **référentiels** toosee une liste de tous les référentiels hello et leurs images.
4. (Facultatif) Sélectionnez un toosee les balises d’image spécifique

![Référentiels dans le portail de hello](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous connaissez les principes de base hello, vous êtes prêt toostart à l’aide de votre Registre ! Par exemple, début du déploiement de conteneur images tooan [Service de conteneur Azure](https://azure.microsoft.com/documentation/services/container-service/) cluster.
