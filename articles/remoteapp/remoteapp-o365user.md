---
title: "Utilisation d’Azure RemoteApp avec des comptes d’utilisateur Office 365 | Microsoft Docs"
description: "Découvrez comment utiliser Azure RemoteApp avec des comptes d’utilisateur Office 365"
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: aba70fd3-60b0-4b44-9321-1ab18760ccd5
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 1bc8949c236afd03415f961cf7a657d4d3926b07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-remoteapp-with-office-365-user-accounts"></a>Utilisation d’Azure RemoteApp avec des comptes d’utilisateur Office 365
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .
> 
> 

Si vous possédez un abonnement Office 365, Azure Active Directory stocke les noms d’utilisateur et mots de passe utilisés pour accéder aux services Office 365. Par exemple, lorsque les utilisateurs activent Office 365 ProPlus, ils s’authentifient auprès d’Azure AD pour rechercher des licences. La plupart des clients souhaitent utiliser le même annuaire avec Azure RemoteApp.

Si vous déployez Azure RemoteApp, vous utilisez probablement un abonnement Azure associé à un autre annuaire Azure AD. Pour utiliser votre annuaire Office 365, vous devez déplacer l’abonnement Azure dans cet annuaire.

Pour plus d’informations sur le déploiement d’applications clientes Office 365, consultez [Utilisation de votre abonnement Office 365 avec Azure RemoteApp](remoteapp-officesubscription.md).

## <a name="phase-1-register-your-free-office-365-azure-active-directory-subscription"></a>Étape 1 : inscrire votre abonnement Office 365 Azure Active Directory gratuit
Si vous utilisez le Portail Azure Classic, utilisez la procédure décrite dans [Inscrire votre abonnement Azure Active Directory gratuit](https://technet.microsoft.com/library/dn832618.aspx) pour obtenir un accès administratif à votre Azure AD avec le Portail de gestion Azure. Une fois que vous avez suivi ce processus, vous devez pouvoir vous connecter au Portail Azure et voir votre annuaire. À ce stade, vous ne voyez que ceci, car l’abonnement Azure complet que vous utilisez avec Azure RemoteApp est associé à un autre annuaire.

Prenez note du nom et du mot de passe du compte d’administrateur créé lors de cette étape : ils vous seront utiles à l’étape 2.

Si vous utilisez le Portail Azure, consultez [Inscription et activation d’un abonnement Azure Active Directory gratuit à l’aide du portail Office 365](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/).

## <a name="phase-2-change-the-azure-ad-associated-with-your-azure-subscription"></a>Étape 2 : modifier l’annuaire Azure AD associé à votre abonnement Azure
Nous allons modifier votre abonnement Azure en remplaçant l’annuaire actuel par l’annuaire Office 365 que nous avons configuré lors de l’étape 1.

Suivez les instructions de la rubrique [Modification du client Azure Active Directory dans Azure RemoteApp](remoteapp-changetenant.md). Prêtez une attention particulière aux étapes suivantes :

* Étape 1 : si vous avez déployé Azure RemoteApp (ARA) dans cet abonnement, vérifiez que vous supprimez tous les comptes d’utilisateur Azure AD des collections ARA avant d’aller plus loin. Vous pouvez également supprimer toutes les collections existantes.
* Étape 2 : il s’agit d’une étape essentielle. Vous devez utiliser un compte Microsoft (par exemple, @outlook.com )en tant qu’administrateur de service sur l’abonnement. En effet, il n’est pas possible que des comptes d’utilisateur de l’annuaire Azure AD existant soient associés à l’abonnement. Sinon, nous ne pouvons pas le déplacer vers un autre annuaire Azure AD.
* Étape 4 : lorsque vous ajoutez un annuaire existant, le système vous demande de vous connecter avec le compte d’administrateur associé. Veillez à utiliser le compte d’administrateur de l’étape 1.
* Étape 5 : remplacez l’annuaire parent de l’abonnement par votre annuaire Office 365. Le résultat final doit être le suivant : sous Paramètres -> Abonnements, votre abonnement répertorie l’annuaire Office 365. 
  ![Remplacer l’annuaire parent de l’abonnement](./media/remoteapp-o365user/settings.png)

À ce stade, votre abonnement Azure RemoteApp est associé à votre annuaire Office 365 Azure AD. Vous pouvez utiliser les comptes d’utilisateur Office 365 existants avec Azure RemoteApp.

