---
title: "Azure Active Directory B2C : Multi-Factor Authentication | Microsoft Docs"
description: "Comment tooenable l’authentification multifacteur dans les applications pour les consommateurs sécurisées par Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 53ef86c4-1586-45dc-9952-dbbd62f68afc
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 29beb1e6ab5d8ab5a65f9c5c068d9e71c60418dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-enable-multi-factor-authentication-in-your-consumer-facing-applications"></a>Azure Active Directory B2C : activation de Multi-Factor Authentication dans vos applications accessibles aux consommateurs
Azure Active Directory (Azure AD) B2C s’intègre directement à [Azure multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) afin que vous pouvez ajouter une deuxième couche de sécurité toosign à distance et connexion des expériences dans vos applications pour les consommateurs. Vous pouvez faire cela sans écrire une seule ligne de code. Actuellement, nous prenons en charge un appel téléphonique et un message texte pour la vérification. Si vous déjà créé des stratégies d’inscription et de connexion, vous pouvez toujours activer Multi-Factor Authentication.

> [!NOTE]
> Vous pouvez également activer Multi-Factor Authentication lors de la création de stratégies d’inscription et de connexion, pas seulement lors de la modification de stratégies existantes.
> 
> 

Cette fonctionnalité permet aux applications de gérer des scénarios tels que les suivants hello :

* Une application de l’authentification multifacteur tooaccess n’est pas nécessaire, mais vous en avez besoin tooaccess un autre. Par exemple, consommateur de hello peuvent se connecter à une application d’assurance automatique avec un compte local ou de réseaux sociaux, mais doit vérifier numéro de téléphone hello avant l’accès à l’application hello de d’assurance accueil Bonjour même répertoire.
* Vous ne nécessitent pas l’authentification multifacteur tooaccess une application en général, mais vous en avez besoin tooaccess des parties hello sensibles qu’il contient. Par exemple, consommateur de hello tooa bancaires application avec un compte local ou de réseaux sociaux et le solde du compte à cocher peut se connecter, mais il doit vérifier le numéro de téléphone hello avant de tenter un transfert réseau.

## <a name="modify-your-sign-up-policy-tooenable-multi-factor-authentication"></a>Modifier votre tooenable de stratégie d’inscription multi-Factor Authentication
1. [Suivez ces Panneau de fonctionnalités étapes toonavigate toohello B2C hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Cliquez sur **Stratégies d'inscription**.
3. Cliquez sur tooopen de votre stratégie d’inscription (par exemple, « B2C_1_SiUp ») il.
4. Cliquez sur **l’authentification multifacteur** et activer hello **état** trop**ON**. Cliquez sur **OK**.
5. Cliquez sur **enregistrer** haut hello du Panneau de hello.

Vous pouvez utiliser la fonctionnalité de « Exécuter maintenant » hello sur hello stratégie tooverify hello expérience des utilisateurs. Validez les éléments suivants de hello :

Un compte grand public est créé dans votre répertoire avant de l’étape de l’authentification multifacteur hello se produit. Pendant l’étape hello, le consommateur de hello est invité tooprovide son numéro de téléphone et vérifiez que l’opération. Si la vérification est réussie, le numéro de téléphone hello est attaché compte du consommateur toohello pour une utilisation ultérieure. Même si le consommateur de hello annule ou est supprimée, il ou elle pouvant être posée tooverify un numéro de téléphone à nouveau au cours de hello connectez-vous suivant (avec l’authentification multifacteur activée).

## <a name="modify-your-sign-in-policy-tooenable-multi-factor-authentication"></a>Modifier votre tooenable de stratégie d’authentification multi-Factor Authentication
1. [Suivez ces Panneau de fonctionnalités étapes toonavigate toohello B2C hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Cliquez sur **Stratégies d’authentification**.
3. Cliquez sur tooopen de votre stratégie d’authentification (par exemple, « B2C_1_SiIn ») il. Cliquez sur **modifier** haut hello du Panneau de hello.
4. Cliquez sur **l’authentification multifacteur** et activer hello **état** trop**ON**. Cliquez sur **OK**.
5. Cliquez sur **enregistrer** haut hello du Panneau de hello.

Vous pouvez utiliser la fonctionnalité de « Exécuter maintenant » hello sur hello stratégie tooverify hello expérience des utilisateurs. Validez les éléments suivants de hello :

Lorsque les consommateurs hello se connecte (à l’aide d’un compte local ou de réseaux sociaux), si un numéro de téléphone vérifié est attaché compte du consommateur toohello, il ou elle est demandée tooverify il. Si aucun numéro de téléphone n’est attachée, consommateur de hello est demandé tooprovide une et vérifiez que l’opération. Vérification réussie, le numéro de téléphone hello est attaché compte du consommateur toohello pour une utilisation ultérieure.

## <a name="multi-factor-authentication-on-other-policies"></a>Authentification multifacteur sur d’autres stratégies
Comme décrit pour les stratégies d’inscription et connexion ci-dessus, il est également possible tooenable l’authentification multifacteur d’abonnement ou réinitialiser les stratégies de mot de passe et stratégies d’authentification. Cette fonctionnalité sera également disponible prochainement sur les stratégies de modification de profil.

