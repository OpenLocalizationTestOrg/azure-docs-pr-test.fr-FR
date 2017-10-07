---
title: aaaBranding instructions pour les Applications | Documents Microsoft
description: "Guide d’une gamme complète des ressources destinées aux toodeveloper pour Azure Active Directory"
services: active-directory
documentationcenter: dev-center-name
author: skwan
manager: mbaldwin
editor: 
ms.assetid: 72f4e464-1352-4a49-a18f-c37f58e7d5c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: skwan
ms.custom: aaddev
ms.openlocfilehash: e43f884c736a0dcb2e6e51293962ef1e2636ad70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="branding-guidelines-for-applications"></a>Directives de personnalisation des applications
Cette rubrique explique hello marque les instructions à suivre lors du développement d’applications avec Azure Active Directory (Azure AD). Ces instructions aideront à orienter les clients lorsqu’ils souhaitent toouse leur travail ou de compte scolaire, géré dans Azure AD ou de son compte personnel pour l’application de tooyour d’inscription et de connexion.

## <a name="personal-accounts-vs-work-or-school-accounts-from-microsoft"></a>Comptes personnels et comptes professionnels/scolaires de Microsoft
Microsoft gère deux types de compte d’utilisateur :

* **Comptes personnels** (anciennement Windows Live ID). Ces comptes représentent la relation hello entre *individuels* utilisateurs et Microsoft et qui servent tooaccess appareils et services de Microsoft. Ces comptes sont prévus pour un usage personnel.
* **Comptes professionnels ou scolaires.** Ces comptes sont gérés par Microsoft pour le compte d’organisations qui utilisent Azure Active Directory. Ces comptes sont utilisé toosign dans tooOffice 365 et d’autres services professionnels de Microsoft.

Microsoft sont généralement des comptes professionnels ou scolaires attribué aux utilisateurs de tooend (employés, étudiants, employés fédéraux) par leurs organisations (entreprise, établissement scolaire, organisme gouvernemental). Ces comptes sont que soit masterisé directement dans le cloud hello, dans la plateforme de hello Azure AD ou synchronisé tooAzure AD à partir d’un répertoire local, tel que Windows Server Active Directory. Microsoft est hello *opérateur* du travail de hello ou comptes d’établissement scolaire, mais hello comptes sont détenus et contrôlés par l’organisation de hello.

## <a name="referring-tooazure-ad-accounts-in-your-application"></a>Référence tooAzure AD des comptes dans votre application
Microsoft n’expose pas les utilisateurs finaux toohello Azure ou noms de marque Active Directory hello et aucun vous convient.

* Une fois que les utilisateurs sont connectés, vous devez utiliser le nom et le logo autant que possible l’organisation hello. Cela est préférable à l’utilisation de termes génériques tels que « votre organisation ».
* Lorsque les utilisateurs n’êtes pas connectés, vous devez consulter les comptes tootheir en tant que « travail comptes professionnels ou scolaires » et utilisez hello Microsoft logo tooconvey que ces comptes sont gérés par Microsoft. N’utilisez pas de termes tels que « compte d’entreprise » et « compte commercial », car ils embrouillent les utilisateurs.

## <a name="user-account-pictogram"></a>Pictogramme de compte d’utilisateur
Dans une version antérieure de ces directives, nous recommandions d’utiliser un pictogramme de « badge bleu ». Selon les commentaires utilisateur et le développeur, nous maintenant recommandons hello utilisation du logo de Microsoft hello à la place. Les utilisateurs comprennent qu’ils peuvent réutiliser le compte de hello qu’ils utilisent avec Office 365 ou autres toosign de services d’entreprise Microsoft dans tooyour application.

## <a name="signing-up-and-signing-in-with-azure-ad"></a>Inscription et connexion avec Azure AD
Votre application peut présenter des chemins d’accès distincts pour l’inscription et connexion et hello les sections suivantes proposent une aide visuelle pour les deux scénarios.

**Si votre application prend en charge l’inscription utilisateur final (par exemple, modèle libre de tootrial ou freemium)**: vous pouvez afficher un **connexion** bouton qui permet aux utilisateurs tooaccess de votre application avec son compte professionnel ou son compte personnel. Azure AD affiche un Bonjour invite de consentement première fois qu’ils accèdent à votre application.

