---
title: "aaaLayered Architecture de sécurité avec les environnements de Service d’application"
description: "Implémentation d’une architecture de sécurité en couche avec les environnements App Service."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 73ce0213-bd3e-4876-b1ed-5ecad4ad5601
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: stefsch
ms.openlocfilehash: 0627ba6fa849908506fe62c451c888c147cabc03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a>Implémentation d’une architecture de sécurité en couche avec les environnements App Service
## <a name="overview"></a>Vue d'ensemble
Dans la mesure où les environnements App Service fournissent un environnement d’exécution isolé déployé dans un réseau virtuel, les développeurs peuvent créer une architecture de sécurité en couche offrant différents niveaux d’accès réseau pour chaque couche application physique.

Une volonté commune est toohide API principaux à partir d’un accès général à Internet et autoriser uniquement les toobe API appelée par les applications web en amont.  [Groupes de sécurité (NSG) réseau] [ NetworkSecurityGroups] peut être utilisé sur les sous-réseaux contenant des applications de tooAPI les environnements App Service toorestrict accès public.

diagramme de Hello ci-dessous illustre une architecture de l’exemple avec une application en fonction de WebAPI déployée sur un environnement App Service.  Trois instances d’application web distinct, déployés sur trois environnements de Service application distincts, rendre principal appelle toohello même WebAPI application.

![Architecture conceptuelle][ConceptualArchitecture] 

Hello signes plus verts indiquent que hello le groupe de sécurité réseau sur le sous-réseau hello contenant « apiase » permet à des applications web en amont, les appels entrants à partir de hello en tant qu’appels bien à partir de lui-même.  Toutefois, hello même groupe de sécurité réseau refuse explicitement l’accès toogeneral le trafic à partir de hello Internet entrant. 

reste Hello de cette rubrique Guide le groupe de sécurité réseau hello étapes nécessaires tooconfigure hello sur sous-réseau hello contenant « apiase ».

## <a name="determining-hello-network-behavior"></a>Hello déterminant le comportement de réseau
Commande tooknow sécurité du réseau les règles sont nécessaires, vous devez toodetermine les clients du réseau peut tooreach hello environnement App Service contenant hello API d’application et les clients qui seront bloqués.

Étant donné que [réseau des groupes de sécurité (NSG)] [ NetworkSecurityGroups] sont appliqués toosubnets et environnements de Service d’application sont déployés dans des sous-réseaux, les règles de hello contenues dans un groupe de sécurité réseau s’appliquent trop**tous les** applications qui s’exécutent sur un environnement App Service.  Exemple d’architecture hello pour cet article, une fois qu’un groupe de sécurité réseau est sous-réseau toohello appliqué contenant « apiase », toutes les applications qui s’exécutent sur hello » apiase « environnement App Service seront protégé par hello même définir des règles de sécurité. 

* **Déterminer l’adresse IP sortante de hello des appelants en amont :** What hello IP ou les adresses des appelants en amont de hello ?  Ces adresses devez toobe explicitement autorisé à accéder hello groupe de sécurité réseau.  Étant donné que les appels entre les environnements App Service sont considérés comme des appels de « Internet », cela signifie que tooeach hello sortant IP adresse attribuée de hello trois en amont les environnements App Service besoins toobe hello groupe de sécurité réseau pour le sous-réseau de « apiase » hello autorisé à accéder.   Pour plus d’informations sur la détermination des adresse IP sortante de hello pour les applications en cours d’exécution dans un environnement App Service voir hello [Architecture réseau] [ NetworkArchitecture] l’article de vue d’ensemble.
* **Application d’API hello principal devez toocall lui-même ?**  Un point de parfois négligé et plus subtil est scénario hello où hello principal application a besoin toocall lui-même.  Si une application API de serveur principal sur un environnement App Service doit toocall proprement dit, il est également traité comme un appel de « Internet ».  Dans l’exemple d’architecture hello cela nécessite l’accès de l’adresse IP sortante de hello Hello « apiase « environnement App Service ainsi.

## <a name="setting-up-hello-network-security-group"></a>Configuration de hello groupe de sécurité réseau
Une fois la hello de sortant des adresses IP sont connues, étape suivante de hello est tooconstruct un groupe de sécurité réseau.  Les groupes de sécurité réseau peuvent être créés pour les réseaux virtuels reposant sur Resource Manager, ainsi que les réseaux virtuels classiques.  exemples Hello ci-dessous montrent la création et la configuration d’un groupe de sécurité réseau sur un réseau virtuel classique à l’aide de Powershell.

Pour un exemple d’architecture hello, environnements de hello sont situés dans Amérique du Sud, un groupe de sécurité réseau vide est créé dans cette région :

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

D’abord explicite Autoriser la règle est ajoutée pour l’infrastructure de gestion Azure hello comme indiqué dans l’article de hello sur [le trafic entrant] [ InboundTraffic] pour les environnements de Service d’application.

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

Ensuite, deux règles sont ajoutées tooallow HTTP et HTTPS des appels à partir de hello première en amont environnement App Service (« fe1ase »).

    #Grant access toorequests from hello first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Rincer et répétez l’opération pour hello deuxième et troisième en amont App Service environnements (« fe2ase » et « fe3ase »).

    #Grant access toorequests from hello second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access toorequests from hello third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Enfin, accorder l’accès toohello adresse IP sortante de l’environnement App Service de l’API hello principal afin qu’il peut rappeler dans elle-même.

    #Allow apps on hello apiase environment toocall back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Aucune autre règle de sécurité réseau ne doivent toobe configuré, car chaque groupe de sécurité réseau comporte un ensemble de règles par défaut qui bloquent l’accès entrant à partir de hello Internet par défaut.

la liste complète des règles dans le groupe de sécurité réseau hello Hello sont indiquées ci-dessous.  Notez comment hello dernière règle, qui est mis en surbrillance, bloque l’accès entrant à partir de tous les appelants autres que ceux qui ont été explicitement accordé l’accès.

![Configuration de NSG][NSGConfiguration] 

étape finale de Hello est un sous-réseau de toohello tooapply hello NSG contenant hello » apiase « environnement App Service.  

     #Apply hello NSG toohello backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

Avec hello NSG appliqué toohello sous-réseau, seuls hello trois environnements de Service d’application en amont et hello hello contenant d’environnement App Service API back-end, sont autorisés toocall dans l’environnement de « apiase » hello.

## <a name="additional-links-and-information"></a>Informations et liens supplémentaires
Tous les articles et comment-de pour les environnements App Service sont disponibles dans hello [fichier Lisezmoi pour les environnements de Service d’Application](../app-service/app-service-app-service-environments-readme.md).

Informations sur les [groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md). 

Présentation des [adresses IP sortantes][NetworkArchitecture] et des environnements App Service.

[Ports réseau][InboundTraffic] utilisés par les environnements App Service.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
