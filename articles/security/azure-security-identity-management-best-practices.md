---
title: "aaaAzure identités et des accès meilleures pratiques de sécurité | Documents Microsoft"
description: "Cet article détaille un ensemble de meilleures pratiques en matière de gestion des identités et du contrôle d’accès à l’aide de fonctionnalités Azure intégrées."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 07d8e8a8-47e8-447c-9c06-3a88d2713bc1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/30/2017
ms.author: yurid
ms.openlocfilehash: af07dfda84758b9124641078ac8f696f725f2bf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-identity-management-and-access-control-security-best-practices"></a>Meilleures pratiques en matière de sécurité du contrôle d’accès et de la gestion des identités Azure
Nombreux envisagez toobe hello nouvelle limite couche d’identité pour la sécurité, la prise en charge ce rôle à partir du point de vue centré sur le réseau traditionnel hello. Cette évolution de pivot principal de hello pour attention de sécurité et les investissements proviennent de faits hello que réseau est désormais plus poreux et la défense de périmètre ne peut pas être aussi efficace qu’une seule fois explosion toohello préalable de [BYOD](http://aka.ms/byodcg) périphériques et des applications de cloud.

Dans cet article, nous allons étudier une collection de meilleures pratiques en matière de sécurité du contrôle d’accès et de la gestion des identités Azure. Ces recommandations sont dérivées de notre expérience avec [AD Azure](../active-directory/active-directory-whatis.md) et les expériences hello de clients telles que vous-même.

Pour chaque meilleure pratique, nous allons détailler les éléments suivants :

* Les meilleures pratiques de hello est
* Raison pour laquelle vous souhaitez tooenable que les meilleures pratiques
* Ce que peut être le résultat de hello si vous ne parvenez pas la meilleure pratique de tooenable hello
* Meilleure pratique de toohello alternatives possibles
* Comment vous pouvez apprendre tooenable hello il est recommandé

Cette gestion des identités d’Azure et contrôle d’accès de sécurité article sur les meilleures pratiques est basé sur un avis de consensus et les fonctionnalités de la plateforme Azure et les ensembles de fonctionnalités, tels qu’ils existent au moment de hello que cet article a été écrit. Avis et les technologies changent au fil du temps et de cet article sera mis à jour sur un tooreflect régulièrement ces modifications.

Dans cet article, nous allons étudier les points suivants :

* Centralisation de la gestion de votre identité
* Activation de l’authentification unique (SSO)
* Déploiement de la gestion des mots de passe
* Application de l’authentification multifacteur (MFA) pour les utilisateurs
* Utilisation du contrôle d’accès en fonction du rôle (RBAC)
* Contrôle des emplacements de création des ressources à l’aide du gestionnaire de ressources
* Guide des fonctionnalités d’identification tooleverage aux développeurs d’applications SaaS
* Surveillance active des activités suspectes

## <a name="centralize-your-identity-management"></a>Centralisation de la gestion de votre identité
Une étape importante vers la sécurisation de votre identité est tooensure qu’il peut gérer des comptes à partir d’un emplacement unique concernant où ce compte a été créé. Alors que la majorité de hello des entreprises de hello organisations informatiques ont leur compte principal répertoire local, les déploiements de cloud hybride se trouvent sur le lieu de hello et il est important de comprendre comment toointegrate local et cloud répertoires et de fournir un expérience transparente toohello l’utilisateur final.

tooaccomplish cela [identité hybride](../active-directory/active-directory-hybrid-identity-design-considerations-overview.md) scénario nous vous recommandons de deux options :

* Synchronisation de votre annuaire local avec votre annuaire de cloud à l’aide d’Azure AD Connect
* Fédération de votre identité en local avec votre annuaire de cloud à l’aide des [Services ADFS](https://msdn.microsoft.com/library/bb897402.aspx)

Les organisations qui échouent toointegrate que leur identité locale avec leur identité cloud feront augmenté d’administration surcharge dans la gestion des comptes, ce qui augmente la probabilité de hello d’erreurs et des failles de sécurité.

Pour plus d’informations sur la synchronisation AD Azure, lisez l’article de hello [intégrer vos identités locales avec Azure Active Directory](../active-directory/active-directory-aadconnect.md).

## <a name="enable-single-sign-on-sso"></a>Activation de l’authentification unique (SSO)
Lorsque vous avez plusieurs répertoires toomanage, cela devient un problème d’administration non seulement pour l’informatique, mais également pour les utilisateurs finaux qui ont tooremember plusieurs mots de passe. À l’aide de [SSO](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) vous permet de fournir vos utilisateurs possibilité hello Hello utilisez même ensemble d’informations d’identification dans toosign et accéder aux ressources hello dont ils ont besoin, peu importe où cette ressource est située localement ou dans le cloud de hello.

Utiliser l’authentification unique tooenable utilisateurs tooaccess leurs [applications SaaS](../active-directory/active-directory-appssoaccess-whatis.md) selon leur compte professionnel dans Azure AD. Ceci s’applique non seulement aux applications SaaS de Microsoft, mais également à d’autres applications, telles que [Google Apps](../active-directory/active-directory-saas-google-apps-tutorial.md) et [Salesforce](../active-directory/active-directory-saas-salesforce-tutorial.md). Votre application peut être configurée toouse Azure AD en tant qu’un [identité basé sur SAML](../active-directory/fundamentals-identity.md) fournisseur. Comme un contrôle de sécurité, Azure AD n’émettra pas un jeton qui permet de les toosign dans l’application hello, sauf si elles ont été accordés l’accès à l’aide d’Azure AD. Les utilisateurs peuvent accorder un accès direct ou via un groupe dont ils sont membres.

> [!NOTE]
> la décision de Hello toouse SSO aura un impact sur comment vous intégrez votre annuaire local avec votre annuaire du cloud. Si vous souhaitez que l’authentification unique, vous devez toouse federation, car la synchronisation d’annuaires fournissons [même expérience d’authentification](../active-directory/active-directory-aadconnect.md).
>
>

Les organisations qui n’appliquent pas l’authentification unique pour les utilisateurs et les applications sont plus exposés tooscenarios où les utilisateurs ont plusieurs mots de passe qui augmente la probabilité de hello d’utilisateurs réutilisation des mots de passe ou à l’aide de mots de passe faibles directement.

Vous pouvez en savoir plus sur Azure AD SSO en lisant l’article de hello [gestion AD FS et personnalisation avec Azure AD Connect](../active-directory/active-directory-aadconnect-federation-management.md).

## <a name="deploy-password-management"></a>Déploiement de la gestion des mots de passe
Dans les scénarios où vous avez plusieurs clients ou vous souhaitez que les utilisateurs de tooenable trop[réinitialiser leur mot de passe](../active-directory/active-directory-passwords-update-your-own-password.md), il est important que vous utilisiez un abus tooprevent de stratégies de sécurité approprié. Dans Azure, vous pouvez exploiter les fonctionnalités de réinitialisation de mot de passe libre-service hello et personnaliser hello sécurité options toomeet besoins de votre entreprise.

Il est particulièrement important tooobtain des commentaires à partir de ces utilisateurs et obtenir des informations à partir de leurs expériences qu’elles tentent de tooperform ces étapes. En fonction de ces expériences, élaborer un plan toomitigate des problèmes potentiels qui peuvent se produire lors du déploiement de hello pour un groupe. Il est également recommandé d’utiliser hello [rapport activité de l’inscription de réinitialisation de mot de passe](../active-directory/active-directory-passwords-get-insights.md) utilisateurs hello toomonitor que l’inscription.

Aux organisations désireuses de mot de passe tooavoid modifier les appels au support technique mais qui n’activent pas les utilisateurs tooreset leurs propres mots de passe sont plus susceptibles d’être tooa plu appel volume toohello service d’assistance en raison de problèmes de toopassword. Dans les organisations qui ont plusieurs clients, il est impératif que vous implémentez ce type de fonctionnalité et activez les utilisateurs tooperform mot de passe réinitialisé dans les limites de sécurité qui ont été établies dans la stratégie de sécurité hello.

Vous en apprendrez davantage sur mot de passe réinitialisé, lisez l’article de hello [déploiement de la gestion de mots de passe et formation utilisateurs toouse il](../active-directory/active-directory-passwords-best-practices.md).

## <a name="enforce-multi-factor-authentication-mfa-for-users"></a>Application de l’authentification multifacteur (MFA) pour les utilisateurs
Pour les organisations qui souhaitent utiliser toobe conforme aux normes du secteur, tel que [PCI DSS version 3.2](http://blog.pcisecuritystandards.org/preparing-for-pci-dss-32), l’authentification multifacteur est indispensable dotées de la fonction pour authentifier les utilisateurs. Au-delà de la conformité aux normes du secteur, en appliquant les utilisateurs de l’authentification Multifacteur tooauthenticate permet également de type de vol d’informations d’identification organisations toomitigate d’attaque, tel que [Pass-the-Hash (PtH)](http://aka.ms/PtHPaper).

En activant l’authentification Multifacteur Azure pour vos utilisateurs, vous ajoutez une deuxième couche de sécurité toouser connexions et transactions. Dans ce cas, une transaction peut accéder à un document situé sur un serveur de fichiers ou sur votre site SharePoint Online. L’authentification Multifacteur Azure permet également la probabilité de hello tooreduce informatique que les informations d’identification compromises aura les données d’accès tooorganization.

Par exemple : mettre en œuvre l’authentification Multifacteur Azure pour vos utilisateurs et de configurer toouse un appel téléphonique ou un message texte en tant que la vérification. Si les informations d’identification de l’utilisateur hello sont compromises, les intrus hello ne sera pas être en mesure de tooaccess n’importe quelle ressource, car il n’a pas de téléphone de d’accès toouser. Les organisations qui n’ajoutent pas de couches supplémentaires de protection d’identité sont plus exposées pour une attaque par vol d’informations d’identification, ce qui peut entraîner des toodata compromission.

Une solution destinée aux organisations désireuses de contrôle d’authentification complète tookeep hello locale est toouse [serveur Azure multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-server.md), également appelée authentification Multifacteur localement. À l’aide de cette méthode, vous serez toujours en mesure de tooenforce une authentification multifacteur, tout en conservant l’authentification Multifacteur hello/server sur site.

Pour plus d’informations sur l’authentification Multifacteur Azure, lisez l’article de hello [prise en main d’Azure multi-Factor Authentication dans le cloud de hello](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

## <a name="use-role-based-access-control-rbac"></a>Utilisation du contrôle d’accès en fonction du rôle (RBAC)
Restreindre l’accès basé sur hello [devez tooknow](https://en.wikipedia.org/wiki/Need_to_know) et [moindre privilège](https://en.wikipedia.org/wiki/Principle_of_least_privilege) principes de sécurité est impérative pour les organisations qui souhaitent utiliser les stratégies de sécurité tooenforce pour accéder aux données. Azure contrôle d’accès en fonction du rôle (RBAC) peut être utilisé tooassign autorisations toousers, des groupes et des applications au niveau d’une certaine étendue. Hello portée d’une attribution de rôle peut être un abonnement, un groupe de ressources ou une seule ressource.

Vous pouvez tirer parti de [intégrée RBAC](../active-directory/role-based-access-built-in-roles.md) rôles dans Azure tooassign privilèges toousers. Envisagez d’utiliser *collaborateur de compte de stockage* pour les opérateurs cloud que vous avez besoin de comptes de stockage toomanage et *collaborateur de compte de stockage classique* comptes de stockage classiques toomanage de rôle. Pour les opérateurs cloud nécessitant des machines virtuelles de toomanage et compte de stockage, envisagez de les ajouter trop*contributeur de l’ordinateur virtuel* rôle.

Les organisations qui n’appliquent pas de contrôle d’accès aux données en tirant parti des fonctionnalités telles que RBAC envoie plus de privilèges que les utilisateurs tootheir nécessaire. Cela peut entraîner la compromission de toodata par permettent aux utilisateurs d’accéder toocertain les types des types de données (par exemple, un fort impact commercial) qui ne doivent pas sont en premier lieu de hello.

Vous pouvez en savoir plus sur Azure RBAC en lisant l’article de hello [du contrôle d’accès](../active-directory/role-based-access-control-configure.md).

## <a name="control-locations-where-resources-are-created-using-resource-manager"></a>Contrôle des emplacements de création des ressources à l’aide du gestionnaire de ressources
Il est très important d’activer le cloud opérateurs tooperform tâches pendant que l’empêche de s’arrêter conventions sont nécessaires toomanage ressources de votre organisation. Aux organisations désireuses d’emplacements de hello toocontrol où sont créés les ressources doivent coder en dur ces emplacements.

tooachieve, les organisations peuvent créer des stratégies de sécurité ayant des définitions qui décrivent les actions hello ou des ressources qui sont spécifiquement refusés. Vous affectez ces définitions de stratégie au niveau de portée hello souhaité, telles que l’abonnement de hello, groupe de ressources ou une ressource individuelle.

> [!NOTE]
> Il est de même hello pas comme RBAC, il exploite réellement RBAC tooauthenticate hello utilisateurs qui ont des privilèges toocreate ces ressources.
>
>

Tirer parti de la [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) toocreate des stratégies personnalisées pour les scénarios où les opérations de tooallow hello organisation souhaite uniquement lorsque hello centre de coût approprié est également associé ; sinon, ils ignore hello demande.

Les organisations qui ne sont pas contrôle comment les ressources sont créés sont plus susceptibles d’être toousers qui peut abuser de son service de hello en créant davantage de ressources qu’ils ont besoin. Sécurisation renforcée des processus de création de ressources hello sont une étape importante de toosecure un scénario de l’architecture mutualisé.

Plus d’informations sur la création de stratégies avec Azure Resource Manager en lisant l’article de hello [ressources toomanage de stratégie d’utilisation et de contrôler l’accès](../azure-resource-manager/resource-manager-policy.md).

## <a name="guide-developers-tooleverage-identity-capabilities-for-saas-apps"></a>Guide des fonctionnalités d’identification tooleverage aux développeurs d’applications SaaS
L’identité de l’utilisateur est exploitée dans de nombreux scénarios lorsque les utilisateurs accèdent aux [applications SaaS](https://azure.microsoft.com/marketplace/active-directory/all/) qui peuvent être intégrées à l’annuaire local ou de cloud. Tout d’abord, nous recommandons que les développeurs utilisent un toodevelop sécurisé méthodologie ces applications, comme [du cycle de vie de développement de sécurité Microsoft (SDL)](https://www.microsoft.com/sdl/default.aspx). Azure AD simplifie l’authentification pour les développeurs en fournissant l’identité en tant que service, avec la prise en charge des protocoles standard tels que [OAuth 2.0](http://oauth.net/2/) et [OpenID Connect](http://openid.net/connect/), ainsi que des bibliothèques open source pour différentes plateformes.

Assurez-vous que tooregister une application qui sous-traite l’authentification tooAzure AD, il s’agit d’une procédure obligatoire. Hello derrière cela fait, car Azure AD a besoin de communication de hello toocoordinate avec l’application hello lors de la gestion des sign-on (SSO) ou l’échange de jetons. Hello session utilisateur expire lorsque hello de durée de vie du jeton hello émis par Azure AD expire. Évaluez toujours si votre application doit utiliser cette durée ou si vous pouvez réduire ce temps. Durée de vie hello réduction peut agir comme une mesure de sécurité qui force toosign utilisateurs out basé sur une période d’inactivité.

Les organisations qui n’appliquent pas l’identité contrôler des applications tooaccess ne pas sur guide et leurs développeurs comment toosecurely intégrer des applications de leur système de gestion d’identité peuvent être plus vulnérable type de vol toocredential d’attaque, tel que [faible gestion de l’authentification et de session décrite dans les 10 premiers de Open Web Application sécurité projet (OWASP avoir)](https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet).

Pour en savoir plus sur les scénarios d’authentification pour les applications SaaS, lisez l’article [Scénarios d’authentification pour Azure AD](../active-directory/active-directory-authentication-scenarios.md).

## <a name="actively-monitor-for-suspicious-activities"></a>Surveillance active des activités suspectes
En fonction de trop[rapport de divulgation de données 2016 Verizon](http://www.verizonenterprise.com/verizon-insights-lab/dbir/2016/), compromission des informations d’identification est toujours en hello et de devenir un des entreprises plus rentables de hello pour cybercrime. Pour cette raison, il est important toohave un identité active Moniteur système qui peut rapidement détecter des activités suspectes comportement et déclencher une alerte pour une analyse approfondie. Azure AD dispose de deux fonctions principales qui peuvent aider les organisations à surveiller leurs identités : les [rapports d’anomalies](../active-directory/active-directory-view-access-usage-reports.md) Azure AD Premium et la fonctionnalité de [protection d’identité](../active-directory/active-directory-identityprotection.md) Azure AD.

Assurez-vous que toouse hello rapports d’anomalies tooidentify tentatives toosign dans [sans suivi](../active-directory/active-directory-reporting-sign-ins-from-unknown-sources.md), [en force brute](../active-directory/active-directory-reporting-sign-ins-after-multiple-failures.md) les attaques contre un compte particulier, toosign tentatives dans à partir de plusieurs emplacements, connectez-vous à partir de [infectés appareils](../active-directory/active-directory-reporting-sign-ins-from-possibly-infected-devices.md) et les adresses IP suspectes. N’oubliez pas qu’il s’agit de rapports. En d’autres termes, vous devez les processus et les procédures de placer ces rapports pour toorun des administrateurs informatiques quotidiennement hello ou à la demande (généralement dans un scénario de réponse aux incidents).

En revanche, la protection d’identité Azure AD est un système de surveillance actif et il sera indicateur risques actuels de hello dans son propre tableau de bord. En outre, vous recevrez également des notifications de synthèse quotidiennes par e-mail. Nous vous recommandons de régler le niveau de risque en fonction des besoins de l’entreprise tooyour hello. le niveau de risque Hello pour un événement à risque est une indication (haute, moyenne ou faible) de gravité hello d’événement à risque hello. niveau de risque Hello permet aux utilisateurs de la Protection d’identité hiérarchiser les actions de hello qu’ils doivent prendre organisation de tootheir tooreduce hello risque.

Les organisations qui ne surveillent pas activement leurs systèmes d’identité risquent de compromettre les informations d’identification des utilisateurs. Sans avoir connaissance des activités suspectes sont prenant placer à l’aide de ces informations d’identification, les organisations ne pourra plus être en mesure de toomitigate ce type de menace.
Pour en savoir plus sur la protection d’identité Azure, lisez l’article [Azure Active Directory Identity Protection](../active-directory/active-directory-identityprotection.md) (Protection de l’identité Azure Active Directory).
