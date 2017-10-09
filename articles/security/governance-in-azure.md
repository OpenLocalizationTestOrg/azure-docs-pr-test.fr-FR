---
title: aaaGovernance dans Azure | Documents Microsoft
description: "En savoir plus sur les services informatiques en nuage qui incluent une large sélection des instances de calcul et de services qui peuvent mettre à l’échelle haut et bas automatiquement toomeet hello aux besoins de votre application ou votre entreprise."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/01/2017
ms.author: TomSh
ms.openlocfilehash: 956e82e92f4232c24069bdb79fed5315f1d6486f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="governance-in-azure"></a>Gouvernance dans Azure

Nous savons que la sécurité est une tâche dans le cloud de hello et combien il est important que vous trouvez des informations précises et actuelles sur la sécurité Azure. Un des hello meilleures raisons toouse Azure pour vos applications et services est parti tootake de sa large gamme d’outils de sécurité et des fonctions. Ces outils et les fonctions permettent de rendre des solutions sécurisées toocreate possible sur la plateforme Azure sécurisé de hello.

toohelp que mieux hello tableau de gouvernance des contrôles implémenté dans Microsoft Azure à partir d’un client à la fois hello et perspectives des opérations de Microsoft, cet article, « Gouvernance dans Azure », est écrit, qui fournit une vision détaillée hello Fonctionnalités de gouvernance disponibles avec Microsoft Azure.

## <a name="azure-platform"></a>Plateforme Azure

Azure est une plateforme de services de cloud public qui prend en charge un large éventail de systèmes d’exploitation, de langages de programmation, d’infrastructures, d’outils, de bases de données et d’appareils. Elle permet d’exécuter des conteneurs Linux avec l’intégration de Docker, de créer des applications avec JavaScript, Python, .NET, PHP, Java et Node.js, de créer des serveurs principaux pour des appareils iOS, Android et Windows. Services de cloud public Azure prend en charge hello mêmes technologies des millions de développeurs et professionnels de l’informatique s’appuient sur déjà et faites confiance.

Lorsque vous générez sur ou migrez les ressources informatiques à, un fournisseur de services de cloud public vous recourez tooprotect des capacités de cette organisation vos applications et les données avec les contrôles de hello et les services de hello ils sécuriser toomanage hello de votre nuage ressources.

L’infrastructure Azure est conçu de tooapplications de fonctionnalité hello pour l’hébergement des millions de clients simultanément, et fournit une base digne de confiance sur lesquelles les entreprises capable de répondre aux impératifs de sécurité. En outre, Azure offre plusieurs options de sécurité et hello capacité toocontrol leur afin que vous pouvez personnaliser les exigences uniques de sécurité toomeet hello des déploiements de votre organisation.

Ce document vous permettra de comprendre comment les fonctionnalités de gouvernance d’Azure peuvent vous aider à répondre à ces besoins.

## <a name="abstract"></a>Résumé

Gouvernance de cloud de Microsoft Azure fournit un audit intégrée et une approche de Conseil pour examiner et conseiller aux organisations de leur utilisation de hello plateforme Azure. Gouvernance de cloud de Microsoft Azure fait référence toohello les processus de prise de décision, les critères et les stratégies impliquées dans la planification de hello, architecture, acquisition, déploiement, opération et la gestion d’un Cloud computing.

toocreate un plan pour la gouvernance de cloud de Microsoft Azure, vous devez tootake explications approfondies sur les personnes hello, les processus et les technologies actuellement en place et, les infrastructures de build qui facilitent informatique tooconsistently prend en charge les besoins tout en offrant de fin utilisateurs avec hello flexibilité toouse hello puissantes fonctionnalités de Microsoft Azure.

Ce document explique comment vous pouvez obtenir un niveau élevé de gouvernance de vos ressources informatiques dans Microsoft Azure. Ce document peut vous aider à comprendre les fonctionnalités de sécurité et de gouvernance hello intégrées tooMicrosoft Azure.

Hello Voici gouvernance hello principal abordés dans ce document :

- Implémentation de stratégies, de processus et de procédures en fonction des objectifs de l’organisation.

- Sécurité et conformité continue aux normes de l’organisation

- Alertes et monitoring

## <a name="implementation-of-policies-processes-and-procedures"></a>Implémentation de stratégies, de processus et de procédures 

Gestion a établi des rôles et responsabilités implémentation toooversee de stratégie de sécurité des informations hello et continuité opérationnelle sur Azure. Les responsables Microsoft Azure sont chargés de surveiller la sécurité et les pratiques de continuité au sein de leurs équipes respectives (y compris celles composées de tiers) et d’optimiser la conformité avec les stratégies de sécurité, les processus et les normes.

Voici les facteurs hello a évolué :

- Approvisionnement des comptes

- Contrôles de l’abonnement

- Contrôles de l’accès en fonction du rôle

- Gestion des ressources

- Suivi des ressources

- Contrôle des ressources critiques

- Accès aux API tooBilling informations

- Contrôles de mise en réseau

## <a name="account-provisioning"></a>Approvisionnement des comptes

Définition de compte hiérarchie est une étape majeure toouse et la structure des services Azure au sein d’une entreprise et structure de gouvernance hello core. En cas de clients avec un contrat d’entreprise hello, les clients peuvent subdiviser environnement hello dans les services, les comptes et enfin, les abonnements.

![Approvisionnement des comptes](./media/governance-in-azure/security-governance-in-azure-fig1.png)

