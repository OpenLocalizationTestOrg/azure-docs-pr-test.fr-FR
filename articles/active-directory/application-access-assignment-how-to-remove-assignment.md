---
title: "d’aaaHow tooremove un utilisateur accéder à application de tooan | Documents Microsoft"
description: "Comprendre comment de tooremove un utilisateur accéder à tooan d’application"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 17017bddb73aad5a0ef3a411ac91bf0423f0b600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooremove-a-users-access-tooan-application"></a>Comment de tooremove un utilisateur accéder à tooan d’application

Cet article vous a-t-il toounderstand comment de tooremove un utilisateur accéder à tooan d’application.

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a>Je veux tooremove un utilisateur spécifique ou du groupe affectation tooan une application

tooremove une application utilisateur ou groupe affectation tooan, suivez les étapes de hello répertoriées dans hello [supprimer une attribution de l’utilisateur ou un groupe à partir d’une application d’entreprise dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) l’article.

. ## souhaitée toodisable tous les accès tooan d’applications pour chaque utilisateur

toodisable toutes les applications de la tooan de connexions utilisateur, suivez les étapes de hello répertoriés dans hello [désactiver des connexions utilisateur pour une application d’entreprise dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) l’article.

## <a name="i-want-toodelete-an-application-entirely"></a>Je veux toodelete une application entièrement

trop**supprimer une application**, suivez les instructions de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

   * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello toodelete.

7.  Une fois le charge de l’application hello, cliquez sur **supprimer** icône à partir de l’application hello supérieur **vue d’ensemble** panneau.

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a>Je veux toodisable tooany application de tous les futurs utilisateur consentement opérations

La désactivation de consentement de l’utilisateur pour éviter que les utilisateurs finaux d’application de tooany terme autorisation tout le répertoire. Les administrateurs peuvent toujours donner leur consentement au nom de l’utilisateur. toolearn en savoir plus sur l’application de consentement, et pourquoi vous pouvez ou pas souhaitiez toodo, lecture [utilisateur de présentation et de consentement de l’administrateur](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).

trop**désactiver toutes les opérations de consentement d’utilisateur futures dans tout le répertoire**, suivez les instructions de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.

5.  Cliquez sur **Paramètres utilisateur**.

6.  Désactiver toutes les opérations de consentement d’utilisateur futures en définissant un hello **les utilisateurs peuvent autoriser des applications tooaccess leurs données** basculer trop**non** et cliquez sur hello **enregistrer** bouton.


# <a name="next-steps"></a>Étapes suivantes
[Gestion des accès tooapps](active-directory-managing-access-to-apps.md)
