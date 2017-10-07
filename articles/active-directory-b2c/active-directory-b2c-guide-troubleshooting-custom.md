---
title: "Azure Active Directory B2C : résoudre les problèmes liés aux stratégies personnalisées | Microsoft Docs"
description: "En savoir plus sur les approches toosolving erreurs lorsque vous travaillez avec des stratégies personnalisées dans Azure Active Directory."
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: joroja
ms.openlocfilehash: b9e1b46df1ddb29cdb90953e4a0d6f1dd085441f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-ad-b2c-custom-policies-and-identity-experience-framework"></a>Résoudre les problèmes liés aux stratégies personnalisées Azure AD B2C et à l’Infrastructure d’expérience d’identité.

Si vous utilisez Azure Active Directory B2C (B2C Active Directory de Azure) des stratégies personnalisées, vous risquez de rencontrer les défis configuration hello Framework rencontrer d’identité dans son format XML du langage stratégie.  Stratégies personnalisées de formation toowrite peuvent être comme un nouveau langage d’apprentissage. Dans cet article, nous décrivons des outils et proposons des conseils qui peuvent vous aider à identifier et résoudre rapidement les problèmes. 

> [!NOTE]
> Cet article est axé sur la résolution des problèmes de configuration de stratégie personnalisée Azure AD B2C. Elle ne répond pas hello application tiers ou sa bibliothèque de l’identité de partie de confiance.

## <a name="xml-editing"></a>Édition XML

Hello erreur la plus courante dans la configuration des stratégies personnalisées n’est pas au format XML. Un bon éditeur XML est quasiment essentiel. Un bon éditeur XML affiche le code XML en mode natif, applique un code couleur au contenu, prérenseigne les termes courants, maintient les éléments indexés et peut valider avec un schéma. Voici deux de nos éditeurs XML préférés :

* [Visual Studio Code](https://code.visualstudio.com/)
* [Notepad++](https://notepad-plus-plus.org/)

La validation du schéma XML identifie les erreurs avant le chargement de votre fichier XML. Dans le dossier racine de hello du pack de démarrage hello, obtenir la définition de schéma XML hello TrustFrameworkPolicy_0.3.0.0.xsd. Pour plus d’informations, dans la documentation de hello de votre éditeur XML, recherchez *outils XML* et *validation XML*.

Il peut être utile de passer en revue les règles XML. Azure AD B2C rejette toute erreur de mise en forme XML qu’il détecte. Parfois, une mauvaise mise en forme XML peut entraîner des messages d’erreur trompeurs.

## <a name="upload-policies-and-policy-validation"></a>Chargement et validation de stratégies

 La validation du chargement de fichier XML est automatique. La plupart des erreurs provoquent hello téléchargement toofail. Validation inclut un fichier de stratégie hello que vous téléchargez. Il inclut également la chaîne hello de téléchargement du fichier hello fait référence trop de fichiers (hello fichier partie de confiance de la stratégie de tiers, fichier des extensions hello et fichier de base hello). 
 
 Erreurs de validation courantes suivantes hello.

Extrait de code de l’erreur :`... makes a reference tooClaimType with id "displaName" but neither hello policy nor any of its base policies contain such an element`
* Hello ClaimType valeur peut être mal orthographié ou n’existe pas dans le schéma de hello.
* Les valeurs de ClaimType doivent être définis dans au moins un des fichiers hello dans la stratégie de hello. 
    Par exemple : ` <ClaimType Id="socialIdpUserId">`
* Si ClaimType est défini dans le fichier des extensions hello, mais il est également utilisé dans une valeur TechnicalProfile dans le fichier de base hello, téléchargement du fichier de base hello génère une erreur.

Extrait de code de l’erreur :`...makes a reference tooa ClaimsTransformation with id...`
* Bonjour les causes de l’erreur de hello peut être hello même que pour les erreurs de ClaimType hello.

Extrait de code de l’erreur :`Reason: User is currently logged as a user of 'yourtenant.onmicrosoft.com' tenant. In order toomanage 'yourtenant.onmicrosoft.com', please login as a user of 'yourtenant.onmicrosoft.com' tenant`
* Vérifiez que hello valeur TenantId Bonjour  **\<TrustFrameworkPolicy\>**  et  **\<BasePolicy\>**  éléments correspondent à votre cible Azure AD B2C client.  

## <a name="troubleshoot-hello-runtime"></a>Résoudre les problèmes de runtime de hello

* Utilisez `Run Now` et `https://jwt.io` tootest vos stratégies indépendamment de votre application mobile ou le web. Ce site web agit comme une application par partie de confiance. Il affiche le contenu hello Hello jeton Web JSON (JWT) qui est généré par votre stratégie Azure Active Directory B2C. toocreate une application test Framework expérience identité hello utilisez valeurs suivantes :
    * Nom : TestApp
    * Application/API web : Non
    * Client natif : Non

* l’échange hello tootrace de messages entre votre navigateur client et dans Azure AD B2C, utilisez [Fiddler](http://www.telerik.com/fiddler). Il peut vous aider à obtenir une indication de l’endroit où vos étapes d’orchestration échouent dans le parcours utilisateur.

* Dans **mode de développement**, utilisez **Application Insights** activité de hello tootrace de votre voyage d’utilisateur expérience infrastructure d’identité. Dans **mode de développement**, vous pouvez observer exchange hello de revendications entre hello infrastructure d’identité expérience et hello différentes revendications qui sont définis par les profils de techniques, telles que les fournisseurs d’identité, services basés sur les API, les fournisseurs répertoire de l’utilisateur Hello Azure AD B2C et d’autres services, tels que Azure Multi-Factor-Authentication.  

## <a name="recommended-practices"></a>Pratiques recommandées

**Conservez plusieurs versions de vos scénarios. Regroupez-les dans un projet avec votre application.** base de Hello, extensions et les fichiers de tiers partie de confiance sont directement dépendantes de l’autre. Enregistrez-les en tant que groupe. Comme les nouvelles fonctionnalités sont ajoutées les stratégies tooyour, conserver des versions de travail distinctes. Les versions de travail stade dans votre propre système de fichiers par code de l’application hello avec qu'ils interagissent.  Vos applications peuvent appeler de nombreuses stratégies de partie de confiance différentes dans un locataire. Ils peuvent devenir dépendantes sur les revendications hello qu’ils attendent à partir de vos stratégies d’Azure AD B2C.

**Développez et testez des profils techniques avec des parcours utilisateur connus.** Utilisez testé starter pack stratégies tooset vos profils techniques. Testez-les séparément avant de les incorporer à vos propres parcours utilisateur.

**Développez et testez des parcours utilisateur avec des profils techniques testés.** Modifier les étapes d’orchestration hello d’un parcours de l’utilisateur par incrément. Générez progressivement vos scénarios prévus.

## <a name="next-steps"></a>Étapes suivantes

* Dans GitHub, téléchargez le fichier .zip (https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) [active-directory-b2c-custom-policy-starterpack] de hello.
