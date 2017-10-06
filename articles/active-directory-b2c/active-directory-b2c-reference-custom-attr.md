---
title: "Azure Active Directory B2C : attributs personnalisés | Microsoft Docs"
description: "Attributs personnalisés de toouse dans Azure Active Directory B2C toocollect plus d’informations sur vos clients."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 055ffb0a-197b-4716-8dad-1fd8a01e174f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: fb1bff77ad54c246c6d2f69f39c03eafb76fe6bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-toocollect-information-about-your-consumers"></a>Azure B2C Active Directory : Utilisez des attributs personnalisés toocollect plus d’informations sur vos clients
Votre annuaire Azure Active Directory (Azure AD) B2C est fourni avec un ensemble intégré d’informations (attributs) : le prénom, le nom, la ville, le code postal, et d’autres attributs. Toutefois, chaque application réservée aux consommateurs a des contraintes uniques sur le toogather attributs des consommateurs. Avec Azure AD B2C, vous pouvez étendre le jeu hello d’attributs stockés sur chaque compte du consommateur. Vous pouvez créer des attributs personnalisés sur hello [portail Azure](https://portal.azure.com/) et l’utiliser dans vos stratégies d’inscription, comme indiqué ci-dessous. Vous pouvez également lire et écrire ces attributs à l’aide de hello [API Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).

> [!NOTE]
> Les attributs personnalisés utilisent les [Extensions de schéma de répertoire de l’API Azure AD Graph](https://msdn.microsoft.com/library/azure/dn720459.aspx).
> 
> 

## <a name="create-a-custom-attribute"></a>Création d’un attribut personnalisé
1. [Suivez ces Panneau de fonctionnalités étapes toonavigate toohello B2C hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Cliquez sur **Attributs utilisateur**.
3. Cliquez sur **+ ajouter** haut hello du Panneau de hello.
4. Fournir un **nom** pour l’attribut personnalisé de hello (par exemple, « ShoeSize ») et, éventuellement, un **Description**. Cliquez sur **Créer**.
   
   > [!NOTE]
   > Uniquement hello « Chaîne » **Type de données** n’est disponible actuellement.
   > 
   > 

attribut personnalisé de Hello est désormais disponible dans la liste des hello **attributs utilisateur**et pour une utilisation dans vos stratégies d’inscription.

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a>Utilisation d’un attribut personnalisé dans votre stratégie d’inscription
1. [Suivez ces Panneau de fonctionnalités étapes toonavigate toohello B2C hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Cliquez sur **Stratégies d'inscription**.
3. Cliquez sur tooopen de votre stratégie d’inscription (par exemple, « B2C_1_SiUp ») il. Cliquez sur **modifier** haut hello du Panneau de hello.
4. Cliquez sur **des attributs d’abonnement** et sélectionnez hello, attribut personnalisé (par exemple, « ShoeSize »). Cliquez sur **OK**.
5. Cliquez sur **revendications Application** et les attributs personnalisés sélectionnez hello. Cliquez sur **OK**.
6. Cliquez sur **enregistrer** haut hello du Panneau de hello.

Vous pouvez utiliser la fonctionnalité de « Exécuter maintenant » hello sur hello stratégie tooverify hello expérience des utilisateurs. Vous devez maintenant voir « ShoeSize » dans la liste hello d’attributs collectées au cours de l’inscription du consommateur et apparaît dans l’application de jeton tooyour de retour envoyé hello.

## <a name="notes"></a>Remarques
* Au-delà des stratégies d’inscription, il est également possible d’utiliser des attributs personnalisés dans les stratégies de connexion ou d’authentification ainsi que dans les stratégies de modification de profil.
* Les attributs personnalisés présentent toutefois un inconvénient connu. Il est uniquement créé hello première fois, il est utilisé dans une stratégie, et pas lorsque vous les ajoutez toohello la liste des **attributs utilisateur**.

