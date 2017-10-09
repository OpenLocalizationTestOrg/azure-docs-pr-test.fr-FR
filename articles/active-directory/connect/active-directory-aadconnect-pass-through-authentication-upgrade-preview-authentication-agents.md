---
title: "Azure AD Connect : authentification directe - mise à niveau de la version préliminaire des agents d’authentification | Microsoft Docs"
description: "Cet article décrit comment tooupgrade votre configuration de l’authentification directe de Azure Active Directory (Azure AD)."
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
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 1695326b182278944e9f1584da72b18862b6ef27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-upgrade-preview-authentication-agents"></a>Azure Active Directory Connect : authentification directe - mise à niveau de la version préliminaire des agents d’authentification

## <a name="overview"></a>Vue d'ensemble

Cet article est destiné aux clients utilisant l’authentification directe Azure AD directe via l’aperçu. Nous avons récemment mis à niveau (et dont) hello logiciel de l’Agent d’authentification. Vous devez too_manually_, aperçu mise à niveau des Agents de l’authentification sur vos serveurs locaux. Cette mise à niveau manuelle s’effectue une seule fois. Toutes les futures mises à jour les Agents tooAuthentication sont automatiques. Hello raisons tooupgrade sont les suivantes :

- versions préliminaires de Hello d’authentification Agents ne recevront pas les plus de sécurité ou les correctifs de bogues.
-   versions préliminaires de Hello d’Agents d’authentification ne peut pas installées sur des serveurs supplémentaires pour la haute disponibilité.

## <a name="check-versions-of-your-authentication-agents"></a>Vérifiez les versions de vos agents d’authentification

### <a name="step-1-check-where-your-authentication-agents-are-installed"></a>Étape 1 : vérifier l’emplacement de l’installation de vos agents d’authentification

Suivez ces étapes toocheck où sont installées vos Agents de l’authentification :

