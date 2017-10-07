---
title: 'Azure AD Connect : authentification directe - Verrouillage intelligent | Documents Microsoft'
description: "Cet article décrit comment l’authentification Azure Active Directory (Azure AD) pass-through protège vos comptes locale contre les attaques de mot de passe en force brute dans le cloud de hello."
services: active-directory
keywords: "Authentification directe Azure AD Connect, installation d’Active Directory, composants requis pour Azure AD, SSO, Authentification unique"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: b02e315c3cc3eae00ca6408d735a416f34c2cdc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a>Authentification directe Azure Active Directory : Verrouillage intelligent

## <a name="overview"></a>Vue d'ensemble

Azure AD protège contre les attaques de mot de passe par recherche exhaustive et empêche le verrouillage des utilisateurs authentiques sur leurs applications Office 365 et SaaS. Cette fonctionnalité, appelée **Verrouillage intelligent**, est pris en charge lorsque vous utilisez l’authentification directe en tant que méthode de connexion. Verrouillage intelligent est activée par défaut pour tous les locataires et protégez vos comptes d’utilisateur de tout temps hello ; Il n’existe aucun besoin tooturn sur.

Le verrouillage intelligent fonctionne en conservant la trace des tentatives de connexion ayant échoué et après un certain **Seuil de verrouillage**, en démarrant une **Durée de verrouillage**. Toutes les tentatives de connexion à partir de l’attaquant hello pendant hello durée de verrouillage sont rejetées. Si hello attaque se poursuit, hello suivantes ayant échoué tentatives de connexion hello durée de verrouillage de fin entraîne des durées de verrouillage de plus de temps.

>[!NOTE]
>la valeur par défaut de Hello seuil de verrouillage est 10 tentatives ayant échoué et par défaut de hello que durée de verrouillage est de 60 secondes.

Verrouillage actif également fait la distinction entre les connexions d’utilisateurs authentiques et contre les personnes malveillantes et des verrous uniquement à des personnes malveillantes hello dans la plupart des cas. Cette fonctionnalité empêche les attaquants de verrouiller à des fins malveillantes des utilisateurs authentiques. Nous utilisons au-delà de connexion comportement, les appareils des utilisateurs & navigateurs et autres toodistinguish signaux entre les utilisateurs authentiques et des personnes malveillantes. Nous améliorons constamment nos algorithmes.

