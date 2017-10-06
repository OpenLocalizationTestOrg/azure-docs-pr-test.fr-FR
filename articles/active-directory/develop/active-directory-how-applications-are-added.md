---
title: "les applications aaaHow sont ajoutées tooAzure Active Directory."
description: "Cet article décrit comment les applications sont ajoutées instance tooan d’Azure Active Directory."
services: active-directory
documentationcenter: 
author: shoatman
manager: kbrint
editor: 
ms.assetid: 3321d130-f2a8-4e38-b35e-0959693f3576
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/09/2016
ms.author: shoatman
ms.custom: aaddev
ms.openlocfilehash: 3ca710c58a403b52e8b728202ad9010f4873bcea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-and-why-applications-are-added-tooazure-ad"></a>Comment et pourquoi les applications sont ajoutées tooAzure AD
Un des hello initialement doivent choses lors de l’affichage d’une liste d’applications dans votre instance d’Azure Active Directory est de comprendre d'où proviennent les applications hello et pourquoi ils sont il.  Cet article fournit une vue d’ensemble de haut niveau de comment les applications sont représentées dans le répertoire de hello et vous fournissent un contexte qui vous aidera à comprendre comment une application fournie toobe dans votre annuaire.

## <a name="what-services-does-azure-ad-provide-tooapplications"></a>Les services AD Azure assure une tooapplications ?
Les applications sont ajoutées tooAzure AD tooleverage une ou plusieurs des services hello qu’il fournit.  Ces services incluent :

* Authentification et autorisation de l'application
* Authentification et autorisation de l'utilisateur
* Authentification unique (SSO) à l'aide de la fédération ou du mot de passe
* Configuration et synchronisation de l'utilisateur
* Contrôle d’accès basé sur le rôle ; Utilisez hello Active toodefine rôles tooperform les rôles d’application en fonction des vérifications d’autorisation dans une application.
* services d’autorisation oAuth (utilisés par Office 365 et d’autres tooAPIs/ressources Microsoft applications tooauthorize accès).
* Publication d’application & proxy ; Publier une application à partir d’un réseau privé de toohello internet

## <a name="how-are-applications-represented-in-hello-directory"></a>Comment les applications sont représentées dans le répertoire de hello ?
Les applications sont représentées dans hello Azure AD en utilisant 2 objets : un objet application et un objet principal de service.  Il existe un objet de l’application, enregistré dans un « accueil » / répertoire « propriétaire » ou « publication » et un ou plusieurs objets entité de sécurité représentant l’application hello dans chaque répertoire dans lequel il s’agit du service.  

Hello objet d’application décrit hello application tooAzure AD (service d’architecture mutualisée hello) et peut inclure les éléments suivants de hello : (*Remarque*: il n’est pas une liste exhaustive.)

* Nom, logo et publication
* Secrets (les clés symétriques ou asymétriques utilisé tooauthenticate hello application)
* Dépendances d'API (oAuth)
* API/ressources/étendues publiés (oAuth)
* Rôles d'application (RBAC)
* Configuration et métadonnées de l'authentification unique (SSO)
* Configuration et métadonnées du déploiement de l'utilisateur
* Configuration et métadonnées du proxy

principal du service Hello est un enregistrement de l’application hello dans chaque répertoire, où application hello agit notamment de son répertoire de base.  principal du service Hello :

* Fait référence au tooan objet d’application via la propriété d’id application hello
* enregistre les attributions de rôle de l'application de l'utilisateur local et du groupe ;
* Enregistrements utilisateur et administrateur autorisations accordées toohello application locale
  * Par exemple : l’autorisation de hello application tooaccess un par courrier électronique des utilisateurs particuliers
* enregistre les stratégies locales, y compris la stratégie d'accès conditionnel ;
* enregistre les paramètres locaux alternatifs pour une application.
  * Revendication des règles de transformation
  * Mappages d'attributs (déploiement de l'utilisateur)
  * Rôles d’application spécifiques du client (si l’application hello prend en charge des rôles personnalisés)
  * Nom/logo

### <a name="a-diagram-of-application-objects-and-service-principals-across-directories"></a>Diagramme des objets d'application et des principaux de service au sein des répertoires
![Diagramme illustrant la façon dont les objets d'application et les principaux du service existent dans les instances d'Azure AD.][apps_service_principals_directory]

Comme vous pouvez le voir dans le diagramme hello ci-dessus.  Microsoft gère deux annuaires en interne (sur hello gauche), il utilise toopublish applications.

