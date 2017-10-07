---
title: "stratégies de laboratoire aaaManage dans Azure DevTest Labs | Documents Microsoft"
description: "Découvrez comment les stratégies de laboratoire toodefine tels que des ordinateurs virtuels tailles, nombre maximal de machines virtuelles par utilisateur et l’automatisation de l’arrêt."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 7756aa64-49ca-45a0-9f90-0fd101c7be85
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 351b3645a1fd729455884e5d177877c2986bd853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a>Gérer toutes les stratégies d’un laboratoire dans Azure DevTest Labs

Azure DevTest Labs vous permet de contrôler les coûts et de réduire le gaspillage dans vos laboratoires en gérant les stratégies (paramètres) de chacun d’entre eux. Cet article explique étape par étape en détail comment tooset chaque stratégie.  

## <a name="set-allowed-virtual-machine-sizes"></a>Définir les tailles de machine virtuelle autorisées
Hello stratégie pour hello de paramètre autorisés tailles de machine virtuelle permet toominimize lab déchets en vous toospecify les tailles des machines virtuelles sont autorisées dans le laboratoire de hello. Si cette stratégie est activée, uniquement les tailles de machine virtuelle à partir de cette liste peuvent être utilisé toocreate VMs.

1. Sur du laboratoire hello **stratégies de Configuration et** panneau, sélectionnez **tailles de machines virtuelles autorisées**.
   
    ![Tailles de machine virtuelle autorisées](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. Sélectionnez **sur** tooenable cette stratégie, et **hors** toodisable il.

1. Si vous activez cette stratégie, sélectionnez une ou plusieurs tailles de machine virtuelle pouvant être créées dans votre laboratoire.

1. Sélectionnez **Enregistrer**.

## <a name="set-virtual-machines-per-user"></a>Définir les machines virtuelles par utilisateur
Hello stratégie pour **machines virtuelles par utilisateur** vous permet de toospecify hello nombre de machines virtuelles qui peuvent être créés par un utilisateur individuel. Si un utilisateur tente de toocreate ou la revendication d’une machine virtuelle lors de la limite d’utilisateurs hello a été atteint, un message d’erreur indique que hello que machine virtuelle ne peut pas être créé/demandé. 

1. Sur du laboratoire hello **stratégies de Configuration et** menu, sélectionnez **machines virtuelles par utilisateur**.
   
    ![Machines virtuelles par utilisateur](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. Sélectionnez **Oui** toolimit hello plusieurs ordinateurs virtuels par utilisateur. Si vous ne souhaitez pas toolimit hello plusieurs ordinateurs virtuels par utilisateur, sélectionnez **non**. Si vous sélectionnez **Oui**, entrez une valeur numérique indiquant le nombre maximal de hello de machines virtuelles qui peuvent être créés ou demandé par un utilisateur. 

1. Sélectionnez **Oui** nombre de hello toolimit de machines virtuelles que vous pouvez utiliser des disques SSD (SSD). Si vous ne souhaitez pas le nombre de hello toolimit de machines virtuelles que vous pouvez utiliser des disques SSD, sélectionnez **non**. Si vous sélectionnez **Oui**, entrez une valeur qui indique le nombre maximal de hello de machines virtuelles qui peuvent être créés à l’aide de disques SSD. 

1. Sélectionnez **Enregistrer**.

## <a name="set-virtual-machines-per-lab"></a>Définir les machines virtuelles par laboratoire
Hello stratégie pour **machines virtuelles par lab** vous permet de toospecify hello nombre de machines virtuelles qui peuvent être créés pour les pratiques hello. Si un utilisateur tente toocreate une machine virtuelle lors de la limite de laboratoire hello a été atteint, un message d’erreur indique que hello que machine virtuelle ne peut pas être créé. 

1. Sur du laboratoire hello **stratégies de Configuration et** menu, sélectionnez **machines virtuelles par lab**.
   
    ![Machines virtuelles par laboratoire](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. Sélectionnez **Oui** toolimit hello différentes machines virtuelles par lab. Si vous ne souhaitez pas le nombre de hello toolimit de machines virtuelles par lab, sélectionnez **non**. Si vous sélectionnez **Oui**, entrez une valeur numérique indiquant le nombre maximal de hello de machines virtuelles qui peuvent être créés ou demandé par un utilisateur. 

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

## <a name="set-expiration-date"></a>Définir une date d’expiration
Vous pouvez définir un délai d’expiration date à laquelle vous [créer hello VM](devtest-lab-add-vm.md). Dans **paramètres avancés**, choisissez toospecify d’icône de calendrier hello une date sur laquelle hello machine virtuelle est automatiquement supprimée.  Par défaut, hello VM n’expirera jamais.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Étapes suivantes
Une fois que vous avez définies et appliquées hello différents paramètres de stratégie de machine virtuelle pour votre laboratoire, Voici certaines choses tootry suivant :

* [Comprendre les adresses IP partagées](devtest-lab-shared-ip.md) -explique comment partagé IP adresses sont utilisées dans le nombre de hello DevTest Labs toominimize du laboratoire tooyour publique IP adresses requis tooconnect machines virtuelles.
* [Configurer la gestion des coûts](devtest-lab-configure-cost-management.md) -illustre comment toouse hello **tendance du coût estimé mensuel** graphique  
  tooview hello estimé coût-to-date du mois en cours et coût de fin de mois de hello projeté.
* [Créer une image personnalisée](devtest-lab-create-template.md) : quand vous créez une machine virtuelle, vous spécifiez une base, qui peut être soit une image personnalisée, soit une image Marketplace. Cet article explique comment toocreate personnalisé de l’image à partir d’un fichier de disque dur virtuel.
* [Configurer des images Marketplace](devtest-lab-configure-marketplace-images.md) : Azure DevTest Labs prend en charge la création de machines virtuelles basées sur des images Azure Marketplace. Cet article explique comment toospecify qui, le cas échéant, les images Azure Marketplace peuvent être utilisés lors de la création de machines virtuelles dans un laboratoire.
* [Créer une machine virtuelle dans un laboratoire](devtest-lab-add-vm-with-artifacts.md) -illustre comment toocreate une machine virtuelle à partir d’une image de base (soit personnalisé ou Marketplace) et comment toowork des artefacts dans votre machine virtuelle.

