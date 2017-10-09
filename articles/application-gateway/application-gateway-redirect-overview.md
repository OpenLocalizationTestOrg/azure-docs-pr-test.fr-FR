---
title: "vue d’ensemble d’aaaRedirect pour la passerelle d’Application Azure | Documents Microsoft"
description: "En savoir plus sur la fonctionnalité de redirection hello dans la passerelle d’Application Azure"
services: application-gateway
documentationcenter: na
author: amsriva
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/18/2017
ms.author: amsriva
ms.openlocfilehash: 7149e3bd000d336c51995fb0e90f971b4d9ba2be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-redirect-overview"></a>Vue d’ensemble de la redirection Application Gateway

Un scénario courant pour de nombreuses applications web est toosupport automatique HTTP tooHTTPS redirection tooensure que toutes les communications entre l’application et ses utilisateurs se produit sur un chemin d’accès chiffré. Bonjour précédentes, les utilisateurs ont des techniques telles que la création d’un pool dédié principal dont le seul objectif est de demandes tooredirect reçues sur HTTP tooHTTPS.  Passerelle d’application prend désormais en charge le trafic de capacité tooredirect sur hello passerelle d’Application. Cela simplifie la configuration de l’application optimise l’utilisation des ressources hello et prend en charge de nouveaux scénarios de redirection, notamment la redirection globale et basée sur le chemin d’accès. Prise en charge de la redirection de passerelle application n’est pas limité tooHTTP -> la redirection de HTTPS uniquement. Il s’agit d’un mécanisme de redirection générique, ce qui permet une redirection du trafic reçu au port d’écoute un port d’écoute tooanother sur la passerelle d’Application. Il prend également en charge la redirection tooan site externe ainsi. Prise en charge de la redirection de passerelle application offre hello suivant de fonctionnalités :

1. Redirection globale à partir d’un seul écouteur tooanother écouter le hello passerelle. Cela permet la redirection HTTP tooHTTPS sur un site.
2. Redirection basée sur un chemin d’accès. Ce type de redirection permet la redirection HTTP tooHTTPS uniquement sur une zone de site spécifique, par exemple une zone de panier d’achat indiqués par/achat / *.
3. Redirection tooexternal site.

![redirection](./media/application-gateway-redirect-overview/redirect.png)

Avec cette modification, les utilisateurs auraient toocreate un nouvel objet de configuration de redirection, qui spécifie le port d’écoute hello cible ou la redirection de toowhich site externe est souhaitée. élément de configuration Hello prend également en charge tooenable options l’ajout de chemin de l’URI hello et chaîne toohello rediriger l’URL de requête. Les clients peuvent également choisir si la redirection est temporaire (code d’état HTTP 302) ou permanente (code d’état HTTP 301). Une fois créé cette configuration de redirection est attaché toohello source port d’écoute une nouvelle règle. Lorsque vous utilisez une règle de base, configuration de redirection hello est associée à un écouteur de source et est une redirection globale. Lorsqu’une règle basée sur le chemin d’accès est utilisée, configuration de redirection hello est définie sur le mappage de chemin d’accès d’URL hello et par conséquent, ne s’applique que toohello zone de chemin d’accès spécifique d’un site.

### <a name="next-steps"></a>Étapes suivantes

[Configurer la redirection d’URL sur une passerelle d’application](application-gateway-configure-redirect-powershell.md)
