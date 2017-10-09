---
title: "type aaaWhat ne de collection que vous avez besoin pour Azure RemoteApp ? | Microsoft Docs"
description: En savoir plus sur les types de collections disponibles avec Azure RemoteApp hello.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c13ec78d-07e9-4646-8194-cf3efafc1760
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: f00b5fe41af597cf75e26300bf7842c3a8ff94fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-kind-of-collection-do-you-need-for-azure-remoteapp"></a>De quel type de collection avez-vous besoin pour Azure RemoteApp ?
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Azure RemoteApp vous permet de partager des applications et des ressources avec des utilisateurs sur n’importe quel appareil. Nous le faire en créant des ressources et les applications de collections toohold hello, puis vous partagez ces collections avec des utilisateurs. Il existe deux options de collection, avec différentes options de réseau et d’authentification. Laquelle vous convient ?

Nous allons étudier différentes considérations de hello et les choix que vous avez besoin de toomake tooget hello plus hors de votre collection Azure RemoteApp. 

## <a name="quick-differences-between-hello-collection-types"></a>Différences rapides entre les types de collection hello
|  | Cloud | Hybride |
| --- | --- | --- |
| Utiliser un réseau virtuel existant |OUI |OUI |
| Nécessite des comptes connectés à AD (DirSync) |Non |OUI |
| Nécessite la jonction au domaine |Non |Oui |
| Requiert tooVNET accessible de contrôleur de domaine |Non |OUI |

## <a name="cloud-collections"></a>Collections cloud
* Toocreate rapide - collection de hello est approvisionné rapidement, ce qui signifie que vos applications obtenir toousers plus rapide.
* Apportez vos propres applications ou partagez les nôtres. Vous pouvez utiliser une image personnalisée (construit à partir d’une machine virtuelle Azure) ou une des images hello inclus dans votre abonnement.
* Vous n’avez pas besoin tooconfigure une connexion entre votre collection et de votre domaine local.
* Mais vous pouvez éventuellement utiliser votre propre accès tooprovide de réseau virtuel Azure dans votre environnement local pour les données partage ou toouse non l’authentification Windows en ressources telles que SQL Server (à l’aide de l’authentification de base de données).

Comment créer une collection ?

* Cloud uniquement ? Créer avec hello **création rapide** option dans le portail de hello.
* Cloud + réseau virtuel ? Créer à l’aide de hello **créer avec le réseau virtuel** option mais toojoin ne choisissez pas un domaine.

## <a name="hybrid-collections"></a>Collections hybrides
* Fournir le réseau de tooon local d’un accès complet + réseau virtuel Azure.
* Offrent un accès avec jonction au domaine pour les applications et les données. Les applications distantes peuvent s’authentifier auprès de votre annuaire Active Directory local. Elles peuvent ensuite accéder aux ressources dans votre domaine.
* Permettent d’effectuer une surveillance et une gestion avancées avec des solutions System Center et des stratégies de groupe Windows existantes (via une image personnalisée basée sur Windows Server 2012 R2).
* Prise en charge [ExpressRoute](https://azure.microsoft.com/services/expressroute/) tooconnect tooyour de votre réseau virtuel Azure réseau virtuel local.

Créer à l’aide de hello **créer avec le réseau virtuel** option et choisissez toojoin un domaine.

## <a name="authentication-options"></a>Options d’authentification
Azure RemoteApp prend en charge les comptes Microsoft et Azure Active Directory, mais les collections ne prennent pas toutes en charge toutes les méthodes. 

| Type de compte |  | Cloud | Cloud + réseau virtuel | Hybride |
| --- | --- | --- | --- | --- |
| Compte Microsoft | |OUI |Oui |Non |
| Azure Active Directory (Azure AD) | | | | |
| Azure AD uniquement |OUI |Oui |Non | |
| AD Connect avec synchronisation de mot de passe |OUI |Oui |OUI | |
| AD Connect sans synchronisation de mot de passe |OUI |Oui |Non | |
| AD Connect avec les services AD FS |OUI |Oui |OUI | |
| Fournisseurs d’identités tiers pris en charge par Azure (par exemple Ping) |OUI |Oui |OUI | |
| Azure Multi-Factor Authentication | |OUI |Oui |OUI |

### <a name="cloud-and-cloud--vnet"></a>Cloud et Cloud + réseau virtuel
Avec les collections de cloud computing, vous pouvez utiliser des comptes Microsoft, des comptes Azure AD ou un mélange de hello deux. Utiliser des comptes hello qui fonctionnent le mieux à vos utilisateurs.

Il n’existe aucune exigence particulière quant à l’utilisation de comptes Microsoft. 

Si vous souhaitez que les comptes d’Azure AD toouse, vous devez toomake que votre client Azure AD correspond à hello associé à votre abonnement. Lorsque vous avez créé votre abonnement Azure RemoteApp, locataire d’Azure AD hello que vous utilisiez a été automatiquement associé à votre abonnement. N’importe quel utilisateur Azure AD que vous donnez autorisation tooneeds toobe ce même client. Si nécessaire, vous pouvez [changer le locataire d’Azure AD de hello](remoteapp-changetenant.md) associés à votre abonnement.

### <a name="hybrid-or-cloud--azure-ad--ad"></a>Hybride (ou cloud + Azure AD + AD)
L’utilisation d’Azure AD + Active Directory local est une condition requise pour une collection hybride. Vous avez besoin de deux répertoires toouse AD Connect toointegrate hello. Mais vous avez certains choix lorsqu’il s’agit de toohow vous configurez AD Connect. 

Il existe deux scénarios AD Connect : utilisation de la synchronisation de mot de passe ou utilisation de la fédération Active Directory. Extraire hello [AD Connect informations](../active-directory/active-directory-aadconnect.md) toofigure à quels ces convient le mieux.

Vous pouvez également utiliser Azure AD + AD avec une collection cloud. Assurez-vous que vous suivez hello même configurer les étapes.

Extraire [AD Azure + Active Directory requise pour Azure RemoteApp](remoteapp-ad.md) pour hello étapes tooconfigure requis Azure AD et Active Directory.

## <a name="go-create-your-collection"></a>Passez à l’action !
Bon, je pense que nous avons trouvé maintenant, par conséquent, il est toodo de gauche chose qu’un seul - permet de créer votre première collection Azure RemoteApp.

[Créez une collection cloud](remoteapp-create-cloud-deployment.md) ou [créez une collection hybride](remoteapp-create-hybrid-deployment.md).

