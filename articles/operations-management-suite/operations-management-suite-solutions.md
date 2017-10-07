---
title: aaaSolutions Operations Management Suite (OMS) | Documents Microsoft
description: "Solutions étendent les fonctionnalités de hello Operations Management Suite (OMS) en fournissant des scénarios de gestion empaquetée que les clients peuvent ajouter tootheir espace de travail OMS.  Cet article explique comment les solutions personnalisées sont créées par les clients et partenaires."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5b5a538f1bc4b5577bec94db08bd43668bc6584a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-management-solutions-in-operations-management-suite-oms-preview"></a>Utilisation de solutions de gestion dans Operations Management Suite (OMS) (préversion)
> [!NOTE]
> Il s’agit d’une documentation préliminaire des solutions de gestion d’OMS qui sont actuellement en version préliminaire.    
> 
> 

Solutions de gestion d’étendent les fonctionnalités de hello Operations Management Suite (OMS) en fournissant des scénarios de gestion empaquetée que les clients peuvent ajouter tootheir environnement.  En outre trop[solutions fournies par Microsoft](../log-analytics/log-analytics-add-solutions.md), partenaires et les clients peuvent créer toobe de solutions de gestion utilisé dans leur propre environnement ou apportées toocustomers disponible via la Communauté de hello.

## <a name="finding-and-installing-management-solutions"></a>Recherche et installation de solutions de gestion
Il existe plusieurs méthodes de localisation et de l’installation des solutions de gestion, comme décrit dans les sections suivantes de hello.

### <a name="azure-marketplace"></a>Azure Marketplace
Solutions de gestion fournies par Microsoft et partenaires approuvés peuvent être installés à partir de hello Azure Marketplace Bonjour portail Azure.

