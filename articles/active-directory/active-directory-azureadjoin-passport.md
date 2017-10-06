---
title: "aaaAuthenticating des identités sans mot de passe via Windows Hello for Business et Azure AD | Documents Microsoft"
description: "Fournit une vue d’ensemble de Windows Hello Entreprise ainsi que des informations supplémentaires sur le déploiement de Windows Hello Entreprise."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: f907bb90-8776-46ca-9e12-279949af66ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 7c1c52e10b7ab7a89ec3226ffa7cf01896267871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-identities-without-passwords-through-windows-hello-for-business"></a>Authentification des identités sans mot de passe via Windows Hello Entreprise
méthodes de Hello en cours de l’authentification avec des mots de passe uniquement n’utilisent pas suffisamment tookeep-safe. Les utilisateurs réutilisent et oublient les mots de passe. Les mots de passe sont pouvant, phishable, susceptible d’engendrer des toocracks et à deviner. Ils récupèrent également tooremember difficile et tooattacks sujets tels que «[passer le hachage de hello](https://technet.microsoft.com/dn785092.aspx)».

## <a name="about-windows-hello-for-business"></a>À propos de Windows Hello Entreprise
Windows Hello Entreprise est une approche d’authentification par clé publique/privée ou basée sur les certificats pour les organisations et les consommateurs qui ne nécessite pas de passer par un mot de passe. Cette forme d’authentification s’appuie sur les informations d’identification de la paire de clés qui peuvent remplacer les mots de passe et résistent toobreaches, vols et hameçonnage.

 Windows Hello for Business permet à un utilisateur authentifier tooa compte Microsoft, un compte Active Directory Windows Server, un compte Microsoft Azure Active Directory (Azure AD) ou un service non Microsoft qui prend en charge l’authentification d’accélérée identité en ligne (Rex). Après une vérification en deux étapes initiales pendant Windows Hello pour l’inscription de l’entreprise, Windows Hello for Business est configuré sur le périphérique de l’utilisateur hello et utilisateur de hello définit un mouvement, qui peut être Windows Hello ou un code confidentiel. utilisateur de Hello fournit hello mouvement tooverify leur identité. Windows utilise Windows Hello pour l’utilisateur de Business tooauthenticate hello et aider les services et ressources de tooaccess protégé.

clé privée de Hello est accessible uniquement par le biais d’un mouvement « utilisateur », comme un code confidentiel, par biométrie ou un périphérique distant comme une carte à puce hello utilisateur utilise toosign toohello périphérique. Cette information est lié tooa certificat ou une paire de clés asymétrique. clé privée de Hello est matériel attestée si le périphérique de hello possède une puce de Module de plateforme sécurisée (TPM). clé privée de Hello ne quitte jamais hello périphérique.

clé publique de Hello est inscrit avec Azure Active Directory et de Windows Server Active Directory (pour local). Fournisseurs d’identité (IDPs) valider l’utilisateur de hello par mappage hello de clé publique hello utilisateur toohello privé et fournissent des informations de connexion via un mécanisme de notification différents, PhoneFactor ou une fois un mot de passe à usage unique.

## <a name="why-enterprises-should-adopt-windows-hello-for-business"></a>Pourquoi est-il conseillé aux entreprises d’adopter Windows Hello Entreprise ?
En activant Windows Hello Entreprise, les entreprises peuvent sécuriser davantage leurs ressources comme suit :

* Configuration de Windows Hello Entreprise avec une option de matériel préféré. ce qui signifie que les clés sont générées sur TPM 1.2 ou TPM 2.0 quand ces derniers sont disponibles Lorsque le module de plateforme sécurisée n’est pas disponible, logiciel génère hello clé.
* Longueur de hello et la complexité de hello définition ÉPINGLER, et si l’utilisation de Hello est activée dans votre organisation.
* Configuration Windows Hello pour les scénarios de type carte à puce toosupport à l’aide basée sur certificat de confiance.

## <a name="how-windows-hello-for-business-works"></a>Fonctionnement de Windows Hello Entreprise
1. Clés sont générées sur du matériel de hello par le module de plateforme sécurisée ou logiciels. De nombreux périphériques ont une puce TPM intégrée qui sécurise le matériel de hello en intégrant des clés de chiffrement dans les appareils. Équipé de TPM 1.2 ou TPM 2.0 génère des clés ou certificats qui sont créés à partir des clés de hello généré.
2. Hello TPM atteste ces clés liées au matériel.
3. Un mouvement unique déverrouiller déverrouille l’appareil de hello. Cette opération permet de toomultiple d’accéder aux ressources si le périphérique de hello est joint au domaine ou Azure appartenant à Active Directory.

## <a name="how-hello-windows-hello-for-business-lifecycle-works"></a>Fonctionne de hello Windows Hello du cycle de vie de l’entreprise
![Cycle de vie de Windows Hello Entreprise](./media/active-directory-azureadjoin/active-directory-azureadjoin-microsoft-passport.png)

Hello diagramme précédent illustre la paire de clés publique/privée hello et la validation par le fournisseur d’identité hello hello. Chacune de ces étapes est décrite en détail ci-dessous :

1. Hello utilisateur destiné à prouver leur identité via plusieurs méthodes intégrées que vérification linguistiques (mouvements, les cartes à puce physiques, l’authentification multifacteur) et envoie cette tooan informations fournisseur d’identité (IDP) comme Azure Active Directory ou Active Directory local.
2. Hello DISPOSITIF puis crée la clé de hello, atteste de la clé de hello, prend la partie publique de hello de cette clé, attache avec des instructions de station, se connecte et il envoie la clé de toohello IDP tooregister hello.
3. Dès que hello IDP enregistre la partie publique de hello de clé de hello, défis de IDP hello hello toosign appareil avec la partie privée de hello de clé de hello.
4. Hello IDP valide puis et problèmes hello jeton d’authentification qui permet des ressources de hello protégé de l’accès de périphérique hello et hello. IDPs peut écrire des applications multiplateformes ou utiliser le navigateur (via l’API de JavaScript/Webcrypto) toocreate et utiliser Windows Hello pour les informations d’identification de l’entreprise pour les utilisateurs.

## <a name="hello-deployment-requirements-for-windows-hello-for-business"></a>Hello les spécifications de déploiement pour Windows Hello for Business
### <a name="at-hello-enterprise-level"></a>Au niveau de l’entreprise hello
* entreprise de Hello possède un abonnement Azure.

### <a name="at-hello-user-level"></a>Au niveau de l’utilisateur hello
* ordinateur de l’utilisateur Hello exécute Windows 10 Professionnel ou entreprise.

Pour obtenir des instructions de déploiement détaillées, consultez [activer Windows Hello for Business dans l’organisation de hello](active-directory-azureadjoin-passport-deployment.md).

## <a name="additional-information"></a>Informations supplémentaires
* [Windows 10 pour les entreprises hello : appareils toouse de méthodes de travail](active-directory-azureadjoin-windows10-devices-overview.md)
* [Extension cloud appareils tooWindows 10 de fonctionnalités via Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [En savoir plus sur les scénarios d’utilisation pour Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Se connecter tooAzure de périphériques joints au domaine Active Directory pour des expériences Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configuration d’Azure AD Join](active-directory-azureadjoin-setup.md)

