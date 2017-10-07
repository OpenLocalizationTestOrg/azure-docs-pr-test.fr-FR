---
title: "aaaApplication ou spécifiques à l’utilisateur Marathon service | Documents Microsoft"
description: "Créer un service Marathon lié à une application ou à un utilisateur donnés"
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Conteneurs, Marathon, micro-services, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 1e6f69ed64e113a3a059788a71ddb57b6d3ad8da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a>Créer un service Marathon lié à une application ou à un utilisateur donnés
Azure Container Service fournit un ensemble de serveurs maîtres sur lesquels nous préconfigurons Apache Mesos et Marathon. Ceux-ci peuvent être utilisé tooorchestrate vos applications sur un cluster de hello, mais elle ne meilleures pas toouse hello serveurs maîtres à cet effet. Par exemple, configuration hello de Marathon un ajustement nécessite la connexion à des serveurs maîtres hello eux-mêmes et apporter des modifications--ce encourage les serveurs maîtres uniques qui sont un peu différente de hello standard et toobe besoin s’et managé indépendamment. En outre, configuration hello requise par une équipe peut-être pas une configuration optimale hello pour une autre équipe.

Dans cet article, nous expliquerons comment tooadd un service Marathon application ou spécifiques à l’utilisateur.

Étant donné que ce service appartiendra tooa seul utilisateur ou l’équipe, ils sont tooconfigure libre de toute manière qu’ils souhaitent. En outre, Service de conteneur Azure garantit que le service de hello continue toorun. Si le service de hello échoue, le Service de conteneur Azure redémarre pour vous. La plupart du temps de hello vous ne même remarquer qu’elle avait le temps d’arrêt.

## <a name="prerequisites"></a>Composants requis
[Déployer une instance de Service de conteneur Azure](container-service-deployment.md) avec orchestrator le type de contrôleur de domaine/système d’exploitation et [vous assurer que votre client peut se connecter tooyour cluster](../container-service-connect.md). En outre, hello comme suit.

[!INCLUDE [install hello DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a>Créer un service Marathon lié à une application ou à un utilisateur donnés
Commencez par créer un fichier de configuration JSON qui définit le nom de hello du service de l’application hello que vous souhaitez toocreate. Ici, nous utilisons `marathon-alice` en tant que nom d’infrastructure hello. Enregistrer le fichier de hello comme `marathon-alice.json`:

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

Ensuite, utiliser hello CLI de contrôleur de domaine/système d’exploitation tooinstall hello Marathon instance avec les options hello qui sont définies dans votre fichier de configuration :

```bash
dcos package install --options=marathon-alice.json marathon
```

Vous devez maintenant voir votre `marathon-alice` service en cours d’exécution dans l’onglet Services de hello de votre interface utilisateur de contrôleur de domaine/système d’exploitation. Hello l’interface utilisateur sera `http://<hostname>/service/marathon-alice/` si vous souhaitez tooaccess directement.

## <a name="set-hello-dcos-cli-tooaccess-hello-service"></a>Définir hello CLI de contrôleur de domaine/système d’exploitation tooaccess service de hello
Vous pouvez éventuellement configurer votre tooaccess CLI de contrôleur de domaine/système d’exploitation ce service en définissant un hello `marathon.url` propriété toopoint toohello `marathon-alice` de l’instance comme suit :

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

Vous pouvez vérifier quelle instance de Marathon utilisée par votre CLI contre hello `dcos config show` commande. Vous pouvez rétablir toousing votre service Marathon maître avec la commande hello `dcos config unset marathon.url`.

