---
title: concepts de laboratoires aaaDevTest | Documents Microsoft
description: "Découvrez les concepts de base hello de DevTest Labs et comment il peut rendre toocreate facile, gérer et surveiller des machines virtuelles"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 105919e8-3617-4ce3-a29f-a289fa608fb2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: d9f1d948002c4d3121e5bdd4e65eb8b54cd91f9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="devtest-labs-concepts"></a>Concepts de DevTest Labs
## <a name="overview"></a>Vue d'ensemble
Hello suivant liste contient les définitions et les principaux concepts DevTest Labs :

## <a name="labs"></a>Laboratoires
Un laboratoire est infrastructure hello englobe un groupe de ressources, telles que les Machines virtuelles (VM), qui vous permet de mieux gérer ces ressources en spécifiant des limites et quotas.

## <a name="virtual-machine"></a>Machine virtuelle
Une machine virtuelle Azure est l’un des différents types de [ressources informatiques évolutives et à la demande](https://docs.microsoft.com/azure/app-service-web/choose-web-site-cloud-service-vm) proposés par Azure. Donnez aux machines virtuelles Azure hello flexibilité de la virtualisation sans avoir toobuy et de mettre à jour de matériel physique hello qui s’exécute, mais vous devez toujours toomaintain hello machine virtuelle en effectuant certaines tâches, telles que la configuration, la mise à jour corrective et l’installation du logiciel de hello qui s’exécute sur celui-ci.

L’article [Vue d’ensemble des machines virtuelles Windows dans Azure](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-overview) vous informe sur les points à prendre en compte avant de créer une machine virtuelle, sur sa création et sur sa gestion.

## <a name="claimable-vm"></a>Machine virtuelle revendicable
Une machine virtuelle Azure revendicable est une machine virtuelle qui peut être utilisée par n’importe quel utilisateur de laboratoire disposant d’autorisations. Un administrateur de laboratoire peut préparer les ordinateurs virtuels avec les artefacts et les images de base spécifiques et enregistrez-les tooa partagé pool. Un laboratoire peut ensuite revendication utilisateur une travail de machine virtuelle à partir du pool de hello lorsqu’ils ont besoin de l’autre avec cette configuration.

Une machine virtuelle qui est qui peuvent être réclamée tooany utilisateur n’est pas initialement affectée, mais s’afficheront dans la liste de tous les utilisateurs sous « Virtuels qui peuvent être réclamés ». Une fois une machine virtuelle est revendiquée par un utilisateur, il est déplacé vers le haut tootheir zone de « Mes machines virtuelles » et n’est plus qui peuvent être réclamés par un autre utilisateur.

## <a name="environment"></a>Environnement
Dans DevTest Labs, un environnement fait référence collection tooa de ressources Azure dans un laboratoire. [Ce billet de blog](https://blogs.msdn.microsoft.com/devtestlab/2016/11/16/connect-2016-news-for-azure-devtest-labs-azure-resource-manager-template-based-environments-vm-auto-shutdown-and-more/) explique comment toocreate les environnements de multi-VM à partir de vos modèles Azure Resource Manager.

## <a name="base-images"></a>Images de base
Les images de base sont des images de machine virtuelle avec tous les outils de hello et paramètres préinstallés et configuré tooquickly créer une machine virtuelle. Vous pouvez configurer une machine virtuelle en sélection d’une base existante et en ajoutant une tooinstall d’artefact de votre agent de test. Vous peuvent ensuite enregistrer hello configuré machine virtuelle comme une base afin que hello base peut être utilisée sans avoir un agent de test tooreinstall hello pour chaque configuration de hello machine virtuelle.

## <a name="artifacts"></a>Artefacts
Artefacts sont toodeploy utilisé et configurer votre application après qu’une machine virtuelle est configurée. Les artefacts peuvent être :

* Outils que vous souhaitez tooinstall sur hello VM - tels que les agents, Fiddler et Visual Studio.
* Actions que vous souhaitez toorun sur hello VM - telles que le clonage d’un référentiel.
* Applications que vous souhaitez tootest.

Les artefacts sont [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) fichiers JSON qui contient des instructions tooperform déploiement et d’appliquent la configuration.

## <a name="artifact-repositories"></a>Référentiels d’artefact
Les référentiels d’artefact sont des dépôts Git dans lesquels les artefacts sont archivés. Référentiels d’artefact peuvent être ajoutés toomultiple labs dans votre organisation, l’activation de réutilisation et de partage.

## <a name="formulas"></a>Formules
Les formules dans les images de toobase addition, fournissent un mécanisme pour l’approvisionnement rapide d’ordinateurs virtuels. Une formule dans DevTest Labs est une liste de toocreate utilisés des valeurs de propriété par défaut un laboratoire de machine virtuelle.
Avec des formules, machines virtuelles avec le même jeu de propriétés, telles que l’image de base, la taille, réseau virtuel et artefacts - VM de hello peuvent être créés sans avoir besoin de toospecify ces propriétés chaque fois. Lorsque vous créez une machine virtuelle à partir d’une formule, les valeurs par défaut de hello utilisable comme-est ou modifiée.

## <a name="policies"></a>Stratégies
Les stratégies vous aident à contrôler les coûts dans votre laboratoire. Par exemple, vous pouvez créer un tooautomatically stratégie arrêter les ordinateurs virtuels selon une planification définie.

## <a name="caps"></a>Limites
Majuscules est un gaspillage de toominimize mécanisme dans votre laboratoire. Par exemple, vous pouvez définir un nombre de hello toorestrict cap de machines virtuelles qui peuvent être créés par l’utilisateur, ou dans un laboratoire.

## <a name="security-levels"></a>Niveaux de sécurité
L’accès à la sécurité est déterminé par le contrôle d’accès en fonction du rôle (RBAC) d’Azure. toounderstand comment accéder aux fonctionne, il vous permet de toounderstand hello différences entre une autorisation, un rôle et une étendue définie par RBAC.

* Autorisation - une autorisation est une action spécifique de la tooa accès définie (par exemple, accès en lecture tooall virtuels).
* Rôle - un rôle est un jeu d’autorisations qui peuvent être regroupées et tooa utilisateur attribué. Par exemple, hello *propriétaire de l’abonnement* rôle dispose des ressources de tooall d’accès au sein d’un abonnement.
* Étendue : une étendue est un niveau de hiérarchie hello d’une ressource Azure, tel qu’un groupe de ressources, d’un même laboratoire ou de tout abonnement de hello.

Relevant de hello DevTest Labs, il existe deux types d’autorisations de rôles toodefine utilisateur : propriétaire du lab et l’utilisateur de laboratoire.

* Propriétaire du lab - propriétaire d’un laboratoire a accès tooany ressources lab de hello. Par conséquent, le propriétaire d’un laboratoire peut modifier des stratégies, lire et écrire les machines virtuelles, modifier le réseau virtuel de hello et ainsi de suite.
* Utilisateur de laboratoire : un utilisateur de laboratoire peut afficher toutes les ressources de laboratoire, telles que les machines virtuelles, les stratégies et les réseaux virtuels, mais il ne peut pas modifier les stratégies ou les machines virtuelles créées par d’autres utilisateurs.

toosee comment toocreate des rôles personnalisés dans DevTest Labs, consultez l’article toohello, [accorder des autorisations utilisateur stratégies de laboratoire toospecific](devtest-lab-grant-user-permissions-to-specific-lab-policies.md).

Étant donné que les étendues sont hiérarchiques, lorsqu’un utilisateur dispose d’autorisations pour une certaine étendue, il reçoit automatiquement ces autorisations pour chaque niveau d’étendue inférieur englobé. Par exemple, si un utilisateur est attribué le rôle toohello de propriétaire de l’abonnement, ils ont les ressources tooall accès dans un abonnement, notamment toutes les machines virtuelles, tous les réseaux virtuels et tous les ateliers pratiques. Par conséquent, un propriétaire d’abonnement hérite automatiquement de rôle hello du propriétaire de laboratoire. Toutefois, hello inverse n’est pas vrai. Propriétaire d’un laboratoire a lab accès tooa, qui est une étendue inférieure à un niveau d’abonnement hello. Par conséquent, un propriétaire du lab ne seront pas en mesure de toosee virtuels ou réseaux virtuels ou toutes les ressources qui sont en dehors de l’atelier de hello.

## <a name="azure-resource-manager-templates"></a>Modèles Microsoft Azure Resource Manager
Tous les hello concepts abordés dans cet article peuvent être configurés à l’aide de modèles Azure Resource Manager, qui vous permettent de définissent hello/configuration de l’infrastructure de votre solution Windows Azure et le déployer à plusieurs reprises dans un état cohérent.

[Comprendre la structure de hello et syntaxe des modèles Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates#template-format) décrit la structure de hello d’un gestionnaire de ressources Azure modèle et hello des propriétés qui sont disponibles dans hello différentes sections d’un modèle.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Étapes suivantes
[Créer un laboratoire dans DevTest Labs](devtest-lab-create-lab.md)