1. Connectez-vous à toohello [centre d’administration Active Directory de Azure](https://aad.portal.azure.com) avec informations d’identification d’administrateur Global de hello pour votre client.
2. Sélectionnez **Azure Active Directory** de navigation de gauche hello.
3. Sélectionnez ensuite **Azure AD Connect**. 
4. Sélectionnez **Authentification directe**. Ce panneau répertorie les serveurs de hello où sont installées vos Agents de l’authentification.

![Centre d’administration Azure Active Directory - panneau Authentification directe](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

### <a name="step-2-check-hello-versions-of-your-authentication-agents"></a>Étape 2 : Vérifier les versions de hello de vos Agents de l’authentification

versions de hello toocheck vos agents de l’authentification, sur chaque serveur identifiée dans hello précédant l’étape, suivent ces instructions :

1. Accédez trop**le panneau de configuration -> Programmes -> Programmes et fonctionnalités** sur le serveur local de hello.
2. S’il existe une entrée pour «**Agent d’authentification Microsoft Azure AD Connect**», vous n’avez pas besoin tootake toute action sur ce serveur.
3. S’il existe une entrée pour «**connecteur de Proxy d’Application Microsoft Azure AD**», les versions 1.5.132.0 ou version antérieure, vous devez toomanually mise à niveau sur ce serveur.

![Version préliminaire de l’agent d’authentification](./media/active-directory-aadconnect-pass-through-authentication/pta6.png)

## <a name="best-practices-toofollow-before-starting-hello-upgrade"></a>Meilleures pratiques toofollow avant de commencer la mise à niveau hello

Avant la mise à niveau, assurez-vous d’avoir des hello éléments en place suivants :

1. **Créer le compte d’administrateur général uniquement dans le cloud**: ne pas mettre à niveau sans avoir un toouse de compte d’administrateur général cloud uniquement en cas d’urgence où vos Agents de l’authentification directe ne fonctionnent pas correctement. Découvrez comment [ajouter un compte d’administrateur général de type cloud uniquement](../active-directory-users-create-azure-portal.md). Cette étape est essentielle pour éviter que votre locataire ne soit verrouillé.
2.  **Garantir une haute disponibilité**: Si ne pas abouti précédemment, installez une deuxième autonome Agent d’authentification tooprovide haute disponibilité pour les demandes de connexion, l’utilisation de ces [instructions](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability).

## <a name="upgrading-hello-authentication-agent-on-your-azure-ad-connect-server"></a>La mise à niveau hello Agent d’authentification sur votre serveur Azure AD Connect

Vous devez mettre à niveau Azure AD Connect avant hello Agent d’authentification sur hello même serveur. Sur votre serveur principal et intermédiaire Azure AD Connect, procédez comme suit :

1. **Mise à niveau d’Azure AD Connect**: suivre ce [article](./active-directory-aadconnect-upgrade-previous-version.md) et toohello dernière Azure AD Connect version de mise à niveau.
2. **Désinstaller la version d’évaluation hello Hello Agent d’authentification**: télécharger [ce script PowerShell](https://aka.ms/rmpreviewagent) et l’exécuter en tant qu’administrateur sur le serveur de hello.
3. **Télécharger hello dernière version de l’Agent d’authentification de hello (versions 1.5.193.0 ou version ultérieure)**: connectez-vous toohello [centre d’administration Active Directory de Azure](https://aad.portal.azure.com) avec des droits d’administrateur Global de votre locataire. Sélectionnez **Azure Active Directory -> Azure AD Connect -> authentification directe -> agent de téléchargement**. Accepter les termes de hello du service et télécharger hello dernière version de hello Agent d’authentification.
4. **Installer version la plus récente de l’Agent d’authentification de hello hello**: hello exécuter exécutable téléchargé à l’étape 3. Fournissez les informations d’identification de l’administrateur général de votre locataire lorsque vous y êtes invité.
5. **Vérifiez que hello la dernière version a été installée**: comme indiqué auparavant, accédez trop**le panneau de configuration -> Programmes -> Programmes et fonctionnalités** et vérifiez qu’il existe une entrée pour «**Microsoft Azure AD Connect Agent d’authentification**».

>[!NOTE]
>Si vous activez le panneau d’authentification directe hello sur hello [centre d’administration Active Directory de Azure](https://aad.portal.azure.com) après avoir effectué les étapes précédentes de hello, vous verrez deux entrées de l’Agent de l’authentification par serveur : une entrée montrant hello Agent d’authentification en tant que **Active** et d’autres comme hello **inactif**. Ceci est _normal_. Hello **inactif** entrée est automatiquement supprimée après quelques jours.

## <a name="upgrading-hello-authentication-agent-on-other-servers"></a>La mise à niveau hello Agent d’authentification sur d’autres serveurs

Suivez ces étapes de tooupgrade authentification Agents sur d’autres serveurs (où Azure AD Connect n’est pas installé) :

1. **Désinstaller la version d’évaluation hello Hello Agent d’authentification**: télécharger [ce script PowerShell](https://aka.ms/rmpreviewagent) et l’exécuter en tant qu’administrateur sur le serveur de hello.
2. **Télécharger hello dernière version de l’Agent d’authentification de hello (versions 1.5.193.0 ou version ultérieure)**: connectez-vous toohello [centre d’administration Active Directory de Azure](https://aad.portal.azure.com) avec des droits d’administrateur Global de votre locataire. Sélectionnez **Azure Active Directory -> Azure AD Connect -> authentification directe -> agent de téléchargement**. Accepter les termes de hello du service et télécharger la version la plus récente hello.
3. **Installer version la plus récente de l’Agent d’authentification de hello hello**: hello exécuter exécutable téléchargé à l’étape 2. Fournissez les informations d’identification de l’administrateur général de votre locataire lorsque vous y êtes invité.
4. **Vérifiez que hello la dernière version a été installée**: comme indiqué auparavant, accédez trop**le panneau de configuration -> Programmes -> Programmes et fonctionnalités** et vérifiez qu’il existe une entrée appelée **Microsoft Azure AD Connect Agent d’authentification**.

>[!NOTE]
>Si vous activez le panneau d’authentification directe hello sur hello [centre d’administration Active Directory de Azure](https://aad.portal.azure.com) après avoir effectué les étapes précédentes de hello, vous verrez deux entrées de l’Agent de l’authentification par serveur : une entrée montrant hello Agent d’authentification en tant que **Active** et d’autres comme hello **inactif**. Ceci est _normal_. Hello **inactif** entrée est automatiquement supprimée après quelques jours.

## <a name="next-steps"></a>Étapes suivantes
- [**Résoudre les problèmes** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -en savoir comment tooresolve commun problèmes avec la fonctionnalité de hello.
