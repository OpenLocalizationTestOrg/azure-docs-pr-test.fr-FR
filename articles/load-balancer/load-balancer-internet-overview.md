---
title: "aaaInternet faisant face à la vue d’ensemble du programme d’équilibrage de charge | Documents Microsoft"
description: "Présentation de l’équilibrage de charge accessible sur Internet et ses fonctionnalités. Fonctionnement de l’équilibrage de charge pour Azure avec des machines virtuelles et des services cloud."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 529b37aa-a45c-41d1-8877-fee8cc1fa375
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3514f945d69ec576ed256cdd01069491e3e43936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-facing-load-balancer-overview"></a>Présentation de l’équilibrage de charge accessible sur Internet

Équilibrage de charge Azure mappe hello publique IP adresse et numéro de port du trafic toohello privé IP adresse et le port numéro entrant de machine virtuelle de hello et vice versa, pour le trafic de réponse hello à partir de l’ordinateur virtuel de hello. Règles d’équilibrage de charge permettent de toodistribute des types spécifiques de trafic entre plusieurs machines virtuelles ou services. Par exemple, vous pouvez répartir la charge hello du trafic de demande web sur plusieurs serveurs web ou les rôles web.

Pour un service cloud qui contient des instances de rôles web ou des rôles de travail, vous pouvez définir un point de terminaison public dans le fichier de définition (.csdef) de service hello.

Hello *servicedefinition.csdef* fichier contient la configuration de point de terminaison hello et lorsque vous avez plusieurs instances de rôle pour un déploiement de rôle web ou de travail, équilibrage de charge hello sera installé pour celle-ci. déploiement de cloud computing Hello moyen tooadd instances tooyour change hello nombre d’instances sur le fichier de configuration de service hello (.csfg).

Hello figure suivante illustre un point de terminaison avec équilibrage de charge pour le trafic web est partagé entre trois machines virtuelles pour hello public et privé le port TCP 80. Celles-ci sont incluses dans un jeu d’équilibrage de la charge.

![exemple d’équilibrage de charge public](./media/load-balancer-internet-overview/IC727496.png)

Figure 1 : point de terminaison d’équilibrage de charge pour le trafic web

Lorsque les clients Internet envoient des demandes de page web toohello une adresse IP publique du service de cloud hello sur le port TCP 80, hello équilibrage de charge Azure distribue les requêtes de hello entre hello trois machines virtuelles dans le jeu d’équilibrage de charge hello. Pour plus d’informations sur les algorithmes d’équilibrage de charge, consultez hello [page de vue d’ensemble d’équilibrage de charge](load-balancer-overview.md#load-balancer-features).

Par défaut, Azure Load Balancer répartit le trafic réseau équitablement sur plusieurs instances de machine virtuelle. Vous pouvez également configurer l’affinité de session. Pour plus d’informations, consultez [Mode de distribution d’équilibrage de charge](load-balancer-distribution-mode.md).

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur [équilibreur de charge interne](load-balancer-internal-overview.md) toobetter comprendre quel équilibreur de charge est plus adaptée à votre déploiement de cloud.

Vous pouvez également [commencer par créer un équilibreur de charge avec accès par Internet](load-balancer-get-started-internet-arm-ps.md) et configurer le type de [mode de distribution](load-balancer-distribution-mode.md) pour un comportement spécifique de trafic réseau d’équilibrage de charge.

Si votre application doit tookeep connexions actives pour les serveurs situés derrière un équilibreur de charge, vous pouvez en savoir plus sur [les paramètres de délai d’expiration TCP pour un équilibrage de charge des temps d’inactivité](load-balancer-tcp-idle-timeout.md). Il aidera toolearn sur le comportement des connexions inactives lorsque vous utilisez l’équilibrage de charge Azure.
