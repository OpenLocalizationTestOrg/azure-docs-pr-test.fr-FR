---
title: aaaAdd un tooyour utilisateur collection Azure RemoteApp | Documents Microsoft
description: "Découvrez comment les utilisateurs de tooadd tooyour collection Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 0ae88e04c8bfc2ed55dc963945ed7e9ff687b603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-user-tooyour-azure-remoteapp-collection"></a>Comment tooadd un tooyour utilisateur collection Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Vos utilisateurs peuvent voir et utiliser vos applications dans Azure RemoteApp, vous devez toogrant les accès tooyour collection. Cela fait partie de facile hello : sur hello **accès utilisateur** onglet, entrez les informations du compte d’utilisateur de hello hello, puis cliquez sur la case à cocher hello.

Quelles sont les informations de compte dont vous avez besoin ? Cela dépend de type hello de collection vous avez créé (cloud ou hybride), et que vous utilisez Office 365 ProPlus dans cette collection.

## <a name="supported-user-identities"></a>Identités d'utilisateurs prises en charge
Hello différents types de collection (cloud ou hybride) prend en charge à l’aide de différentes identités d’utilisateur pour l’accès tooapplications.  

Pour une collection hybride de RemoteApp, tooset une infrastructure de domaine Active Directory sur site et un locataire Azure Active Directory avec l’intégration Active (et éventuellement l’authentification unique). En outre, vous devez toocreate certains objets Active Directory dans le répertoire local de hello.  

Pour une collection de cloud de RemoteApp, tout utilisateur disposant d’Azure Active Directory prend en charge les identités peut être accordée utilisateur accès tooRemoteApp tooinclude Accounts Microsoft.  Consultez le tableau de hello ci-dessous.

Les utilisateurs Office 365 sont des utilisateurs Azure Active Directory. S'ils possèdent des comptes Azure Active Directory hybrides synchronisés, ils peuvent bénéficier de l'accès utilisateur dans un déploiement hybride de RemoteApp.   

Vous pouvez utiliser cette table comme une référence rapide pour lequel identity est pris en charge dans votre collection et quelles sont les exigences d’Active Directory hello.

| Comptes d'utilisateurs | Cloud | Hybride |
| --- | --- | --- |
| Compte Microsoft |Oui |Non |
| Azure Active Directory (Azure AD) | | |
| Cloud Azure AD uniquement |OUI |Non |
| ADsync avec synchronisation de mot de passe |OUI |OUI |
| ADsync sans synchronisation de mot de passe |OUI |Non |
| ADsync avec AD FS |OUI |OUI |
| [Fournisseurs d’identités tiers pris en charge par Azure](https://msdn.microsoft.com/library/azure/jj679342.aspx) (par exemple Ping) |OUI |OUI |
| Azure Multi-Factor Authentication |OUI |OUI |

Consultez [plus d'informations](remoteapp-ad.md) sur la configuration d'Active Directory pour RemoteApp.

> [!NOTE]
> utilisateurs d’Azure Active Directory Hello doivent provenir de locataire hello qui est associé à votre abonnement. (Vous pouvez afficher et modifier votre abonnement sur hello **paramètres** hello portail. Consultez [client Azure Active Directory de modification hello utilisé par RemoteApp](remoteapp-changetenant.md) pour plus d’informations.)
> 
> 

## <a name="office-365-proplus-user-account-information"></a>Informations de compte d'utilisateur Office 365 ProPlus
Si vous utilisez une image de modèle Office 365 ProPlus hello dans votre collection de *ou* si vous avez créé une image personnalisée qui utilise Office 365, vous êtes uniquement autorisé tooadd les utilisateurs d’Azure Active Directory qui ont des abonnements Office 365 pour hello domaine par défaut de votre abonnement. Consultez [Utilisation d'Office 365 avec Azure RemoteApp](remoteapp-o365.md) pour plus d'informations.

