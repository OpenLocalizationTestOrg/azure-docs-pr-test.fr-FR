---
title: aaaAuthenticate avec un Registre de conteneur Azure | Documents Microsoft
description: "Comment toolog dans le Registre de conteneur Azure tooan à l’aide d’Azure Active Directory service principal ou un compte d’administrateur"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 128a937a-766a-415b-b9fc-35a6c2f27417
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a0b0462e8432b2567689debca322e2426baa7fa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a>S’authentifier avec un registre de conteneurs Docker
toowork avec les images de conteneur dans un Registre de conteneur Azure, vous vous connectez à l’aide de hello `docker login` commande. Vous pouvez vous connecter en utilisant un **[principal du service Azure Active Directory](../active-directory/active-directory-application-objects.md)** ou un **compte d’administrateur** spécifique à un registre. Cet article fournit des détails sur ces identités.



## <a name="service-principal"></a>Principal du service

Vous pouvez [affecter un principal de service](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour Registre et l’utiliser pour l’authentification de base Docker. L’utilisation d’un principal du service est recommandée dans la plupart des scénarios. Fournir l’ID de l’application hello et le mot de passe toohello principal du service hello `docker login` de commande, comme indiqué dans hello l’exemple suivant :

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Une fois connecté, Docker met en cache les informations d’identification de hello, vous n’avez pas besoin d’identifiant d’application tooremember hello.

> [!TIP]
> Si vous le souhaitez, vous pouvez régénérer le mot de passe hello d’un principal de service en exécutant hello `az ad sp reset-credentials` commande.
>


Autoriser les principaux du service [accès en fonction du rôle](../active-directory/role-based-access-control-configure.md) tooa Registre. Les rôles disponibles sont les suivants :
  * Lecteur (extraction).
  * Contributeur (extraction et envoi).
  * Propriétaire (par extraction de données, par envoi de données et affecter des rôles utilisateurs tooother).

L’accès anonyme n’est pas disponible sur les registres de conteneur Azure. Pour des images publiques, vous pouvez utiliser [Docker Hub](https://docs.docker.com/docker-hub/).

Vous pouvez affecter plusieurs principaux de service de Registre tooa, ce qui vous permet d’accéder toodefine pour différents utilisateurs ou les applications. Principaux de service permettent également de Registre tooa connectivité « sans affichage » développeur ou DevOps scénarios hello exemple suivant :

  * Déploiements de conteneur à partir d’un système de tooorchestration de Registre, y compris le contrôleur de domaine/système d’exploitation, Docker Swarm et Kubernetes. Vous pouvez également extraire toorelated de registres de conteneur des services Azure tels que [Service de conteneur](../container-service/index.yml), [du Service d’applications](../app-service/index.md), [lot](../batch/index.md), [Service Fabric](/azure/service-fabric/)et d’autres.

  * Continue intégration et le déploiement des solutions (tels que Visual Studio Team Services ou Jenkins) qui génèrent des images de conteneur et de les transmettre tooa Registre.





## <a name="admin-account"></a>Compte d’administrateur
Un compte d’administrateur est créé automatiquement pour chaque registre que vous créez. Compte de hello est désactivé par défaut, mais vous pouvez l’activer et gérer les informations d’identification hello, par exemple via hello [portal](container-registry-get-started-portal.md#manage-registry-settings) ou à l’aide de hello [Azure CLI 2.0 commandes](container-registry-get-started-azure-cli.md#manage-admin-credentials). Chaque compte d’administrateur reçoit deux mots de passe qui peuvent être régénérés. deux mots de passe Hello permettent de Registre de toohello toomaintain connexions en utilisant un mot de passe pendant la régénération de hello autre mot de passe. Si le compte de hello est activé, vous pouvez passer le nom d’utilisateur hello et soit toohello de mot de passe `docker login` commande de Registre toohello de l’authentification de base. Par exemple :

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> compte d’administrateur Hello est conçu pour un seul utilisateur tooaccess hello du Registre, principalement à des fins de test. Il est recommandé pas les informations d’identification du compte de l’administrateur tooshare hello parmi d’autres utilisateurs. Tous les utilisateurs apparaissent sous la forme d’un Registre de toohello utilisateur unique. La modification ou la désactivation de ce compte désactive l’accès au Registre pour tous les utilisateurs qui utilisent des informations d’identification hello.
>


### <a name="next-steps"></a>Étapes suivantes
* [Push de votre première image à l’aide de hello Docker CLI](container-registry-get-started-docker-cli.md).
* Pour plus d’informations sur l’authentification dans l’aperçu du Registre de conteneur hello, consultez hello [billet de blog](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).
