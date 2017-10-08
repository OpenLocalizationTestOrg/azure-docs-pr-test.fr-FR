---
title: "utilisateurs d’Azure pile aaaMake machines virtuelles disponibles tooyour | Documents Microsoft"
description: Didacticiel toomake virtuels disponibles sur la pile de Azure
services: azure-stack
documentationcenter: 
author: vhorne
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/22/2017
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: 345206912f17662e51341c71175c5fe87b692ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="make-virtual-machines-available-tooyour-azure-stack-users"></a>Rendre tooyour disponible des ordinateurs virtuels aux utilisateurs de pile de Azure
En tant qu’un administrateur de cloud Azure pile, vous pouvez créer vos utilisateurs (clients tooas parfois visés) peuvent s’abonner à des offres. Avec leur abonnement, les utilisateurs peuvent utiliser les services Azure Stack.

Cet article vous montre comment toocreate une offre, puis du tester. Pour le test de hello, vous connectez-vous au portail toohello en tant qu’utilisateur, s’abonner toohello offre et ensuite créer un ordinateur virtuel à l’aide d’abonnement de hello.

Contenu :

> [!div class="checklist"]
> * Créer une offre
> * Ajouter une image
> * Offre de hello de test


Dans la pile d’Azure, les services sont remis toousers à l’aide d’abonnements, les offres et les plans. Les utilisateurs peuvent s’abonner à des offres toomultiple. Les offres peuvent contenir un ou plusieurs plans, et les plans peuvent contenir un ou plusieurs services.

![Abonnements, offres et plans](media/azure-stack-key-features/image4.png)

toolearn, voir [principales fonctionnalités et les concepts dans Azure pile](azure-stack-key-features.md).

## <a name="create-an-offer"></a>Créer une offre

Il est maintenant possible d’effectuer toutes les étapes de préparation pour vos utilisateurs. Lorsque vous démarrez le processus de hello, vous êtes première offre de hello toocreate demandées, un plan et les quotas.

3. **Créer une offre**

   Offres sont des groupes d’un ou plusieurs plans que toopurchase de toousers fournisseurs présents ou s’y abonner.

   a. [Connectez-vous](azure-stack-connect-azure-stack.md) portal toohello comme un administrateur du cloud puis cliquez sur **nouveau** > **client offre + Plans** > **offrent**.
   ![Nouvelle offre](media/azure-stack-tutorial-tenant-vm/image01.png)

   b. Bonjour **offrent de nouveaux** section, renseignez **nom d’affichage** et **nom de la ressource**, puis sélectionnez un nouveau ou existant **groupe de ressources**. Hello nom complet est le nom convivial de l’offre de hello. Seul l’opérateur hello cloud peut voir hello nom de la ressource. Son nom hello qu’administrateurs utiliser toowork hello offre une ressource Azure Resource Manager.

   ![Nom complet](media/azure-stack-tutorial-tenant-vm/image02.png)

   c. Cliquez sur **plans de Base**et Bonjour **Plan** , cliquez sur **ajouter** tooadd une nouvelle offre de toohello de plan.

   ![Ajouter un plan](media/azure-stack-tutorial-tenant-vm/image03.png)

   d. Bonjour **nouveau Plan** section, renseignez **nom d’affichage** et **nom de la ressource**. Hello nom complet est le nom convivial du plan hello que les utilisateurs voient. Seul l’opérateur hello cloud peut voir hello nom de la ressource. Son nom hello que les opérateurs cloud utilisent toowork avec hello plan comme une ressource Azure Resource Manager.

   ![Nom d’affichage du plan](media/azure-stack-tutorial-tenant-vm/image04.png)

   e. Cliquez sur **Services**, sélectionnez **Microsoft.Compute**, **Microsoft.Network** et **Microsoft.Storage**, puis cliquez sur **Sélectionner**.

   ![Services du plan](media/azure-stack-tutorial-tenant-vm/image05.png)

   f. Cliquez sur **Quotas**, puis sélectionnez hello premier service pour lequel vous souhaitez toocreate un quota. Pour un quota IaaS, suivez ces étapes pour les services de calcul, réseau et stockage hello.

   Dans cet exemple, nous créons d’abord un quota pour le service de calcul hello. Dans la liste d’espace de noms hello, sélectionnez hello **Microsoft.Compute** espace de noms, puis **créer nouveau quota**.
   
   ![Créer un quota](media/azure-stack-tutorial-tenant-vm/image06.png)

   g. Sur hello **créer quota** , tapez un nom pour le quota de hello et le jeu de paramètres souhaités pour le quota de hello et cliquez sur hello **OK**.

   ![Nom du quota](media/azure-stack-tutorial-tenant-vm/image07.png)

   h. À présent, pour **Microsoft.Compute**, sélectionnez quota hello que vous avez créé.

   ![Sélectionner un quota](media/azure-stack-tutorial-tenant-vm/image08.png)

   Répétez ces étapes pour les services réseau et de stockage hello, puis cliquez sur **OK** sur hello **Quotas** section.

   i. Cliquez sur **OK** sur hello **nouveau plan** section.

   j. Sur hello **Plan** , sélectionnez le nouveau plan de hello et cliquez sur **sélectionnez**.

   k. Sur hello **nouvelle offre** , cliquez sur **créer**. Vous voyez une notification lors de l’offre de hello a été créé.

   l. Cliquez sur tableau de bord hello, **offre** puis cliquez sur offre hello vous avez créé.

   m. Cliquez sur **Changer l’état**, puis sur **Public**.

   ![État Public](media/azure-stack-tutorial-tenant-vm/image09.png)

