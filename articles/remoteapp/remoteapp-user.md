---
title: "Ajouter un utilisateur à votre collection Azure RemoteApp | Microsoft Docs"
description: "Découvrez comment ajouter des utilisateurs dans votre collection Azure RemoteApp"
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
ms.openlocfilehash: 281e74c7941c42d8a3e4351953391229e54ce0a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-a-user-to-your-azure-remoteapp-collection"></a>Procédure : ajout d'un utilisateur dans votre collection Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .
> 
> 

Avant que vos utilisateurs puissent afficher et utiliser vos applications dans Azure RemoteApp, vous devez leur accorder l’accès à votre collection. C'est l'étape la plus facile : sous l'onglet **Accès utilisateur** , entrez les informations de compte de l'utilisateur, puis cliquez sur la coche.

Quelles sont les informations de compte dont vous avez besoin ? Cela dépend du type de collection que vous avez créé (cloud ou hybride) et si vous utilisez Office 365 ProPlus dans cette collection.

## <a name="supported-user-identities"></a>Identités d'utilisateurs prises en charge
Les différents types de collection (cloud ou hybride) prennent en charge différentes identités d’utilisateur pour l’accès aux applications.  

Pour une collection hybride de RemoteApp, vous devez configurer une infrastructure de domaine Active Directory locale et un locataire Azure Active Directory avec intégration d'annuaire (et éventuellement l'authentification unique). Par ailleurs, vous devez créer des objets Active Directory dans l'annuaire local.  

Pour une collection cloud de RemoteApp, tout utilisateur prenant en charge les identités Azure Active Directory peut recevoir l'accès utilisateur à RemoteApp pour inclure des comptes Microsoft.  Consultez le tableau ci-dessous.

Les utilisateurs Office 365 sont des utilisateurs Azure Active Directory. S'ils possèdent des comptes Azure Active Directory hybrides synchronisés, ils peuvent bénéficier de l'accès utilisateur dans un déploiement hybride de RemoteApp.   

Vous pouvez utiliser ce tableau de référence pour déterminer rapidement quelle identité est prise en charge dans votre collection et quelle configuration est requise pour Active Directory.

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
> Les utilisateurs Azure Active Directory doivent provenir du locataire associé à votre abonnement. (Vous pouvez afficher et modifier votre abonnement sous l’onglet **Paramètres** du portail. Consultez [Modifier le locataire Azure Active Directory utilisé par RemoteApp](remoteapp-changetenant.md) pour plus d'informations.)
> 
> 

## <a name="office-365-proplus-user-account-information"></a>Informations de compte d'utilisateur Office 365 ProPlus
Si vous utilisez l’image de modèle Office 365 ProPlus dans votre collection *ou* si vous avez créé une image personnalisée qui utilise Office 365, vous êtes uniquement autorisé à ajouter des utilisateurs Azure Active Directory disposant d’abonnements Office 365 pour le domaine par défaut de votre abonnement. Consultez [Utilisation d'Office 365 avec Azure RemoteApp](remoteapp-o365.md) pour plus d'informations.

