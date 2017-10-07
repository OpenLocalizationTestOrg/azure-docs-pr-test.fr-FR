---
title: "aaaHow Azure abonnements sont associés à Active Directory de Azure | Documents Microsoft"
description: "L’ouverture de session tooMicrosoft Azure et les problèmes tels que relation hello entre un abonnement Azure et l’Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: bc4773c2-bc4a-4d21-9264-2267065f0aea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4f831cfb972efec57083fcaa63adb43fde7b2faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-subscriptions-are-associated-with-azure-active-directory"></a>Association des abonnements Azure avec Azure Active Directory
Cet article fournit des informations sur la relation hello entre un abonnement Azure et l’Azure Active Directory (Azure AD) et comment tooadd un répertoire de tooyour Azure AD abonnement existant.

## <a name="your-azure-subscriptions-relationship-tooazure-ad"></a>TooAzure de relation de votre abonnement Azure AD
Votre abonnement Azure a une relation d’approbation avec Azure AD, ce qui signifie qu’il approuve les périphériques, services et utilisateurs Active Directory tooauthenticate hello. Plusieurs abonnements peuvent approuver hello même répertoire, mais chaque abonnement fait confiance à un seul répertoire. 

relation d’approbation Hello ayant un abonnement à un annuaire diffère de la relation hello qu’il possède avec d’autres ressources dans Azure (sites Web, bases de données et ainsi de suite). Si un abonnement expire, l’accès toohello arrête également d’autres ressources associées d’abonnement de hello. Mais un annuaire Azure AD reste dans Azure, et vous pouvez associer un autre abonnement à ce répertoire et gérer le répertoire hello à l’aide d’un nouvel abonnement hello.

![diagramme relatif à l’association des abonnements](./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png)

Tous les utilisateurs disposent d'un répertoire de base unique qui les authentifie, mais ils peuvent également être invités dans d'autres répertoires. Dans Azure AD, vous pouvez voir les répertoires hello dont votre compte d’utilisateur est membre ou invité.

## <a name="azure-ad-and-cloud-service-subscriptions"></a>Azure AD et les abonnements de service cloud
Azure AD fournit hello core annuaire et identité derrière la plupart des services de cloud de Microsoft, y compris les fonctionnalités de gestion :

* Microsoft Azure
* Microsoft Office 365
* Microsoft Dynamics CRM Online
* Microsoft Intune

Vous obtenez hello service Azure AD gratuit lorsque vous vous inscrivez pour chacun de ces services de cloud de Microsoft. Si vous voulez tooadd un répertoire tooan Azure AD d’abonnement Azure supplémentaires, vous devez être connecté avec un compte Microsoft. Si vous connectez-vous tooAzure avec un travail ou scolaire de compte, vous ne pouvez pas ajouter un répertoire existant de tooan abonnement Azure, car votre compte professionnel ou scolaire ne peut pas être authentifié directement par Azure. 

## <a name="tooadd-an-existing-subscription-tooyour-azure-ad-directory"></a>tooadd un répertoire de tooyour Azure AD abonnement existant
Vous devez vous connecter avec un compte qui existe dans les deux répertoire actif hello quels hello abonnement est associé, et dans le répertoire de hello souhaité tooadd à. 

1. Connectez-vous à toohello [centre des comptes Azure](https://account.windowsazure.com/Home/Index) avec un compte qui est administrateur de compte de l’abonnement de hello hello compte dont la propriété souhaitée tootransfer.
2. Vérifiez que hello utilisateur propriétaire de l’abonnement toobe hello est dans le répertoire de hello ciblé.
3. Cliquez sur **Transférer la propriété de l’abonnement**.
4. Spécifiez le destinataire de hello. destinataire de Hello obtient automatiquement un message électronique contenant un lien d’acceptation.
5. destinataire de Hello clique sur le lien de hello et suit les instructions hello, y compris comment entrer leurs informations de paiement. Destinataire de hello réussit, l’abonnement de hello est transféré. 
6. répertoire par défaut de Hello d’abonnement de hello est modifié toohello répertoire utilisateur hello est dans.


## <a name="suggestions-toomanage-both-a-subscription-and-a-directory"></a>Toomanage des suggestions à la fois un abonnement et un répertoire
Hello des rôles d’administration pour un abonnement Azure gèrent les ressources liées toohello abonnement Azure. Cette section explique les différences de hello entre les administrateurs de l’abonnement Azure et les administrateurs d’annuaires Azure AD. Rôles d’administrateur et autres suggestions pour les utiliser toomanage votre abonnement sont couverts à [attribution de rôles d’administrateur dans Azure Active Directory](active-directory-assign-admin-roles.md).

Par défaut, vous est attribué le rôle d’administrateur de Service hello lorsque vous vous inscrivez. Si d’autres utilisateurs doivent toosign dans et accéder aux services à l’aide de hello même abonnement, vous pouvez les ajouter en tant que coadministrateurs. 

Azure AD a un ensemble différent de répertoire de hello toomanage rôles d’administrateur et les fonctionnalités liées à identité. Par exemple, administrateur global de hello d’un annuaire peut ajouter des utilisateurs et le répertoire toohello de groupes ou exiger une authentification multifacteur pour les utilisateurs. Un utilisateur qui crée un répertoire est attribué le rôle d’administrateur général toohello et ils peuvent attribuer des rôles administratifs tooother utilisateurs. Les rôles administratifs Azure AD sont également utilisés par d'autres services tels que Office 365 et Microsoft Intune. 

Les administrateurs d'abonnement Azure et les administrateurs de répertoires Azure AD possèdent deux rôles bien différents. 
* Les administrateurs d’abonnements Azure peuvent gérer des ressources dans Azure et peuvent utiliser Azure AD dans hello portail Azure (car hello portail Azure lui-même est une ressource Azure). 
* Administrateurs d’annuaires peuvent gérer les propriétés uniquement dans Windows Azure AD hello.

Une personne peut se voir attribuer deux rôles, mais ceci n'est en aucun cas obligatoire. Un administrateur général de répertoires peut ne pas être administrateur de services ou coadministrateur d’un abonnement Azure, et inversement. Sans être un administrateur d’abonnement de hello, utilisateur de hello toohello portail Azure peut se connecter, mais ne peut pas gérer les répertoires hello pour cet abonnement dans le portail de hello. Toutefois, cet utilisateur peut gérer les répertoires à l’aide d’autres outils tels que PowerShell Azure AD ou hello centre d’administration Office 365.

## <a name="next-steps"></a>Étapes suivantes
* toolearn savoir plus sur les administrateurs de toochange pour un abonnement Azure, voir [transférer la propriété d’un compte de tooanother abonnement Azure](../billing/billing-subscription-transfer.md)
* toolearn en savoir plus sur la façon dont l’accès aux ressources est contrôlé dans Microsoft Azure, consultez [présentation de l’accès aux ressources dans Azure](active-directory-understanding-resource-access.md)
* Pour plus d’informations sur la façon de rôles tooassign dans Azure AD, consultez [attribution de rôles d’administrateur dans Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)

<!--Image references-->
[1]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_PassThruAuth.png
[2]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png
[3]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_SignInDisambiguation.PNG
