---
title: application de conteneur DC/OS aaaEnable access tooAzure | Documents Microsoft
description: "Comment tooenable public accéder aux conteneurs tooDC/système d’exploitation dans le Service de conteneur Azure."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: Docker, conteneurs, micro-services, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 1ba251ba5a176a6a5e1c7831655164e380a62b27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-public-access-tooan-azure-container-service-application"></a>Activer l’application de Service de conteneur Azure tooan accès public
N’importe quel conteneur de contrôleur de domaine/système d’exploitation Bonjour ACS [pool d’agents publics](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) est exposé automatiquement toohello internet. Par défaut, les ports **80**, **443**, **8080** sont ouverts, et tous les conteneurs (publics) à l’écoute sur ces ports sont accessibles. Cet article vous explique comment tooopen ports plus pour vos applications dans le conteneur de Service Azure.

## <a name="open-a-port-portal"></a>Ouvrir un port (portail)
Tout d’abord, nous avons besoin du port de hello tooopen que nous voulons.

1. Ouvrez une session dans toohello portal.
2. Groupe de ressources hello recherche que vous avez déployé Bonjour Azure conteneur de Service.
3. Sélectionnez l’équilibrage de charge de l’agent hello (qui est le même nom trop**XXXX-agent-lb-XXXX**).
   
    ![Équilibrage de charge dans Azure Container Service](./media/container-service-enable-public-access/agent-load-balancer.png)
4. Cliquez sur **Sondes**, puis sur **Ajouter**.
   
    ![Sondes d’équilibrage de charge dans Azure Container Service](./media/container-service-enable-public-access/add-probe.png)
5. Remplissez le formulaire de sonde hello et cliquez sur **OK**.
   
   | Champ | Description |
   | --- | --- |
   | Nom |Un nom descriptif de sonde de hello. |
   | Port |port Hello hello conteneur tootest. |
   | Chemin |(En mode HTTP) hello tooprobe de chemin d’accès relatif de site Web. HTTPS non pris en charge. |
   | Intervalle |Durée Hello entre sonde tentatives en secondes. |
   | Seuil de défaillance sur le plan de l’intégrité |Nombre de sonde consécutifs tentatives avant de considérer le conteneur de hello défectueux. |
6. Retour sur les propriétés de hello d’équilibrage de charge de l’agent de hello, cliquez sur **règles d’équilibrage de charge** , puis **ajouter**.
   
    ![Règles d’équilibrage de charge dans Azure Container Service](./media/container-service-enable-public-access/add-balancer-rule.png)
7. Remplissez le formulaire d’équilibrage de charge hello et cliquez sur **OK**.
   
   | Champ | Description |
   | --- | --- |
   | Nom |Un nom descriptif d’équilibrage de charge hello. |
   | Port |Hello publique le port entrant. |
   | Port principal |port public interne Hello hello conteneur tooroute le trafic. |
   | Pool principal |conteneurs Hello dans ce pool seront cible hello pour cet équilibrage de charge. |
   | Sonde |Hello toodetermine de sonde utilisée si une cible Bonjour **pool principal** est sain. |
   | Persistance de session |Détermine comment le trafic à partir d’un client doit être géré pour la durée de session de hello hello.<br><br>**Aucun**: les demandes successives d’hello même client peut être gérée par n’importe quel conteneur.<br>**Client IP**: les demandes successives d’hello même adresse IP du client sont gérées par hello même conteneur.<br>**Client IP et le protocole**: les demandes successives d’hello même combinaison d’adresse IP et le protocole du client sont gérées par hello même conteneur. |
   | Délai d’inactivité |TCP (uniquement) En quelques minutes, hello tookeep de temps un client TCP/HTTP ouvrir sans se baser sur *KeepAlive* messages. |

## <a name="add-a-security-rule-portal"></a>Ajouter une règle de sécurité (portail)
Ensuite, nous devons tooadd une règle de sécurité qui achemine le trafic à partir de notre port ouvert via le pare-feu hello.

1. Ouvrez une session dans toohello portal.
2. Groupe de ressources hello recherche que vous avez déployé Bonjour Azure conteneur de Service.
3. Sélectionnez hello **public** groupe de sécurité de l’agent réseau (qui est le même nom trop**XXXX-agent-public-groupe de sécurité réseau-XXXX**).
   
    ![Groupe de sécurité réseau Azure Container Service](./media/container-service-enable-public-access/agent-nsg.png)
4. Sélectionnez les **règles de sécurité de trafic entrant**, puis cliquez sur **Ajouter**.
   
    ![Règles du groupe de sécurité réseau Azure Container Service](./media/container-service-enable-public-access/add-firewall-rule.png)
5. Entrez votre port public tooallow de règle de pare-feu hello et cliquez sur **OK**.
   
   | Champ | Description |
   | --- | --- |
   | Nom |Un nom descriptif hello de règle de pare-feu. |
   | Priorité |Rang de priorité pour la règle de hello. Hello inférieur hello numéro hello hello prioritaires. |
   | Source |Restreindre hello entrants IP adresse plage toobe autorisé ou refusé par cette règle. Utilisez **tout** toonot spécifient une restriction. |
   | Service |Sélectionner un ensemble de services prédéfinis concerné par cette règle de sécurité. Sinon, utilisez **personnalisé** toocreate votre propre. |
   | Protocole |Restreindre le trafic basé sur **TCP** ou **UDP**. Utilisez **tout** toonot spécifient une restriction. |
   | Plage de ports |Lorsque **Service** est **personnalisé**, spécifie la plage de hello de ports que cette règle affecte. Vous pouvez utiliser un port unique, tel que **80** ou une plage comme **1024-1500**. |
   | Action |Autoriser ou refuser le trafic qui répond aux critères de hello. |

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur la différence de hello [agents de contrôleur de domaine/système d’exploitation publiques et privées](container-service-dcos-agents.md).

En savoir plus sur la [gestion de vos conteneurs DC/OS](container-service-mesos-marathon-ui.md).

