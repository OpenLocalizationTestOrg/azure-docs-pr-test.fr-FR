---
title: "aaaAdding Azure Active Directory à l’aide des Services connectés dans Visual Studio | Documents Microsoft"
description: "Ajouter un annuaire Azure Active Directory à l’aide de boîte de dialogue hello Visual Studio ajouter des Services connectés"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f599de6b-e369-436f-9cdc-48a0165684cb
ms.service: active-directory
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: kraigb
ms.openlocfilehash: 26c8f68edf9ec5f7bf65cbab34e4f9b4085ed18d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-an-azure-active-directory-by-using-connected-services-in-visual-studio"></a>Ajout d’un annuaire Azure Active Directory à l’aide de services connectés dans Visual Studio
En utilisant Azure Active Directory (Azure AD), vous pouvez prendre en charge l’authentification unique (SSO) pour les applications web MVC ASP.NET ou l’authentification Active Directory dans les services API web. Avec l’authentification Azure Active Directory, vos utilisateurs peuvent utiliser leurs comptes à partir d’Azure Active Directory tooconnect tooyour des applications web. les avantages de Hello d’authentification Azure Active Directory avec l’API Web incluent la sécurité renforcée des données lors de l’exposition d’une API à partir d’une application web. Avec Azure AD, il est inutile toomanage un système d’authentification distinct avec sa propre gestion de compte et d’utilisateur.

## <a name="prerequisites"></a>Composants requis
- Compte Azure : si vous ne possédez pas de compte Azure, vous pouvez [vous inscrire à un essai gratuit](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [activer les avantages de votre abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

### <a name="connect-tooazure-active-directory-using-hello-connected-services-dialog"></a>Se connecter tooAzure Active Directory à l’aide des Services connectés hello boîte de dialogue
1. Dans Visual Studio, créez ou ouvrez un projet d’API Web ASP.NET ou un projet MVC ASP.NET.

1. À partir de l’Explorateur de solutions de hello, avec le bouton droit hello **Services connectés** nœud et, dans le menu contextuel de hello, sélectionnez **ajouter des Services connectés**.

1. Sur hello **Services connectés** page, sélectionnez **l’authentification avec Azure Active Directory**.
   
    ![Page des services connectés](./media/vs-azure-tools-connected-services-add-active-directory/connected-services-add-active-directory.png)

1. Sur hello **Introduction** page Hello **configurer Azure AD Authentication** Assistant, sélectionnez **suivant**.
   
    ![Page d’introduction](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-1.png)

1. Sur hello **l’authentification unique sur** page Hello **configurer Azure AD Authentication** Assistant, sélectionnez un domaine à partir de hello **domaine** liste déroulante. liste Hello des domaines contient tous les domaines accessibles par les comptes hello répertoriés dans la boîte de dialogue Paramètres de compte hello. En guise d’alternative, vous pouvez entrer un nom de domaine si vous n’en trouvez hello que vous recherchez, tel que `mydomain.onmicrosoft.com`. Vous pouvez choisir l’application Azure Active Directory hello option toocreate ou utiliser des paramètres hello à partir d’une application Azure Active Directory existante. Sélectionnez **Suivant** lorsque vous avez terminé.
   
    ![Page de l’authentification unique](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-2.png)

1. Sur hello **accès à l’annuaire** page Hello **configurer Azure AD Authentication** Assistant, vérifiez que hello **lire les données d’annuaire** option est activée. 
   
    ![Page d’accès à l’annuaire](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-3.png)

1. Sélectionnez **Terminer** tooadd hello tooenable de code et les références nécessaires de la configuration de votre projet pour l’authentification Azure AD. Vous pouvez voir le domaine Active Directory de hello sur hello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Visual Studio affiche un [que s’est-il passé](#how-your-project-is-modified) article tooshow vous comment votre projet a été modifié. Si vous souhaitez toocheck tout fonctionnait, ouvrez un des fichiers de configuration hello modifié et vérifiez existe-t-il des paramètres hello mentionnés dans l’article de hello. 

## <a name="how-your-project-is-modified"></a>Modifications apportées à votre projet
Lorsque vous exécutez hello Assistant, Visual Studio ajoute Azure Active Directory et projet tooyour de références associées. Fichiers de configuration et les fichiers de code dans votre projet sont également modifiées tooadd pris en charge pour Azure AD. modifications spécifiques Hello que Visual Studio apporte dépendent du type de projet hello. Pour plus d’informations sur la façon dont les projets ASP.NET MVC sont modifiés, consultez [Que s’est-il passé : projets ASP.NET MVC](http://go.microsoft.com/fwlink/p/?LinkID=513809). Pour les projets d’API web, consultez [Que s’est-il passé : projets d’API web](http://go.microsoft.com/fwlink/p/?LinkId=513810).

## <a name="next-steps"></a>Étapes suivantes
* [Forum MSDN pour Azure Active Directory](https://social.msdn.microsoft.com/forums/azure/home?forum=WindowsAzureAD)
* [Documentation Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)
* [Billet de blog : Introduction tooAzure Active Directory](http://blogs.msdn.com/b/brunoterkaly/archive/2014/03/03/introduction-to-windows-azure-active-directory.aspx)

