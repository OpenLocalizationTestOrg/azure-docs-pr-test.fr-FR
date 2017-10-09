---
title: "aaaUse Azure DevTest Labs pour l’apprentissage | Documents Microsoft"
description: "Découvrez comment toouse Azure DevTest Labs pour les scénarios de formation."
services: devtest-lab,virtual-machines
documentationcenter: na
author: steved0x
manager: douge
editor: 
ms.assetid: 57ff4e30-7e33-453f-9867-e19b3fdb9fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/12/2016
ms.author: sdanie
ms.openlocfilehash: 4a5f44a282d8f6a58849c730ff89237ccff39ca8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-training"></a>Utiliser Azure DevTest Labs à des fins de formation
Azure DevTest Labs peut être utilisé tooimplement nombreux scénarios clés dans toodev Ajout/de test. Un de ces scénarios est tooset d’un laboratoire pour l’apprentissage. Azure DevTest Labs vous permet de toocreate un laboratoire dans laquelle vous pouvez fournir des modèles personnalisés que chaque candidat peut utiliser des environnements identiques et isolé toocreate pour l’apprentissage. Vous pouvez appliquer des stratégies les tooensure que les environnements de formation sont disponibles tooeach candidat uniquement lorsqu’ils ont besoin contiennent suffisamment de ressources - telles que des machines virtuelles - requis pour l’apprentissage de hello. Enfin, vous pouvez facilement partager lab de hello avec stagiaires, auxquelles ils peuvent accéder en un seul clic.

![Utiliser DevTest Labs à des fins de formation](./media/devtest-lab-training-lab/devtest-lab-training.png)

Azure DevTest Labs répond aux hello suivant les exigences de formation tooconduct requis dans n’importe quel environnement virtuel : 

* Les participants ne voient pas les machines virtuelles créées par les autres participants.
* Toutes les machines de formation sont identiques.
* Les participants peuvent configurer rapidement leur environnement de formation.
* Contrôler les coûts en vous assurant que les stagiaires ne peut pas obtenir davantage d’ordinateurs virtuels que nécessaire pour apprentissage de hello et également l’arrêt de machines virtuelles lorsqu’elles ne les utilisez pas
* Partager facilement atelier pratique hello avec chaque candidat
* Réutilisation hello atelier pratique fois

Dans cet article, vous Découvrez diverses fonctionnalités Azure DevTest Labs qui peuvent être utilisées toomeet hello décrites précédemment des besoins de formation et des instructions détaillées que vous pouvez suivre tooset d’un laboratoire pour l’apprentissage.  

## <a name="implementing-training-with-azure-devtest-labs"></a>Mise en œuvre de formations avec Azure DevTest Labs
1. **Créez le laboratoire de hello** 
   
    Laboratoires sont hello point de départ dans Azure DevTest Labs. Une fois que vous créez un lab, vous pouvez effectuer ces comme ajouter lab de toohello utilisateurs (personnel), définir des stratégies toocontrol les coûts, définissent des images de machine virtuelle qui permettent de créer rapidement des tâches et bien plus encore.   
   
    En savoir plus en cliquant sur les liens hello Bonjour tableau suivant :
   
   | Task | Contenu |
   | --- | --- |
   | [Créer un laboratoire dans Azure DevTest Labs](devtest-lab-create-lab.md) |Découvrez comment toocreate un laboratoire dans Azure DevTest Labs dans hello portail Azure. |
2. **Créer des machines virtuelles de formation en quelques minutes à l’aide d’images Marketplace prêtes à l’emploi et d’images personnalisées** 
   
    Vous pouvez choisir les images prêtes à l’emploi à partir d’un grand nombre d’images Bonjour Azure Marketplace et les rendre disponibles pour les stagiaires hello dans le laboratoire de hello. Si les images prêtes à l’emploi hello ne répondent pas à vos besoins, vous pouvez créer une image personnalisée en créant un machine virtuelle à l’aide d’une image de prêts à l’emploi à partir d’Azure Marketplace, installer tous les logiciels hello dont vous avez besoin pour l’apprentissage de hello et l’enregistrement hello machine virtuelle en tant qu’image personnalisée dans le laboratoire de hello du laboratoire. 
   
    En savoir plus en cliquant sur les liens hello Bonjour tableau suivant :
   
   | Task | Contenu |
   | --- | --- |
   | [Configurer des images Azure Marketplace](devtest-lab-configure-marketplace-images.md) |Découvrez comment vous pouvez images Azure Marketplace de liste blanche ; rendre disponible pour les images de hello seule sélection souhaité pour l’apprentissage de hello. |
   | [Créer une image personnalisée](devtest-lab-create-template.md) |Créer une image personnalisée de préinstaller le logiciel hello que nécessaire pour l’apprentissage de hello qui stagiaires permettent de créer rapidement une machine virtuelle à l’aide d’image personnalisée de hello. |
