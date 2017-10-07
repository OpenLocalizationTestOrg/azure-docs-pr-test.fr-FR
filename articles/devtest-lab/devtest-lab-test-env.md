---
title: environnements de test aaaUse Azure DevTest Labs et de machine virtuelle PaaS | Documents Microsoft
description: "Découvrez comment toouse Azure DevTest Labs et de machine virtuelle PaaS tester les scénarios de l’environnement."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: d4e2c334-643a-40c9-9051-625b8f39fc86
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tarcher
ms.openlocfilehash: 9285090da768491e1275942318b094fae89e3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-vm-and-paas-test-environments"></a>Utiliser Azure DevTest Labs pour les environnements de test de machine virtuelle et PaaS

Vous pouvez utiliser Azure DevTest Labs tooimplement de nombreux scénarios clés, mais un scénario principal implique l’utilisation de machines de toohost DevTest Labs pour les développeurs. 

Dans ce scénario, DevTest Labs offre les avantages suivants :

- Testeurs peuvent tester la version la plus récente de leur application hello en configurant rapidement les environnements Windows et Linux à l’aide des artefacts et des modèles réutilisables.
- Ils peuvent faire monter en puissance leur test de charge en approvisionnant plusieurs agents de test.
- Les administrateurs peuvent contrôler les coûts en s’assurant que :
  - Les testeurs ne peuvent pas obtenir plus de machines virtuelles qu’il n’est nécessaire.
  - Les machines virtuelles sont éteintes lorsqu’elles ne sont pas utilisées.

