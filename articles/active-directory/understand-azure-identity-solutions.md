---
title: "aaaUnderstand identité Azure | Documents Microsoft"
description: "Obtenir une compréhension de base de termes de solution d’identité Microsoft Azure, les concepts et les recommandations pour vous toomake hello meilleure identité gouvernance décision pour votre organisation."
keywords: 
author: jeffgilb
manager: femila
ms.reviewer: jsnow
ms.author: jeffgilb
ms.date: 7/17/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: 4d9c90bd7a6bcc9637be3107998f9da5bd4cbdae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-identity-solutions"></a>Comprendre les solutions d’identité Azure
Microsoft Azure Active Directory (Azure AD) est une solution cloud de gestion des identités et des accès qui associe des services d’annuaire, une gouvernance des identités et la gestion de l’accès aux applications. Azure AD rapidement [permet l’authentification unique (SSO)](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-sso) too1, les applications commerciales et personnalisées pré-intégrées Bonjour 000 [Galerie d’applications Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/). Vous utilisez probablement déjà bon nombre de ces applications : Office 365, Salesforce.com, Box, ServiceNow et Workday.

Un annuaire Azure AD est automatiquement associé à un abonnement Azure lors de la création de celui-ci. En tant que service d’identité hello dans Azure, Azure AD puis fournit tous les gestion des identités et des fonctions de contrôle d’accès pour les ressources de cloud. Ces ressources peuvent inclure des utilisateurs, des applications et des groupes pour un locataire (organisation) comme indiqué dans hello suivant schéma :

![Azure Active Directory](./media/understand-azure-identity-solutions/azure-ad.png)

Microsoft Azure offre plusieurs identités tooleverage de méthodes en tant que service (IDaaS) avec différents niveaux de complexité toomeet des besoins de votre organisation. reste Hello de cet article vous aide à comprendre la terminologie de base Azure identity et concepts ainsi que des recommandations pour vous toomake hello meilleur choix parmi les options disponibles hello.

## <a name="terms-tooknow"></a>Termes du contrat tooknow

Avant de décider sur une solution d’identité Azure pour votre organisation, vous devez comprendre les termes du contrat de hello couramment utilisés lors de la distinction entre les services d’identité Azure.

