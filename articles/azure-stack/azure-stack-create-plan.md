---
title: aaaCreate un plan dans la pile de Azure | Documents Microsoft
description: "En tant qu’administrateur cloud, créez un plan permettant aux abonnés d’approvisionner des machines virtuelles."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 3dc92e5c-c004-49db-9a94-783f1f798b98
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/10/2017
ms.author: erikje
ms.openlocfilehash: 3665bae5d212002da43316e62ce73686b4c66eea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-plan-in-azure-stack"></a>Créer un plan dans Azure Stack
Les [plans](azure-stack-key-features.md) regroupent un ou plusieurs services. En tant que fournisseur, vous pouvez créer des plans toooffer tooyour locataires. À son tour, vos clients de s’abonner tooyour offres toouse hello plans et services qu’ils comprennent. Cet exemple vous montre comment toocreate un plan qui inclut hello des fournisseurs de ressources de calcul, réseau et de stockage. Ce plan offre abonnés hello capacité tooprovision virtual machines.

1. Se connecter toohello portail d’administration Azure pile (https://adminportal.local.azurestack.external). Entrez des informations d’identification de hello compte hello que vous avez créé à l’étape 5 de hello [exécuter le script PowerShell de hello](azure-stack-run-powershell-script.md) section.

2. toocreate un plan et offre que les clients peuvent s’abonner, cliquez sur **nouveau** > **client offre + Plans** > **Plan**.

   ![](media/azure-stack-create-plan/image01.png)
3. Bonjour **nouveau Plan** panneau, renseignez **nom d’affichage** et **nom de la ressource**. Hello nom complet est le nom convivial du plan hello clients plus. Seul l’administrateur hello peut voir hello nom de la ressource. Son nom hello qu’administrateurs utiliser toowork hello plan comme une ressource Azure Resource Manager.

   ![](media/azure-stack-create-plan/image02.png)
4. Créer un nouveau **groupe de ressources**, ou sélectionnez-en un existant, comme un conteneur pour un plan de hello.

   ![](media/azure-stack-create-plan/image02a.png)
5. Cliquez sur **Services**, sélectionnez **Microsoft.Compute**, **Microsoft.Network** et **Microsoft.Storage**, puis cliquez sur **Sélectionner**.

   ![](media/azure-stack-create-plan/image03.png)
6. Cliquez sur **Quotas**, cliquez sur **Microsoft.Storage (local)**et puis soit hello sélection par défaut de quota ou cliquez sur **créer nouveau quota** quota de hello toocustomize.

   ![](media/azure-stack-create-plan/image04.png)
7. Si vous créez un nouveau quota, entrez un nom pour le quota de hello > définir des valeurs de quota hello > cliquez sur **OK** > cliquez sur le nom hello du quota de nouveau hello.

   ![](media/azure-stack-create-plan/image06.png)
8. Cliquez sur **Microsoft.Network (local)**et puis soit hello sélection par défaut de quota ou cliquez sur **créer nouveau quota** quota de hello toocustomize.

    ![](media/azure-stack-create-plan/image07.png)
9. Si vous créez un nouveau quota, tapez un nom pour le quota de hello > définir des valeurs de quota hello > cliquez sur **OK** > cliquez sur le nom hello du quota de nouveau hello.

    ![](media/azure-stack-create-plan/image08.png)
10. Cliquez sur **Microsoft.Compute (local)**et puis soit hello sélection par défaut de quota ou cliquez sur **créer nouveau quota** quota de hello toocustomize.

    ![](media/azure-stack-create-plan/image09.png)
11. Si vous créez un nouveau quota, tapez un nom pour le quota de hello > définir des valeurs de quota hello > cliquez sur **OK** > cliquez sur le nom hello du quota de nouveau hello.

    ![](media/azure-stack-create-plan/image10.png)
12. Bonjour **Quotas** panneau, cliquez sur **OK**, puis dans hello **nouveau Plan** panneau, cliquez sur **créer** plan de hello toocreate.

    ![](media/azure-stack-create-plan/image11.png)
13. toosee votre nouveau plan, cliquez sur **toutes les ressources**, puis recherchez le plan de hello et cliquez sur son nom.

    ![](media/azure-stack-create-plan/image12.png)

### <a name="next-steps"></a>Étapes suivantes
[Créer une offre](azure-stack-create-offer.md)