![Utiliser DevTest Labs à des fins de formation](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

Dans cet article, vous en savoir plus sur les différentes exigences de testeur toomeet Azure DevTest Labs fonctionnalités utilisées et hello tooset toofollow de la procédure détaillée d’un laboratoire.

## <a name="implementing-test-environments-with-azure-devtest-labs"></a>Implémentation d’environnements de test avec Azure DevTest Labs
1. **Créez le laboratoire de hello** 
   
    Laboratoires sont hello point de départ dans Azure DevTest Labs. Une fois que vous créez un lab, vous pouvez effectuer des tâches telles que l’ajout de laboratoire de toohello les utilisateurs (les testeurs), des coûts toocontrol paramètre les stratégies, définition des images de machine virtuelle qui permettent de créer rapidement et bien plus encore.  
   
    En savoir plus en cliquant sur les liens hello Bonjour tableau suivant :
   
   | Task | Contenu |
   | --- | --- |
   | [Créer un laboratoire dans Azure DevTest Labs](devtest-lab-create-lab.md) |Découvrez comment toocreate un laboratoire dans Azure DevTest Labs dans hello portail Azure. |
2. **Créer des machines virtuelles en quelques minutes à l’aide d’images Marketplace prêtes à l’emploi et d’images personnalisées** 
   
    Vous pouvez choisir les images prêtes à l’emploi à partir d’un grand nombre d’images Bonjour Azure Marketplace et les rendre disponibles dans le laboratoire de hello. Si les images prêtes à l’emploi hello ne répondent pas à vos besoins, vous pouvez créer une image personnalisée en créant un machine virtuelle à l’aide d’une image prêts à l’emploi à partir d’Azure Marketplace, installer tous les logiciels hello dont vous avez besoin, et l’enregistrement hello machine virtuelle comme une image personnalisée dans le laboratoire de hello du laboratoire.

    Si vous utilisez des images personnalisées, envisagez d’utiliser un toocreate de fabrique d’image et distribuer vos images. Une fabrique d’images est une solution en tant que code de configuration qui crée et distribue vos images configurées automatiquement. Cette toomanually de durée hello enregistre configurer le système de hello après une machine virtuelle a été créée avec hello du système d’exploitation de base.
  
    En savoir plus en cliquant sur les liens hello Bonjour tableau suivant :
   
   | Task | Contenu |
   | --- | --- |
   | [Configurer des images Azure Marketplace](devtest-lab-configure-marketplace-images.md) |Découvrez comment vous pouvez images Azure Marketplace de liste blanche d’adresses, les rendre disponibles pour les images hello uniquement de sélection souhaité pour les testeurs hello.|
   | [Créer une image personnalisée](devtest-lab-create-template.md) |Créer une image personnalisée de préinstaller le logiciel hello que nécessaire afin que les testeurs peuvent créer rapidement une machine virtuelle à l’aide d’image personnalisée de hello.|
   | [Découvrir la fabrique d’images](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |Regardez une vidéo qui décrit comment tooset configurer et utiliser une fabrique d’image.|

3. **Créer des modèles réutilisables pour les machines de test** 
   
    Une formule dans Azure DevTest Labs est qu'une liste de valeurs de propriété par défaut utilisé toocreate une machine virtuelle. Vous pouvez créer une formule dans le laboratoire de hello en choisissant une image, une taille de machine virtuelle (il s’agit d’une combinaison de processeur et de RAM) et un réseau virtuel. Chaque testeur peut voir formule hello dans le laboratoire de hello et utiliser toocreate une machine virtuelle. 
   
    En savoir plus en cliquant sur les liens hello Bonjour tableau suivant :
   
   | Task | Contenu |
   | --- | --- |
   | [Gérer des formules de DevTest Labs toocreate machines virtuelles](devtest-lab-manage-formulas.md) |Découvrez comment créer une formule en choisissant une image, une taille de machine virtuelle (une combinaison de puissance processeur et de RAM) et un réseau virtuel.|

3. **Créer des environnements de test multimachine virtuelle** 
   
    Vous pouvez utiliser l’infrastructure de hello de toodefine de modèles Azure Resource Manager et configuration de votre solution Azure et déployer à plusieurs reprises de test de plusieurs machines virtuelles dans un état cohérent.

    Les ressources PaaS Azure peuvent être approvisionnées dans un environnement à partir d’un modèle Azure Resource Manager et apparaître dans le suivi des coûts. Toutefois, arrêt automatique de machine virtuelle ne s’applique pas les ressources tooPaaS.

    En savoir plus en cliquant sur les liens hello Bonjour tableau suivant :
   
   | Task | Contenu |
   | --- | --- |
   | [Créer des environnements de plusieurs machines virtuelles et des ressources PaaS avec les modèles Azure Resource Manager](devtest-lab-create-environment-from-arm.md) |Découvrez comment vous déployer plusieurs machines virtuelles dans un état cohérent pour votre environnement de test.|

4. **Créer de personnalisation artefacts tooenable flexible**

   Artefacts sont toodeploy utilisé et configurer votre application après qu’une machine virtuelle est configurée. Les artefacts peuvent être :

   - Outils que vous souhaitez tooinstall sur hello VM - tels que les agents, Fiddler et Visual Studio.
   - Actions que vous souhaitez toorun sur hello VM - telles que le clonage d’un référentiel.
   - Applications que vous souhaitez tootest.

   De nombreux artefacts prêts à l’emploi sont disponibles. Toutefois, si vos besoins spécifiques requièrent davantage de personnalisation, vous pouvez créer vos propres artefacts personnalisés.

   En savoir plus en cliquant sur les liens hello Bonjour tableau suivant :
   
   | Task | Contenu |
   | --- | --- |
   | [Créer des artefacts personnalisés pour vos machines virtuelles DevTest Labs](devtest-lab-artifact-author.md) |Créez vos propres artefacts personnalisés pour les ordinateurs virtuels de hello dans votre laboratoire.|
   | [Ajoutez un artefacts de personnalisée toostore de référentiel Git et les modèles Azure Resource Manager pour une utilisation dans Azure DevTest Labs](devtest-lab-add-artifact-repo.md) |Découvrez comment toostore vos artefacts personnalisés dans votre propre référentiel Git privé.|

5. **Contrôle des coûts**
   
    Azure DevTest Labs vous permet de tooset une stratégie hello lab toospecify hello nombre maximal de machines virtuelles qui peuvent être créés par un testeur dans le laboratoire de hello. 
   
    Si votre équipe de test possède un ensemble de planification de travail et que vous souhaitez toostop toutes les machines virtuelles de hello à un moment donné de la journée de hello et puis redémarrez automatiquement les hello suivant jour, vous pouvez facilement effectuer que par paramètre arrêt automatique et le démarrage automatique des stratégies dans le laboratoire de hello. 
   
    Enfin, lorsque le développement d’applications est terminé, vous pouvez supprimer en même temps toutes les machines virtuelles de hello en exécutant un script PowerShell unique. 
   
    En savoir plus en cliquant sur les liens hello Bonjour tableau suivant :
   
   | Task | Contenu |
   | --- | --- |
   | [Définir des stratégies de laboratoire](devtest-lab-set-lab-policy.md) |Contrôler les coûts en définissant des stratégies dans le laboratoire de hello. |
   | [Supprimer lab hello toutes les machines virtuelles à l’aide d’un script PowerShell](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |Supprimez tous les ateliers hello en une seule opération lorsque le test est terminé.|

1. **Ajouter un tooa de réseau virtuel lab.** 
   
    DevTest Labs crée un réseau virtuel (VNET) à chaque création de laboratoire. Si vous avez configuré votre propre réseau virtuel – par exemple, en utilisant ExpressRoute ou VPN de site à site – vous pouvez ajouter des paramètres de réseau virtuel de ce laboratoire tooyour réseau virtuel afin qu’il soit disponible lors de la création de machines virtuelles.

    En outre, il est un Azure Active Directory domaine jointure artefact disponible qui rejoint un domaine de tooa de machine virtuelle lorsque hello machine virtuelle est créée. 
   
    En savoir plus en cliquant sur les liens hello Bonjour tableau suivant :
   
   | Task | Contenu |
   | --- | --- |
   | [Configuration d’un réseau virtuel dans Azure DevTest Labs](devtest-lab-configure-vnet.md) |Découvrez comment tooconfigure un réseau virtuel à l’aide d’Azure DevTest Labs hello portail Azure.|

6. **Lab de hello partage avec chaque testeur**
   
    Les laboratoires sont directement accessibles à l’aide d’un lien que vous partagez avec les testeurs. Ils n’ont pas toohave un compte Azure, tant qu’ils ont une [compte Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account). Les testeurs ne voient pas les machines virtuelles créées par d’autres testeurs.  
   
    En savoir plus en cliquant sur les liens hello Bonjour tableau suivant :
   
   | Task | Contenu |
   | --- | --- |
   | [Ajouter un laboratoire de tooa testeur dans Azure DevTest Labs](devtest-lab-add-devtest-user.md) |Utilisez hello tooadd portail Azure testeurs tooyour laboratoire.|
   | [Ajouter le laboratoire de toohello testeurs à l’aide d’un script PowerShell](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |Utilisez tooautomate PowerShell ajoutant laboratoire tooyour de testeurs. |
   | [Obtenir un laboratoire toohello de lien](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |Découvrez comment les testeurs peuvent accéder directement à un laboratoire via un lien hypertexte.|

7. **Automatiser la création de laboratoire pour d’autres équipes** 
   
    Vous pouvez automatiser la création du laboratoire, y compris les paramètres personnalisés, création d’un modèle de gestionnaire de ressources et l’utilisation labs identiques de toocreate fois. 
   
    En savoir plus en cliquant sur les liens hello Bonjour tableau suivant :
   
   | Task | Contenu |
   | --- | --- |
   | [Créer un laboratoire à l’aide d’un modèle Resource Manager](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |Créez des laboratoires dans Azure DevTest Labs à l’aide de modèles Resource Manager. |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