Si vous n’avez pas d’un contrat entreprise, envisagez d’utiliser [balises Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) au niveau de la hiérarchie de niveau toodefine d’abonnement. Un abonnement Azure est l’unité de base hello où toutes les ressources sont contenues. Il définit également plusieurs limites au sein d’Azure, par exemple le nombre de cœurs, de ressources, etc. Les abonnements peuvent contenir des [groupes de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview), qui à leur tour peuvent contenir des ressources. Les principes [RBAC](https://docs.microsoft.com/azure/api-management/api-management-role-based-access-control) s’appliquent à ces trois niveaux.

Chaque entreprise est différente et hiérarchie hello à l’aide de balises de Azure en cas de non entreprises permet une grande flexibilité dans l’organisation au sein de la société de hello Azure. Avant de déployer des ressources de Microsoft Azure, vous devez hiérarchie du modèle et comprendre l’impact de hello sur la facturation, de l’accès aux ressources et de complexité.

## <a name="subscription-controls"></a>Contrôles de l’abonnement

L’abonnement contrôle la manière dont l’utilisation des ressources est signalée et facturée. Il est possible de configurer les abonnements pour obtenir une facturation et un paiement séparés. Comme mentionné plus haut, un seul compte Azure peut contenir plusieurs abonnements. Les abonnements peuvent être utilisés toodetermine l’utilisation des ressources Azure hello de plusieurs départements d’une entreprise.

Par exemple, une entreprise ayant un service informatique, un service RH et un service marketing avec différents projets en cours d’exécution. Après utilisation hello de ressources Azure telles que des machines virtuelles par chaque service, qu’ils peuvent être facturés en conséquence. En cela, nous pouvons contrôler finances hello de chaque service.

Les abonnements Azure établissent trois paramètres :

- un ID d’abonné unique ;

- un emplacement de facturation ;

- un ensemble de ressources disponibles.

Une personne, qui inclut un ID de compte Microsoft, une carte de crédit numéro et hello suite complète d’Azure services--bien que Microsoft impose des limites de consommation, selon le type d’abonnement hello.

Les hiérarchies d’inscription Azure définissent la structure des services dans un contrat Entreprise. Hello Enterprise Portal permet aux clients toodivide accéder aux ressources de tooAzure associé à un contrat d’entreprise en fonction des besoins uniques de l’organisation des hiérarchies flexibles tooan personnalisable. modèle de hiérarchie Hello doit correspondre à l’administration et structure géographique d’une organisation afin que hello associées à la facturation et l’accès aux ressources peut être correctement pris en compte.

modèles de haut niveau Hello trois sont fonctionnel, centre de profit, et géographiques, à l’aide des services comme une construction d’administration pour le compte des regroupements. Au sein de chaque service, des abonnements peuvent être affectés aux comptes, ce qui crée des silos pour la facturation et plusieurs limites clés dans Azure (par exemple, nombre de machines virtuelles, comptes de stockage, etc.).

![Contrôles de l’abonnement](./media/governance-in-azure/security-governance-in-azure-fig2.png)


Pour les organisations disposant d’un contrat Entreprise, les abonnements Azure respectent une hiérarchie à quatre niveaux :

- administrateur d’inscription d’entreprise ;

- administrateur de service ;

- propriétaire du compte ;

- Administrateur de services fédérés

Cette hiérarchie régit les éléments suivants de hello :

- Relation de facturation

- Administration des comptes

- Tooartifacts de contrôle d’accès basé sur (RBAC) de rôle

- Limites

- Limites

  - Utilisation et facturation (carte de tarifs basée sur le numéro de l’offre)

  - limites

  - Réseau virtuel

- Joint too1 AAD (1 AAD être associé à plusieurs abonnements)

- Compte de l’inscription d’entreprise tooan associé

## <a name="role-based-access-controls"></a>Contrôles de l’accès en fonction du rôle

Lorsque Azure a été initialement publiée, l’accès aux contrôles tooa abonnement ont été base : administrateur ou Coadministrateur. Abonnement tooa d’accès dans hello classique modèle impliqué accès tooall hello ressources du portail de hello. Cette absence d’un contrôle affiné led prolifération toohello des abonnements tooprovide un niveau de contrôle d’accès raisonnable pour une inscription à Azure.

![Contrôles de l’accès en fonction du rôle](./media/governance-in-azure/security-governance-in-azure-fig3.png)

Cette prolifération d’abonnements n’est plus nécessaire. Avec le contrôle d’accès basé sur un rôle, vous pouvez affecter des utilisateurs rôles toostandard (par exemple, commun « lecture » et les types de « writer » des rôles). Vous pouvez également définir des rôles personnalisés.

Le [contrôle d’accès en fonction du rôle (RBAC) Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) permet une gestion précise de l’accès pour Azure. À l’aide de RBAC, vous pouvez accorder uniquement les quantité hello d’accès que les utilisateurs doivent tooperform leur travail. Orientée sécurité doit se concentrent sur fournir aux employés les autorisations exactes hello que dont ils ont besoin. Trop d’autorisations exposent un tooattackers de compte. Si le nombre d’autorisations est trop faible, les employés ne peuvent pas effectuer leur travail efficacement. Le contrôle d’accès en fonction du rôle (RBAC) Azure permet de résoudre ce problème en offrant une gestion précise de l’accès pour Azure. RBAC vous aide à droits toosegregate dans votre équipe et accordez uniquement hello délai toousers d’accès dont ils ont besoin tooperform leur travail. Plutôt que de donner à tous des autorisations illimitées au sein de votre abonnement ou de vos ressources Azure, vous pouvez autoriser uniquement certaines actions.

Par exemple, un employé d’utiliser RBAC toolet gérer des ordinateurs virtuels dans un abonnement, tandis que l’autre peut gérer les bases de données SQL dans hello même abonnement.

RBAC Azure a trois rôles de base qui s’appliquent à des types de ressources tooall :

- **Propriétaire** dispose des ressources de tooall un accès complet, y compris hello toodelegate droit accès tooothers.

- **Collaborateur** peut créer et gérer tous les types de ressources Azure, mais ne peut pas accorder l’accès tooothers.

- **Lecteur** peut consulter les ressources Azure existantes.

autres rôles RBAC hello dans Azure Hello autoriser la gestion de ressources Azure spécifiques. Par exemple, hello collaborateur d’un ordinateur virtuel permet hello utilisateur toocreate et gérer des ordinateurs virtuels. Il ne leur confère pas accéder au réseau virtuel de toohello ou sous-réseau hello hello machine virtuelle se connecte à.

[Les rôles intégrés RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) listes hello rôles disponibles dans Azure. Il spécifie les opérations hello et étendue que chaque rôle prédéfini accorde toousers.

Accorder l’accès en assignant hello toousers du rôle RBAC appropriés, les groupes et les applications à une certaine étendue. Hello portée d’une attribution de rôle peut être un abonnement, un groupe de ressources ou une seule ressource. Un rôle attribué à une portée parent accorde également l’accès toohello les enfants qu’il contient.

Par exemple, un utilisateur avec le groupe de ressources tooa accès peut gérer toutes les ressources de hello qu’elle contient, comme les sites Web, des ordinateurs virtuels et des sous-réseaux.

Azure RBAC uniquement prend en charge les opérations de gestion de hello ressources Azure dans hello portail Azure et les API du Gestionnaire de ressources Azure. Il ne peut pas autoriser toutes les opérations au niveau des données pour les ressources Azure. Par exemple, vous pouvez autoriser une personne BLOB toomanage comptes de stockage, mais pas toohello ou des tables au sein d’un compte de stockage ne peut pas. De même, une base de données SQL peut être géré, mais pas hello tables qu’il contient.

Si vous souhaitez plus d’informations sur la gestion des droits d’accès avec RBAC, consultez [Prise en main de la gestion des accès dans le portail Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is).

Vous pouvez également [créer un rôle personnalisé](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles) de contrôle d’accès du (RBAC) si aucun des rôles intégrés de hello répond à votre accès spécifique a besoin. Des rôles personnalisés peuvent être créés à l’aide de [Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell), [Azure Interface de ligne de commande (CLI)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-azure-cli)et hello [API REST](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-rest). Tout comme les rôles intégrés, des rôles personnalisés peuvent avoir toousers, des groupes et des applications au niveau d’abonnement, de groupe de ressources et de portées de ressource.

Dans chaque abonnement, vous pouvez accorder des attributions de rôles too2000.

## <a name="resource-management"></a>Gestion des ressources

Initialement, Azure fourni uniquement le modèle de déploiement classique hello. Dans ce modèle, chaque ressource existe indépendamment ; Il n’existait aucun moyen toogroup les ressources associées ensemble. Au lieu de cela, vous aviez toomanually suivre les ressources qui composés votre solution ou votre application et n’oubliez pas de toomanage dans une approche coordonnée.

toodeploy une solution, vous aviez tooeither créer chaque ressource individuellement via le portail classique de hello ou créer un script qui déployé toutes les ressources hello dans l’ordre correct de hello. toodelete une solution, vous aviez toodelete chaque ressource individuellement. Il était difficile d’appliquer et de mettre à jour des stratégies de contrôle d’accès pour des ressources liées. Enfin, vous ne pouvez pas appliquer balises tooresources toolabel les termes du contrat qui vous aident à surveiller vos ressources et que vous gérez la facturation.

En 2014, Azure introduit le Gestionnaire de ressources qui a ajouté le concept de hello d’un groupe de ressources. Un groupe de ressources est un conteneur de ressources qui partagent un cycle de vie commun. modèle de déploiement du Gestionnaire de ressources Hello offre plusieurs avantages :

- Vous pouvez déployer, gérer et surveiller tous les services hello pour votre solution en tant qu’un groupe, au lieu de gérer ces services individuellement.

- Vous pouvez déployer votre solution à plusieurs reprises tout au long de son cycle de vie et avoir ainsi l’assurance que vos ressources présentent un état cohérent lors de leur déploiement.

- Vous pouvez appliquer tooall contrôler les accès aux ressources dans votre groupe de ressources, et ces stratégies sont appliquées automatiquement lorsque de nouvelles ressources sont ajoutés à groupe de ressources toohello.

- Vous pouvez appliquer des balises tooresources toologically organiser toutes les ressources hello dans votre abonnement.

- Vous pouvez utiliser l’infrastructure de hello toodefine JavaScript Objet Notation (JSON) pour votre solution. fichier JSON de Hello est connu en tant que gestionnaire de ressources du modèle.

- Vous pouvez définir des dépendances de hello entre les ressources de sorte qu’ils sont déployés dans l’ordre correct de hello.

![Gestion des ressources](./media/governance-in-azure/security-governance-in-azure-fig4.png)

Le Gestionnaire de ressources vous permet de tooput ressources en groupes explicites pour l’affinité de facturation ou naturel de gestion. Comme mentionné précédemment, Azure dispose de deux modèles de déploiement. Bonjour précédemment [modèle classique](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model), unité de gestion de base hello a été abonnement de hello. Il était difficile toobreak vers le bas des ressources au sein d’un abonnement ayant entraîné la création d’un grand nombre d’abonnements toohello. Avec le modèle de gestionnaire de ressources hello, nous avons vu introduction hello des groupes de ressources.

Un groupe de ressources est un conteneur réunissant les ressources associées d’une solution Azure. [groupe de ressources Hello](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) peut inclure toutes les ressources de hello pour les solutions hello ou uniquement les ressources que vous souhaitez toomanage en tant que groupe. Vous décidez comment vous souhaitez que les ressources de tooallocate tooresource groupes en fonction de ce que hello plus logique pour votre organisation.

Pour des recommandations sur les modèles, voir [Bonnes pratiques relatives à la création de modèles Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices).

Azure Resource Manager analyse les dépendances des ressources de tooensure sont créés dans l’ordre correct de hello. Si une ressource dépend d’une valeur d’une autre ressource (par exemple, une machine virtuelle ayant besoin d’un compte de stockage pour les disques), vous devez définir une dépendance.

>[!Note]
>Pour plus d’informations, consultez [Définition de dépendances dans des modèles Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-define-dependencies).

Vous pouvez également utiliser le modèle de hello pour infrastructure toohello des mises à jour. Par exemple, vous pouvez ajouter une solution tooyour de ressources et ajouter des règles de configuration pour les ressources de hello qui sont déjà déployées. Si le modèle de hello spécifie la création d’une ressource, mais que la ressource existe déjà, le Gestionnaire de ressources Azure effectue une mise à jour au lieu de créer un nouvel élément multimédia. Azure Resource Manager les mises à jour hello existant asset toohello même état tel qu’il serait en tant que nouveaux.

Le Gestionnaire de ressources fournit des extensions pour les scénarios lorsque vous avez besoin d’autres opérations telles que l’installation du logiciel qui n’est pas inclus dans le programme d’installation hello.

## <a name="resource-tracking"></a>Suivi des ressources

Les utilisateurs de votre organisation ajoutent l’abonnement aux ressources de toohello, il devient tooassociate plus en plus importante des ressources avec le service approprié de hello, client et l’environnement. Vous pouvez attacher tooresources de métadonnées via des balises. Vous utilisez [balises](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) tooprovide plus d’informations sur la ressource de hello ou un propriétaire de hello. Balises vous permettent de toonot uniquement d’agrégation et les ressources du groupe de plusieurs façons, mais utilisent ces données à des fins hello de rétrofacturation.

Utiliser des balises lorsque vous avez un ensemble complexe de groupes de ressources et de ressources, devez toovisualize ces ressources de manière hello qui rend hello la plupart des tooyou de sens. Par exemple, vous pouvez baliser des ressources qui servent un rôle similaire dans votre organisation ou appartiennent toohello même service.

Sans les balises, les utilisateurs de votre organisation peuvent créer plusieurs ressources qui peuvent être difficile toolater identifient et gérer. Par exemple, vous souhaiterez toodelete toutes les ressources hello pour un projet. Si ces ressources ne sont pas marqués pour le projet de hello, vous devez manuellement les trouver. Le balisage peut être un moyen important pour vous tooreduce des coûts inutiles dans votre abonnement.

Ressources n’est pas nécessaire de tooreside Bonjour tooshare de groupe de ressources même une balise. Vous pouvez créer votre propre tooensure de taxonomie balise que tous les utilisateurs de votre organisation utilisent courantes balises plutôt que les utilisateurs de l’application par inadvertance des balises légèrement différentes (par exemple, « dept » au lieu de « département »).

Stratégies de ressources permettent de toocreate de règles standard pour votre organisation. Vous pouvez créer des stratégies qui garantissent que les ressources sont balisés avec des valeurs appropriées de hello.

> [!Note]
> Pour plus d’informations, consultez [Appliquer des stratégies de ressources pour les balises](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags).

Vous pouvez également afficher des ressources avec balises via hello portail Azure.

Hello [rapport d’utilisation](https://docs.microsoft.com/azure/billing/billing-understand-your-bill) pour votre abonnement inclut les noms de balise et les valeurs, qui vous permet de toobreak les coûts par des balises.

> [!Note]
> Pour plus d’informations sur les balises, consultez [à l’aide des balises tooorganize vos ressources Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

Hello limites suivantes s’appliquent à tootags :

- Chaque ressource ou groupe de ressources peut inclure un maximum de 15 paires clé/valeur de balise. Cette limitation s’applique uniquement tootags appliquées directement toohello ressource groupe ou une ressource. Un groupe de ressources peut contenir de nombreuses ressources qui ont chacune 15 paires clé/valeur de balise.

- nom de la balise Hello est limitée too512 caractères.

- valeur de balise Hello est limitée too256 caractères.

- Groupe de ressources toohello balises appliquées ne sont pas héritées par les ressources hello dans ce groupe de ressources.

Si vous avez plus de 15 valeurs que vous avez besoin de tooassociate avec une ressource, utilisez une chaîne JSON pour la valeur de balise hello. Hello chaîne JSON peut contenir plusieurs valeurs qui sont la clé de balise unique tooa appliqué.

### <a name="tags-and-billing"></a>Balises et facturation

Balises activer vous toogroup vos données de facturation. Par exemple, si vous exécutez plusieurs ordinateurs virtuels pour différentes organisations, vous pouvez utiliser hello balises toogroup utilisation par centre de coûts. Vous pouvez également utiliser des balises toocategorize coûts par l’environnement d’exécution ; hello, telles que l’utilisation de facturation pour les machines virtuelles en cours d’exécution dans un environnement de production.

Vous pouvez récupérer des informations sur les balises via hello [l’utilisation des ressources Azure et RateCard APIs](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview) ou un fichier de valeurs séparées par des virgules (CSV) de l’utilisation de hello. Vous téléchargez le fichier de l’utilisation de hello de hello [portail des comptes Azure](https://account.windowsazure.com/) ou [portal d’EA](https://ea.azure.com/).

>[!Note]
> Pour plus d’informations sur les informations de toobilling l’accès par programme, consultez [obtenir votre consommation de ressources Microsoft Azure](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview). Pour plus d’informations sur les opérations de l’API REST, consultez [Informations de référence sur l’API REST Azure Billing](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).

Lorsque vous téléchargez l’utilisation de hello volume partagé de cluster pour les services qui prennent en charge les balises de facturation, hello apparaissent dans la colonne de balises hello.

## <a name="critical-resource-controls"></a>Contrôles des ressources critiques

Quand votre organisation ajoute un abonnement de toohello core services, il devient tooensure plus en plus important que ces services sont disponibles tooavoid interruption de service. [Verrous de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources) vous activer les opérations de toorestrict sur les ressources de valeur élevée où suppression ou leur modification aurait un impact significatif sur vos applications ou d’une infrastructure cloud. Vous pouvez appliquer des verrous tooa abonnement, groupe de ressources ou ressource. En règle générale, vous appliquez des ressources de toofoundational de verrous, telles que les réseaux virtuels, les passerelles et les comptes de stockage.

Les verrous de ressource prennent actuellement en charge deux valeurs : CanNotDelete et ReadOnly. CanNotDelete signifie que les utilisateurs (avec les droits appropriés hello) peuvent toujours lire ou modifier une ressource, mais ne peut le supprimer. ReadOnly signifie que les utilisateurs autorisés ne peuvent pas supprimer ou modifier une ressource.

Verrous de gestionnaire de ressources s’appliquent uniquement aux toooperations qui se produisent dans le plan de gestion de hello, qui se compose d’opérations envoyées trop<https://management.azure.com>. les verrous hello ne limitent pas la façon dont les ressources effectuent leurs propres fonctions. Les modifications des ressources sont limitées, mais pas les opérations sur les ressources. Par exemple, un verrou en lecture seule sur une base de données SQL vous empêche de supprimer ou modifier la base de données hello, mais il ne vous empêche pas de création, mise à jour ou supprimer des données dans la base de données hello.

Application **ReadOnly** peut entraîner des résultats de toounexpected, car certaines opérations semblent lire opérations requièrent des actions supplémentaires. Par exemple, placer un **ReadOnly** verrou sur un compte de stockage empêche tous les utilisateurs d’afficher la liste des clés de hello. liste Hello opération clés est gérée via une demande POST car hello retourné clés sont disponibles pour les opérations d’écriture.

![Contrôles des ressources critiques](./media/governance-in-azure/security-governance-in-azure-fig5.png)

Pour un autre exemple, placer un verrou en lecture seule sur une ressource du Service d’applications empêche l’Explorateur de serveurs Visual Studio à partir de l’affichage des fichiers pour la ressource de hello, car cette interaction nécessite un accès en écriture.

Contrairement au contrôle d’accès basé sur un rôle, vous utilisez Gestion des verrous tooapply une restriction sur tous les utilisateurs et les rôles. toolearn sur la définition des autorisations pour les utilisateurs et les rôles, consultez [Azure Role-based Access Control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure).

Lorsque vous appliquez un verrou sur une portée parent, toutes les ressources dans cette étendue héritent hello même verrou. Même les ressources que vous ajouterez ultérieurement héritent de verrou de hello parent de hello. verrou de Hello plus restrictif dans l’héritage hello est prioritaire.

toocreate ou supprimer les verrous de gestion, vous devez avoir accès tooMicrosoft.Authorization/ _ou Microsoft.Authorization/locks/_ actions. Hello rôles intégrés uniquement **propriétaire** et **administrateur de l’accès utilisateur** sont accordées à ces actions.

## <a name="api-access-toobilling-information"></a>Informations de toobilling accès API

Utilisez les données d’utilisation et de la ressource toopull API de facturation d’Azure à vos outils d’analyse de données par défaut. Hello l’utilisation des ressources Azure et RateCard APIs peuvent vous aider à prévoir avec précision et de gérer les coûts. Hello API sont implémentés en tant qu’un fournisseur de ressources et la partie de la famille hello d’API exposées par hello Azure Resource Manager.

### <a name="azure-resource-usage-api-preview"></a>API Azure Resource Usage (préversion)

Hello d’utiliser Azure [API de l’utilisation des ressources](https://msdn.microsoft.com/library/azure/mt219003) tooget vos données de consommation Azure estimée. Hello API inclut :

- **Role-based Access Control de Azure** -configurer l’accès à des stratégies sur hello [portail Azure](https://portal.azure.com/) ou via [applets de commande Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview) toospecify les utilisateurs ou les applications peut accéder données d’utilisation de l’abonnement toohello. Les appelants doivent utiliser les jetons Azure Active Directory standard pour l’authentification. Ajoutez hello appelant tooeither hello du lecteur de facturation, lecteur, le propriétaire ou contributeur rôle tooget accès toohello données d’utilisation pour un abonnement Azure spécifique.

- **Agrégations horaires ou quotidiennes** : les appelants peuvent indiquer s’ils souhaitent visualiser leurs données d’utilisation Azure par intervalles de temps horaires ou quotidiens. valeur par défaut Hello est quotidienne.

- **Métadonnées de l’instance (y compris les balises de ressources)** – obtenir des détails au niveau de l’instance comme hello uri de ressource complet (/subscriptions/ {id d’abonnement} /...), hello des informations sur les groupes de ressources et les balises de ressources. Ces métadonnées vous permet de façon déterministe et allouer par programmation de l’utilisation par des balises hello, pour les cas d’usage, comme la charge entre.

- **Métadonnées des ressources** -détails de la ressource comme nom de compteur hello, catégorie de compteur, sous-catégorie de jauge, unité et région donner à l’appelant de hello une meilleure compréhension de ce qui a été consommé. Nous travaillons également la terminologie de métadonnées tooalign ressource hello portail Azure, Azure utilisation CSV, EA CSV, de facturation et autres expériences publics, toolet vous corréler les données des expériences.

- **Utilisation pour tous les types d’offre** : les données d’utilisation sont accessibles pour tous les types d’offre, tels que Paiement à l’utilisation, MSDN, Engagement monétaire, Crédit monétaire et Contrat Entreprise (EA).

**API Azure Resource RateCard (préversion)**

Utilisez hello API RateCard de ressources Azure tooget hello la liste des ressources Azure disponibles et estimé des informations de tarification pour chacun. Hello API inclut :

- **Contrôle d’accès en fonction du rôle Azure** - configurer vos stratégies d’accès sur hello portail Azure ou via toospecify d’applets de commande Azure PowerShell que les utilisateurs ou les applications peuvent obtenir accéder toohello RateCard données. Les appelants doivent utiliser les jetons Azure Active Directory standard pour l’authentification. Ajoutez hello appelant tooeither hello du lecteur, le propriétaire ou contributeur rôle tooget accès toohello données d’utilisation pour un abonnement Azure spécifique.

- **Prise en charge des offres Paiement à l’utilisation, MSDN, Engagement monétaire et Crédit monétaire (offre EA non prise en charge)** : cette API fournit des informations de tarif au niveau des offres Azure. appelant Hello de cette API doit passer taux et les détails de la ressource tooget informations offre hello. Nous sommes taux d’EA tooprovide actuellement impossible, car les offres EA personnalisé taux par l’inscription. Voici quelques scénarios hello sont rendues possibles avec une combinaison de hello de hello d’utilisation et hello RateCard APIs :

- **Azure dépenses au cours des mois de hello** -combinaison de hello d’utilisation de hello d’utilisation et RateCard APIs tooget mieux appréhender votre cloud dépenses au cours des mois de hello. Vous pouvez analyser toutes les heures hello et des estimations de compartiments quotidiennes de l’utilisation et la facturation.

- **Configurer des alertes** : hello d’utilisation et hello RateCard APIs tooget estimée de la consommation de cloud et les frais, configurer des alertes basée monétaire ou ressource.

- **Prédire la facture** – Get votre consommation estimée cloud dépenses et appliquer d’apprentissage algorithmes toopredict quel facture hello serait à fin hello Hello cycle de facturation.

- **Avant la consommation de l’analyse du coût** – utilisez hello RateCard API toopredict est la quantité de votre facture serait pour votre utilisation attendue lorsque vous déplacez votre tooAzure les charges de travail. Si vous avez des charges de travail existantes dans d’autres clouds ou les clouds privés, vous pouvez également mapper votre utilisation avec tooget de taux Azure hello passent d’une meilleure estimation de Azure. Cela donne estimation hello toopivot de capacité sur l’offre et de comparaison entre les types d’autre offre hello au-delà de paiement à l’utilisation, telles qu’engagement et crédit. Hello API vous donne également hello capacité toosee coût différences par région et vous permet de toodo un toohelp d’analyse de simulation coût décisions de déploiement.

- **Analyse de simulation** -vous pouvez déterminer s’il est plus économique toorun les charges de travail dans une autre région ou dans une autre configuration de ressource Azure de hello. Ressource Azure, les coûts peuvent différer selon hello région Azure que vous utilisez.

- Vous pouvez également déterminer si un autre type d’offre Azure propose un meilleur tarif pour une ressource Azure.

## <a name="networking-controls"></a>Contrôles de mise en réseau

Accès tooresources peuvent être externes ou internes (dans le réseau de l’entreprise hello) (via hello internet). Il est facile pour les utilisateurs dans votre organisation tooinadvertently put ressources place incorrect de hello et potentiellement ouvrir toomalicious accès. Comme avec localement / appareils, les entreprises doivent ajouter tooensure contrôles appropriés que les utilisateurs Azure décisions hello appropriées.

![Contrôles de mise en réseau](./media/governance-in-azure/security-governance-in-azure-fig6.png)

Pour la gouvernance de l’abonnement, nous identifions des ressources principales qui fournissent le contrôle d’accès de base. ressources principales du Hello sont constitués de :

### <a name="network-connectivity"></a>Connectivité réseau

Les [réseaux virtuels](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) sont des objets Conteneur de sous-réseaux. S’il est absolument nécessaire, il est souvent utilisé lors de la connexion des applications toointernal des ressources d’entreprise. Bonjour permet de service de réseau virtuel Azure vous toosecurely connecter des ressources Azure tooeach autres avec des réseaux virtuels (réseaux virtuels).

Un réseau virtuel est une représentation de votre propre réseau dans le cloud de hello. Un réseau virtuel est une isolation logique de hello Azure cloud dédié tooyour abonnement. Vous pouvez également connecter le réseau local de tooyour des réseaux virtuels.

Voici les fonctionnalités des réseaux virtuels Azure :

- **Isolement** : les réseaux virtuels sont isolés les uns des autres. Vous pouvez créer des réseaux virtuels distincts pour le développement, test et de production que hello utilisez mêmes blocs d’adresses CIDR. À l’inverse, vous pouvez créer plusieurs réseaux virtuels qui utilisent différents blocs d’adresses CIDR et connecter les réseaux entre eux. Vous pouvez segmenter un réseau virtuel en plusieurs sous-réseaux. Azure fournit la résolution de noms interne pour les machines virtuelles et instances de rôle Services de cloud computing connecté tooa réseau virtuel. Vous pouvez éventuellement configurer un réseau virtuel toouse vos propres serveurs DNS, au lieu d’utiliser la résolution de noms interne Azure.

- **Connectivité Internet**: instances de rôle de tous les Azure Machines virtuelles (VM) et les Services de cloud computing tooa connecté réseau virtuel ont accèdent toohello Internet, par défaut. Vous pouvez également activer des ressources toospecific accès entrant, en fonction des besoins.

- **Connectivité de la ressource Azure**: ressources Azure telles que les Services de cloud computing et machines virtuelles peuvent être connecté toohello même réseau virtuel. ressources de Hello peuvent se connecter tooeach autres privé adresses IP, même si elles sont dans des sous-réseaux différents. Azure fournit par défaut le routage entre sous-réseaux, les réseaux virtuels et sur des réseaux locaux, afin que vous n’avez tooconfigure et gérer les itinéraires.

- **Connectivité de réseau virtuel**: réseaux virtuels peuvent être connectée tooeach autres, l’activation de ressources connecté toocommunicate de réseau virtuel tooany avec n’importe quelle ressource sur n’importe quel autre réseau virtuel.

- **Connectivité locale**: réseaux virtuels peuvent être connectés tooon des réseaux locaux par le biais des connexions de réseau privé entre votre réseau et Azure, ou via une connexion VPN de site à site sur Internet de hello.

- **Filtrage du trafic** : le trafic réseau entrant et sortant des machines virtuelles et des instances de rôle Services cloud peut être filtré par adresse IP source et port, adresse IP de destination et port, et protocole.

- **Routage** : vous pouvez également remplacer le routage Azure par défaut en configurant votre propre routage ou en utilisant des itinéraires BGP via une passerelle réseau.

## <a name="network-access-controls"></a>Contrôles d’accès réseau

[Groupes de sécurité réseau](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) sont telles qu’un pare-feu et de fournir de la façon dont une ressource peut « communiquer » avec des règles de réseau hello. Ils fournissent un contrôle granulaire sur la façon / si un sous-réseau (ou un ordinateur virtuel) peut se connecter toohello Internet ou autres sous-réseaux dans hello même réseau virtuel.

Un groupe de sécurité réseau (NSG) contient une liste de règles de sécurité qui autorisent ou refusent tooresources de trafic réseau connecté tooAzure de réseaux virtuels (VNet). Groupes de sécurité réseau peuvent être associé toosubnets, des ordinateurs virtuels individuels (classique), ou l’interface réseau (NIC) attaché tooVMs (Resource Manager).

Lorsqu’un groupe de sécurité réseau est associé tooa sous-réseau, les règles de hello s’appliquent tooall ressources toohello connecté sous-réseau. Le trafic peut encore être limité en également associer un tooa groupe de sécurité réseau de machine virtuelle ou la carte réseau.

## <a name="security-and-continuous-compliance-with-organizational-standards"></a>Sécurité et conformité continue aux normes de l’organisation

Chaque entreprise a des besoins différents et tire des avantages différents des solutions cloud. Néanmoins, les clients de tous les types ont hello mêmes questions de base sur le déplacement toohello cloud. Ils veulent contrôle tooretain de leurs données, et qu’ils souhaitent que toobe de données conservée sécurisée et privée, tout en maintenant la transparence et la conformité.

Voici ce que les clients veulent obtenir des fournisseurs de solutions cloud :

- **Sécuriser les données de notre** lors de l’accusé de réception que le cloud de hello peut fournir une augmentation de la sécurité des données et contrôle administratif, les responsables informatiques sont toujours concernées par qui migration toohello cloud les laisse toohackers plus vulnérables à leur actuellement solutions internes.

- **Maintenir la confidentialité des données** : les services cloud représentent des défis uniques pour les entreprises en termes de confidentialité. Comme les entreprises rechercher toohello cloud toosave les coûts d’infrastructure et améliorent leur flexibilité, ils soucier également toute perte de contrôle d’où leurs données sont stockées, qui accède à, et comment il obtient utilisé.

- **Faites-nous part de contrôle** même quand ils tirer parti de hello cloud toodeploy de plusieurs solutions innovantes, les entreprises sont très inquiet de la perte de contrôle de leurs données. fournir des informations récentes Hello des agences gouvernementales l’accès aux données client, par des moyens juridiques et très juridiques, assurez-vous des directeurs ne pas stocker leurs données dans le cloud de hello.

- **Promouvoir la transparence** alors que sécurité et confidentialité contrôle sont importantes toobusiness décideurs, ils veulent également la possibilité de hello tooindependently vérifier comment leurs données sont stockées, utilisées et sécurisées.

- **Conserver la conformité** élargissement de leur utilisation des technologies de cloud computing, la complexité de hello et l’étendue des normes et réglementations continuent tooevolve. Les entreprises doivent tooknow leurs normes de conformité sont atteints, et cette conformité va-t-il comme modification réglementations au fil du temps.

## <a name="security-configuration-monitoring-and-alerting"></a>Configuration de la sécurité, monitoring et alertes

Les abonnés Azure peuvent gérer leurs environnements cloud à partir de différents périphériques, comme les stations de travail de gestion, les ordinateurs de développement ou encore les périphériques d’utilisateurs finaux privilégiés, qui disposent d’autorisations spécifiques. Dans certains cas, les fonctions d’administration sont effectuées via le web basée sur les consoles telles que hello portail Azure. Dans d’autres cas, il peut être tooAzure des connexions directes à partir des systèmes locaux réseaux privés virtuels (VPN), les Services Terminal Server, les protocoles d’application client ou (par programmation) hello API de gestion de Service Azure (SMAPI). Par ailleurs, les points de terminaison de client peuvent être joints au domaine ou isolés et non gérés, comme les tablettes ou les smartphones.

Bien que plusieurs fonctionnalités d’accès et l’administration fournissent un riche ensemble d’options, variabilité peut ajouter un déploiement de cloud tooa risque. Il peut être difficile toomanage, suivre et auditer les actions d’administration. Variabilité peut-être également introduire des menaces de sécurité via l’accès non réglementées tooclient points de terminaison qui sont utilisés pour la gestion des services de cloud computing. Les stations de travail personnelles ou communes destinées au développement et à la gestion de l’infrastructure introduisent des menaces imprévisibles, notamment avec la navigation Web (par exemple, lors d’attaques de point d’eau) ou la messagerie électronique (par exemple, ingénierie sociale et hameçonnage).

Surveillance, la journalisation et audit fournissent une base pour le suivi et la présentation des activités d’administration, mais il peut être pas toujours possible tooaudit toutes les actions de terminer le détail due toohello de données générées. L’audit de l’efficacité des stratégies de gestion hello hello n’est cependant recommandé.

Gouvernance de sécurité Azure à partir de la stratégie de groupe AD DS toocontrol Windows de tous les administrateurs hello interfaces, telles que le partage de fichiers. Incluez les stations de travail de gestion dans l’audit, la surveillance et la journalisation. Effectuez le suivi des accès et de l’utilisation au niveau administrateur et développeur.

### <a name="azure-security-center"></a>Azure Security Center

Hello [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) fournit une vue centralisée de l’état de la sécurité des ressources dans les abonnements hello hello et fournit des recommandations qui permettent d’éviter les compromis de ressources. Elle peut activer des stratégies plus précis (par exemple, application stratégies toospecific groupes de ressources qui permettent de hello entreprise tootailor risque toohello posture qu'ils résolvent).

![Azure Security Center](./media/governance-in-azure/security-governance-in-azure-fig7.png)

Security Center fournit une surveillance de la sécurité et une gestion des stratégies intégrées pour l’ensemble de vos abonnements Azure, vous aidant ainsi à détecter les menaces qui pourraient passer inaperçues. De plus, il est compatible avec un vaste écosystème de solutions de sécurité. Après avoir activé [des stratégies de sécurité](https://docs.microsoft.com/azure/security-center/security-center-policies) pour les ressources d’un abonnement, le centre de sécurité analyse la sécurité de hello des vulnérabilités potentielles tooidentify ressources. Les informations sur la configuration du réseau sont instantanément disponibles.

Azure Security Center constitue une combinaison des meilleures pratiques en matière d’analyse et de gestion de la stratégie de sécurité pour toutes les ressources dans un abonnement Azure. Cet outil puissant et facile toouse permet aux équipes de sécurité et tooprevent aux personnes chargées de risque, détecter, répondre toosecurity menaces comme elle collecte et analyse les données de sécurité de vos ressources Azure, hello réseau et les solutions de partenaire comme automatiquement les programmes malveillants et les pare-feu.

En outre, Azure Security Center s’applique analytique avancée, y compris d’apprentissage automatique et analyse comportementale tout en tirant parti des menaces global à partir de Microsoft hello de produits et services, hello Microsoft Digital Crimes unité (DCU), Microsoft Centre de réponse de sécurité (MSRC) et les flux externes. [Gouvernance de sécurité](https://www.credera.com/blog/credera-site/azure-governance-part-4-other-tools-in-the-toolbox/) peuvent être appliquées globalement au niveau d’abonnement hello ou toospecific, exigences granulaire appliquées tooindividual affinée des ressources via la définition de la stratégie.

Enfin, Azure Security Center analyse l’intégrité des ressources sécurité basée sur les stratégies et utilise cette tooprovide développent les tableaux de bord et les alertes pour les événements tels que la détection des logiciels malveillants ou les connexions IP malveillantes de tentatives.

>[!Note]
> Pour plus d’informations sur la façon tooapply recommandations, lire [mise en œuvre des recommandations de sécurité dans le centre de sécurité Azure](https://docs.microsoft.com/azure/security-center/security-center-recommendations).

Centre de sécurité collecte les données de vos machines virtuelles de tooassess leur état de sécurité, fournir des recommandations de sécurité et vous alerter toothreats. Lorsque vous accédez au Centre de sécurité pour la première fois, la collecte de données est activée sur toutes les machines virtuelles de votre abonnement. Collecte de données est recommandée, mais vous pouvez annuler par [la désactivation de la collecte des données](https://docs.microsoft.com/azure/security-center/security-center-faq) Bonjour stratégie du centre de sécurité.

Enfin, le centre de sécurité Azure est une plateforme ouverte qui permet aux partenaires de Microsoft et logiciels fournisseurs toocreate logiciel qui se connecte au centre de sécurité Azure tooenhance de ses fonctionnalités.

Centre de sécurité Azure surveille hello suivant des ressources Azure :

- Machines virtuelles (notamment les services cloud)

- Réseaux virtuels Azure

- Service SQL Azure

- Solutions de partenaires intégrées à votre abonnement Azure, par exemple un pare-feu d’applications web sur les machines virtuelles et sur [App Service Environment](https://docs.microsoft.com/azure/app-service/app-service-app-service-environments-readme).

### <a name="operations-management-suite"></a>Operations Management Suite

Hello du développement du logiciel OMS et la sécurité des informations de l’équipe de service et [programme de gouvernance](https://github.com/Microsoft/azure-docs/blob/master/articles/log-analytics/log-analytics-security.md) prend en charge ses besoins et respecte les réglementations et toolaws comme décrit dans [Microsoft Azure Trust Center ](https://azure.microsoft.com/support/trust-center/) et [Microsoft Trust Center conformité](https://www.microsoft.com/TrustCenter/Compliance/default.aspx). Ceux-ci expliquent également comment OMS fixe les exigences de sécurité, identifie les contrôles de sécurité, et gère et analyse les risques. Chaque année, nous révisons les stratégies, normes, procédures et directives.

Chaque membre de l’équipe de développement d’OMS reçoit une formation formelle en matière de sécurité des applications. En interne, nous utilisons un système de contrôle de version pour le développement de logiciels. Chaque projet de logiciel est protégé par le système de contrôle de version hello.

Microsoft dispose d’une équipe dédiée à la sécurité et à la conformité, qui surveille et évalue tous les services en son sein. Responsables de la sécurité des informations constituent les équipe hello et ne sont pas associés avec hello départements développement OMS d’ingénierie. responsables de la sécurité Hello ont leur propre chaîne de gestion et effectuer des évaluations de produits et de sécurité tooensure de services et de conformité indépendantes.

Operations Management Suite (également appelé OMS) est une collection de services de gestion qui ont été conçus dans le cloud hello du début de hello. Plutôt que de déployer et de gérer des ressources locales, les composants OMS sont entièrement hébergés dans Azure. OMS ne requiert qu’une configuration minime et vous permet d’être opérationnel en quelques minutes seulement.

![Operations Manager Suite](./media/governance-in-azure/security-governance-in-azure-fig8.png)

Le fait qu’OMS services s’exécutent dans cloud de hello ne signifie pas qu’ils ne peuvent pas gérer efficacement votre environnement local.

Place un agent sur toutes les fenêtres ou ordinateur Linux dans votre centre de données et il enverra tooLog données Analytique où il peut être analysé, ainsi que toutes les autres données collectées à partir du cloud ou sur les services locaux. Utiliser le cloud de hello tooleverage Azure Backup et Azure Site Recovery pour la sauvegarde et la haute disponibilité pour les ressources de site.

Procédures opérationnelles dans le cloud de hello ne peut pas accéder en général de vos ressources locales, mais vous pouvez installer un agent sur un ou plusieurs ordinateurs trop qui hébergera les runbooks dans votre centre de données. Lorsque vous démarrez un runbook, vous spécifiez simplement si vous souhaitez toorun dans le cloud de hello ou sur un thread de travail local.

fonctionnalités principales de Hello d’OMS sont fournie par un ensemble de services qui s’exécutent dans Azure. Chaque service fournit une fonction de gestion spécifique, et vous pouvez combiner des scénarios de gestion de services tooachieve.

![Operations Manager Suite](./media/governance-in-azure/security-governance-in-azure-fig9.JPG)

Azure Operation Manager étend ses fonctionnalités en fournissant des solutions de gestion. Les [solutions de gestion](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solutions) constituent des ensembles de logiques prépackagés qui implémentent un scénario de gestion tirant profit d’un ou de plusieurs services OMS.

![Gestion des opérations Azure](./media/governance-in-azure/security-governance-in-azure-fig10.png)

Différentes solutions sont disponibles à partir de Microsoft et de partenaires que vous pouvez facilement ajouter valeur de hello tooincrease tooyour abonnement Azure de votre investissement dans OMS.

En tant que partenaire, vous pouvez créer vos propres solutions toosupport vos applications et services et les fournir toousers via hello Azure Marketplace ou modèles de démarrage rapide.

## <a name="performance-alerting-and-monitoring"></a>Alertes et monitoring relatifs aux performances

### <a name="alerting"></a>Génération d’alertes

Les alertes sont une méthode d’analyse des mesures des ressources événements ou journaux Azure, puis d’avertissement quand une condition spécifiée est remplie.

**Alertes dans différents services Azure**

Les alertes sont disponibles dans différents services, notamment les suivants :

- Application Insights : prend en charge les tests web et les alertes de mesure.

>[!Note]
> Consultez [Définir des alertes dans Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-alerts) et [Analyser la disponibilité et la réactivité d’un site web](https://docs.microsoft.com/azure/application-insights/app-insights-monitor-web-app-availability).

- Analytique de journal (Operations Management Suite) : Active le routage de hello d’activité et des journaux de Diagnostic tooLog Analytique. Operations Management Suite autorise les alertes de mesure, de journal, etc.

>[!Note]
> Pour plus d’informations, consultez Alertes dans [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-alerts).

- Azure Monitor : prend en charge les alertes sur la base de valeurs de mesures et d’événements de journal d’activité. Vous pouvez utiliser hello [API REST de Azure moniteur](https://msdn.microsoft.com/library/dn931943.aspx) toomanage alertes.

>[!Note]
> Pour plus d’informations, consultez [à l’aide de hello portail Azure, PowerShell ou les alertes de toocreate une interface de ligne de hello](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-alerts-portal).

### <a name="monitoring"></a>Surveillance

Les problèmes de performances dans votre application cloud peuvent affecter votre entreprise. Avec plusieurs composants interconnectés et de nouvelles versions fréquentes, des dégradations peuvent se produire à tout moment. Et si vous développez une application, vos utilisateurs découvrent généralement des problèmes que vous n’avez pas trouvés dans le test. Vous devez savoir immédiatement sur ces problèmes et disposer des outils de diagnostic et résolution des problèmes de hello. Microsoft Azure a une gamme d’outils permettant d’identifier ces problèmes.

**Comment surveiller mes applications cloud Azure ?**

Il existe une gamme d’outils pour la surveillance des services et applications Azure. Certaines de leurs fonctionnalités se chevauchent. C’est en partie pour des raisons historiques et en partie en raison de toohello flou entre le développement et le fonctionnement d’une application.

Voici les outils principaux hello :

- **Azure Monitor** est l’outil de base pour la surveillance des services s’exécutant sur Azure. Il vous fournit des données de niveau de l’infrastructure sur débit hello d’un service et un hello entourant l’environnement. Si vous gérez vos applications dans Azure, vous décidez si tooscale vers le haut ou vers le bas des ressources, analyse d’Azure vous donne ensuite ce que vous utilisez toostart.

- **Application Insights** peut être utilisé pour le développement et comme solution de surveillance de la production. Il fonctionne en installant un package dans votre application et vous donne donc une vue plus interne de ce qui se passe. Ses données comprennent les temps de réponse des dépendances, les traces des exceptions, le débogage des captures instantanées et les profils d’exécution. Il fournit des outils de smart puissants pour l’analyse de ces données de télémétrie deux toohelp vous déboguez une application et les toohelp vous comprenez ce que font les utilisateurs avec lui. Vous pouvez savoir si un pic dans le temps de réponse échéance toosomething dans une application ou un problème passait externe. Si vous utilisez Visual Studio et l’application hello est en cause, vous pouvez dirigé toohello droite problème ou les lignes de code pour vous pouvez de le résoudre.

- **Ouvrez une session Analytique** est destiné à ceux qui ont besoin de maintenance de plan et de performances tootune sur les applications qui s’exécutent en production. Il est basé dans Azure. Il collecte et agrège les données de nombreuses sources, mais avec un délai de 10 minutes too15. Il fournit une solution de gestion informatique globale holistique pour Azure, en local et dans les infrastructures cloud tierces (par exemple, Amazon Web Services). Fournit des outils plus riches tooanalyze données sur d’autres sources, permet des requêtes complexes sur tous les journaux et pouvez alertes sur les conditions spécifiées. Vous pouvez même collecter des données personnalisées dans son référentiel central pour les interroger et visualiser.

- **System Center Operations Manager (SCOM)** pour gérer et surveiller les installations cloud à grande échelle. Vous le connaissez peut-être déjà comme outil de gestion local pour Windows Server en local et les solutions cloud basées sur Hyper-V, mais il peut également s’intégrer à et gérer des applications Azure. Entre autres choses, il peut installer Application Insights sur des applications en direct existantes. Si une application est en panne, vous en êtes informé sous quelques secondes.


## <a name="next-steps"></a>Étapes suivantes

- [Meilleures pratiques relatives à la création de modèles Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices).

- [Exemples d’implémentation de la gouvernance des abonnements Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-subscription-examples).

- [Microsoft Azure Government](https://docs.microsoft.com/azure/azure-government/).
