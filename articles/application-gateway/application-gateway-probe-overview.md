---
title: "aaaHealth la présentation des moniteurs pour la passerelle d’Application Azure | Documents Microsoft"
description: "En savoir plus sur hello surveillance des fonctionnalités de la passerelle d’Application Azure"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7eeba328-bb2d-4d3e-bdac-7552e7900b7f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 5091d80394a354ff849ce7ccee8cc9d2fd0456db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-health-monitoring-overview"></a>Vue d’ensemble de l’analyse d’intégrité Application Gateway

Passerelle d’Application Azure par défaut surveille l’intégrité de hello de toutes les ressources dans son pool principal et supprime automatiquement n’importe quelle ressource considéré comme non intègre de pool de hello. Passerelle d’application continue des instances non intègre de toomonitor hello et ajoute les sauvegarder pool principal intègre de toohello une fois qu’ils deviennent disponibles et des sondes toohealth de répondre. Passerelle d’application envoie les sondes d’intégrité hello hello même port est défini dans les paramètres HTTP hello back-end. Cette configuration garantit que sonde hello teste hello même port que les clients utilisent tooconnect toohello principal.

![exemple de sonde application gateway][1]

Ajout toousing par défaut d’intégrité sonde analyse, vous pouvez également personnaliser toosuit de sonde d’intégrité hello exigences de votre application. Dans cet article, nous nous intéressons aux sondes d’intégrité par défaut et personnalisées.

> [!NOTE]
> S’il existe un groupe de sécurité réseau sur le sous-réseau de passerelle d’Application, les plages de ports 65503-65 534 doivent être ouvert sur le sous-réseau de passerelle d’Application hello pour le trafic entrant. Ces ports sont requis pour hello principal d’intégrité API toowork.

## <a name="default-health-probe"></a>Sonde d’intégrité par défaut

Une passerelle d’application configure automatiquement une sonde d’intégrité par défaut lorsque vous ne définissez pas de configuration de sonde personnalisée. Hello analyse le comportement fonctionne en créant que des adresses IP toohello demande HTTP configuré pour le pool principal de hello. Pour les sondes par défaut si hello principal http est configuré pour le protocole HTTPS, sonde de hello utilise HTTPS en tant que contrôle d’intégrité tootest bien des serveurs principaux hello.

Par exemple : vous configurez votre application passerelle toouse serveurs principaux A, B et C tooreceive HTTP le trafic réseau sur le port 80. surveillance de l’état par défaut de Hello teste trois serveurs de hello pour une réponse HTTP intègre toutes les 30 secondes. Le [code d’état](https://msdn.microsoft.com/library/aa287675.aspx) d’une réponse HTTP correcte est compris entre 200 et 399.

En cas de vérification de sonde hello par défaut pour le serveur A, passerelle d’application hello retire son pool principal et le trafic réseau cesse de circuler toothis server. Sonde Hello garde toocheck pour le serveur une toutes les 30 secondes. Lorsque le serveur A répond correctement tooone demande à partir d’une sonde d’intégrité par défaut, il est rajouté en tant que pool principal de toohello intègre et démarre le trafic circulant toohello server à nouveau.

### <a name="default-health-probe-settings"></a>Paramètres de sonde d’intégrité par défaut

| Propriétés de la sonde | Valeur | Description |
| --- | --- | --- |
| URL de sonde |http://127.0.0.1:\<port\>/ |Chemin d'accès de l'URL |
| Intervalle |30 |Intervalle d’analyse en secondes |
| Délai d’attente |30 |Délai d’expiration de l’analyse en secondes |
| Seuil de défaillance sur le plan de l’intégrité |3 |Nombre de tentatives d’analyse serveur principal de Hello est marquée vers le bas après que le nombre d’échecs de sonde consécutifs hello a atteint le seuil de défaillance hello. |

> [!NOTE]
> Hello port est hello même port en tant que paramètres de HTTP hello back-end.

Sonde Hello examine uniquement http://127.0.0.1 :\<port\> toodetermine l’état d’intégrité. Si vous devez tooconfigure hello d’intégrité toogo tooa personnalisé URL de sonde ou modifiez d’autres paramètres, vous devez utiliser les sondes personnalisé comme décrit dans hello comme suit :

## <a name="custom-health-probe"></a>Sonde d’intégrité personnalisée

Les sondes personnalisées permettent de toohave un contrôle plus précis sur la surveillance de l’intégrité hello. Lorsque vous utilisez des sondes personnalisés, vous pouvez configurer intervalle d’analyse hello tootest d’URL et le chemin d’accès hello et combien tooaccept d’échecs de réponse avant de marquer l’instance du pool de back-end hello comme étant défectueux.

### <a name="custom-health-probe-settings"></a>Paramètres de sonde d’intégrité personnalisée

Hello tableau suivant fournit les définitions pour les propriétés d’une sonde de l’intégrité personnalisée hello.

| Propriétés de la sonde | Description |
| --- | --- |
| Nom |Nom de la sonde de hello. Ce nom est sonde de toohello toorefer utilisés dans les paramètres HTTP du serveur principal. |
| Protocole |Protocole utilisé sonde de hello toosend. Sonde de Hello utilise le protocole de hello définie dans les paramètres HTTP hello principal |
| Host |Hôte toosend hello de sonde à nom. S’applique uniquement lorsque plusieurs sites sont configurés sur Application Gateway, sinon utilisez '127.0.0.1'. Cette valeur est différente du nom d’hôte de la machine virtuelle. |
| Chemin |Chemin d’accès relatif de sonde de hello. chemin d’accès valide de Hello commence à partir de '/'. |
| Intervalle |Intervalle d’analyse en secondes. Cette valeur est l’intervalle de temps hello entre deux analyses consécutives. |
| Délai d’attente |Délai d’expiration de l’analyse en secondes. Si une réponse valide n’est pas reçue dans ce délai, la sonde de hello est marquée comme ayant échoué.  |
| Seuil de défaillance sur le plan de l’intégrité |Nombre de tentatives d’analyse serveur principal de Hello est marquée vers le bas après que le nombre d’échecs de sonde consécutifs hello a atteint le seuil de défaillance hello. |

> [!IMPORTANT]
> Si la passerelle d’Application est configurée pour un site unique, par hello de valeur par défaut hôte nom doit être spécifié sous la forme '127.0.0.1', à moins que sinon configurés dans une sonde personnalisée.
> Pour référence, une sonde personnalisée est envoyée trop\<protocole\>://\<hôte\>:\<port\>\<chemin d’accès\>. Hello port utilisé sera hello même port, tel que défini dans les paramètres HTTP hello back-end.

## <a name="next-steps"></a>Étapes suivantes
Après l’apprentissage sur la surveillance de l’intégrité de passerelle d’Application, vous pouvez configurer un [sonde de l’intégrité personnalisée](application-gateway-create-probe-portal.md) Bonjour portail Azure ou un [sonde de l’intégrité personnalisée](application-gateway-create-probe-ps.md) à l’aide de PowerShell et hello Azure Resource Manager modèle de déploiement.

[1]: ./media/application-gateway-probe-overview/appgatewayprobe.png
