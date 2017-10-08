---
title: "Considérations de conception pour les identités hybrides aaaAzure Active Directory - déterminer la stratégie d’adoption du cycle de vie des identités hybrides | Documents Microsoft"
description: "Permet de définir les tâches de gestion des identités hybride hello selon les options de toohello disponibles pour chaque phase du cycle de vie."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 420b6046-bd9b-4fce-83b0-72625878ae71
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 86ec0a9896f069bc93e49e06006954848f8e4d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-hybrid-identity-lifecycle-adoption-strategy"></a>Déterminer la stratégie d’adoption du cycle de vie des identités hybrides
Dans cette tâche, vous allez définir la stratégie de gestion des identités hello pour hybride identité solution toomeet hello besoins de votre entreprise que vous avez définie dans [déterminer les tâches de gestion d’identité hybride](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md).

vous aurez toodefine hello hybride identité des tâches de gestion selon présenté précédemment dans cette étape du cycle de vie toohello identité de bout en bout, options de hello tooconsider disponibles pour chaque phase du cycle de vie.

## <a name="access-management-and-provisioning"></a>Gestion des accès et approvisionnement
Avec une solution de gestion des accès bon compte, votre organisation peut suivre précisément disposant d’informations toowhat d’accès de l’entreprise hello.

Le contrôle d’accès est une fonction essentielle d’un système d’approvisionnement centralisé et unique. Outre la protection des informations sensibles, les contrôles d’accès exposent les comptes existants qui ont des autorisations non approuvées ou qui ne sont plus nécessaires. les comptes obsolètes toocontrol, hello les informations de compte ensemble de liens configuration système avec des informations faisant autoritées sur les utilisateurs de hello qui possèdent des comptes de hello. Informations d’identité utilisateur ne faisant pas autorité sont généralement conservées dans les bases de données hello et les répertoires des ressources humaines.

Comptes dans des entreprises informatiques sophistiquées contiennent des centaines de paramètres qui définissent les autorités de hello, et ces informations peuvent être contrôlées par votre système d’approvisionnement. Nouveaux utilisateurs peuvent être identifiés avec les données de salutation que vous fournissez à partir de la source d’autorité hello. capacité d’approbation demande Hello accès lance des processus hello approuvent (ou rejeter) d’une ressource de configuration pour les.

