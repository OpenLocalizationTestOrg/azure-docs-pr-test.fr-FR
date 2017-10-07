---
title: "aaaUsing Azure DNS avec d’autres services Azure | Documents Microsoft"
description: "Comprendre comment nommer des toouse Azure DNS tooresolve pour d’autres services Azure"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure dns
ms.assetid: e9b5eb94-7984-4640-9930-564bb9e82b78
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 09/21/2016
ms.author: gwallace
ms.openlocfilehash: 791f93d6aff2c638c08518e9f1e8ab89ac8de3f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-dns-works-with-other-azure-services"></a>Fonctionnement d’Azure DNS avec d’autres services Azure

Azure DNS est un service hébergé de gestion de DNS et de résolution de noms. Ainsi, vous toocreate publiques noms DNS pour hello autres applications et services que vous avez déployé dans Azure. Création d’un nom pour un service Azure dans votre domaine personnalisé est aussi simple que l’ajout d’un enregistrement de type approprié de hello pour votre service.

* Pour les adresses IP allouées dynamiquement, vous devez créer un enregistrement DNS CNAME ce nom DNS de toohello mappages créés dans Azure pour votre service. Les normes DNS vous empêchent d’utiliser un enregistrement CNAME pour apex de zone hello.
* Pour les adresses IP statiques, vous pouvez créer un enregistrement A DNS à l’aide de n’importe quel nom, y compris un *domaine naked* nom au sommet de zone hello.

Hello hello de plans de table suivants pris en charge types d’enregistrements qui peuvent être utilisés pour différents services Azure. Comme vous pouvez le voir à partir de cette table, Azure DNS prend uniquement en charge les enregistrements DNS pour les ressources réseau accessibles sur Internet. Azure DNS ne peut pas être utilisé pour la résolution de nom d’adresses privées internes.

| Service Azure | Interface réseau | Description |
| --- | --- | --- |
| Application Gateway |[Adresse IP publique frontale](dns-custom-domain.md#public-ip-address) |Vous pouvez créer un enregistrement DNS A ou CNAME. |
| Équilibreur de charge |[Adresse IP publique frontale](dns-custom-domain.md#public-ip-address)  |Vous pouvez créer un enregistrement DNS A ou CNAME. L’équilibreur de charge peut disposer d’une adresse IP publique IPv6 affectée de manière dynamique. Par conséquent, vous devez créer un enregistrement CNAME pour une adresse IPv6. |
| Traffic Manager |Nom public |Vous ne pouvez créer un enregistrement CNAME qui mappe le nom de trafficmanager.net toohello affecté tooyour profil Traffic Manager. Pour plus d’informations, consultez l’article [Fonctionnement de Traffic Manager](../traffic-manager/traffic-manager-overview.md#traffic-manager-example). |
| Service cloud |[Adresse IP publique](dns-custom-domain.md#public-ip-address) |Pour les adresses IP allouées de manière statique, vous pouvez créer un enregistrement DNS A. Pour les adresses IP allouées dynamiquement, vous devez créer un enregistrement CNAME qui mappe toohello *cloudapp.net* nom. Cette règle s’applique tooVMs créé dans le portail classique de hello, car elles sont déployées sous la forme d’un service cloud. Pour plus d’informations, consultez [Configurer un nom de domaine personnalisé dans Services cloud](../cloud-services/cloud-services-custom-domain-name-portal.md). |
| App Service | [Adresse IP externe](dns-custom-domain.md#app-service-web-apps) |Pour les adresses IP externes, vous pouvez créer un enregistrement DNS A. Dans le cas contraire, vous devez créer un enregistrement CNAME qui mappe le nom de azurewebsites.net toohello. Pour plus d’informations, consultez [mapper un tooan de nom de domaine personnalisé application Azure](../app-service-web/web-sites-custom-domain-name.md) |
| Machines virtuelles Resource Manager |[Adresse IP publique](dns-custom-domain.md#public-ip-address) |Les machines virtuelles Resource Manager peuvent avoir des adresses IP publiques. Une machine virtuelle avec une adresse IP publique peut également être derrière un équilibreur de charge. Vous pouvez créer un enregistrement DNS A ou CNAME pour hello adresse publique. Ce nom personnalisé peut être VIP de hello toobypass utilisé sur l’équilibrage de charge hello. |
| les machines virtuelles Classic, |[Adresse IP publique](dns-custom-domain.md#public-ip-address) |Les machines virtuelles classiques créées à l’aide de PowerShell ou de l’interface de ligne de commande peuvent être configurées avec une adresse virtuelle (réservée) dynamique ou statique. Vous pouvez créer un enregistrement DNS CNAME ou A, respectivement. |
