---
title: "aaaAn application de Proxy d’Application prend trop de temps tooload | Documents Microsoft"
description: "Les problèmes de performances de chargement de page avec hello Proxy d’Application Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4c7a51f96840966a1d88933fa4e30f39479d8a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="an-application-proxy-application-takes-too-long-tooload"></a>Une application de Proxy d’Application prend trop de temps tooload

Cet article vous a-t-il toounderstand pourquoi une application de Proxy d’Application Azure AD peut prendre un tooload beaucoup de temps et ce que vous pouvez effectuer tooresolve ce problème.

## <a name="overview"></a>Vue d'ensemble
Si vos applications fonctionnent, mais que vous consultez un temps de latence, il peut être quelques modifications mineures dans votre topologie de réseau que vous pouvez envisager la vitesse tooimprove hello. Pour une évaluation des différentes topologies, consultez hello [document de considérations réseau](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).

Si ces considérations ne vous aident pas à résoudre le problème, nous n’avons malheureusement pas d’autres recommandations relatives au réglage des performances. Comme hello service Proxy d’Application développe toomore des centres de données qui peuvent être tooyou plus proche, vous pouvez démarrer une latence toosee améliorée directement. les centres de toosee hello la liste complète des données Azure, vous pouvez voir hello [page de test de latence](http://www.azurespeed.com/Azure/Latency). 

Hello centres de données avec le service de Proxy d’Application hello sont accessibles par hello [outil de Test des Ports connecteur](https://aadap-portcheck.connectorporttest.msappproxy.net/). 

## <a name="feedback-on-application-proxy-data-center-locations"></a>Commentaires sur les emplacements des centres de données du Proxy d’application 
Il peut y avoir des centres de données Azure qui n’incluent pas encore le Proxy d’Application, mais risque d’entraîner l’amélioration latence élevée tooa pour vous. emplacement du centre de données de Hello < aadapfeedback@microsoft.com > afin de pouvoir utiliser votre tooplan de commentaires que nous allons développer.

Nous travaillons sur certaines des fonctionnalités supplémentaires qui aident à améliorer la latence des hello pour les clients que vous consultez actuellement les latences et que vous être sûr de documentation de tooshare une fois disponible.

## <a name="next-steps"></a>Étapes suivantes
[Travailler avec des serveurs proxy locaux existants](application-proxy-working-with-proxy-servers.md)
