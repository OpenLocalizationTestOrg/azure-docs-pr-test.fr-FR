---
title: "Considérations relatives à la conception d’identités hybrides Azure Active Directory : déterminer la stratégie d’adoption du cycle de vie des identités hybrides | Microsoft Docs"
description: "Permet de définir les tâches de gestion des identités hybrides selon les options disponibles pour chaque phase du cycle de vie."
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
ms.openlocfilehash: 18b40486a66d8e092a8af299460145989a1ab99d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="determine-hybrid-identity-lifecycle-adoption-strategy"></a>Déterminer la stratégie d’adoption du cycle de vie des identités hybrides
Dans cette tâche, vous allez définir la stratégie de gestion des identités pour que votre solution d’identités hybrides réponde aux exigences de l’entreprise définies dans [Déterminer les tâches de gestion des identités hybrides](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md).

Pour définir les tâches de gestion des identités hybrides selon le cycle de vie des identités de bout en bout présenté précédemment dans cette étape, vous devez tenir compte des options disponibles pour chaque phase du cycle de vie.

## <a name="access-management-and-provisioning"></a>Gestion des accès et approvisionnement
Avec une bonne solution de gestion des accès aux comptes, votre organisation peut suivre précisément qui a accès aux informations à travers l’organisation.

Le contrôle d’accès est une fonction essentielle d’un système d’approvisionnement centralisé et unique. Outre la protection des informations sensibles, les contrôles d’accès exposent les comptes existants qui ont des autorisations non approuvées ou qui ne sont plus nécessaires. Pour contrôler les comptes obsolètes, le système d’approvisionnement associe informations de compte et informations faisant autorité concernant les utilisateurs qui possèdent les comptes. Les informations relatives à l’identité des utilisateurs faisant autorité sont généralement conservées dans les bases de données et répertoires des services de ressources humaines.

Dans les entreprises informatiques modernes, les comptes contiennent des centaines de paramètres qui définissent les autorités, et ces informations peuvent être contrôlées par votre système d’approvisionnement. Les nouveaux utilisateurs peuvent être identifiés avec les données que vous fournissez à partir de la source faisant autorité. La fonctionnalité d’approbation des demandes d’accès lance les processus qui approuvent (ou refusent) l’approvisionnement des ressources qui leur sont destinées.

