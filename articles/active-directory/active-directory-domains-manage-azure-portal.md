---
title: "les noms de domaines personnalisés aaaManaging dans Azure Active Directory | Documents Microsoft"
description: "Concepts de gestion et procédures pour gérer un nom de domaine dans Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5063cd0a-dba2-4ba9-aa65-b8117490d73a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: curtand;jeffsta
ms.openlocfilehash: 4719524c4e972f6c981db39f016729da13b37670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a>Gestion des noms de domaine personnalisés dans Azure Active Directory
Un nom de domaine est une partie importante de l’identificateur hello pour de nombreuses ressources de répertoire : il fait partie d’un utilisateur nom ou adresse de messagerie pour un utilisateur, la partie de l’adresse hello pour un groupe et peut faire partie de l’URI ID d’application hello pour une application. Une ressource dans Azure Active Directory (Azure AD) peut inclure un nom de domaine qui est déjà vérifié comme appartenant au répertoire de hello qui contient les ressources hello. Seul un administrateur général peut effectuer des tâches de gestion de domaine dans Azure AD.

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a>Définir le nom de domaine principal hello pour votre annuaire Azure AD
Lors de la création de votre annuaire, nom de domaine initial hello, par exemple, « contoso.onmicrosoft.com », est également nom de domaine principal hello. domaine principal de Hello est le nom de domaine par défaut hello pour un nouvel utilisateur lorsque vous créez un nouvel utilisateur. Définition d’un nom de domaine principal rationalise hello pour un administrateur toocreate nouveaux utilisateurs dans le portail de hello. nom de domaine principal toochange hello :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.
2. Sélectionnez **davantage de services**, entrez **Azure Active Directory** dans hello de zone de texte, puis sélectionnez **entrée**.
   
   ![Ouvrir la gestion des utilisateurs](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Sur hello ***-nom du répertoire*** panneau, sélectionnez **les noms de domaine**.
4. Sur hello  ***-nom du répertoire* -les noms de domaine** panneau, nom de domaine Sélectionnez hello vous souhaitez que le nom de domaine principal toomake hello.
5. Sur hello ***nom de domaine*** blade (autrement dit, hello panneau qui s’ouvre contenant votre nouveau nom de domaine dans le titre de hello), sélectionnez hello **rendre primaire** commande. Confirmez votre choix lorsque vous y êtes invité.
   
   ![Créer un nom de domaine principal](./media/active-directory-domains-manage-azure-portal/make-primary.png)

Vous pouvez modifier le nom de domaine principal hello pour votre répertoire de toobe n’importe quel domaine personnalisé vérifié qui n’est pas fédéré. Modification hello principal de domaine pour votre annuaire ne changera pas les noms d’utilisateur hello pour tous les utilisateurs existants.

## <a name="add-custom-domain-names-tooyour-azure-ad"></a>Ajouter des noms de domaine personnalisé tooyour Azure AD
Vous pouvez ajouter jusqu'à too900 domaine personnalisé noms tooeach Windows Azure AD. Hello processus trop[ajouter un nom de domaine personnalisés supplémentaires](add-custom-domain.md) est même hello pour le premier nom de domaine personnalisé hello.

## <a name="add-subdomains-of-a-custom-domain"></a>Ajouter des sous-domaines d’un domaine personnalisé
Si vous voulez tooadd un nom de domaine de troisième niveau tels que « europe.contoso.com » tooyour active, vous devez tout d’abord ajouter et vérifier le domaine de second niveau hello, par exemple, contoso.com. sous-domaine de Hello est ensuite vérifié automatiquement par Azure AD. toosee qui hello sous-domaine que vous venez d’ajouter a été vérifié, page hello d’actualisation dans le navigateur hello qui répertorie les domaines hello.

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a>Quelles toodo si vous modifiez le bureau d’enregistrement de hello DNS pour le nom de votre domaine personnalisé
Si vous modifiez le bureau d’enregistrement de hello DNS pour le nom de votre domaine personnalisé, vous pouvez continuer à toouse votre nom de domaine personnalisé avec Azure AD elle-même sans interruption et sans tâches de configuration supplémentaires. Si vous utilisez votre nom de domaine personnalisé à Office 365, Intune ou autres services qui s’appuient sur les noms de domaines personnalisés dans Azure AD, consultez la documentation du toohello pour ces services.

## <a name="delete-a-custom-domain-name"></a>Supprimer un nom de domaine personnalisé
Si votre organisation n’utilise plus ce nom de domaine, ou si vous devez toouse ce nom de domaine avec un autre Azure AD, vous pouvez supprimer un nom de domaine personnalisé à partir de votre annuaire Azure AD.

toodelete un nom de domaine personnalisé, vous devez tout d’abord vous assurer qu’aucune ressource dans votre annuaire s’appuient sur nom de domaine hello. Vous ne pouvez pas supprimer un nom de domaine de votre répertoire si :

* Tout utilisateur a un nom d’utilisateur, une adresse de messagerie ou une adresse proxy qui inclut le nom de domaine hello.
* N’importe quel groupe possède une adresse de messagerie ou l’adresse de proxy qui inclut le nom de domaine hello.
* N’importe quelle application dans Azure AD a un URI d’ID qui inclut le nom de domaine hello d’application.

Vous devez modifier ou supprimer n’importe quelle ressource de ce type dans votre annuaire Azure AD avant de supprimer le nom de domaine personnalisé hello.

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a>Utilisez des noms de domaine toomanage PowerShell ou l’API Graph
La plupart des tâches de gestion des noms de domaine dans Azure Active Directory peuvent également être accomplies à l’aide de Microsoft PowerShell, ou encore par programmation à l’aide d’API Graph d’Azure AD.

* [À l’aide de noms de domaine toomanage PowerShell dans Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [À l’aide de noms de domaine de l’API Graph toomanage dans Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a>Étapes suivantes
* [Ajouter des noms de domaines personnalisés](add-custom-domain.md)