|Terme tooknow| Description|
|-----|-----|
|Abonnement Azure |Les abonnements sont toopay utilisé pour les services cloud Azure et carte de crédit tooa généralement lié. Vous pouvez avoir plusieurs abonnements, mais il peut être difficile de tooshare des ressources entre les abonnements.|
|Client Azure | Un client Azure AD représente une organisation. Il s’agit d’une instance dédiée et approuvée d’Azure AD automatiquement créée quand une organisation souscrit un abonnement à un service Microsoft Cloud tel qu’Azure, Microsoft Intune ou Office 365. Les clients peuvent obtenir un tooservices d’accès dans un environnement dédié (un seul locataire) ou dans un environnement partagé avec d’autres organisations (plusieurs locataires).|
|Annuaire Azure AD | Chaque locataire Azure possède un Azure dédié, approuvé annuaire AD qui contient des utilisateurs, des groupes et des applications du locataire hello. Il s’agit des fonctions de gestion des identités et des accès tooperform utilisés pour les ressources du client. Étant donné qu’unique Windows Azure AD est automatiquement configuré toorepresent votre organisation lorsque vous vous inscrivez pour un service de cloud de Microsoft Azure, Microsoft Intune ou Office 365, parfois termes s’affichent, hello *client*, *Azure AD*, et *annuaire Azure AD* de manière interchangeable. |
|Domaine personnalisé | Lorsque vous souscrivez pour la première fois un abonnement à un service Microsoft Cloud, votre client (ou organisation) utilise un nom de domaine *.onmicrosoft.com*. Toutefois, la plupart des organisations ont un ou plusieurs noms de domaine sont utilisés toodo entreprise et que les utilisateurs finaux utilisent des ressources de l’entreprise tooaccess. Vous pouvez ajouter votre tooAzure de nom de domaine personnalisé AD afin que hello nom de domaine est familier tooyour utilisateurs, tel que  *alice@contoso.com*  au lieu de  *alice@contoso.onmicrosoft.com* . |
|Compte Azure AD | Il s’agit d’identités créées à l’aide d’Azure AD ou d’un autre service Microsoft Cloud tel qu’Office 365. Ils sont stockés dans Azure AD et accessible tooany des abonnements de service de cloud de l’organisation hello. |
|Administrateur d’abonnement Azure| administrateur de compte Hello est hello personne inscrit ou acheté hello abonnement Azure. Ils peuvent utiliser hello [centre des comptes](https://account.windowsazure.com/Home/Index) tooperform diverses tâches de gestion telles que créer des abonnements, annuler les abonnements, remplacer la facturation hello pour un abonnement ou modifier hello administrateur de Service. |
|Administrateur général Azure AD | Un administrateur Global Azure AD ont des fonctionnalités d’administration de l’accès complet tooall Azure AD. personne Hello qui s’inscrit automatiquement pour un abonnement au service cloud Microsoft devient un administrateur global par défaut. Vous pouvez avoir plusieurs administrateurs globaux, mais seuls les administrateurs généraux peuvent affecter l’un des [hello d’autres rôles d’administrateur](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) toousers. |
|Compte Microsoft | Les comptes Microsoft (créées par vous pour une utilisation personnelle) fournissent des produits Microsoft access tooconsumer et cloud services, tels que Outlook (Hotmail), OneDrive, Xbox LIVE ou Office 365. Ces identités sont créées et stockées dans hello Microsoft consommateur identité du compte système par Microsoft.|
|Comptes professionnels ou scolaires | Les comptes professionnels ou scolaires (émis par un administrateur pour une utilisation de l’entreprise/éducation) fournissent un accès tooenterprise au niveau de l’entreprise Microsoft cloud services, comme Office 365, Intune ou Azure.|


## <a name="concepts-toounderstand"></a>Concepts toounderstand

Maintenant que vous connaissez les termes du contrat de base identité Azure hello, vous devez plus d’informations sur ces concepts d’identité Azure qui vous aident à prendre une décision de service d’identité Azure informé.

|Concept toounderstand |Description|
|-----|-----|
|[Association des abonnements Azure avec Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-how-subscriptions-associated-directory) |Chaque abonnement Azure a une relation d’approbation avec Azure AD tooauthenticate utilisateurs, services et Active les appareils. *Répertoire de hello même instance Azure AD peuvent faire confiance à plusieurs abonnements, mais un abonnement ne fait confiance à un seul annuaire Azure AD*. Cette relation d’approbation diffère de la relation hello ayant un abonnement avec d’autres ressources Azure (sites Web, bases de données et ainsi de suite), qui sont apparentent à des ressources enfants d’un abonnement. Si un abonnement expire, tooresources d’accès associés à abonnement hello autres que Azure AD arrête également. Toutefois, répertoire de hello Azure AD reste dans Azure, afin que vous pouvez associer un autre abonnement à ce répertoire et continuer toomanage ressources du client.|
|[Comment fonctionne la gestion des licences Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-licensing-get-started-azure-portal) | Lorsque vous achetez ou activez Enterprise Mobility Suite, Azure AD Premium ou Azure AD Basic, votre annuaire est mis à jour avec abonnement hello, y compris sa période de validité et prépayé des licences. Une fois l’abonnement de hello est actif, service de hello peut être géré par un administrateur global Azure AD et utilisé par les utilisateurs sous licence. Vos informations d’abonnement, y compris nombre hello de licences attribuées ou disponibles, sont disponibles dans hello portail Azure à partir de hello **Azure Active Directory** > **licences** panneau. Cela est également hello meilleures place toomanage les affectations de licence.|
|[Contrôle d’accès en fonction du rôle Bonjour portail Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is)|La fonctionnalité de contrôle d’accès en fonction du rôle (RBAC) Azure permet de gérer avec précision l’accès aux ressources Azure. Trop d’autorisations peuvent exposer et tooattackers de compte. Si le nombre d’autorisations est trop faible, les employés ne peuvent pas effectuer leur travail efficacement. À l’aide de RBAC, vous pouvez donner aux employés hello autorisations exactes dont ils ont besoin en fonction de trois rôles de base qui s’appliquent à des groupes de ressources tooall : propriétaire, collaborateur, lecteur. Vous pouvez également créer des too2, 000 vos propres [des rôles personnalisés RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles) a besoin de vos toomeet. |
|[Identité hybride](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)|Vous obtenez une identité hybride en intégrant votre Windows Server Active Directory (AD DS) local avec Azure AD à l’aide d’[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect). Cela vous permet de tooprovide une identité commune pour vos utilisateurs pour Office 365, Azure et les applications locales ou les applications SaaS intégrée à Azure AD. Identité hybride, vous efficacement étendez votre service cloud de toohello d’environnement pour l’accès et d’identité.|

### <a name="hello-difference-between-windows-server-ad-ds-and-azure-ad"></a>différence Hello entre Windows Server AD DS et Azure AD
Azure Active Directory (Azure AD) et Active Directory local (Active Directory Domain Services ou AD DS) sont tous deux des systèmes qui stockent des données d’annuaire et gèrent les communications entre les utilisateurs et les ressources, notamment les processus d’ouverture de session, d’authentification des utilisateurs et de recherche dans l’annuaire.

Si vous êtes déjà familiarisé avec local Windows Server Active Directory domaine Services (AD DS), introduite avec Windows 2000 Server, puis vous comprenez probablement concept de base de hello d’un service d’identité. Toutefois, il est également important toounderstand que Azure AD n’est pas simplement un contrôleur de domaine dans le cloud de hello. Il est une manière entièrement nouvelle de fournir l’identité en tant que service (IDaaS) dans Azure qui requiert une manière entièrement nouvelle de fonctions nuage de réfléchir toofully prise en charge et de protéger votre organisation contre les menaces modernes. 

AD DS est un rôle serveur sur Windows Server, ce qui signifie qu’il peut être déployé sur des ordinateurs physiques ou des machines virtuelles. Il a une structure hiérarchique basée sur X.500. Il utilise le système DNS pour la localisation d’objets, peut être contacté par le biais du protocole LDAP et utilise principalement Kerberos pour l’authentification. Active Directory permet aux unités d’organisation (UO) et les objets de stratégie de groupe (GPO) de plus toojoining machines toohello approbations de domaine et sont créées entre les domaines.

Traditionnellement, les informaticiens protègent leur périmètre de sécurité à l’aide d’AD DS. Toutefois, les entreprises modernes, sans périmètre, qui prennent en charge les besoins d’identité de leurs employés, clients et partenaires nécessitent un nouveau plan de contrôle. Azure AD est ce plan de contrôle des identités. Sécurité a été déplacé au-delà de cloud computing toohello hello pare-feu d’entreprise où Azure AD protège les ressources de l’entreprise et l’accès en fournissant une identité commune pour les utilisateurs (localement ou dans le cloud de hello). Cela donne à votre toosecurely de souplesse aux utilisateurs hello accès hello les applications que dont ils ont besoin tooget leur travail à partir de presque n’importe quel appareil. Transparente des données en fonction des risques protection contrôles, soutenues par les fonctionnalités de l’apprentissage automatique et les rapports approfondie, sont également fournies cette société tookeep de besoins informatiques sécuriser les données.

Azure AD est un service d’annuaire public multiclient, ce qui signifie que vous pouvez créer un locataire pour vos applications comme Office 365 et vos serveurs cloud dans Azure AD. Les utilisateurs et les groupes sont créés selon une structure plate sans unités d’organisation ou objets de stratégie de groupe. L’authentification s’effectue suivant des protocoles tels que SAML, WS-Federation et OAuth. Il est possible de tooquery Azure AD, mais au lieu d’utiliser LDAP, vous devez utiliser une API REST appelée API AD Graph. Toutes fonctionnent sur HTTP et HTTPS.

### <a name="extend-office-365-management-and-security-capabilities"></a>Étendre les fonctionnalités de gestion et de sécurité d’Office 365
Vous utilisez déjà Office 365 ? Vous pouvez accélérer votre transformation numérique en étendant les fonctionnalités d’Office 365 intégrées avec Azure AD toosecure toutes vos ressources, l’activation de la productivité sécurisée pour votre personnel entière. Lorsque vous utilisez Azure AD, en outre les fonctionnalités de tooOffice 365, vous pouvez sécuriser votre portefeuille d’applications avec une identité qui permet l’authentification unique pour toutes les applications. Vous pouvez étendre vos capacités d’accès conditionnel en fonction, non seulement de l’état de l’appareil, mais aussi de l’utilisateur, de l’emplacement, de l’application et du risque. Les fonctionnalités d’authentification multifacteur (Multi-Factor Authentication, MFA) offrent davantage de protection lorsque vous en avez besoin. Vous allez bénéficier d’un meilleur contrôle des privilèges d’utilisateur et de la possibilité de fournir un accès administratif juste-à-temps à la demande. Vos utilisateurs seront plus productifs et créer des tickets de support technique moins, fonctionnalités de libre-service toohello Merci Azure AD fournit comme la réinitialisation des mots de passe oubliés, des demandes d’accès application et la création et la gestion des groupes.

> [!TIP]
> Vous souhaitez toolearn plus d’informations sur l’utilisation de la gestion des identités Azure AD avec Office 365 ? [Obtenir les livres hello](https://info.microsoft.com/Extend-Office-365-security-with-EMS.html).

## <a name="microsoft-azure-identity-solutions"></a>Solutions Microsoft Azure pour le contrôle des identités

Microsoft Azure offre plusieurs façons toomanage les identités des utilisateurs si elles sont gérées entièrement en local, uniquement dans hello cloud, ou même quelque part entre les deux. Ces options sont les suivantes : AD DS à configurer en libre service dans Azure, Azure Active Directory (Azure AD), identité hybride et Azure AD Domain Services.

### <a name="do-it-yourself-diy-ad-ds"></a>AD DS à configurer en libre service
Pour les entreprises qui doivent uniquement un faible encombrement mémoire dans le cloud de hello, **personnalisables (soi-même) les services AD DS** dans Azure peut être utilisé. Cette option prend en charge de nombreux scénarios de Windows Server AD DS bien adaptés au déploiement de machines virtuelles sur Azure. Par exemple, vous pouvez créer une machine virtuelle Azure en tant qu’un contrôleur de domaine en cours d’exécution dans un centre de données qui habitent loin est réseau distant de toohello connecté. À partir de là, hello VM serait être en mesure de toosupport les demandes d’authentification des utilisateurs distants et améliorer les performances de l’authentification. Cette option convient également comme un sites de récupération d’urgence coûteux toootherwise relativement faible coût de substitution en hébergeant un petit nombre de contrôleurs de domaine et un seul réseau virtuel sur Azure. Enfin, vous deviez toodeploy une application sur Azure, tels que SharePoint, ce qui nécessite Windows Server AD DS, mais n’a aucune dépendance sur le réseau local de hello ou hello d’entreprise Windows Server Active Directory. Dans ce cas, vous pouvez déployer une forêt isolée sur les exigences d’Azure toomeet hello SharePoint batterie de serveurs. Il a également pris en charge les applications réseau toodeploy ne nécessitant pas de réseau local de toohello connectivité hello locales et dans Active Directory.

### <a name="azure-active-directory-azure-ad"></a>Azure Active Directory (Azure AD)
Une **instance Azure AD autonome** est solution de gestion des accès et des identités en tant que service (IDaaS) entièrement basée sur le cloud. Azure AD vous offre un ensemble robuste de fonctionnalités toomanage utilisateurs et groupes. Il permet de sécuriser l’accès tooon local et cloud d’applications, y compris les services web de Microsoft comme Office 365 et de nombreux éditeurs de logiciels non Microsoft comme une application de service (SaaS). Azure AD est proposé en 3 versions : Gratuite, De base et Premium. Azure AD améliore l’efficacité organisationnelle et étend la sécurité au-delà de hello périmètre pare-feu tooa nouveau plan de contrôle protégée par Azure machine learning et d’autre fonctionnalités de sécurité avancée.

### <a name="hybrid-identity"></a>Identité hybride
Plutôt que choisir entre les solutions d’identité basé sur le cloud ou locaux, nombreux avance directeurs informatiques et les entreprises, qui ont commencé à anticiper les tendances à long terme de l’entreprise, sont étendre leurs locaux cloud toohello de répertoires via **identité hybride** solutions. Avec l’identité hybride, vous obtenez une identité globale réellement, et solution de gestion d’accès qui fournit un accès sécurisé et productif toohello utilisateurs d’applications doivent toodo leur travail.

> [!TIP]
> toolearn en savoir plus sur comment directeurs apportées à Azure Active Directory la partie centrale de leurs stratégies informatiques, téléchargez hello [tooAzure de Guide de responsables informatiques Active Directory](https://aka.ms/AzureADCIOGuide).

### <a name="azure-ad-domain-services"></a>Services de domaine Azure AD
**Les Services de domaine Active Directory Azure** fournit une option basée sur le cloud de toouse AD DS pour le contrôle de configuration de machine virtuelle Azure léger et un toomeet de façon exigences d’identité locale pour le développement d’applications de réseau et de test. Les Services de domaine Active Directory Azure toolift n’est pas conçu et déplacer votre site AD DS infrastructure tooAzure ordinateurs virtuels gérés par les Services de domaine Active Directory de Azure. Au lieu de cela, hello machines virtuelles Azure dans les domaines gérés doit être utilisé toosupport hello développement, le test et le déplacement des applications sur site qui nécessitent les services AD DS authentification méthodes toohello cloud.

## <a name="common-scenarios-and-recommendations"></a>Scénarios et recommandations courants

Voici quelques scénarios courants d’identité et accès avec les recommandations comme toowhich option identité Azure peut être plus approprié pour chaque.

|Scénario d’identité| Recommandation|
|-----|-----|
|Mon organisation a investi volumineux dans Active Directory sur site Windows Server, mais nous voulons cloud de toohello tooextend identité.| solution d’identité Azure Hello plus largement utilisé est [identité hybride](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview). Si vous avez déjà effectué des investissements localement les services AD DS, vous pouvez facilement étendre le cloud de toohello d’identité à l’aide d’Azure AD Connect.|
|Mon entreprise est né en cloud de hello et nous n’avons aucune investissements dans les solutions d’identité locale.| [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) hello meilleur choix pour les entreprises de cloud uniquement sans aucune local investissements.|
|J’ai nécessitent léger Azure VM configuration et contrôle toomeet local identité pour le développement d’applications et les tests.|[Les Services de domaine Active Directory Azure](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-overview) est un bon choix si vous devez toouse les services AD DS pour le contrôle de configuration de machine virtuelle Azure léger ou cherchez toodevelop ou migrez hérité, répertoire prenant en charge les applications toohello cloud local.|  
|J’ai besoin toosupport quelques machines virtuelles dans Azure, mais mon entreprise est toujours beaucoup investi dans locale Active Directory (AD DS).|Utilisez [sur AD DS](https://msdn.microsoft.com/library/azure/jj156090.aspx) toouse machines virtuelles de Azure quand vous devez toosupport quelques machines virtuelles et que vous avez volumineux AD DS investissements locaux. |

## <a name="where-can-i-learn-more"></a>Où en savoir plus ?
Nous avons énormément de ressources de toohelp en ligne que vous tout savoir sur Azure AD. Voici une liste de tooget des articles commencer :

* [Activation de votre annuaire pour la gestion hybride avec Azure AD Connect](active-directory-aadconnect.md)
* [Sécurité supplémentaire pour un monde toujours connecté](../multi-factor-authentication/multi-factor-authentication.md)
* [Automatiser la configuration de l’utilisateur et Deprovisioning tooSaaS Applications avec Azure Active Directory](active-directory-saas-app-provisioning.md)
* [Prise en main de la création de rapports Azure AD](active-directory-reporting-getting-started.md)
* [Gestion de vos mots de passe en tout lieu](active-directory-passwords.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
* [Automatiser la configuration de l’utilisateur et Deprovisioning tooSaaS Applications avec Azure Active Directory](active-directory-saas-app-provisioning.md)
* [Comment tooprovide sécuriser l’accès à distance des applications tooon-site](active-directory-application-proxy-get-started.md)
* [La gestion des accès tooresources avec les groupes Azure Active Directory](active-directory-manage-groups.md)
* [Qu’est-ce que la gestion des licences Microsoft Azure Active Directory ?](active-directory-licensing-what-is.md)
* [Comment puis-je détecter les applications cloud non approuvées utilisées au sein de mon organisation ?](active-directory-cloudappdiscovery-whatis.md)

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous comprenez les concepts d’identité Azure et tooyou de hello options disponibles, vous pouvez utiliser hello suivant option hello implémentation tooget démarré les ressources que vous avez choisie :

[En savoir plus sur les solutions d’identité hybride Azure](https://docs.microsoft.com/azure/active-directory/choose-hybrid-identity-solution)

[En apprendre davantage dans un environnement de preuve de concept Azure](https://aka.ms/aad-poc)

[Déployer Azure AD en production](https://aka.ms/aad-onboard)
