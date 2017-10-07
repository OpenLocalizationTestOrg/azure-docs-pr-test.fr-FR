---
title: aaaPush Docker image tooprivate Registre Azure | Documents Microsoft
description: "Push et pull Docker Registre de conteneur privé tooa images dans Azure à l’aide de hello Docker CLI"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 64fbe43f-fdde-4c17-a39a-d04f2d6d90a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a81a6f4bfcb23642a89ac7631348d40e2f4911a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="push-your-first-image-tooa-private-docker-container-registry-using-hello-docker-cli"></a>Push de votre première image tooa privé Docker Registre de conteneur à l’aide de hello Docker CLI
Un Registre de conteneur Azure stocke et gère des privé [Docker](http://hub.docker.com) les images de conteneur, toohello similaire moyen [Hub d’ancrage](https://hub.docker.com/) stocke les images Docker publiques. Vous utilisez hello [Interface de ligne de commande Docker](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) pour [connexion](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [extraction](https://docs.docker.com/engine/reference/commandline/pull/)et d’autres opérations sur le conteneur Registre.

Pour plus d’informations et des concepts, consultez [hello vue d’ensemble](container-registry-intro.md)



## <a name="prerequisites"></a>Composants requis
* **Azure Container Registry** : créez un Registre de conteneur dans votre abonnement Azure. Par exemple, utiliser hello [portail Azure](container-registry-get-started-portal.md) ou hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).
* **Docker CLI** -tooset de votre ordinateur local en tant qu’un ordinateur hôte et l’accès hello Docker CLI commandes Docker, installez [moteur Docker](https://docs.docker.com/engine/installation/).

## <a name="log-in-tooa-registry"></a>Ouvrez une session dans le Registre de tooa
Exécutez `docker login` toolog dans le Registre de conteneur tooyour avec votre [informations d’identification du Registre](container-registry-authentication.md).

Hello exemple suivant passe hello ID et mot de passe d’Azure Active Directory [principal du service](../active-directory/active-directory-application-objects.md). Par exemple, vous avez peut-être affectés un Registre tooyour principal de service pour un scénario d’automatisation.

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> Rend le nom de Registre complet de hello de que toospecify (tout en minuscules). Dans cet exemple, il s’agit de `myregistry.azurecr.io`.

## <a name="steps-toopull-and-push-an-image"></a>Étapes toopull et transmettez une image
Hello suivre exemple téléchargements hello image Nginx à partir du Registre du Hub Docker publique hello, balises pour le Registre de votre conteneur Azure privée, il transmet tooyour Registre, puis il extrait à nouveau.

**1. Extraire l’image officiel du Docker hello pour Nginx**

Première extraction hello publique Nginx image tooyour ordinateur local.

```
docker pull nginx
```
**2. Démarrez le conteneur de Nginx hello**

Hello commande suivante démarre les conteneur Nginx local hello interactivement sur le port 8080, ce qui permet de sortie de toosee de Nginx. Il supprime hello conteneur une fois arrêté en cours d’exécution.

```
docker run -it --rm -p 8080:80 nginx
```

Parcourir trop[http://localhost : 8080](http://localhost:8080) hello tooview conteneur en cours d’exécution. Vous voyez un toohello similaire écran suivant un.

![Nginx sur un ordinateur local](./media/container-registry-get-started-docker-cli/nginx.png)

toostop hello conteneur en cours d’exécution, appuyez sur [CTRL] + [C].

**3. Créer un alias de l’image de hello dans votre Registre.**

Hello commande suivante crée un alias de l’image de hello, avec un Registre tooyour de chemin d’accès qualifié complet. Cet exemple spécifie hello `samples` encombrement de l’espace de noms tooavoid dans la racine du Registre de hello hello.

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

**4. Push hello image tooyour Registre**

```
docker push myregistry.azurecr.io/samples/nginx
```

**5. Image de hello par extraction de données à partir de votre Registre.**

```
docker pull myregistry.azurecr.io/samples/nginx
```

**6. Démarrer le conteneur de Nginx hello du Registre**

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

Parcourir trop[http://localhost : 8080](http://localhost:8080) hello tooview conteneur en cours d’exécution.

toostop hello conteneur en cours d’exécution, appuyez sur [CTRL] + [C].

**7. (Facultatif) Supprimer une image de hello**

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a>Limites simultanées
Dans certains scénarios, l’exécution des appels simultanément peut générer des erreurs. Hello tableau suivant contient les limites de hello d’appels simultanés avec des opérations « Émission » et « Collecte » sur le Registre de conteneur Azure :

| Opération  | Limite                                  |
| ---------- | -------------------------------------- |
| PULL       | Des too10 simultanées extrait par le Registre |
| PUSH       | Des too5 simultanées exécute un push par le Registre |

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous connaissez les principes de base hello, vous êtes prêt toostart à l’aide de votre Registre ! Par exemple, début du déploiement de conteneur images tooan [Service de conteneur Azure](https://azure.microsoft.com/documentation/services/container-service/) cluster.
