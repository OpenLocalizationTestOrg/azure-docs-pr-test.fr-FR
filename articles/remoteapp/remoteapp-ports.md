---
title: "aaaList de toowhitelist de Ports et les URL pour le déploiement de Azure RemoteApp dans le réseau virtuel du client | Documents Microsoft"
description: "Découvrez les ports et les URL que vous devez tooconfigure pour la communication via Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: 5a001ff7-14c9-47fa-9b39-78fd5a5f0250
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 039866f7b64ac763ca833d66031ade3def1d3543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="list-of-ports-and-urls-toopermit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a>Liste d’URL et les Ports d’accès de toopermit pour le déploiement de RemoteApp Azure client réseau virtuel
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Si vous déployez une collection de cloud ou hybride Azure RemoteApp dans un réseau virtuel (VNET), passez en revue hello suivant des informations sur le port. Pour plus d’informations sur les réseaux virtuels, consultez [Présentation du réseau virtuel](../virtual-network/virtual-networks-overview.md). Si vous avez créé un groupe de sécurité réseau (NSG) limitant le trafic toohello réseau virtuel ressources dans votre collection, assurez-vous que hello suivant ports est accessibles et autorisées par le biais des stratégies de sécurité hello sur le réseau virtuel de hello. Pour plus d’informations sur les groupes de sécurité réseau, consultez [Qu’est qu’un groupe de sécurité réseau ?](../virtual-network/virtual-networks-nsg.md).

## <a name="azure-remoteapp-subnet-needs-access-toothese-endpoints-and-urls"></a>Azure RemoteApp sous-réseau a besoin de points de terminaison toothese accès et les URL :
* *.servicebus.windows.net
* *.servicebus.net
* https://*.remoteapp.windowsazure.com  
* https://www.remoteapp.windowsazure.com 
* https://*remoteapp.windowsazure.com  
* https://*.core.windows.net  
* Sortant : TCP : TCP : 443, 9351, 9352, 10101-10175 
* Facultatif – UDP : 10201-10275  

## <a name="azure-remoteapp-clients-need-access-toothese-endpoints-and-urls"></a>Azure RemoteApp clients doivent accéder aux points de terminaison toothese et les URL :
Par les clients, que je veux dire, hello de postes de travail, les périphériques que les utilisateurs etc. Utilisez tooconnect toohello applications déploiement Bonjour collection Azure RemoteApp.

* https://telemetry.remoteapp.windowsazure.com  
* https://*.RemoteApp.windowsazure.com (les ports UDP facultatif hello sont pour cette adresse) 
* https://login.windows.net  
* https://login.microsoftonline.com  
* https://www.remoteapp.windowsazure.com 
* https://*.core.windows.net  
* Sortant : TCP : 443  
* Facultatif - UDP : 3391 

