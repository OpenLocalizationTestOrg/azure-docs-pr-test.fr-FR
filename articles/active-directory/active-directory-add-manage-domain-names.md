---
title: "les noms de domaines personnalisés aaaManaging dans Azure Active Directory | Documents Microsoft"
description: "Concepts de gestion et procédures pour gérer un domaine personnalisé dans Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cf3523bd-9ee0-439e-963d-ccea038867b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 4b6d06fecf3be0621be51c38a1330eafdc1b4d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a>Gestion des noms de domaine personnalisés dans Azure Active Directory
Un nom de domaine peut être un identificateur important pour de nombreuses ressources de répertoire, lorsqu’il est compris dans :

* Un nom d’utilisateur ou une adresse e-mail d’un utilisateur
* adresse Hello pour un groupe
* URI ID d’application Hello pour une application

Une ressource dans Azure Active Directory (Azure AD) peut inclure un nom de domaine qui est a déjà été vérifié toobe détenus par le répertoire de hello qui contient les ressources hello. Seul un administrateur général peut effectuer des tâches de gestion de domaine dans Azure AD.

> [!IMPORTANT]
> Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article. Pour comment toomanage vos noms de domaine dans le centre d’administration hello Azure AD, consultez [la gestion des noms de domaines personnalisés dans Azure Active Directory](active-directory-domains-manage-azure-portal.md).

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a>Définir le nom de domaine principal hello pour votre annuaire Azure AD
Lors de la création de votre annuaire, nom de domaine initial hello, par exemple, « contoso.onmicrosoft.com », est également le nom de domaine principal hello pour votre annuaire. domaine principal de Hello est le nom de domaine par défaut hello pour un nouvel utilisateur lorsque vous créez un nouvel utilisateur dans hello [portail Azure classic](https://manage.windowsazure.com/), ou autres portails comme portail d’administration hello Office 365. Cela simplifie le processus hello pour un administrateur toocreate nouveaux utilisateurs dans le portail de hello.

nom de domaine principal toochange hello pour votre annuaire :

1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com/) avec un compte d’utilisateur qui est un administrateur global de votre annuaire Azure AD.
2. Sélectionnez **Active Directory** sur la barre de navigation gauche hello.
3. Ouvrez votre annuaire.
4. Sélectionnez hello **domaines** onglet.
5. Sélectionnez hello **modification principal** bouton de barre de commandes hello.
6. Sélectionnez le domaine hello que vous souhaitez toobe hello nouveau principal de domaine de votre annuaire.

Vous pouvez modifier le nom de domaine principal hello pour votre répertoire de toobe n’importe quel domaine personnalisé vérifié qui n’est pas fédéré. Modification hello principal de domaine pour votre annuaire ne changera pas les noms d’utilisateur hello pour tous les utilisateurs existants.

## <a name="add-custom-domain-names-tooyour-azure-ad"></a>Ajouter des noms de domaine personnalisé tooyour Azure AD
Vous pouvez ajouter jusqu'à too900 domaine personnalisé noms tooeach Windows Azure AD. Hello processus trop[ajouter un nom de domaine personnalisés supplémentaires](active-directory-add-domain.md) est même hello pour le premier nom de domaine personnalisé hello.

## <a name="add-subdomains-of-a-custom-domain"></a>Ajouter des sous-domaines d’un domaine personnalisé
Si vous voulez tooadd un nom de domaine de troisième niveau tels que « europe.contoso.com » tooyour active, vous devez tout d’abord ajouter et vérifier le domaine de second niveau hello, par exemple, contoso.com. sous-domaine de Hello est ensuite vérifié automatiquement par Azure AD. toosee qui hello sous-domaine que vous venez d’ajouter a été vérifié, page hello d’actualisation dans le navigateur hello qui répertorie les domaines hello dans votre annuaire.

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a>Quelles toodo si vous modifiez le bureau d’enregistrement de hello DNS pour le nom de votre domaine personnalisé
Si vous modifiez le bureau d’enregistrement de hello DNS pour le nom de votre domaine personnalisé, vous pouvez continuer à toouse votre nom de domaine personnalisé avec Azure AD elle-même sans interruption et sans tâches de configuration supplémentaires. Si vous utilisez votre nom de domaine personnalisé à Office 365, Intune ou autres services qui s’appuient sur les noms de domaines personnalisés dans Azure AD, consultez la documentation du toohello pour ces services.

## <a name="delete-a-custom-domain-name"></a>Supprimer un nom de domaine personnalisé
Si votre organisation n’utilise plus ce nom de domaine, ou si vous devez toouse ce nom de domaine avec un autre Azure AD, vous pouvez supprimer un nom de domaine personnalisé à partir de votre annuaire Azure AD.

toodelete un nom de domaine personnalisé, vous devez tout d’abord vous assurer qu’aucune ressource dans votre annuaire s’appuient sur nom de domaine hello. Vous ne pouvez pas supprimer un nom de domaine de votre répertoire si :

* Tout utilisateur a un nom d’utilisateur, une adresse de messagerie ou une adresse proxy qui incluent le nom de domaine hello.
* N’importe quel groupe possède une adresse de messagerie ou l’adresse de proxy qui inclut le nom de domaine hello.
* N’importe quelle application dans Azure AD a un URI d’ID qui inclut le nom de domaine hello d’application.

Vous devez modifier ou supprimer n’importe quelle ressource de ce type dans votre annuaire Azure AD avant de supprimer le nom de domaine personnalisé hello.

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a>Utilisez des noms de domaine toomanage PowerShell ou l’API Graph
La plupart des tâches de gestion des noms de domaine dans Azure Active Directory peuvent également être accomplies à l’aide de Microsoft PowerShell, ou encore par programmation à l’aide d’API Graph d’Azure AD.

* [À l’aide de noms de domaine toomanage PowerShell dans Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [À l’aide de noms de domaine de l’API Graph toomanage dans Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur les noms de domaine dans Azure AD](active-directory-add-domain-concepts.md)
* [Gérer les noms de domaine personnalisés](active-directory-add-manage-domain-names.md)

