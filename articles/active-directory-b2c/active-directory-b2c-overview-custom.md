---
title: "Azure Active Directory B2C : stratégies personnalisées | Microsoft Docs"
description: "Une rubrique sur les stratégies personnalisées Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1ff398a4-2079-4615-94f1-57de22c0aad6
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: bada9cf5f1a86f3dd047536f6fd9359c0231a384
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-custom-policies"></a>Azure Active Directory B2C : stratégies personnalisées

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

## <a name="what-are-custom-policies"></a>Que sont les stratégies personnalisées ?

Les stratégies personnalisées sont des fichiers de configuration qui définissent le comportement de hello de votre locataire Azure AD B2C. Alors que **stratégies intégrées** sont prédéfinies dans le portail de hello Azure AD B2C pour hello tâches identité les plus courantes, les stratégies personnalisées peuvent être entièrement modifié par un toocomplete de développeur d’identité un nombre illimité de proche de tâches. Lisez la suite toodetermine si les stratégies personnalisées sont droite pour vous et votre scénario d’identité.

**La modification de stratégies personnalisées ne s’adresse pas à tout le monde.** demande de la courbe d’apprentissage Hello, temps de démarrage hello est plus long, et stratégies toocustom de futures modifications nécessitera toomaintain d’expertise similaire. Il est important de commencer par étudier attentivement les stratégies prédéfinies dans le cadre de votre scénario avant d’utiliser des stratégies personnalisées.

## <a name="comparing-built-in-policies-and-custom-policies"></a>Comparaison des stratégies prédéfinies et des stratégies personnalisées

| | Stratégies prédéfinies | Stratégies personnalisées |
|-|-------------------|-----------------|
|Utilisateurs cibles | Tous les développeurs d’applications avec ou sans expertise de l’identité | Professionnels de l’identité : intégrateurs système, consultants et équipes d’identité internes. Ils sont à l’aise avec les flux OpenID Connect et comprennent les fournisseurs d’identité et l’authentification basée sur les revendications. |
|Mode de configuration | Portail Azure avec interface utilisateur conviviale | Modifier directement les fichiers XML, puis téléchargez toohello portail Azure |
|Personnalisation de l’interface utilisateur | Personnalisation complète de l’interface utilisateur, avec prise en charge HTML, CSS et JScript (nécessite un domaine personnalisé)<br><br>Prise en charge multilingue avec chaînes personnalisées | Identique |
| Personnalisation des attributs | Attributs standard et personnalisés | Identique |
|Gestion des jetons et des sessions | Options de jetons personnalisés et de sessions multiples | Identique |
|Identity Providers| **Aujourd'hui** : fournisseur social local prédéfini<br><br>**À l’avenir** : OIDC basé sur les normes, SAML, OAuth | **Aujourd'hui** : OIDC basé sur les normes, OAuth, SAML<br><br>**À l’avenir** : WS-Fed |
|Tâches d’identité (exemples) | Inscription ou connexion avec des comptes locaux et de nombreux comptes sociaux<br><br>Réinitialisation du mot de passe en libre-service<br><br>Modification de profil<br><br>Scénarios d’authentification multifacteur<br><br>Personnalisation des jetons et des sessions<br><br>Flux de jetons d’accès | Terminer hello même tâches en tant que stratégies intégrées à l’aide de fournisseurs d’identité personnalisé ou utiliser les étendues personnalisées<br><br>Utilisateur de disposition dans un autre système au moment de hello d’enregistrement<br><br>Envoi d’un courrier électronique de bienvenue avec votre propre fournisseur de service de messagerie<br><br>Utilisation d’un magasin d’utilisateurs en dehors de B2C<br><br>Validation des informations fournies par l’utilisateur avec un système approuvé via une API |

## <a name="policy-files"></a>Fichiers de stratégie

Une stratégie personnalisée est représentée comme un ou plusieurs fichiers au format XML qui font référence tooeach autre dans une chaîne hiérarchique. définissent les éléments XML de Hello : schéma de revendications, les revendications transformations, les définitions de contenu, profils de fournisseurs et techniques de revendications et étapes d’orchestration Userjourney, entre autres éléments.

Nous vous recommandons d’utiliser hello des trois types de fichiers de stratégie :