## <a name="add-an-image"></a>Ajouter une image

Vous pouvez configurer des machines virtuelles, vous devez ajouter un marketplace d’Azure pile toohello image. Vous pouvez ajouter l’image hello de votre choix, y compris les images Linux, à partir de hello Azure Marketplace.

Si vous opérez dans un scénario connecté et si vous avez enregistré votre instance de la pile d’Azure avec Azure, vous pouvez télécharger image de machine virtuelle de Windows Server 2016 hello de hello Azure Marketplace à l’aide des étapes hello Bonjour [télécharger éléments du Marketplace à partir d’Azure tooAzure pile](azure-stack-download-azure-marketplace-item.md) rubrique.

Pour plus d’informations sur l’ajout d’éléments différents toohello marketplace, consultez [hello Azure Marketplace de pile](azure-stack-marketplace.md).

## <a name="test-hello-offer"></a>Offre de hello de test

Maintenant que vous avez créé une offre, vous pouvez le tester. Connectez-vous en tant qu’utilisateur et vous abonner toohello offre et puis ajoutez un ordinateur virtuel.

1. **S’abonner tooan offre**

   Maintenant, vous pouvez consigner dans le portail de toohello en tant qu’une offre de tooan toosubscribe utilisateur.

   a. Sur l’ordinateur du Kit de déploiement de pile Azure hello, connectez-vous trop`https://portal.local.azurestack.external` comme utilisateur et cliquez sur **obtenir un abonnement**.

   ![Prendre un abonnement](media/azure-stack-subscribe-plan-provision-vm/image01.png)

   b. Bonjour **nom d’affichage** , tapez un nom pour votre abonnement, cliquez sur **offrent**, cliquez sur une des offres hello Bonjour **choisissez une offre** section, puis cliquez sur **Créer**.

   ![Créer une offre](media/azure-stack-subscribe-plan-provision-vm/image02.png)

   c. abonnement de hello tooview que vous avez créé, cliquez sur **davantage de services**, cliquez sur **abonnements**, puis cliquez sur votre nouvel abonnement.  

   Après que vous être abonné tooan offre, actualiser les toosee portail hello les services qui font partie d’un nouvel abonnement hello.

2. **Approvisionner une machine virtuelle**

   Maintenant vous pouvez vous connecter toohello portal comme une tooprovision utilisateur un ordinateur virtuel à l’aide d’abonnement de hello. 

   a. Sur l’ordinateur du Kit de déploiement de pile Azure hello, connectez-vous trop`https://portal.local.azurestack.external` en tant qu’utilisateur, puis cliquez sur **nouveau** > **de calcul** > **Datacenter de Windows Server 2016 Eval**.  

   b. Bonjour **notions de base** , tapez un **nom**, **nom d’utilisateur**, et **mot de passe**. Pour **Type de disque de machine virtuelle**, choisissez **HDD**. Choisissez un **Abonnement**. Créez un **Groupe de ressources** ou sélectionnez un groupe existant, puis cliquez sur **OK**.  

   c. Bonjour **choisir une taille** , cliquez sur **base A1**, puis cliquez sur **sélectionnez**.  

   d. Bonjour **paramètres** , cliquez sur **réseau virtuel**. Bonjour **réseau virtuel de choisir** , cliquez sur **nouvel**. Bonjour **créer un réseau virtuel** , acceptez toutes les valeurs par défaut de hello et cliquez sur **OK**. Bonjour **paramètres** , cliquez sur **OK**.

   ![Création d’un réseau virtuel](media/azure-stack-provision-vm/image04.png)

   e. Bonjour **Résumé** , cliquez sur **OK** toocreate hello virtual machine.  

   f. toosee votre nouvel ordinateur virtuel, cliquez sur **toutes les ressources**, puis recherchez l’ordinateur virtuel de hello et cliquez sur son nom.

    ![Toutes les ressources](media/azure-stack-provision-vm/image06.png)

Ce que vous avez appris dans ce didacticiel :

> [!div class="checklist"]
> * Créer une offre
> * Ajouter une image
> * Offre de hello de test

> [!div class="nextstepaction"]
> [Rendre web, mobiles et utilisateurs d’Azure pile API apps tooyour disponibles](azure-stack-tutorial-app-service.md)