1. Ouvrez une session dans toohello portail Azure.
2. Dans le volet gauche de hello, sélectionnez **davantage de services**.
3. Soit défiler trop**Solutions** ou type *solutions* dans hello **filtre** boîte de dialogue.
4. Cliquez sur hello **+ ajouter** bouton.
5. Rechercher des solutions qui vous intéressent en parcourant, en cliquant sur hello **filtre** bouton, ou en tapant dans hello **recherche Everthing** boîte.
6. Cliquez sur un tooview d’élément de marketplace des informations détaillées.
7. Cliquez sur **créer** tooopen hello **ajouter la Solution** volet.
8. Vous serez toorequired demandées par invite des informations telles que hello [OMS espace de travail et le compte Automation](#oms-workspace-and-automation-account) en outre toovalues pour tous les paramètres dans hello solution.
9. Cliquez sur **créer** solution de hello tooinstall.

### <a name="oms-portal"></a>Portail OMS
Des solutions de gestion fournies par Microsoft peuvent être installées à partir de hello galerie de Solutions dans le portail OMS est hello.

1. Ouvrez une session dans toohello portail OMS.
2. Cliquez sur hello **galerie des Solutions** vignette.
3. Sur la page Galerie des Solutions OMS hello en savoir plus sur chacune des solutions disponibles. Cliquez sur nom hello solution hello que vous souhaitez tooadd tooOMS.
4. Sur la page hello pour la solution hello que vous avez choisi, des informations détaillées sur les solutions hello s’affiche. Cliquez sur **Add**.
5. Une nouvelle vignette représentant hello solution que vous avez ajouté apparaît sur hello page Vue d’ensemble d’OMS et vous pouvez commencer à utiliser une fois que le service de hello OMS a traité vos données.

### <a name="azure-quickstart-templates"></a>Modèles de démarrage rapide Microsoft Azure
Membres de la Communauté de hello peuvent soumettre des tooAzure de solutions de gestion des modèles de démarrage rapide.  Vous pouvez télécharger ces modèles pour une installation ultérieure ou les inspecter toolearn comment trop[créer vos propres solutions](#creating-a-solution).

1. Suivez hello est décrite dans [OMS espace de travail et le compte Automation](#oms-workspace-and-automation-account) toolink un compte et un espace de travail.
2. Accédez trop[modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/).  
3. Recherchez une solution qui vous intéresse.
4. Sélectionnez les solutions hello hello résultats tooview ses détails.
5. Cliquez sur hello **déployer tooAzure** bouton.
6. Vous seront demandées tooprovide des informations telles que le groupe de ressources hello et l’emplacement dans toovalues Ajout pour tous les paramètres dans la solution de hello.
7. Cliquez sur **achat** solution de hello tooinstall.

### <a name="deploy-azure-resource-manager-template"></a>Déployer un modèle Azure Resource Manager
Les solutions que vous obtenez à partir de la Communauté de hello ou que vous avez [créer vous-même](#creating-a-solution) sont implémentés en tant que gestionnaire de ressources du modèle, et vous pouvez utiliser une des méthodes standard de hello pour [déploiement d’un modèle](../azure-resource-manager/resource-group-template-deploy-portal.md).  Notez qu’avant d’installer la solution de hello, vous devez créer et lier hello [OMS espace de travail et le compte Automation](#oms-workspace-and-automation-account).

## <a name="oms-workspace-and-automation-account"></a>Espace de travail OMS et compte Automation
La plupart des solutions de gestion requièrent une [espace de travail OMS](../log-analytics/log-analytics-manage-access.md) toocontain vues et une [compte Automation](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks et les ressources associées. Hello d’espace de travail et de compte doit répondre aux hello suivant les exigences.

* Une solution ne peut utiliser qu’un seul espace de travail OMS et un seul compte Automation.  
* Hello espace de travail OMS et le compte Automation utilisé par une solution doivent être lié tooone une autre. Un espace de travail OMS ne peut-être être lié tooone compte Automation, et un compte Automation peut être uniquement l’espace de travail lié tooone OMS.
* toobe lié, hello espace de travail OMS et Automation compte doit être dans hello même groupe de ressources et de région.  exception de Hello est un espace de travail OMS dans la région est des États-Unis et et compte Automation dans est des États-Unis 2.

### <a name="creating-a-link-between-an-oms-workspace-and-automation-account"></a>Création d’un lien entre un espace de travail OMS et un compte Automation
Manière dont vous spécifiez l’espace de travail OMS hello et compte Automation dépend de la méthode d’installation hello pour votre solution.

* Lorsque vous installez une solution Microsoft par le biais du portail OMS hello, il est installé dans l’espace de travail OMS actuel hello et aucun compte Automation n’est requis.
* Lorsque vous installez une solution via hello Azure Marketplace, vous êtes invité à entrer un espace de travail OMS et un compte Automation, et lien hello entre eux est créé pour vous.  
* Pour les solutions en dehors de hello Azure Marketplace, vous devez lier les espace de travail OMS hello et compte Automation avant d’installer la solution de hello.  Ce faire, vous pouvez sélectionner n’importe quelle solution Bonjour Azure Marketplace et espace de travail OMS hello et compte Automation.  Vous n’avez tooactually d’installer la solution de hello, car le lien de hello sera créé dès que l’espace de travail OMS hello et compte Automation sont sélectionnées.  Une fois le lien de hello est créé, vous pouvez utiliser cet espace de travail OMS et un compte Automation pour une solution. 

### <a name="verifying-hello-link-between-an-oms-workspace-and-automation-account"></a>Vérification de lien de hello entre un espace de travail OMS et un compte Automation
Vous pouvez vérifier le lien hello entre un espace de travail OMS et un compte Automation à l’aide de la procédure de hello.

1. Sélectionnez le compte Automation de hello Bonjour portail Azure.
2. Défiler vers le bas de hello toohello **paramètres** volet.
3. S’il existe une section intitulée **ressources OMS** Bonjour **paramètres** volet, ce compte est attaché tooan espace de travail OMS.
4. Sélectionnez **espace de travail** détails de hello tooview d’espace de travail OMS hello lié toothis compte d’automatisation.

## <a name="listing-management-solutions"></a>Liste des solutions de gestion
Utilisez hello suivant la procédure tootooview hello solutions de gestion hello espaces de travail tooyour lié abonnement Azure.

1. Ouvrez une session dans toohello portail Azure.
2. Dans le volet gauche de hello, sélectionnez **davantage de services**.
3. Soit défiler trop**Solutions** ou type *solutions* dans hello **filtre** boîte de dialogue.
4. Les solutions installées dans tous vos espaces de travail sont listées.

Notez que vous pouvez afficher uniquement des solutions Microsoft hello installées dans l’espace de travail actuel hello à l’aide du portail OMS hello.

## <a name="removing-a-management-solution"></a>Suppression d’une solution de gestion
Lorsqu’une solution de gestion est supprimée, toutes les ressources dans les solutions hello sont également supprimés.  

1. Localiser des solutions de hello Bonjour Azure portal à l’aide de la procédure hello dans [répertoriant les solutions](#listing-solutions).
2. Sélectionnez la solution hello souhaité tooremove.
3. Cliquez sur hello **supprimer** bouton.

## <a name="creating-a-management-solution"></a>Création d’une solution de gestion
Une aide complète à la création de solutions de gestion est disponible dans [Création de solutions dans Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md). 

## <a name="next-steps"></a>Étapes suivantes
* Dans [Modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates), recherchez des exemples de modèles Resource Manager.
* Créez vos propres [solutions de gestion](operations-management-suite-solutions-creating.md).

