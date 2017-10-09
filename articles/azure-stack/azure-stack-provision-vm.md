---
title: aaaCreate un test de machine virtuelle dans Azure pile | Documents Microsoft
description: "Découvrez comment tooprovision une machine virtuelle dans la pile d’Azure sous la forme d’un opérateur cloud de test."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: c86646e1-a12e-493f-b396-f17bfacd60c2
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/21/2017
ms.author: erikje
ms.openlocfilehash: 9633cc20852e16283ad4522da78971133028efdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-test-virtual-machine-in-azure-stack"></a>Créer une machine virtuelle de test dans Azure Stack
Comme un opérateur cloud, vous pouvez créer un toovalidate d’ordinateur virtuel de test votre déploiement Azure pile.

> [!NOTE]
> Vous pouvez configurer des machines virtuelles, vous devez [ajouter le marketplace Azure pile toohello hello Windows Server 2016 Evaluation image](azure-stack-add-default-image.md).
> 
> 

## <a name="create-a-virtual-machine"></a>Création d'une machine virtuelle
1. Sur l’hôte du Kit de développement de pile Azure hello, [connectez-vous](azure-stack-connect-azure-stack.md) toohello portail d’administration (`https://adminportal.local.azurestack.external`), puis cliquez sur **nouveau** > **de calcul**  >  **Windows Server 2016 Datacenter Eval** > **créer**.  
2. Bonjour **notions de base** panneau, tapez un **nom**, **nom d’utilisateur**, et **mot de passe**. Choisissez un **Abonnement**. Créez un **Groupe de ressources** ou sélectionnez un groupe existant, puis cliquez sur **OK**.  
3. Bonjour **choisir une taille** panneau, cliquez sur **A1 Standard**, puis cliquez sur **sélectionnez**.  
4. Bonjour **paramètres** panneau, acceptez les valeurs par défaut hello et cliquez sur **OK**
5. Bonjour **Résumé** panneau, cliquez sur **OK** toocreate hello virtual machine.  
6. toosee votre nouvel ordinateur virtuel, cliquez sur **toutes les ressources**, puis recherchez l’ordinateur virtuel de hello et cliquez sur son nom.
    ![](media/azure-stack-provision-vm/image06.png)


## <a name="next-steps"></a>Étapes suivantes
[À l’aide des portails d’administrateur et utilisateur hello dans la pile de Azure](azure-stack-manage-portals.md)