Étant donné que l’authentification directe transfère les demandes de validation de mot de passe sur votre système local Active Directory (AD), vous devez les personnes malveillantes tooprevent de verrouillage des comptes de vos utilisateurs AD. Étant donné que vous avez vos propres stratégies de verrouillage de compte Active Directory (en particulier, [ **seuil de verrouillage de compte** ](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) et [ **réinitialiser compte le verrouillage du compteur après stratégies** ](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), vous devez le seuil de verrouillage tooconfigure d’Azure AD et durée de verrouillage de valeurs correctement toofilter des attaques dans le cloud de hello avant qu’ils atteignent votre service Active Directory.

>[!NOTE]
>est gratuite et fonctionnalité de verrouillage actives Hello _sur_ par défaut pour tous les clients. Toutefois, la modification du seuil de verrouillage d’Azure AD et les valeurs de durée de verrouillage à l’aide de l’API Graph doit votre licence de Premium P2 toohave AD Azure au moins un client. Vous n’avez pas besoin d’une licence Azure AD Premium P2 _par utilisateur_ fonctionnalité de verrouillage actives hello tooget avec l’authentification directe.

tooensure que vos utilisateurs AD comptes locaux sont correctement protégés, vous devez tooensure qui :

1.  le seuil de verrouillage d’Azure AD est _inférieur_ au seuil de verrouillage du compte AD. Nous vous recommandons de définir les valeurs hello telles que le seuil de verrouillage de compte de l’annonce est au moins deux ou trois fois le seuil de verrouillage d’Azure AD.
2.  La durée de verrouillage d’Azure AD (représentée en secondes) est _plus longue_ que Réinitialiser le compteur de verrouillage du compte après (exprimée en minutes) d’AD.

## <a name="verify-your-ad-account-lockout-policies"></a>Vérifiez vos stratégies de verrouillage de compte AD

Utilisez hello suivant les instructions tooverify vos stratégies de verrouillage de compte Active Directory :

1.  Ouvrez l’outil de gestion de stratégie de groupe hello.
2.  Modifier hello stratégie de groupe qui est appliqué tooall utilisateurs, par exemple, hello stratégie de domaine par défaut.
3.  Accédez tooComputer stratégie de verrouillage de compte Configuration ordinateur\Stratégies\Paramètres Windows\Paramètres paramètres.
4.  Vérifiez vos valeurs de Seuil de verrouillage de compte et Réinitialiser le compteur de verrouillage du compte après.

![Stratégies de verrouillage de compte AD](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-hello-graph-api-toomanage-your-tenants-smart-lockout-values"></a>Utiliser des valeurs de verrouillage intelligente de votre locataire hello API Graph toomanage

>[!IMPORTANT]
>Modifier les valeurs du seuil de verrouillage et de la durée de verrouillage d’Azure AD à l’aide de l’API Graph est une fonctionnalité d’Azure AD Premium P2. Il doit également toobe un administrateur Global sur votre client.

Vous pouvez utiliser [Explorateur graphique](https://developer.microsoft.com/graph/graph-explorer) tooread, définir et mettre à jour les valeurs de verrouillage actives d’Azure AD. Mais vous pouvez également effectuer ces opérations par programme.

### <a name="read-smart-lockout-values"></a>Lire les valeurs de verrouillage intelligent

Suivez ces étapes tooread valeurs de verrouillage intelligente de votre locataire :

1. Connectez-vous à l’Explorateur graphique en tant qu’administrateur global de votre client. Si vous y êtes invité, accordez l’accès hello les autorisations demandées.
2. Cliquez sur « Modifier les autorisations » et sélectionnez l’autorisation « Directory.ReadWrite.All » hello.
3. Demande d’API Graph hello le configurer comme suit : définir la version trop « BETA », type de demande trop « GET » et l’URL trop`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.
4. Cliquez sur « Exécuter la requête » toosee de valeurs de verrouillage intelligente de votre locataire. Si vous n’avez pas défini les valeurs de votre client avant, un ensemble vide s’affiche.

### <a name="set-smart-lockout-values"></a>Définir les valeurs de verrouillage intelligent

Suivez ces étapes tooset valeurs de verrouillage intelligente de votre locataire (pour hello uniquement la première fois) :

1. Connectez-vous à l’Explorateur graphique en tant qu’administrateur global de votre client. Si vous y êtes invité, accordez l’accès hello les autorisations demandées.
2. Cliquez sur « Modifier les autorisations » et sélectionnez l’autorisation « Directory.ReadWrite.All » hello.
3. Demande d’API Graph hello le configurer comme suit : définir la version trop « BETA », type de demande trop « POST » et l’URL trop`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.
4. Copiez et collez hello suivant de demande JSON dans le champ de « Corps de la demande » hello. Modifier les valeurs de verrouillage actives hello comme il convient et utiliser un GUID aléatoire pour `templateId`.
5. Cliquez sur « Exécuter la requête » tooset de valeurs de verrouillage intelligente de votre locataire.

```
{
  "templateId": "5cf42378-d67d-4f36-ba46-e8b86229381d",
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "300"
    },
    {
      "name": "LockoutThreshold",
      "value": "5"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

>[!NOTE]
>Si vous ne les utilisez pas, vous pouvez laisser hello **BannedPasswordList** et **EnableBannedPasswordCheck** valeurs sous la forme vide (« ») et « false » respectivement.

Vérifiez que vous avez défini les valeurs de verrouillage intelligent de votre client correctement à l’aide de [ces étapes](#read-smart-lockout-values).

### <a name="update-smart-lockout-values"></a>Mettre à jour les valeurs de verrouillage intelligent

Suivez ces tooupdate étapes valeurs de verrouillage intelligente de votre locataire (si vous avez déjà défini les avant) :

1. Connectez-vous à l’Explorateur graphique en tant qu’administrateur global de votre client. Si vous y êtes invité, accordez l’accès hello les autorisations demandées.
2. Cliquez sur « Modifier les autorisations » et sélectionnez l’autorisation « Directory.ReadWrite.All » hello.
3. [Suivez ces étapes tooread valeurs de verrouillage intelligente de votre locataire](#read-smart-lockout-values). Hello de copie `id` valeur (GUID) de l’élément hello avec « displayName » en tant que « PasswordRuleSettings ».
4. Demande d’API Graph hello le configurer comme suit : définir la version trop « BETA », type de demande trop « Corriger » et l’URL trop`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` -utiliser hello GUID à partir de l’étape 3 pour `<id>`.
5. Copiez et collez hello suivant de demande JSON dans le champ de « Corps de la demande » hello. Modifier les valeurs de verrouillage actives hello comme il convient.
6. Cliquez sur « Exécuter la requête » tooupdate de valeurs de verrouillage intelligente de votre locataire.

```
{
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "30"
    },
    {
      "name": "LockoutThreshold",
      "value": "4"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

Vérifiez que vous avez mis à jour les valeurs de verrouillage intelligent de votre client correctement à l’aide de [ces étapes](#read-smart-lockout-values).

## <a name="next-steps"></a>Étapes suivantes
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) : pour formuler des requêtes de nouvelles fonctionnalités.