| Phase de gestion du cycle de vie | En local | Cloud | Hybride |
| --- | --- | --- | --- |
| Gestion des comptes et approvisionnement |En utilisant le rôle de serveur des services de domaine Active Directory® (AD DS), vous pouvez créer une infrastructure évolutive, sécurisée et gérable pour l’utilisateur et la gestion des ressources, et fournir une assistance pour les applications utilisant des répertoires telles que Microsoft® Exchange Server. <br><br> [Vous pouvez configurer des groupes dans AD DS via un gestionnaire d’identité](https://technet.microsoft.com/library/ff686261.aspx) <br>[Vous pouvez configurer des utilisateurs dans AD DS](https://technet.microsoft.com/library/ff686263.aspx) <br><br> Les administrateurs peuvent utiliser le contrôle d’accès pour gérer l’accès utilisateur aux ressources partagées pour des raisons de sécurité. Dans Active Directory, le contrôle d’accès est géré au niveau de l’objet en définissant différents niveaux d’accès, ou des autorisations sur les objets, par exemple Contrôle total, Écriture, Lecture ou Aucun accès. Le contrôle d’accès dans Active Directory définit la manière dont les différents utilisateurs peuvent utiliser les objets Active Directory. Par défaut, les autorisations sur les objets dans Active Directory sont définies sur le paramètre le plus sécurisé. |Vous devez créer un compte pour chaque utilisateur ayant besoin d’accéder à un service cloud Microsoft. Vous pouvez également modifier des comptes d’utilisateurs ou les supprimer lorsqu’ils ne sont plus nécessaires. Par défaut, les utilisateurs ne reçoivent pas d’autorisations d’administrateur, mais vous pouvez éventuellement leur affecter de telles autorisations. Pour plus d’informations, consultez [Gestion des utilisateurs dans Azure AD](active-directory-create-users.md). <br><br> Dans Azure Active Directory, l’une des principales fonctionnalités est la possibilité de gérer l’accès aux ressources. Ces ressources peuvent faire partie du répertoire, comme dans le cas des autorisations de gestion des objets via des rôles dans le répertoire ou les ressources externes au répertoire, comme les applications SaaS, les services Azure et les sites SharePoint ou les ressources locales. <br><br> Les groupes de sécurité sont au cœur de la solution de gestion de l’accès Azure Active Directory. Le propriétaire de la ressource (ou l’administrateur de l’annuaire) peut affecter un groupe pour fournir un certain droit d’accès aux ressources dont il dispose. Les membres de groupe se voient fournir l’accès et le propriétaire de la ressource peut déléguer le droit de gérer la liste des membres d’un groupe à quelqu’un d’autre, comme le chef de service ou l’administrateur du support technique.<br> <br> La rubrique Gestion de groupes dans Azure AD fournit de plus amples informations sur la gestion de l’accès via les groupes. |Étendre des identités Active Directory dans le cloud via la synchronisation et la fédération |

## <a name="role-based-access-control"></a>Contrôle d’accès en fonction du rôle
Le contrôle d’accès en fonction du rôle (RBAC) utilise les rôles et les stratégies d’approvisionnement pour évaluer, tester et appliquer vos processus et règles d’entreprise afin d’accorder l’accès aux utilisateurs. Les administrateurs de clés créent des stratégies d’approvisionnement et affectent les utilisateurs à des rôles, et ceci définit des ensembles de droits aux ressources pour ces rôles. RBAC étend la solution de gestion d’identité pour utiliser des processus basés sur des logiciels et réduire l’intervention manuelle de l’utilisateur dans le processus d’approvisionnement.
Azure AD RBAC permet aux entreprises de limiter la quantité d’opérations qu’un individu peut effectuer une fois qu’il a accès au portail de gestion Azure. En utilisant RBAC pour contrôler l’accès au portail, les administrateurs informatiques peuvent déléguer l’accès à l’aide des approches de gestion de l’accès suivantes :

* **Affectation de rôles basés sur les groupes**: vous pouvez affecter l’accès aux groupes Azure AD qui peuvent être synchronisés à partir de votre Active Directory local. Cela vous permet d’exploiter les investissements existants effectués par votre organisation dans les outils et processus pour la gestion des groupes. Vous pouvez également utiliser la fonctionnalité de gestion déléguée des groupes d’Azure AD Premium.
* **Exploitation des rôles intégrés dans Azure**: vous pouvez utiliser trois rôles (Propriétaire, Contributeur et Lecteur), pour vous assurer que les utilisateurs et groupes sont uniquement autorisés à effectuer les tâches dont ils ont besoin pour faire leur travail.
* **Accès granulaire aux ressources**: vous pouvez affecter des rôles aux utilisateurs et aux groupes pour un abonnement spécifique, un groupe de ressources ou une ressource Azure individuelle comme un site web ou une base de données. De cette façon, vous pouvez vous assurer que les utilisateurs ont accès à toutes les ressources dont ils ont besoin, et non aux ressources qu’ils n’ont pas besoin de gérer.

## <a name="provisioning-and-other-customization-options"></a>Approvisionnement et autres options de personnalisation
Votre équipe peut utiliser des plans d’activités et des exigences pour décider du degré de personnalisation de la solution d’identité. Par exemple, une grande entreprise peut requérir un plan de déploiement échelonné pour les workflows et des adaptateurs personnalisés, basés sur une ligne de temps pour approvisionner de façon incrémentielle les applications largement utilisées dans le monde entier. Un autre plan de personnalisation peut fournir deux applications ou plus à approvisionner dans toute l’organisation, après un test réussi. L’interaction utilisateur-application peut être personnalisée et les procédures d’approvisionnement des ressources peuvent être modifiées pour prendre en charge l’approvisionnement automatisé.

Vous pouvez annuler l’approvisionnement pour supprimer un service ou un composant. Par exemple, l’annulation de l’approvisionnement d’un compte signifie que le compte est supprimé d’une ressource.

Le modèle hybride d’approvisionnement des ressources combine les approches basées sur la demande et sur les rôles, toutes deux prises en charge par Azure AD. Pour un sous-ensemble d’employés ou des systèmes gérés, une entreprise peut souhaiter automatiser l’accès avec une affectation basée sur les rôles. Une entreprise peut également gérer toutes les autres demandes d’accès ou exceptions via un modèle basé sur la demande. Certaines entreprises peuvent commencer par l’affectation manuelle et évoluer vers un modèle hybride, avec l’intention de procéder à un déploiement entièrement basé sur les rôles à l’avenir.

D’autres entreprises peuvent trouver difficile pour des raisons internes de parvenir à l’approvisionnement basé sur les rôles, et cibler une approche hybride comme objectif souhaité. D’autres entreprises encore peuvent être satisfaites de l’approvisionnement basé sur la demande uniquement, et ne pas souhaiter investir des efforts supplémentaires pour définir et gérer les stratégies d’approvisionnement automatisées, basées sur les rôles.

## <a name="license-management"></a>Gestion des licences
La gestion des licences basée sur les groupes dans Azure AD permet aux administrateurs d’affecter des utilisateurs à un groupe de sécurité, et Azure AD affecte automatiquement des licences à tous les membres du groupe. Si un utilisateur est ensuite ajouté au groupe ou supprimé, une licence sera automatiquement affectée ou supprimée selon le cas.

Vous pouvez utiliser les groupes que vous synchronisez à partir d’AD en local ou gérer dans Azure AD. En couplant cela avec la gestion de groupes en libre-service Azure AD Premium, vous pouvez facilement déléguer l’affectation de licences aux décideurs appropriés. Vous avez l’assurance que des problèmes tels que les conflits de licence et les données d’emplacement manquantes sont automatiquement résolus.

## <a name="self-regulating-user-administration"></a>Administration des utilisateurs autorégulée
Lorsque votre organisation commence à approvisionner les ressources dans toutes les organisations internes, vous implémentez la fonctionnalité d’administration des utilisateurs autorégulée. Vous pouvez tirer parti des avantages de l’approvisionnement des utilisateurs au-delà des limites organisationnelles. Dans cet environnement, une modification de l’état d’un utilisateur est automatiquement répercutée dans les droits d’accès au-delà des limites organisationnelles et géographiques. Vous pouvez réduire les coûts d’approvisionnement et rationaliser les processus d’accès et d’approbation. La mise en œuvre exploite l’intégralité du potentiel de l’implémentation du contrôle d’accès en fonction du rôle pour la gestion de l’accès de bout en bout dans votre organisation. Vous pouvez réduire les coûts administratifs grâce à des procédures automatisées pour régir l’approvisionnement des utilisateurs. Vous pouvez améliorer la sécurité en automatisant l’application des stratégies de sécurité, et simplifier et centraliser la gestion du cycle de vie des utilisateurs, ainsi que l’approvisionnement pour les utilisateurs nombreux.

> [!NOTE]
> Pour plus d’informations, consultez Configuration d’Azure AD pour gérer l’accès aux applications en libre-service
> 
> 

Les services Azure AD basés sur des licences (sur des droits) reposent sur l’activation d’un abonnement dans votre annuaire/client de service Azure AD. Une fois que l’abonnement est actif, les fonctionnalités de service peuvent être gérées par les administrateurs d’annuaire/de service et utilisées par les utilisateurs sous licence. Pour plus d’informations, consultez Comment fonctionne la gestion de licences Azure AD ?
Intégration avec des fournisseurs tiers

Azure Active Directory fournit l’authentification unique et une sécurité de l’accès aux applications améliorée à des milliers d’applications SaaS et à des applications web locales. Pour obtenir une liste détaillée de la galerie d’applications Azure Active Directory pour les applications SaaS prises en charge, consultez la liste de compatibilité de fédération Azure Active Directory : les fournisseurs d’identité tiers qui peuvent être utilisés pour mettre en œuvre l’authentification unique.

## <a name="define-synchronization-management"></a>Définir la gestion de la synchronisation
L’intégration de vos annuaires locaux avec Azure AD améliore la productivité de vos utilisateurs en leur fournissant une identité commune pour accéder aux ressources cloud et locales. Cette intégration procure aux utilisateurs et aux organisations les avantages suivants :

* Les organisations peuvent fournir aux utilisateurs une identité hybride commune entre différents services locaux ou cloud exploitant Windows Server Active Directory et la connexion à Azure Active Directory.
* Les administrateurs peuvent fournir un accès conditionnel basé sur des ressources d’application, des identités d’appareil et d’utilisateur, un emplacement réseau et une authentification multifacteur.
* Les utilisateurs peuvent exploiter leur identité commune via des comptes dans d’Azure AD vers Office 365, Intune, des applications SaaS et des applications tierces.
* Les développeurs peuvent créer des applications qui exploitent le modèle d’identité commune en intégrant des applications dans une version locale d’Active Directory ou des applications cloud Azure.

La figure suivante est un exemple d’une vue d’ensemble du processus de synchronisation d’identité.

![](./media/hybrid-id-design-considerations/identitysync.png)

Processus de synchronisation d’identité

Consultez le tableau suivant pour comparer les options de synchronisation :

| Option de gestion de la synchronisation | Avantages | Inconvénients |
| --- | --- | --- |
| En fonction de la synchronisation (via DirSync ou AADConnect) |Utilisateurs et groupes synchronisés en local ou à partir du cloud  <br>  **Contrôle de stratégie**: des stratégies de compte peuvent être définies via Active Directory, ce qui donne à l’administrateur la possibilité de gérer des stratégies de mot de passe, postes de travail, restrictions, contrôles de verrouillage, etc., sans avoir à effectuer des tâches supplémentaires dans le cloud.  <br>  **Contrôle d’accès**: possibilité de restreindre l’accès au service cloud de sorte que les services soient accessibles via l’environnement d’entreprise, les serveurs en ligne, ou les deux. <br>  Réduction des appels au support : si les utilisateurs ont moins de mots de passe à mémoriser, ils sont moins susceptibles de les oublier. <br>  Sécurité : les identités et informations des utilisateurs sont protégées, car tous les serveurs et services utilisés dans l’authentification unique sont supervisés et contrôlés localement. <br>  Prise en charge de l’authentification forte : vous pouvez utiliser l’authentification forte (également appelée authentification à 2 facteurs) avec le service cloud. Toutefois, si vous utilisez l’authentification forte, vous devez utiliser l’authentification unique. | |
| En fonction de la fédération (via AD FS) |Activation par le service d’émission de jeton de sécurité (STS). Lorsque vous configurez un STS pour fournir l’accès à l’authentification unique avec un service cloud Microsoft, vous créez une approbation fédérée entre votre STS local et le domaine fédéré que vous avez spécifié dans votre client Azure AD. <br> Permet aux utilisateurs finaux d’utiliser le même jeu d’informations d’identification pour accéder à plusieurs ressources <br>Les utilisateurs finaux n’ont pas à gérer plusieurs jeux d’informations d’identification. Pourtant, les utilisateurs doivent fournir leurs informations d’identification à chacune des ressources participantes. Les scénarios B2B et B2C sont pris en charge. |Requiert un personnel spécialisé pour le déploiement et la maintenance de serveurs AD FS locaux dédiés. Il existe des restrictions relatives à l’utilisation de l’authentification forte si vous prévoyez d’utiliser AD FS pour votre STS. Pour plus d’informations, consultez [Configuration des options avancées pour AD FS 2.0](http://go.microsoft.com/fwlink/?linkid=235649). |

> [!NOTE]
> Pour plus d’informations, consultez [Intégration des identités locales avec Azure Active Directory](active-directory-aadconnect.md).
> 
> 

## <a name="see-also"></a>Voir aussi
[Présentation des considérations relatives à la conception](active-directory-hybrid-identity-design-considerations-overview.md)