- **Un fichier de BASE**, qui contient la plupart des définitions de hello et pour lequel Azure fournit un exemple complet.  Nous vous recommandons de que procéder à un nombre minimal de modifications toothis toohelp résolution des problèmes de fichiers et de maintenance à long terme de vos stratégies
- **un fichier d’EXTensions** qui contient les modifications de configuration unique hello pour votre client
- **un fichier de partie de confiance (RP)** qui est hello unique tâche axée sur le fichier qui est appelé directement par l’application hello ou un service (c'est-à-dire dans la partie de confiance).  Lire l’article hello des définitions de fichier de stratégie pour plus d’informations.  Chaque tâche unique requiert son propre RP et en fonction de la configuration requise de la marque, nombre de hello peut être « total des applications x le nombre total de cas d’utilisation ».


Les stratégies intégrées dans Azure AD B2C procèdent hello 3-fichier mentionnés ci-dessus, mais le développeur de hello uniquement voit hello fichier du tiers de confiance (RP), tandis que le portail de hello apporte des modifications dans le fichier des extensions de hello arrière-plan toohello.

## <a name="core-concepts-you-should-know-when-using-custom-policies"></a>Principaux concepts à connaître pour utiliser les stratégies personnalisées

### <a name="azure-active-directory-b2c"></a>Azure Active Directory B2C

Service de gestion des accès et des identités clients d’Azure. le service Hello inclut :

1. Un répertoire de l’utilisateur sous forme de hello d’un spécial Azure Active Directory accessible via Microsoft Graph et qui contient les données utilisateur pour les comptes locaux et fédérés 
2. Accès toohello **infrastructure d’identité expérience** qui orchestre la relation d’approbation entre les utilisateurs et les entités et transmet les revendications entre eux toocomplete une tâche de gestion d’identité ou d’y accéder 
3. Un service jeton de sécurité (STS) émettre id jetons, actualisation des jetons et accès jetons (et les assertions SAML équivalentes) et en les validant tooprotect ressources.

Azure AD B2C interagit avec les fournisseurs d’identité, les utilisateurs, d’autres systèmes et le répertoire utilisateur local hello dans la séquence tooachieve une tâche d’identité (par exemple, la connexion utilisateur, inscrire un nouvel utilisateur, un mot de passe). Hello plateforme sous-jacente qui établit l’approbation de partie multiples et exécute ces étapes est appelée hello infrastructure expérience d’identité et une stratégie (également appelé un déplacement de l’utilisateur ou d’une stratégie d’approbation d’infrastructure) définit explicitement les acteurs hello, les actions hello, hello protocoles et séquence hello d’étapes toocomplete.

### <a name="identity-experience-framework"></a>Identity Experience Framework (Infrastructure d’expérience d’identité)

Plateforme Azure cloud, entièrement configurable et pilotée par des stratégies, qui orchestre les relations de confiance entre entités (en général des fournisseurs de revendications) dans des formats de protocoles standard, notamment OpenID Connect, OAuth, SAML, WS-Fed, ainsi que quelques protocoles non standard (par exemple, des échanges de revendications intersystèmes basés sur l’API REST). Hello I2E crée conviviale, whitelabelled rencontre qui prennent en charge HTML, CSS et jscript.  Aujourd'hui, hello identité expérience Framework est disponible uniquement dans un contexte de hello Azure AD B2C service hello et hiérarchisés pour tooCIAM associés de tâches.

### <a name="built-in-policies"></a>Stratégies prédéfinies

Fichiers de configuration que comportement hello directe d’identité de Azure AD B2C tooperform hello couramment utilisé (enregistrement d’utilisateur, ouverture de session, réinitialisation de mot de passe) des tâches et d’interagir avec les parties de confiance dont la relation est également prédéfinie dans Azure AD B2C (de prédéfinies par exemple, fournisseur d’identité Facebook, LinkedIn, Microsoft Account, comptes Google).  Bonjour futures, les stratégies intégrées peuvent également fournir pour la personnalisation des fournisseurs d’identité qui sont en général dans le domaine d’entreprise hello tels que Azure Active Directory Premium, Active Directory/ADFS, etc. de Salesforce ID fournisseur.


### <a name="custom-policies"></a>Stratégies personnalisées

Fichiers de configuration qui définissent le comportement hello de l’infrastructure d’identité expérience dans votre locataire Azure AD B2C. Une stratégie personnalisée est accessible en tant qu’un ou plusieurs fichiers XML (voir les définitions de fichiers de stratégie) qui sont exécutées par hello identité expérience Framework lorsqu’elle est appelée par une tierce partie de confiance (par exemple, une application). Stratégies personnalisées peuvent être modifiées directement par un toocomplete de développeur d’identité un nombre illimité de proche de tâches. Aux développeurs de configurer les stratégies personnalisées doivent définir hello des relations approuvées dans les points de terminaison de métadonnées de détail prudent tooinclude, les revendications exactes échangent des définitions et configurer les clés secrètes, clés et certificats selon les besoins de chaque fournisseur d’identité.

## <a name="policy-file-definitions-for-identity-experience-framework-trustframeworks"></a>Définitions de fichiers de stratégie pour les infrastructures de confiance de l’infrastructure d’expérience d’identité

### <a name="policy-files"></a>Fichiers de stratégie

Une stratégie personnalisée est représentée comme un ou plusieurs fichiers au format XML qui font référence tooeach autre dans une chaîne hiérarchique. définissent les éléments XML de Hello : schéma de revendications, les revendications transformations, les définitions de contenu, profils de fournisseurs et techniques de revendications et étapes d’orchestration Userjourney, entre autres éléments.  Nous vous recommandons d’utiliser hello des trois types de fichiers de stratégie :

- **Un fichier de BASE**, qui contient la plupart des définitions de hello et pour lequel Azure fournit un exemple complet.  Nous vous recommandons de que procéder à un nombre minimal de modifications toothis toohelp résolution des problèmes de fichiers et de maintenance à long terme de vos stratégies
- **un fichier d’EXTensions** qui contient les modifications de configuration unique hello pour votre client
- **un fichier de partie de confiance (RP)** qui est hello unique tâche axée sur le fichier qui est appelé directement par l’application hello ou un service (c'est-à-dire dans la partie de confiance).  Lire l’article hello des définitions de fichier de stratégie pour plus d’informations.  Chaque tâche unique requiert son propre RP et en fonction de la configuration requise de la marque, nombre de hello peut être « total des applications x le nombre total de cas d’utilisation ».

![Types de fichiers de stratégie](media/active-directory-b2c-overview-custom/active-directory-b2c-overview-custom-policy-files.png)

| Type de fichier de stratégie | Exemples de noms de fichier | Utilisation recommandée | Hérite de |
|---------------------|--------------------|-----------------|---------------|
| BASE |TrustFrameworkBase.xml<br><br>Mytenant.onmicrosoft.com-B2C-1A_BASE1.xml | Inclut le schéma de revendications principal hello, les transformations de revendications, les fournisseurs de revendications et trajets utilisateur configurés par Microsoft<br><br>Vérifiez le fichier toothis des modifications minimales | Aucun |
| Extension (EXT) | TrustFrameworkExtensions.xml<br><br>Mytenant.onmicrosoft.com-B2C-1A_EXT.xml | Consolider ici votre fichier BASE toohello modifications<br><br>Fournisseurs de revendications modifiés.<br><br>Parcours utilisateur modifiés.<br><br>Vos propres définitions de schéma personnalisées. | Fichier de BASE |
| Partie de confiance (RP) | B2C_1A_sign_up_sign_in.xml| Modifiez les paramètres de jeton, de forme et de session ici| Fichier Extensions(EXT) |

### <a name="inheritance-model"></a>Modèle d’héritage

Lorsqu’une application appelle un fichier de stratégie de RP hello, hello infrastructure d’identité expérience dans B2C ajouter tous les éléments hello de BASE, puis à partir des EXTENSIONS et enfin de hello RP stratégie fichier tooassemble hello stratégie actuellement en vigueur.  Éléments de hello même type et nom de fichier RP hello remplacent celles de hello EXTENSIONS et remplacements d’EXTENSIONS BASE.

**Stratégies intégrées** dans Azure AD B2C procèdent hello 3-fichier mentionnés ci-dessus, mais le développeur de hello uniquement voit hello fichier du tiers de confiance (RP), tandis que le portail de hello apporte des modifications dans le fichier des extensions de hello arrière-plan toohello.  Tous les Azure AD B2C partage un fichier de stratégie de BASE qui est sous contrôle de code hello de l’équipe de hello Azure B2C et est fréquemment mis à jour.
