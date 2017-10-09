---
title: "aaaHow toouse Azure RemoteApp avec des comptes d’utilisateur Office 365 | Documents Microsoft"
description: "Découvrez comment toouse Azure RemoteApp avec des comptes d’utilisateurs Office 365"
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
ms.openlocfilehash: d2dbed2a6838adf9bb0f7508eb7dcecb0a74a62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-remoteapp-with-office-365-user-accounts"></a>Comment toouse Azure RemoteApp avec des comptes d’utilisateur Office 365
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Si vous avez un abonnement Office 365 vous avez Azure Active Directory qui stocke les noms d’utilisateur et mots de passe utilisés tooaccess services Office 365. Par exemple, quand les utilisateurs activent Office 365 ProPlus qu’ils s’authentifient toocheck Azure AD pour obtenir des licences. La plupart des clients serait comme toouse hello même annuaire avec Azure RemoteApp.

Si vous déployez Azure RemoteApp, vous utilisez probablement un abonnement Azure associé à un autre annuaire Azure AD. Dans commande toouse votre annuaire d’Office 365, vous devez toomove hello abonnement Azure dans ce répertoire.

Pour plus d’informations sur la façon des applications clientes toodeploy Office 365, consultez [comment toouse votre abonnement Office 365 avec Azure RemoteApp](remoteapp-officesubscription.md).

## <a name="phase-1-register-your-free-office-365-azure-active-directory-subscription"></a>Étape 1 : inscrire votre abonnement Office 365 Azure Active Directory gratuit
Si vous utilisez hello portail Azure classic, utilisez les étapes de hello dans [enregistrer votre abonnement Azure Active Directory gratuit](https://technet.microsoft.com/library/dn832618.aspx) tooget d’un accès administratif tooyour Azure AD via le portail de gestion de hello. En tant que résultat de hello de ce processus, vous devez être en mesure de toolog dans hello portail Azure et voir votre répertoire – à ce stade vous ne verrez pas beaucoup plus étant hello abonnement Azure complet que vous utilisez avec Azure RemoteApp dans un autre répertoire.

N’oubliez pas de nom de hello et le mot de passe du compte d’administrateur hello créé dans cette étape, elles seront nécessaires à la Phase 2.

Si vous utilisez hello portail Azure, consultez [comment tooregister et activer un annuaire Azure Active Directory gratuit, à l’aide du portail Office 365](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/).

## <a name="phase-2-change-hello-azure-ad-associated-with-your-azure-subscription"></a>Phase 2 : Hello de modification AD Azure associé à votre abonnement Azure.
Nous allons toochange votre abonnement Azure à partir de son répertoire actif dans l’annuaire d’Office 365 hello que nous avons travaillées avec à la Phase 1.

Suivez les instructions de hello décrites dans [locataire d’Azure Active Directory hello modification dans Azure RemoteApp](remoteapp-changetenant.md). Payer toohello une attention toute particulière comme suit :

* Étape 1 : si vous avez déployé Azure RemoteApp (ARA) dans cet abonnement, vérifiez que vous supprimez tous les comptes d’utilisateur Azure AD des collections ARA avant d’aller plus loin. Vous pouvez également supprimer toutes les collections existantes.
* Étape 2 : il s’agit d’une étape essentielle. Vous devez toouse un compte Microsoft (par exemple, @outlook.com) en tant qu’un administrateur de Service sur l’abonnement de hello ; il s’agit, car nous ne pouvons pas avoir des comptes d’utilisateur à partir de hello existant associé à Azure AD toohello abonnement – dans ce cas, nous ne pourra plus être en mesure de toomove il tooa autre Azure AD.
* Étape 4 de # : Lorsque vous ajoutez un répertoire existant, hello système vous demandera toosign avec un compte d’administrateur hello pour ce répertoire. Vérifiez que compte d’administrateur hello toouse à partir de la Phase 1.
* Étape #5 : Modifier le répertoire parent de hello du répertoire de hello abonnement tooyour Office 365. résultat final de Hello doit être que sous les paramètres -> abonnements votre abonnement indique répertoire de hello Office 365. 
  ![Remplacez le répertoire parent hello d’abonnement de hello](./media/remoteapp-o365user/settings.png)

À ce stade, votre abonnement Azure RemoteApp est associé à votre Office 365, Azure AD ; Vous pouvez utiliser des comptes d’utilisateur existants hello Office 365 avec Azure RemoteApp !