| Phase de gestion du cycle de vie | En local | Cloud | Hybride |
| --- | --- | --- | --- |
| Gestion des comptes et approvisionnement |En utilisant le rôle de serveur Services de domaine Active Directory® (AD DS) hello, vous pouvez créer une infrastructure évolutive, sécurisée et gérable pour l’utilisateur et de gestion des ressources et fournir la prise en charge pour les applications d’annuaire telles que Microsoft® Exchange Server. <br><br> [Vous pouvez configurer des groupes dans AD DS via un gestionnaire d’identité](https://technet.microsoft.com/library/ff686261.aspx) <br>[Vous pouvez configurer des utilisateurs dans AD DS](https://technet.microsoft.com/library/ff686263.aspx) <br><br> Les administrateurs peuvent utiliser l’accès contrôle toomanage tooshared utilisateur accéder aux ressources pour des raisons de sécurité. Dans Active Directory, le contrôle d’accès est géré au niveau de l’objet hello en définissant des niveaux différents de tooobjects d’accès ou les autorisations, telles que contrôle total, écriture, lecture ou aucun accès. Le contrôle d’accès dans Active Directory définit la manière dont les différents utilisateurs peuvent utiliser les objets Active Directory. Par défaut, les autorisations sur les objets dans Active Directory sont définies toohello paramètre le plus sécurisé. |Vous avez toocreate un compte pour chaque utilisateur qui accède à un service cloud Microsoft. Vous pouvez également modifier des comptes d’utilisateurs ou les supprimer lorsqu’ils ne sont plus nécessaires. Par défaut, les utilisateurs ne reçoivent pas d’autorisations d’administrateur, mais vous pouvez éventuellement leur affecter de telles autorisations. Pour plus d’informations, consultez [Gestion des utilisateurs dans Azure AD](active-directory-create-users.md). <br><br> Dans Azure Active Directory, une des principales fonctionnalités de hello est hello capacité toomanage accès tooresources. Ces ressources peuvent faire partie du répertoire hello, comme dans les cas de hello d’objets de toomanage autorisations via des rôles dans le répertoire de hello ou des ressources qui sont Active toohello externes, tels que les applications SaaS, les services Azure et les sites SharePoint ou sur site ressources. <br><br> Solution de gestion des accès center d’Azure Active Directory hello est groupe de sécurité hello. propriétaire de la ressource Hello (ou administrateur hello du répertoire de hello) peut affecter un tooprovide groupe un certaines ressources de le toohello droit accès qu’ils possèdent. les membres du groupe de hello Hello seront fournies lors de l’accès hello et propriétaire de la ressource hello peut déléguer la liste des membres de hello hello toomanage droite d’un groupe de toosomeone autre – par exemple un responsable ou un administrateur de support technique<br> <br> Gestion de groupes de Hello dans la rubrique d’Azure AD fournit plus d’informations sur la gestion de l’accès via des groupes. |Étendre des identités Active Directory dans le cloud hello via la synchronisation et la fédération |

## <a name="role-based-access-control"></a>Contrôle d’accès en fonction du rôle
Contrôle d’accès basé sur un rôle (RBAC) utilise des rôles et tooevaluate des stratégies de configuration, de test et appliquer votre processus d’entreprise et les règles d’octroi d’accès toousers. Administrateurs créer des stratégies de configuration et affecter des utilisateurs tooroles et qui définissent des ensembles de tooresources de droits pour ces rôles. RBAC étend hello identity management solution toouse logiciel processus et de réduire une intervention manuelle Bonjour processus d’approvisionnement utilisateur.
Azure AD RBAC permet hello entreprise toorestrict hello quantité opérations un individu peut faire une fois qu’il a accès tooAzure portail de gestion. En utilisant le portail de toohello d’accès RBAC toocontrol, les administrateurs informatiques peuvent l’accès délégué autorité de certification à l’aide de hello suivant de gestion de l’accès s’approche de :

* **Attribution de rôle de groupe**: vous pouvez affecter l’accès à des groupes de tooAzure AD qui peuvent être synchronisés à partir de votre Active Directory local. Cela vous permet de tooleverage hello investissements de votre organisation dans les outils et processus de gestion des groupes. Vous pouvez également utiliser la fonctionnalité de gestion déléguée des groupes hello d’Azure AD Premium.
* **Exploitez générée dans les rôles dans Azure**: vous pouvez utiliser trois rôles : tooensure propriétaire, collaborateur et lecteur, que les utilisateurs et groupes ont des autorisations toodo uniquement hello les tâches dont ils ont besoin toodo leurs travaux.
* **Un accès granulaire tooresources**: vous pouvez affecter des rôles toousers et des groupes pour un abonnement spécifique, groupe de ressources ou une ressource individuelle Azure tel qu’un site Web ou d’une base de données. De cette façon, vous pouvez garantir que les utilisateurs ont accéder aux ressources de hello tooall que dont ils ont besoin et aucun tooresources accès qu’ils toomanage n’avez pas besoin.

## <a name="provisioning-and-other-customization-options"></a>Approvisionnement et autres options de personnalisation
Votre équipe peut utiliser toodecide plans et des exigences d’entreprise quelle solution d’identité toocustomize hello. Par exemple, une grande entreprise peut requérir un plan de déploiement échelonné pour les workflows et des adaptateurs personnalisés, basés sur une ligne de temps pour approvisionner de façon incrémentielle les applications largement utilisées dans le monde entier. Un autre plan de personnalisation peut fournir pour deux ou plusieurs toobe d’applications dans un ensemble de l’organisation, le test réussit. Interaction de l’application de l’utilisateur peut être personnalisée et des procédures pour l’approvisionnement des ressources peuvent être modifiée tooaccommodate automatisée de configuration.

Vous pouvez annuler le déploiement tooremove un service ou composant. Par exemple, la mise hors service d’un compte signifie que le compte de hello est supprimé d’une ressource.

modèle hybride de Hello de provisionnement des ressources combine la demande et approches en fonction du rôle, qui sont tous deux pris en charge par Azure AD. Pour un sous-ensemble des employés ou des systèmes gérés, une entreprise souhaite accès tooautomate avec affectation basée sur le rôle. Une entreprise peut également gérer toutes les autres demandes d’accès ou exceptions via un modèle basé sur la demande. Certaines entreprises peuvent commencer par l’affectation manuelle et évoluer vers un modèle hybride, avec l’intention de procéder à un déploiement entièrement basé sur les rôles à l’avenir.

Autres sociétés peuvent s’avérer peu pratique pour entreprise raisons tooachieve complète en fonction du rôle de configuration et la cible une approche hybride comme objectif que vous souhaitez conserver. Toujours d’autres sociétés peuvent être satisfaites avec uniquement des demandes de configuration et pas souhaitez tooinvest effort supplémentaire toodefine et gérer les stratégies de configuration automatiques, en fonction du rôle.

## <a name="license-management"></a>Gestion des licences
Gestion basée sur le groupe de licences dans Azure AD permet aux administrateurs d’affecter le groupe de sécurité utilisateurs tooa et Azure AD affecte des licences automatiquement membres de hello tooall du groupe de hello. Si un utilisateur est ensuite ajouté ou supprimé du groupe de hello, une licence sera automatiquement attribuée ou supprimée selon le cas.

Vous pouvez utiliser les groupes que vous synchronisez à partir d’AD en local ou gérer dans Azure AD. Ce couplage avec Azure Active Directory premium, gestion de groupe libre-service vous pouvez facilement déléguer licence affectation toohello approprié décideurs. Vous avez l’assurance que des problèmes tels que les conflits de licence et les données d’emplacement manquantes sont automatiquement résolus.

## <a name="self-regulating-user-administration"></a>Administration des utilisateurs autorégulée
Au démarrage de votre organisation tooprovision ressources dans toutes les organisations internes, vous implémentez la fonctionnalité d’administration hello régule utilisateur. Vous pouvez bénéficier des avantages de hello et les avantages de l’approvisionnement des utilisateurs au-delà des limites d’organisation. Dans cet environnement, une modification de l’état d’un utilisateur est automatiquement répercutée dans les droits d’accès au-delà des limites organisationnelles et géographiques. Vous pouvez réduire les coûts de déploiement et simplifier les processus d’accès et d’approbation hello. implémentation de Hello se rend compte potentiel hello d’implémentation du contrôle d’accès basé sur un rôle pour la gestion de bout en bout pour l’accès de votre organisation. Vous pouvez réduire les coûts administratifs grâce à des procédures automatisées pour régir l’approvisionnement des utilisateurs. Vous pouvez améliorer la sécurité en automatisant l’application des stratégies de sécurité, et simplifier et centraliser la gestion du cycle de vie des utilisateurs, ainsi que l’approvisionnement pour les utilisateurs nombreux.

> [!NOTE]
> Pour plus d’informations, consultez Configuration d’Azure AD pour gérer l’accès aux applications en libre-service
> 
> 

Les services Azure AD basés sur des licences (sur des droits) reposent sur l’activation d’un abonnement dans votre annuaire/client de service Azure AD. Une fois que l’abonnement hello est active des fonctionnalités de service hello peuvent être gérées par des administrateurs de service d’annuaire et utilisées par les utilisateurs sous licence. Pour plus d’informations, consultez Comment fonctionne la gestion de licences Azure AD ?
Intégration avec des fournisseurs tiers

Azure Active Directory fournit l’authentification unique sur et amélioré toothousands de sécurité d’accès application des applications SaaS et des applications web sur site. Pour obtenir une liste détaillée de la galerie d’applications Azure Active Directory pour les applications SaaS pris en charge, consultez la liste de compatibilité de fédération Azure Active Directory : fournisseurs d’identité tiers qui peuvent être utilisé tooimplement l’authentification unique

## <a name="define-synchronization-management"></a>Définir la gestion de la synchronisation
L’intégration de vos annuaires locaux avec Azure AD améliore la productivité de vos utilisateurs en leur fournissant une identité commune pour accéder aux ressources cloud et locales. Avec cette intégration utilisateurs et des organisations peuvent tirer parti des éléments suivants de hello :

* Les organisations peuvent fournir aux utilisateurs une identité hybride commune entre les services cloud en tirant parti de Windows Server Active Directory, puis connexion tooAzure Active Directory ou locaux.
* Les administrateurs peuvent fournir un accès conditionnel basé sur des ressources d’application, des identités d’appareil et d’utilisateur, un emplacement réseau et une authentification multifacteur.
* Les utilisateurs peuvent utiliser leur identité commune via des comptes dans Azure AD tooOffice 365, Intune, les applications SaaS et des applications tierces.
* Les développeurs peuvent créer des applications qui tirent parti du modèle d’identité commune hello, intégration d’applications dans Active Directory en local ou Azure pour les applications cloud

Hello figure suivante est un exemple d’une vue d’ensemble du processus de synchronisation d’identité.

![](./media/hybrid-id-design-considerations/identitysync.png)

Processus de synchronisation d’identité

Passez en revue hello table toocompare hello synchronisation des options suivantes :

| Option de gestion de la synchronisation | Avantages | Inconvénients |
| --- | --- | --- |
| En fonction de la synchronisation (via DirSync ou AADConnect) |Utilisateurs et groupes synchronisés en local ou à partir du cloud  <br>  **Contrôle de la stratégie**: stratégies de compte peuvent être définis via Active Directory, ce qui donne des stratégies de mot de passe hello administrateur hello capacité toomanage, station de travail, restrictions, les contrôles de verrouillage, etc., sans avoir tooperform supplémentaire tâches dans le cloud de hello.  <br>  **Contrôle d’accès**: peut restreindre l’accès toohello cloud service afin que les services hello est accessible via hello environnement d’entreprise, les serveurs en ligne, ou les deux. <br>  Réduit les appels au support technique : si les utilisateurs ont moins tooremember de mots de passe, ils sont moins susceptibles de tooforget les. <br>  Sécurité : Plus d’informations et les identités des utilisateurs sont protégés, car tous les serveurs de hello et services utilisés dans l’authentification unique, sont contrôlées et contrôlés localement. <br>  Prise en charge de l’authentification forte : vous pouvez utiliser l’authentification forte (également appelée authentification à deux facteurs) avec le service cloud hello. Toutefois, si vous utilisez l’authentification forte, vous devez utiliser l’authentification unique. | |
| En fonction de la fédération (via AD FS) |Activation par le service d’émission de jeton de sécurité (STS). Lorsque vous configurez un STS tooprovide-accès authentification unique avec un service cloud Microsoft, vous allez créer une approbation fédérée entre votre STS local et un domaine fédéré de hello dans votre locataire Azure AD que vous avez spécifié. <br> Permet aux utilisateurs finaux hello toouse d’accéder aux ressources toomultiple d’informations d’identification tooobtain <br>les utilisateurs finaux n’ont pas de toomaintain plusieurs jeux d’informations d’identification. Pourtant, les utilisateurs de hello ont tooprovide leur informations d’identification tooeach une hello participantes ressources., les scénarios B2B et B2C pris en charge. |Requiert un personnel spécialisé pour le déploiement et la maintenance de serveurs AD FS locaux dédiés. Il existe des restrictions sur l’utilisation de hello de l’authentification forte si vous envisagez de toouse AD FS pour votre STS. Pour plus d’informations, consultez [Configuration des options avancées pour AD FS 2.0](http://go.microsoft.com/fwlink/?linkid=235649). |

> [!NOTE]
> Pour plus d’informations, consultez [Intégration des identités locales avec Azure Active Directory](active-directory-aadconnect.md).
> 
> 

## <a name="see-also"></a>Voir aussi
[Présentation des considérations relatives à la conception](active-directory-hybrid-identity-design-considerations-overview.md)

