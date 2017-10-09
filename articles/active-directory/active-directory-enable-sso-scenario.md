---
title: aaaManaging Applications avec Azure Active Directory | Documents Microsoft
description: "Cet article hello profiter des avantages de l’intégration d’Azure Active Directory avec vos locaux et cloud applications SaaS ;"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 95b96f10-2d5c-4b78-8af8-d3657a24140f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 0016f8b433e101d8a150bc6d9be3931851578241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-applications-with-azure-active-directory"></a>Gestion des applications avec Azure Active Directory
Au-delà de flux de travail réelle hello ou le contenu, les entreprises ont deux exigences de base pour toutes les applications :

1. tooincrease productivité, les applications doivent être toodiscover facile et accès
2. sécurité de tooenable et gouvernance, hello organisation a besoin de supervision sur qui peut et réellement est l’accès à chaque application et contrôle

Dans les applications cloud mieux cela à l’aide d’identité toocontrol hello world »*qui est autorisé toodo que*».

Dans la terminologie de l’informatique :

* *Qui* est appelé *identité* -hello gestion des utilisateurs et groupes
* *Ce que* est appelé *accéder à la gestion* : hello gestion de ressources tooprotected

Les deux composants réunies sous le nom *Identity and Access Management (IAM)*, qui est défini par hello [Gartner](http://www.gartner.com/it-glossary/identity-and-access-management-iam) groupe en tant que «*hello discipline de sécurité qui permet à droite de hello personnes tooaccess hello ressources à hello avec le bouton droit fois pour des raisons de droit hello*».

OK, alors, quel est le problème de hello ? Si IAM n’est *pas gérée* à un seul emplacement avec une solution intégrée :

* Les administrateurs d’identité ont tooindividually créer et mettre à jour des comptes d’utilisateur dans toutes les applications séparément, une activité redondant et beaucoup de temps.
* Les utilisateurs ont des applications hello tooaccess plusieurs informations d’identification avec que dont ils ont besoin toowork toomemorize. Par conséquent, les utilisateurs ont tendance à toowrite leurs mots de passe ou utilisent d’autres solutions de gestion de mot de passe qui présente les autres risques de sécurité des données.
* Les activités redondantes, beaucoup de temps réduisent hello temps que les utilisateurs et administrateurs travaillez sur des activités d’entreprise qui augmentent le récapitulatif de votre entreprise.

Alors, de manière générale, qu’est-ce qui empêche les entreprises d’adopter des solutions IAM intégrées ?

* Solutions techniques plus sont basées sur des plateformes logicielles qui doivent toobe déployé et adaptée à chaque organisation pour leurs propres applications.
* Les applications cloud sont souvent adoptées à une fréquence plus élevée que la capacité des services informatiques à intégrer des solutions IAM existantes.
* Sécurité et les outils d’analyse requièrent personnalisation et l’intégration tooachieve complète E2E des scénarios supplémentaires.

## <a name="azure-active-directory-integrated-with-applications"></a>Azure Active Directory intégré à des applications
Azure Active Directory est une solution Microsoft de type IDaaS (Identity as a Service) qui :

* active IAM en tant que service cloud ; 
* assure la centralisation de la gestion de l’accès, l’authentification unique et le compte-rendu ; 
* Prend en charge la gestion des accès intégré pour [des milliers d’applications](https://azure.microsoft.com/marketplace/active-directory/) dans la galerie d’applications hello, notamment Salesforce, Google Apps, Box, Concur et bien plus encore. 

Avec Azure Active Directory, toutes les applications que vous publiez pour vos partenaires et les clients (professionnels et particuliers) ont hello mêmes fonctions de gestion des identités et des accès.<br> Cela permet de vous toosignificantly réduire les coûts d’exploitation.

Que se passe-t-il si vous avez besoin de tooimplement une application qui ne figure pas encore dans la galerie d’applications hello ? Bien que cela soit un peu plus long que la configuration de l’authentification unique pour les applications à partir de la galerie d’applications hello, Azure AD vous fournit un Assistant qui vous aide à la configuration de hello.

valeur Hello d’Azure AD va au-delà de « juste » les applications cloud. La solution s’utilise également avec des applications locales, pour lesquelles elle procure un accès sécurisé à distance. Accès à distance sécurisé, vous pouvez éliminer la nécessité de hello de hello pour les réseaux privés virtuels ou d’autres implémentations de gestion de l’accès à distance traditionnel.

En fournissant l’authentification unique (SSO) et gestion d’accès centralisée pour toutes vos applications, Azure AD fournit des solutions de hello problèmes de sécurité et la productivité de données principale toohello.

* Les utilisateurs peuvent accéder à plusieurs applications avec une seule connexion donnant plus temps tooincome génération ou d’entreprise activités d’opérations effectuées.
* Les administrateurs d’identité peuvent gérer tooapplications d’accès dans un seul emplacement.

avantage Hello pour hello utilisateur et votre société est évident. Examinons une présentation avantages hello pour une organisation de hello et un administrateur d’identité.

## <a name="integrated-application-benefits"></a>Avantages des applications intégrées
Hello processus d’authentification unique comporte deux étapes :

* Authentification, hello processus de validation de l’identité de l’utilisateur hello.
* Autorisation, hello tooenable de décision ou bloquer l’accès des ressources de tooa avec une stratégie d’accès.

Lorsque vous utilisez des applications de toomanage Azure AD et activer l’authentification unique :

* L’authentification est effectuée sur l’utilisateur hello (par exemple, AD) local ou compte Azure AD.
* L’autorisation s’exécute sur hello Azure AD d’affectation et de protection stratégie garantissant l’expérience utilisateur cohérente et l’activation d’attribution de tooadd, des emplacements et des conditions de l’authentification Multifacteur sur n’importe quelle application, indépendamment de ses fonctionnalités internes.

Il est important de toounderstand qui hello d’autorisation de façon hello est activé dans l’application cible hello varie en fonction de la manière dont l’application hello a été intégrée avec Azure AD.

* **Applications préintégrées par le fournisseur de services** À l’instar d’Office 365 et d’Azure, ce sont des applications directement intégrées sur Azure AD et dépendantes pour l’intégralité de leurs fonctionnalités de gestion de l’identité et de l’accès. Applications d’accès aux toothese est activée par le biais d’émission de jeton et les informations Active.
* **Applications préintégrées par Microsoft et applications personnalisées** Ce sont des applications cloud indépendantes qui s’appuient sur un répertoire d’applications internes et peuvent fonctionner indépendamment d’Azure AD. Applications d’accès aux toothese est activée par l’émission d’un compte d’application tooan application des informations d’identification spécifiques mappé. Selon les fonctionnalités d’application hello, les informations d’identification de hello peuvent être un jeton de fédération ou le nom d’utilisateur et le mot de passe d’un compte qui a été configuré précédemment dans l’application hello.
* **Applications locales** les Applications publiées via le proxy d’application hello Azure AD principalement permettant aux applications de tooon local d’accès. Ces applications reposent sur un répertoire local central comme Windows Server Active Directory. Applications d’accès aux toothese est activé en déclenchant l’utilisateur final toohello contenu de l’application hello proxy toodeliver hello tout en honorant les exigence de l’authentification locale hello.

Par exemple, si un utilisateur joint à votre organisation, vous devez toocreate un compte d’utilisateur de hello dans Azure AD pour les opérations d’authentification principales de l’hello. Si cet utilisateur requiert une application tooa géré d’accès telles que Salesforce, vous également besoin toocreate un compte pour cet utilisateur dans Salesforce et liez le travail de l’authentification unique toomake toohello compte Azure. Lorsque l’utilisateur de hello quitte votre organisation, il est conseillé de toodelete hello compte Azure AD et tous les comptes d’homologue hello magasins IAM d’applications hello hello utilisateur ait accès au.

## <a name="access-detection"></a>Détection de l’accès
Dans les entreprises modernes, les services informatiques sont souvent pas conscients de toutes les applications cloud hello sont utilisées. Conjointement avec Cloud App Discovery, Azure AD vous offre une solution toodetect ces applications.

## <a name="account-management"></a>Account Management
En règle générale, la gestion des comptes dans hello diverses applications est un processus manuel effectué par informatique ou prend en charge personnels dans l’organisation de hello. Azure AD a entièrement automatisé la gestion des comptes dans toutes les applications intégrées de fournisseur de services, ainsi que les applications préintégrées par Microsoft prenant en charge l’approvisionnement automatique des utilisateurs ou SAML JIT.

## <a name="automated-user-provisioning"></a>Approvisionnement automatique des utilisateurs
Certaines applications fournissent des interfaces d’automatisation pour la création et la suppression (ou la désactivation) de comptes. Si un fournisseur offre une interface de ce type, elle est exploitée par Azure AD. Cela réduit les coûts d’exploitation, car les tâches d’administration s’exécutent automatiquement et améliore la sécurité de hello de votre environnement, car elle diminue le risque de hello d’accès non autorisé.

## <a name="access-management"></a>gestion de l’accès
À l’aide d’Azure AD vous pouvez gérer les accès tooapplications à l’aide des ou la règle pilotée par les affectations. Vous pouvez également déléguer accès gestion toohello aux personnes dans hello organisation assurant hello meilleures supervision et réduction charge hello sur le support technique.

## <a name="on-premises-applications"></a>Applications locales
Hello généré dans le proxy d’application vous permet de toopublish votre local applications tooyour résultant à la fois cohérente dans accès au expérience avec les avantages hello et les applications cloud modernes depuis Azure AD d’analyse, des rapports et des fonctionnalités de sécurité .

## <a name="reporting-and-monitoring"></a>Création de rapports et surveillance
Azure AD vous offre de création de rapports déjà intégrée et la surveillance des fonctionnalités qui vous permettent de tooknow qui a accès tooapplications et lorsqu’elles ont réellement utilisées les.

## <a name="related-capabilities"></a>Fonctionnalités associées
Avec Azure AD, vous pouvez sécuriser vos applications avec des stratégies d’accès précises et la MFA préintégrée. toolearn d’informations sur l’authentification Multifacteur Azure, consultez [Azure MFA](https://azure.microsoft.com/services/multi-factor-authentication/).

## <a name="getting-started"></a>Prise en main
tooget étape de l’intégration des applications avec Azure AD, examinons hello [Guide d’intégration d’Azure Active Directory avec les applications de mise en route](active-directory-integrating-applications-getting-started.md).

## <a name="see-also"></a>Voir aussi
[Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)

