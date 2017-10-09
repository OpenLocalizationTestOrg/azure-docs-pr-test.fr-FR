---
title: "aaaCreate basée sur un chemin d’accès de règle - passerelle d’Application Azure - Azure Portal | Documents Microsoft"
description: "Découvrez comment toocreate une règle basée sur le chemin d’accès pour une passerelle d’application à l’aide de hello portail"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 87bd93bc-e1a6-45db-a226-555948f1feb7
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 21cb52c426ca5f7dfedf07a96e87fbc85d243647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-hello-portal"></a>Créer une règle basée sur le chemin d’accès pour une passerelle d’application à l’aide du portail de hello

> [!div class="op_single_selector"]
> * [Portail Azure](application-gateway-create-url-route-portal.md)
> * [Commandes PowerShell pour Azure Resource Manager](application-gateway-create-url-route-arm-ps.md)
> * [Azure CLI 2.0](application-gateway-create-url-route-cli.md)

Le routage basé sur le chemin d’accès URL permet d’itinéraires tooassociate vous basés sur le chemin de l’URL de demande Http hello. Il vérifie s’il existe un pool de back-end tooa itinéraire configuré pour les URL hello répertorié dans hello passerelle d’Application et envoie toohello de trafic réseau hello défini par pool de back-end. Une utilisation courante pour le routage basé sur l’URL est équilibrer les demandes de tooload pour les pools de serveur principal toodifferent différents types de contenu.

Le routage basé sur des URL introduit une nouvelle passerelle de tooapplication de type de règle. La passerelle d’application a deux types de règles : des règles de base et des règles basées sur un chemin. Hello du type de règle de base, fournit service tourniquet pour les principaux hello pools lors de règles basées sur le chemin d’accès en outre distribution Round robin de tooround, prend également le modèle de chemin d’accès de l’URL de demande hello en compte tout en appuyant sur le pool principal approprié de hello.

## <a name="scenario"></a>Scénario

Hello scénario suivant passe par la création d’une règle basée sur le chemin d’accès dans une passerelle d’application existant.
Hello scénario part du principe que vous avez déjà suivi les étapes de hello trop[créer une passerelle d’Application](application-gateway-create-gateway-portal.md).

![itinéraire d’URL][scenario]

## <a name="createrule"></a>Créer une règle basée sur le chemin d’accès hello

Une règle basée sur le chemin d’accès requiert son propre port d’écoute, avant de créer la règle de hello être tooverify que vous avez un toouse écouteur disponible.

### <a name="step-1"></a>Étape 1

Accédez toohello [portail Azure](http://portal.azure.com) et sélectionnez une passerelle d’application existant. Cliquer sur **Règles**

![Vue d’ensemble d’Application Gateway][1]

### <a name="step-2"></a>Étape 2

Cliquez sur **basée sur le chemin d’accès** bouton tooadd une règle basée sur le chemin d’accès.

### <a name="step-3"></a>Étape 3 :

Hello **ajouter une règle basée sur le chemin d’accès** panneau a deux sections. première section de Hello est où vous avez défini l’écouteur de hello, nom hello de règle de hello et les paramètres de chemin d’accès par défaut hello. paramètres de chemin d’accès par défaut Hello sont pour les itinéraires qui ne relèvent pas de l’itinéraire de basée sur le chemin d’accès personnalisées hello. Hello deuxième section Hello **ajouter une règle basée sur le chemin d’accès** lame est où vous définissez les règles de chemin d’accès hello eux-mêmes.

**Paramètres de base**

* **Nom** -cette valeur est une règle de toohello nom convivial qui est accessible dans le portail de hello.
* **Écouteur** -cette valeur est le port d’écoute hello est utilisé pour la règle de hello.
* **Par défaut du pool principal** -ce paramètre est le paramètre hello qui définit hello principal toobe est utilisé pour la règle par défaut de hello
* **Paramètres HTTP par défaut** -ce paramètre est le paramètre hello qui définit toobe de paramètres hello HTTP utilisé pour la règle par défaut de hello.

**Path-based rules (Règles basées sur le chemin)**

* **Nom** -cette valeur est une règle nom toopath convivial.
* **Chemins d’accès** -ce paramètre définit hello chemin hello règle recherche lors de la transmission du trafic
* **Pool principal** -ce paramètre est le paramètre hello qui définit hello principal toobe est utilisé pour la règle de hello
* **Paramètre HTTP** -ce paramètre est le paramètre hello qui définit toobe de paramètres hello HTTP utilisé pour la règle de hello.

> [!IMPORTANT]
> Chemins d’accès : liste hello de toomatch de modèles de chemin d’accès. Chacun doit commencer par / et hello uniquement une «\*» est autorisé à hello fin. /xyz, /xyz* ou /xyz/* sont des exemples valides.  

![Ajouter un panneau Règle basée sur le chemin contenant toutes les informations][2]

Ajout d’une règle basée sur le chemin d’accès de tooan passerelle d’application existant est un processus simple via le portail de hello. Après avoir créé une règle basée sur le chemin d’accès, il peut être modifié tooadd des règles supplémentaires. 

![ajouter des règles supplémentaires basés sur le chemin][3]

Cette étape configure une route basée sur un chemin. Il toounderstand important que les demandes ne sont pas réécrit, comme les demandes proviennent de la passerelle d’application inspecte la demande de hello et basic en hello url modèle envoie hello demande toohello approprié back-end.

## <a name="next-steps"></a>Étapes suivantes

toolearn tooconfigure le déchargement SSL avec la passerelle d’Application Azure, voir [configurer le déchargement SSL](application-gateway-ssl-portal.md)

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