**Si votre application nécessite des autorisations auxquelles seuls les administrateurs peuvent consentir ou si votre application requiert une licence d’entreprise**: vous devez séparer l’acquisition administrateur de la connexion utilisateur. Hello **bouton « obtenir cette application »** va rediriger toosign administrateurs dans puis demandez-lui de consentement toogrant part des utilisateurs dans leur organisation. Cela a hello avantage de supprimer les utilisateurs finaux consentement invites tooyour application.

## <a name="visual-guidance-for-app-acquisition"></a>Aide visuelle pour l’acquisition de l’application
Le lien « obtenir une application hello » doit rediriger accorder l’accès hello utilisateur toohello Azure AD (autoriser) page, tooallow tooauthorize d’administrateur d’une organisation des données de l’organisation tootheir qui sont hébergées par Microsoft d’accéder aux toohave de votre application. Plus d’informations sur comment toorequest accès sont abordés dans hello [intégration d’Applications avec Azure Active Directory](active-directory-integrating-applications.md) l’article.

Une fois que les administrateurs de consentement tooyour application, ils peuvent choisir tooadd il expérience de lanceur d’applications tootheir utilisateurs Office 365 (accessible à partir d’alvéolée de hello et de [https://portal.office.com/myapps](https://portal.office.com/myapps)). Si vous souhaitez tooadvertise cette fonctionnalité, vous pouvez utiliser des termes comme « Ajouter cette organisation de tooyour application » et d’afficher un bouton comme suit :

![Types d’application et scénarios](./media/active-directory-branding-guidelines/add-to-my-org.png)

Toutefois, nous vous recommandons de fournir un texte explicatif plutôt que de vous contenter des boutons. Par exemple :

> *Si vous utilisez déjà Office 365 ou autre service de l’entreprise à partir de Microsoft, vous pouvez accorder simplement les données de l’organisation tooyour < your_app_name > accès. Cela permettra à vos utilisateurs de tooaccess < your_app_name > avec leurs comptes de travail existant.*
> 
> 

## <a name="visual-guidance-for-sign-in"></a>Aide visuelle pour la connexion
Votre application doit afficher un signe de bouton qui redirige les utilisateurs toohello connexion point de terminaison qui correspond le protocole toohello vous utilisez toointegrate avec Azure AD. Hello suivant la section fournit des détails sur ce bouton qui doit ressembler à.

### <a name="pictogram-and-sign-in-with-microsoft"></a>Pictogramme et « Se connecter avec Microsoft »
C’est l’association hello de logo de Microsoft hello et hello « Sign in with « termes du contrat Microsoft qui représente de manière unique Azure AD parmi les autres fournisseurs d’identité que votre application peut prendre en charge. Si vous n’avez pas suffisamment d’espace pour « Microsoft in with de l’authentification », il est OK tooshorten il trop « connexion ».

![Types d’application et scénarios](./media/active-directory-branding-guidelines/sign-in-with-microsoft-light.png)

![Types d’application et scénarios](./media/active-directory-branding-guidelines/sign-in-light.png)

Vous pouvez également utiliser un jeu de couleurs foncé pour les boutons de hello.

![Types d’application et scénarios](./media/active-directory-branding-guidelines/sign-in-with-microsoft-dark.png)

![Types d’application et scénarios](./media/active-directory-branding-guidelines/sign-in-dark.png)

## <a name="branding-dos-and-donts"></a>Choses à faire et à éviter en matière de personnalisation
**FAIRE** utilisez « compte professionnel ou scolaire » en combinaison avec les utilisateurs finaux hello « Microsoft in with de l’authentification » bouton tooprovide explication supplémentaire toohelp reconnaît s’ils peuvent l’utiliser. **N’UTILISEZ PAS** de termes tels que « compte d’entreprise » ou « compte commercial ».

**N’UTILISEZ PAS** « ID Office 365 » ni « ID Azure ». Office 365 est également hello nom d’un offre de Microsoft, qui n’utilise pas Azure AD pour l’authentification du client.

**Ne pas** modifier le logo de Microsoft hello.

**Ne pas** exposer les marques les utilisateurs finaux toohello Azure ou Active Directory. Il est toutefois OK toouse ce termes du contrat avec les développeurs, les professionnels de l’informatique et les administrateurs.

## <a name="navigation-dos-and-donts"></a>Choses à faire et à éviter pour la navigation
**FAIRE** fournissent un moyen de toosign utilisateurs out et basculer le compte d’utilisateur tooanother. Bien que la plupart des gens aient un seul compte personnel Microsoft/Facebook/Google/Twitter, ils sont souvent associés à plus d’une organisation. La prise en charge de plusieurs utilisateurs connectés sera bientôt offerte.

