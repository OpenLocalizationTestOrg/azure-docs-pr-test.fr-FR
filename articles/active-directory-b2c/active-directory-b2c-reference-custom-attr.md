---
title: "Azure Active Directory B2C : attributs personnalisés | Microsoft Docs"
description: "Utilisation d’attributs personnalisés dans Azure Active Directory B2C pour collecter des informations sur vos consommateurs"
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
ms.openlocfilehash: 356aaeff3a78fc7b682d621e8e0de9312582b2fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-to-collect-information-about-your-consumers"></a>Azure Active Directory B2C : utilisation d’attributs personnalisés pour recueillir des informations sur vos consommateurs
Votre annuaire Azure Active Directory (Azure AD) B2C est fourni avec un ensemble intégré d’informations (attributs) : le prénom, le nom, la ville, le code postal, et d’autres attributs. Cependant, toute application accessible aux consommateurs a des exigences uniques sur les attributs à recueillir auprès des consommateurs. Avec Azure AD B2C, vous pouvez étendre l’ensemble d’attributs stockés sur chaque compte client. Vous pouvez créer des attributs personnalisés sur le [portail Azure](https://portal.azure.com/) et les utiliser dans vos stratégies d’abonnement, comme illustré ci-dessous. Vous pouvez également lire et écrire ces attributs à l’aide de [l’API Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).

> [!NOTE]
> Les attributs personnalisés utilisent les [Extensions de schéma de répertoire de l’API Azure AD Graph](https://msdn.microsoft.com/library/azure/dn720459.aspx).
> 
> 

## <a name="create-a-custom-attribute"></a>Création d’un attribut personnalisé
1. [Suivez ces étapes pour accéder au panneau de fonctionnalités B2C sur le portail Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Cliquez sur **Attributs utilisateur**.
3. Cliquez sur **+Ajouter** dans la partie supérieure du panneau.
4. Fournissez un **nom** pour l’attribut personnalisé (par exemple, « ShoeSize ») et, éventuellement, une **description**. Cliquez sur **Create**.
   
   > [!NOTE]
   > Actuellement, seul le **Type de données** « String » est disponible.
   > 
   > 

L’attribut personnalisé est actuellement disponible dans la liste des **attributs utilisateur**, et pour une utilisation dans vos stratégies d’inscription.

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a>Utilisation d’un attribut personnalisé dans votre stratégie d’inscription
1. [Suivez ces étapes pour accéder au panneau de fonctionnalités B2C sur le portail Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Cliquez sur **Stratégies d'inscription**.
3. Ouvrez votre stratégie d’inscription (par exemple, « B2C_1_SiUp ») en cliquant dessus. Cliquez sur **Modifier** dans la partie supérieure du panneau.
4. Cliquez sur **Attributs d’inscription** , puis sélectionnez l’attribut personnalisé (par exemple, « ShoeSize »). Cliquez sur **OK**.
5. Cliquez sur **revendications d’applications** , puis sélectionnez l’attribut personnalisé. Cliquez sur **OK**.
6. Cliquez sur **Enregistrer** dans la partie supérieure du panneau.

La fonctionnalité « Exécuter maintenant » de la stratégie permet de vérifier l’expérience utilisateur. Vous devez maintenant voir « ShoeSize » dans la liste d’attributs collectés lors de l’inscription du consommateur, et le voir dans le jeton retourné à votre application.

## <a name="notes"></a>Remarques
* Au-delà des stratégies d’inscription, il est également possible d’utiliser des attributs personnalisés dans les stratégies de connexion ou d’authentification ainsi que dans les stratégies de modification de profil.
* Les attributs personnalisés présentent toutefois un inconvénient connu. L’attribut est créé lors de sa première utilisation dans une stratégie, et non pas lorsque vous l’ajoutez à la liste des **Attributs utilisateur**.