* Une pour Microsoft Apps (répertoire de services Microsoft)
* Une pour des applications tierces pré-intégrées (répertoire de la galerie d'applications)

Serveurs de publication/fournisseurs d’applications qui s’intègrent à Azure AD sont requis toohave un répertoire de publication.  (certains répertoires SAAS).

Les applications que vous ajoutez vous-même comprennent :

* les applications que vous avez développées (intégrées avec AAD) ;
* les applications que vous avez connectées à l'authentification unique ;
* Vous avez publié à l’aide des applications hello proxy d’application Azure AD.

### <a name="a-couple-of-notes-and-exceptions"></a>Quelques remarques et exceptions
* Pas tous les principaux de service point précédent tooapplication objets.  C'est-à-dire que Lorsque Azure AD a été créé à l’origine des services de hello fournis tooapplications ont été beaucoup plus limité et principal du service hello était suffisant pour l’établissement d’une identité de l’application.  principal du service d’origine Hello était plus proche en forme toohello compte de service Windows Server Active Directory.  Pour cette raison, qu'il est toujours possible de toocreate principaux de service à l’aide de hello PowerShell Azure AD sans créer au préalable un objet application.  Hello API Graph nécessite un objet de l’application avant de créer un service principal.
* Toutes les informations de hello décrites ci-dessus est actuellement affiché par programme.  Hello suivantes sont uniquement disponibles dans l’interface utilisateur de hello :
  * Revendication des règles de transformation
  * Mappages d'attributs (déploiement de l'utilisateur)
