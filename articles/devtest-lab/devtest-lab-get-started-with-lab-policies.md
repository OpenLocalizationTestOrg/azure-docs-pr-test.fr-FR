---
title: "stratégies de base lab aaaManage dans Azure DevTest Labs | Documents Microsoft"
description: "Découvrez comment tooset certaines des stratégies de base hello (paramètres) pour un atelier de DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: tarcher
ms.openlocfilehash: 792c0d19cfe73964be9c03d3de7751a868fd86e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a>Gérer les stratégies de laboratoire de base dans Azure DevTest Labs

Azure DevTest Labs vous toocontrol coût et réduire les pertes dans vos laboratoires grâce à la gestion des stratégies (paramètres) correspondant à chaque atelier. Dans cet article, commencer à utiliser les stratégies par apprendre comment tooset deux des stratégies les plus critiques de hello - limitation hello nombre de machines virtuelles (VM) peut être créés ou demandés par un utilisateur unique et une configuration arrêt automatique. tooview comment tooset chaque stratégie lab, consultez l’article hello, [définir des stratégies de lab dans Azure DevTest Labs](devtest-lab-set-lab-policy.md).  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a>Accès aux stratégies d’un laboratoire dans Azure DevTest Labs
Hello étapes suivantes vous guident dans la configuration des stratégies pour un atelier de Azure DevTest Labs :

les stratégies hello tooview (et modifier) pour un laboratoire, procédez comme suit :

1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Sélectionnez **davantage de services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.

1. Dans liste hello labs, sélectionnez lab souhaité de hello.   

1. Sélectionnez **Configuration et stratégies**.

    ![Panneau Paramètres de stratégie](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. Hello **stratégies de Configuration et** panneau contienne un menu des paramètres que vous pouvez spécifier. Cet article traite uniquement les paramètres de hello pour **machines virtuelles par utilisateur** et **arrêt automatique**. toolearn sur hello restant des paramètres, consultez [gérer toutes les stratégies pour un atelier de Azure DevTest Labs](./devtest-lab-set-lab-policy.md). 
   
## <a name="set-virtual-machines-per-user"></a>Définir les machines virtuelles par utilisateur
Hello stratégie pour **machines virtuelles par utilisateur** vous permet de toospecify hello nombre de machines virtuelles qui peuvent être créés par un utilisateur individuel. Si un utilisateur tente de toocreate ou la revendication d’une machine virtuelle lors de la limite d’utilisateurs hello a été atteint, un message d’erreur indique que hello que machine virtuelle ne peut pas être créé/demandé. 

1. Sur du laboratoire hello **stratégies de Configuration et** menu, sélectionnez **machines virtuelles par utilisateur**.
   
    ![Machines virtuelles par utilisateur](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. Sélectionnez **Oui** toolimit hello plusieurs ordinateurs virtuels par utilisateur. Si vous ne souhaitez pas toolimit hello plusieurs ordinateurs virtuels par utilisateur, sélectionnez **non**. Si vous sélectionnez **Oui**, entrez une valeur numérique indiquant le nombre maximal de hello de machines virtuelles qui peuvent être créés ou demandé par un utilisateur. 

1. Sélectionnez **Oui** nombre de hello toolimit de machines virtuelles que vous pouvez utiliser des disques SSD (SSD). Si vous ne souhaitez pas le nombre de hello toolimit de machines virtuelles que vous pouvez utiliser des disques SSD, sélectionnez **non**. Si vous sélectionnez **Oui**, entrez une valeur qui indique le nombre maximal de hello de machines virtuelles qui peuvent être créés à l’aide de disques SSD. 

1. Sélectionnez **Enregistrer**.

## <a name="set-auto-shutdown"></a>Définir l’arrêt automatique
stratégie d’arrêt automatique Hello permet toominimize lab déchets, ce qui permet des temps de hello toospecify permettant d’arrêter des machines virtuelles de ce laboratoire.

1. Sur du laboratoire hello **stratégies de Configuration et** panneau, sélectionnez **arrêt automatique**.
   
    ![Arrêt automatique](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. Sélectionnez **sur** tooenable cette stratégie, et **hors** toodisable il.

1. Si vous activez cette stratégie, spécifiez tooshut de temps (et le fuseau horaire) hello tous les ordinateurs virtuels vers le bas dans le lab actuel de hello.

1. Spécifiez **Oui** ou **non** pour hello option toosend un toohello préalable de 15 minutes de notification spécifié des temps d’arrêt automatique. Si vous spécifiez **Oui**, entrez une notification de webhook URL du point de terminaison tooreceive hello. Pour plus d’informations sur les webhooks, consultez [Créer une fonction Azure d’API ou de webhook](../azure-functions/functions-create-a-web-hook-or-api-function.md). 

1. Sélectionnez **Enregistrer**.

    Par défaut, une fois activée, cette stratégie s’applique des machines virtuelles tooall pratiques hello. tooremove ce paramètre à partir d’un ordinateur virtuel spécifique, ouvrir le panneau et la modification de la machine virtuelle hello son **arrêt automatique** paramètre 

## <a name="set-auto-start"></a>Définir le démarrage automatique
permet de stratégie de démarrage automatique Hello vous toospecify hello machines virtuelles dans le lab actuel de hello doit être démarré.  

1. Sur du laboratoire hello **stratégies de Configuration et** panneau, sélectionnez **démarrage automatique**.
   
    ![Démarrage automatique](./media/devtest-lab-set-lab-policy/auto-start.png)

2. Sélectionnez **sur** tooenable cette stratégie, et **hors** toodisable il.

3. Si vous activez cette stratégie, spécifiez l’heure de début planifiée de hello, fuseau horaire et hello les jours de semaine hello pour le hello temps s’applique. 

4. Sélectionnez **Enregistrer**.

    Une fois activée, cette stratégie n’est pas appliqué automatiquement tooany VM dans pratiques hello. tooapply tooa de ce paramètre ordinateur virtuel spécifique, la machine virtuelle hello ouvrir Panneau et change son **démarrage automatique** paramètre 

## <a name="next-steps"></a>Étapes suivantes

- [Définir des stratégies de lab dans Azure DevTest Labs](devtest-lab-set-lab-policy.md) -en savoir comment toomodify autres stratégies de laboratoire 
