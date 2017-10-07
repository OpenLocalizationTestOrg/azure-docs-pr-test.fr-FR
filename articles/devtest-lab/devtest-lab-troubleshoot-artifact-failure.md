---
title: "échecs d’artefact aaaDiagnose dans une machine virtuelle de Azure DevTest Labs | Documents Microsoft"
description: "Découvrez comment les échecs d’artefact tootroubleshoot dans DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 115e0086-3293-4adf-8738-9f639f31f918
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: tarcher
ms.openlocfilehash: 40b3cea72cf071cc5d9a6d002d309d923c3d3084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-artifact-failures-in-hello-lab"></a>Diagnostiquer les échecs d’artefact dans le laboratoire de hello 
Après avoir créé un artefact, vous pouvez vérifier toosee si elle a réussi ou échoué. Journaux d’artefact dans DevTest Labs fournissent des informations vous pouvez utiliser toodiagnose un échec de l’artefact. Il existe plusieurs façons différentes, vous pouvez afficher les informations de journal d’artefact hello pour une machine virtuelle Windows.

> [!NOTE]
> tooensure que les échecs sont correctement identifiés et expliqués, il est important de cet artefact hello est correctement structuré. Pour plus d’informations sur comment toocorrectly construire un artefact, consultez [créer des artefacts personnalisés](devtest-lab-artifact-author.md). Et toosee, par exemple, d’un objet structuré correctement, consultez ce [les Types de paramètres de Test](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artefact.

## <a name="troubleshoot-artifact-failures-using-hello-azure-portal"></a>Résoudre les échecs d’artefact à l’aide de hello portail Azure
échecs de toodiagnose portail Azure hello toouse lors de la création de l’artefact, procédez comme suit :

1. Dans la liste hello des ressources, sélectionnez votre laboratoire.

2. Choisissez hello machine virtuelle Windows qui inclut l’artefact hello souhaité tooinvestigate.

3. Dans le volet gauche, hello sous **général**, choisissez **artefacts**. Une liste des artefacts associés à cette machine virtuelle s’affiche, indique nom hello d’artefact de hello et son état.

   ![Exemple de dépôt git d'artefacts](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. Choisissez un artefact qui présente l’état **Échec**. artefact de Hello s’ouvre et affiche un message d’extension qui inclut des détails sur les échecs de hello d’artefact de hello.

   ![Exemple de dépôt git d'artefacts](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-hello-vm"></a>Résoudre les échecs d’artefact de hello machine virtuelle
tooview des journaux à partir de l’artefact de hello dans la machine virtuelle de hello, procédez comme suit :

1. Connectez-vous toohello machine virtuelle qui contient l’artefact hello souhaité toodiagnose.

2. Accédez tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status où « 1.9 est le numéro de version d’extension côté client hello.

   ![Exemple de dépôt git d'artefacts](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. Ouvrez hello **état** fichier tooview les informations que vous aide à diagnostiquer les échecs de l’artefact pour cette machine virtuelle.




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Billets de blog connexes
* [Joindre un domaine Active Directory à l’aide d’un modèle de gestionnaire de ressources dans Azure DevTest Labs de tooexisting machine virtuelle](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[ajouter un laboratoire tooa du référentiel Git](devtest-lab-add-artifact-repo.md).

