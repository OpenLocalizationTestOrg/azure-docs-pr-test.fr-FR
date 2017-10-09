---
title: aaaCreate une offre dans la pile de Azure | Documents Microsoft
description: "En tant qu’un administrateur de cloud, découvrez comment toocreate une offre pour vos clients dans la pile de Azure."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 96b080a4-a9a5-407c-ba54-111de2413d59
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: erikje
ms.openlocfilehash: 924526a0ff1c634b7c127c03a4572057c35b497b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-offer-in-azure-stack"></a>Créer une offre dans Azure Stack
[Offre](azure-stack-key-features.md) sont des groupes d’un ou plusieurs plans que toopurchase de tootenants fournisseurs présents ou s’y abonner. Ce document vous montre comment toocreate une offre qui inclut hello [plan que vous avez créé](azure-stack-create-plan.md) dans la dernière étape de hello. Cette offre permet les abonnés hello capacité tooprovision virtual machines.

1. Connectez-vous au portail d’administration Azure pile toohello (https://adminportal.local.azurestack.external) > cliquez sur **nouveau** > **client offre + Plans**  >   **Offre**.

   ![](media/azure-stack-create-offer/image01.png)
2. Bonjour **offrent de nouveaux** panneau, renseignez **nom d’affichage** et **nom de la ressource**, puis sélectionnez un nouveau ou existant **groupe de ressources**. Hello nom complet est le nom convivial de l’offre de hello et est hello seule information sur les offres de hello hello doit s’afficher lors de l’abonnement. Par conséquent, être toouse que pour un nom évocateur qui permet de comprendre ce qui est fourni avec l’offre de hello utilisateur de hello. Seul l’administrateur hello peut voir hello nom de la ressource. Son nom hello qu’administrateurs utiliser toowork hello offre une ressource Azure Resource Manager.

   ![](media/azure-stack-create-offer/image01a.png)
3. Cliquez sur **plans de Base** et hello **planifier** panneau, les plans hello Sélectionnez votre choix tooinclude dans l’offre de hello, puis cliquez sur **sélectionnez**. Cliquez sur **créer** offre de hello toocreate.

   ![](media/azure-stack-create-offer/image02.png)
4. Cliquez sur **toutes les ressources**, recherchez votre offre, cliquez sur Nouvelle offre de hello, cliquez sur **changement d’état**, puis cliquez sur **Public**.

   ![](media/azure-stack-create-offer/image03.png)

Offres doivent rendre publics pour une vue complète de locataires tooget hello lors de l’abonnement. Les offres peuvent être :

* **Public**: tootenants Visible.
* **Privé**: seuls les administrateurs de cloud toohello visible. Utile lors de plan de hello rédactionnelle ou de l’offre, ou si l’administrateur du cloud hello veut tooapprove chaque abonnement.
* **Mise hors service**: fermé toonew abonnés. administrateur du cloud Hello, vous pouvez utiliser les abonnements de futures tooprevent mis hors service, mais laisser les abonnés actuels inchangés.

Offre de toohello de modifications ne sont pas immédiatement visible toohello client. modifications de hello toosee, vous pouvez avoir nouvel abonnement toologout/connexion toosee hello dans hello « Sélecteur d’abonnement » lorsque la création de groupes de ressources.

> [!NOTE]
>Vous pouvez également créer des offres de valeur par défaut, les plans et les quotas à l’aide de PowerShell comme expliqué dans hello [Lisezmoi de l’administrateur du Service Azure pile](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin).
>


## <a name="next-steps"></a>Étapes suivantes
[S’abonner tooan offre et ensuite configurer une machine virtuelle](azure-stack-subscribe-plan-provision-vm.md)