3. **Créer des modèles réutilisables pour les machines de formation** 
   
    Une formule dans Azure DevTest Labs est qu'une liste de valeurs de propriété par défaut utilisé toocreate une machine virtuelle. Vous pouvez créer une formule dans le laboratoire de hello en choisissant une image, une taille de machine virtuelle (il s’agit d’une combinaison de processeur et de RAM) et un réseau virtuel. Chaque candidat peut voir formule hello dans le laboratoire de hello et l’utiliser toocreate une machine virtuelle. 
   
    En savoir plus en cliquant sur les liens hello Bonjour tableau suivant :
   
   | Task | Contenu |
   | --- | --- |
   | [Gérer des formules de DevTest Labs toocreate machines virtuelles](devtest-lab-manage-formulas.md) |Découvrez comment créer une formule en choisissant une image, une taille de machine virtuelle (une combinaison de puissance processeur et de RAM) et un réseau virtuel. |
4. **Contrôle des coûts**
   
    Azure DevTest Labs vous permet de tooset une stratégie hello lab toospecify hello nombre maximal de machines virtuelles qui peuvent être créés par un candidat dans le laboratoire de hello. 
   
    Si vous effectuez la formation de plusieurs jour et souhaitez toostop toutes les machines virtuelles de hello à un moment donné de la journée de hello et puis redémarrez automatiquement les hello suivant jour, vous pouvez facilement accomplir cela en définissant l’arrêt automatique et des stratégies dans le laboratoire de hello à démarrage automatique. 
   
    Enfin, lorsque l’apprentissage est terminée vous pouvez supprimer en même temps toutes les machines virtuelles de hello en exécutant un script PowerShell unique. 
   
    En savoir plus en cliquant sur les liens hello Bonjour tableau suivant :
   
   | Task | Contenu |
   | --- | --- |
   | [Définir des stratégies de laboratoire](devtest-lab-set-lab-policy.md) |Contrôler les coûts en définissant des stratégies dans le laboratoire de hello. |
   | [Supprimer lab hello toutes les machines virtuelles à l’aide d’un script PowerShell](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |Supprimez tous les ateliers hello en une seule opération lors de la formation de hello est terminée. |
5. **Lab de hello partage avec chaque candidat**
   
    Les laboratoires sont directement accessibles à l’aide d’un lien que vous partagez avec les participants. Stagiaires ne même ont toohave un compte Azure, tant qu’ils ont une [compte Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account). Les participants ne voient pas les machines virtuelles créées par les autres participants.  
   
    En savoir plus en cliquant sur les liens hello Bonjour tableau suivant :
   
   | Task | Contenu |
   | --- | --- |
   | [Ajouter un laboratoire de tooa du candidat dans Azure DevTest Labs](devtest-lab-add-devtest-user.md) |Utilisez hello tooadd portail Azure stagiaires tooyour formation laboratoire. |
   | [Ajouter le laboratoire de toohello stagiaires à l’aide d’un script PowerShell](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |Utilisez tooautomate PowerShell Ajout atelier pratique tooyour stagiaires. |
   | [Obtenir un laboratoire toohello de lien](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |Découvrez comment rendre un laboratoire directement accessible via un lien hypertexte. |
6. **Réutilisation hello lab fois** 
   
    Vous pouvez automatiser la création du laboratoire, y compris les paramètres personnalisés, création d’un modèle de gestionnaire de ressources et l’utilisation labs identiques de toocreate fois. 
   
    En savoir plus en cliquant sur les liens hello Bonjour tableau suivant :
   
   | Task | Contenu |
   | --- | --- |
   | [Créer un laboratoire à l’aide d’un modèle Resource Manager](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |Créez des laboratoires dans Azure DevTest Labs à l’aide de modèles Resource Manager. |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

