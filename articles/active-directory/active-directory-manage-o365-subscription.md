---
title: "répertoire de hello aaaManage pour votre abonnement Office 365 dans Azure | Documents Microsoft"
description: "La gestion d’un annuaire d’abonnement Office 365 à l’aide d’Azure Active Directory et hello portail Azure classic"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 746987b7-2dfd-4b35-819d-37c1b65c5c81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4faf9936d7e94b85356a18adfcf3d2a48e5b025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-directory-for-your-office-365-subscription-in-azure"></a>Gérer le répertoire hello pour votre abonnement Office 365 dans Azure
Cet article décrit comment toomanage un répertoire a été créé pour un abonnement Office 365, à l’aide de hello portail Azure classic. Vous devez être soit hello administrateur de services fédérés ou coadministrateur d’un toosign d’abonnement Azure dans toohello portail Azure classic. Si vous n’avez pas d’abonnement Azure, vous pouvez vous inscrire pour une [période d’essai gratuite de 30 jours](https://azure.microsoft.com/trial/get-started-active-directory/) , puis déployer votre première solution cloud en moins de 5 minutes à l’aide de ce lien. Toouse vraiment hello travail ou scolaire de compte que vous utilisez toosign dans tooOffice 365.

> [!IMPORTANT]
> Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article.

Après avoir terminé hello abonnement Azure, vous pouvez vous connecter toohello portail Azure classic et accéder aux services Azure. Cliquez sur une extension Active Directory hello toomanage hello même annuaire qui authentifie vos utilisateurs Office 365.

Si vous avez déjà d’un abonnement Azure, hello processus toomanage un annuaire supplémentaire est également simple. Par exemple, Michael Smith a un abonnement Office 365 pour Contoso.com. Il a également un abonnement Azure obtenu via son compte Microsoft msmith@hotmail.com. Dans ce cas, il gère deux annuaires.

| Abonnement | Office 365 | Les tables Azure |
| --- | --- | --- |
|   Nom complet |Contoso |Répertoire Azure Active Directory (Azure AD) par défaut |
|   Nom de domaine |contoso.com |msmithhotmail.onmicrosoft.com |

Il souhaite que les identités des utilisateurs toomanage hello dans l’annuaire Contoso hello pendant qu’il est connecté dans tooAzure à l’aide de son compte Microsoft, afin qu’il peut activer des fonctionnalités d’Azure AD telles que l’authentification multifacteur. Hello suivant schéma peut aider le processus de hello tooillustrate.

![Diagramme des répertoires toomanage indépendant](./media/active-directory-manage-o365-subscription/AAD_O365_03.png)

Dans ce cas, hello deux annuaires sont indépendants de l’autre.

## <a name="toomanage-two-independent-directories"></a>répertoires indépendants toomanage deux
Dans commande de Michael Smith toomanage les deux annuaires pendant qu’il est connecté dans tooAzure comme msmith@hotmail.com, il doit terminer hello comme suit :

> [!NOTE]
> Ces étapes ne peuvent être effectuées que lorsqu'un utilisateur est connecté via un compte Microsoft. Si l’utilisateur de hello est connecté avec un compte professionnel ou scolaire, hello option trop**utiliser un annuaire existant** n’est pas disponible. Un compte professionnel ou scolaire peut être authentifié uniquement par son répertoire de base (autrement dit, hello directory emplacement hello compte professionnel ou scolaire, et cette entreprise de hello school est propriétaire).
>
>

1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com) comme msmith@hotmail.com.
2. Cliquez sur **Nouveau** > **App Services** > **Active Directory** > **Répertoire** > **Création personnalisée**.
3. Cliquez sur utiliser existant hello directory et sélectionnez **je suis prêt toobe me déconnecter** case à cocher.
4. Se connecter toohello portail classique Azure en tant qu’administrateur global de Contoso.onmicrosoft.com (par exemple, msmith@contoso.com).
5. Lorsque vous y êtes invité trop**utiliser un annuaire hello Contoso avec Azure ?**, cliquez sur **continuer**.
6. Cliquez sur **Se déconnecter maintenant**.
7. Se connecter toohello portail classique Azure en tant que msmith@hotmail.com. l’annuaire Contoso hello et le répertoire par défaut de hello apparaissent dans hello extension Active Directory.

Après avoir effectué ces étapes, msmith@hotmail.com est un administrateur global dans l’annuaire Contoso hello.

## <a name="tooadminister-resources-as-hello-global-admin"></a>ressources tooadminister comme hello administrateur général
Maintenant Supposons que Jane Doe doit administrer les sites Web et des ressources de base de données qui sont associées aux hello abonnement Azure pour msmith@hotmail.com. Avant de lui faire, Michael Smith doit toocomplete supplémentaires comme suit :

1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com) à l’aide du compte d’administrateur de Service hello pour hello abonnement Azure (dans cet exemple, msmith@hotmail.com).
2. Transfert de l’annuaire Contoso hello abonnement toohello : cliquez sur **paramètres** > **abonnements** > sélectionnez hello abonnement > **modifier l’annuaire** > sélectionnez **Contoso (Contoso.com)**. Dans le cadre du transfert de hello, toute entreprise ou école comptes qui sont coadministrateurs de hello abonnement sont supprimés.
3. Ajouter des Jane Doe en tant que coadministrateur de l’abonnement de hello : cliquez sur **paramètres** > **administrateurs** > sélectionnez hello abonnement > **ajouter** > type **JohnDoe@Contoso.com**.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur la relation hello entre les abonnements et des répertoires, consultez [comment un abonnement est associé à un répertoire](active-directory-how-subscriptions-associated-directory.md).