* Pour plus d’informations détaillées sur les principaux de service hello et objets d’application, consultez la documentation de référence toohello API REST Azure AD Graph.  *Indicateur*: hello documentation de l’API Azure AD Graph est la référence du schéma de tooa chose hello le plus proche pour Azure AD, qui est actuellement disponible.  
  * [Application](https://msdn.microsoft.com/library/azure/dn151677.aspx)
  * [Principal du service](https://msdn.microsoft.com/library/azure/dn194452.aspx)

## <a name="how-are-apps-added-toomy-azure-ad-instance"></a>Comment les applications sont ajoutées toomy instance d’Azure AD ?
Il existe plusieurs façons que tooazure AD peut être ajoutée à une application :

* Ajouter une application à partir de hello [Galerie d’applications Azure Active Directory](https://azure.microsoft.com/updates/azure-active-directory-over-1000-apps/)
* Connexion à une application tierce intégrée à Azure Active Directory (par exemple : [Smartsheet](https://app.smartsheet.com/b/home) ou [DocuSign](https://www.docusign.net/member/MemberLogin.aspx))
  * Lors de l’authentification/utilisateurs sont fréquentes toogive autorisation toohello application tooaccess leur profil et les autres autorisations.  les causes de consentement Hello première personne toogive un principal de service représentant hello application toobe ajouté toohello répertoire.
* Connexion aux services en ligne de Microsoft comme [Office 365](http://products.office.com/)
  * Lorsque vous vous abonnez tooOffice 365 commencer une version d’évaluation ou plusieurs principaux de service est créés dans le répertoire hello représentant hello différents services qui sont utilisé toodeliver toutes les fonctionnalités de hello associés à Office 365.
  * Certains services Office 365, tel que SharePoint créer des principaux de service sur une en permanence tooallow une communication sécurisée entre les composants, y compris les workflows.
* Ajouter une application que vous développez dans hello voir du portail de gestion Azure : https://msdn.microsoft.com/library/azure/dn132599.aspx
* Ajout d'une application que vous développez à l'aide de Visual Studio :
  * [Méthode d'authentification ASP.Net](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions)
  * [Services connectés](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx)
* Ajouter un hello de toouse toouse application [Proxy d’Application Azure AD](https://msdn.microsoft.com/library/azure/dn768219.aspx)
* Mise en relation avec une application pour l'authentification unique à l'aide de SAML ou Password SSO ;
* Beaucoup d'autres, notamment les différentes expériences de développement dans Azure et/dans les expériences d'explorateur d'API dans tous les centres de développement.

## <a name="who-has-permission-tooadd-applications-toomy-azure-ad-instance"></a>Qui a l’instance Azure AD toomy autorisation tooadd applications ?
Seuls les administrateurs généraux peuvent :

* Ajouter des applications à partir de la galerie d’applications (applications pré-intégrées 3e partie) hello Azure AD
* Publier une application à l’aide de hello Proxy d’Application Azure AD

Tous les utilisateurs dans votre annuaire ont des applications tooadd droits qu’ils développent et discrétion sur les applications qu’ils partagent/permettent d’organisation de tootheir accéder aux données.  *N’oubliez pas d’utilisateur de connexion à distance/tooan application et accordez les autorisations peuvent entraîner une entité en cours de création de service.*

Ce peut initialement son concernant, mais hello conserver suivant à l’esprit :

* Les applications ont été en mesure de tooleverage Windows Server Active Directory pour l’authentification utilisateur depuis de nombreuses années, sans nécessiter de toobe d’application hello inscrit/enregistrés dans le répertoire de hello.  Maintenant l’organisation de hello sera ont amélioré la visibilité tooexactly combien d’applications sont à l’aide de répertoire de hello et pour quelles raisons.
* Pas besoin d'un processus de publication/inscription d'application piloté par l'administrateur.  Dans Active Directory Federation Services, il est probable qu’un administrateur devait tooadd une application comme une partie de confiance pour le compte de développeurs.  Les développeurs sont désormais libres.
* Les utilisateurs/des tooapps à l’aide de leurs comptes d’organisation à des fins commerciales de signature sont une bonne chose.  Si par la suite, ils laissent organisation hello que compte tootheir d’accès dans l’application hello qu'ils utilisaient seront perdues.
* Il est bon de disposer d'un enregistrement permettant de savoir avec quelle application les données ont été partagées.  Les données sont plus que jamais transportables, et il est utile de disposer d'un enregistrement précisant qui a partagé quelles données, et à l'aide de quelles applications.
* Les applications qui utilisent Azure AD pour oAuth décider exactement quelles sont les autorisations que les utilisateurs sont en mesure de toogrant tooapplications et les autorisations qui nécessitent une tooagree admin pour.  Il va sans dire que seuls les administrateurs peuvent donner son consentement toolarger étendues et des autorisations plus importantes.
* Les utilisateurs ajout et de laisser tooaccess applications que leurs données sont les événements audités afin de pouvoir consulter les rapports d’Audit hello toodetermine portail de gestion de Azure hello comment une application a été ajoutée toohello active.

**Remarque :** *Microsoft lui-même a été utilisé à l’aide de la configuration par défaut de hello pour le nombre de mois maintenant.*

Avec tous les qui dit que tooprevent possible des utilisateurs dans votre annuaire à partir de l’ajout d’applications et d’exercer discrétion les informations qu’ils partagent avec des applications en modifiant la configuration active dans le portail de gestion Azure hello.  Hello configuration suivante sont accessibles dans le portail de gestion Azure hello sur l’onglet « Configurer » de votre annuaire.

![Une capture d’écran de hello l’interface utilisateur pour la configuration des paramètres de l’application intégrée][app_settings]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur la façon tooadd tooAzure d’applications AD et comment tooconfigure services pour les applications.

* Développeurs : [apprendre comment toointegrate une application avec AAD](https://msdn.microsoft.com/library/azure/dn151122.aspx)
* Développeurs : [Consulter des exemples de code pour les applications intégrées à Azure Active Directory sur GitHub](https://github.com/AzureADSamples)
* Les développeurs et professionnels de l’informatique : [passez en revue la documentation des API REST hello pour hello API Graph Azure Active Directory](https://msdn.microsoft.com/library/azure/hh974478.aspx)
* Professionnels de l’informatique : [toouse Azure Active Directory intégration des applications à partir de la galerie d’applications de hello](https://msdn.microsoft.com/library/azure/dn308590.aspx)
* Professionnels de l'informatique : [Rechercher des didacticiels pour la configuration des applications spécifiques pré-intégrées](https://msdn.microsoft.com/library/azure/dn893637.aspx)
* Professionnels de l’informatique : [savoir comment une application à l’aide de toopublish hello Proxy d’Application Azure Active Directory](https://msdn.microsoft.com/library/azure/dn768219.aspx)

## <a name="see-also"></a>Voir aussi
* [Index d’articles pour la gestion des applications dans Azure Active Directory](../active-directory-apps-index.md)

<!--Image references-->
[apps_service_principals_directory]:../media/active-directory-how-applications-are-added/HowAppsAreAddedToAAD.jpg
[app_settings]:../media/active-directory-how-applications-are-added/IntegratedAppSettings.jpg
