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
# <a name="create-an-offer-in-azure-stack"></a><span data-ttu-id="2a396-103">Créer une offre dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="2a396-103">Create an offer in Azure Stack</span></span>
<span data-ttu-id="2a396-104">[Offre](azure-stack-key-features.md) sont des groupes d’un ou plusieurs plans que toopurchase de tootenants fournisseurs présents ou s’y abonner.</span><span class="sxs-lookup"><span data-stu-id="2a396-104">[Offers](azure-stack-key-features.md) are groups of one or more plans that providers present tootenants toopurchase or subscribe to.</span></span> <span data-ttu-id="2a396-105">Ce document vous montre comment toocreate une offre qui inclut hello [plan que vous avez créé](azure-stack-create-plan.md) dans la dernière étape de hello.</span><span class="sxs-lookup"><span data-stu-id="2a396-105">This document shows you how toocreate an offer that includes hello [plan that you created](azure-stack-create-plan.md) in hello last step.</span></span> <span data-ttu-id="2a396-106">Cette offre permet les abonnés hello capacité tooprovision virtual machines.</span><span class="sxs-lookup"><span data-stu-id="2a396-106">This offer gives subscribers hello ability tooprovision virtual machines.</span></span>

1. <span data-ttu-id="2a396-107">Connectez-vous au portail d’administration Azure pile toohello (https://adminportal.local.azurestack.external) > cliquez sur **nouveau** > **client offre + Plans**  >   **Offre**.</span><span class="sxs-lookup"><span data-stu-id="2a396-107">Sign in toohello Azure Stack administrator portal (https://adminportal.local.azurestack.external) > click **New** > **Tenant Offers + Plans** > **Offer**.</span></span>

   ![](media/azure-stack-create-offer/image01.png)
2. <span data-ttu-id="2a396-108">Bonjour **offrent de nouveaux** panneau, renseignez **nom d’affichage** et **nom de la ressource**, puis sélectionnez un nouveau ou existant **groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="2a396-108">In hello **New Offer** blade, fill in **Display Name** and **Resource Name**, and then select a new or existing **Resource Group**.</span></span> <span data-ttu-id="2a396-109">Hello nom complet est le nom convivial de l’offre de hello et est hello seule information sur les offres de hello hello doit s’afficher lors de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="2a396-109">hello Display Name is hello offer's friendly name and is hello only information about hello offer that hello users will see when subscribing.</span></span> <span data-ttu-id="2a396-110">Par conséquent, être toouse que pour un nom évocateur qui permet de comprendre ce qui est fourni avec l’offre de hello utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="2a396-110">Therefore, be sure toouse an intuitive name that helps hello user understand what comes with hello offer.</span></span> <span data-ttu-id="2a396-111">Seul l’administrateur hello peut voir hello nom de la ressource.</span><span class="sxs-lookup"><span data-stu-id="2a396-111">Only hello admin can see hello Resource Name.</span></span> <span data-ttu-id="2a396-112">Son nom hello qu’administrateurs utiliser toowork hello offre une ressource Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2a396-112">It's hello name that admins use toowork with hello offer as an Azure Resource Manager resource.</span></span>

   ![](media/azure-stack-create-offer/image01a.png)
3. <span data-ttu-id="2a396-113">Cliquez sur **plans de Base** et hello **planifier** panneau, les plans hello Sélectionnez votre choix tooinclude dans l’offre de hello, puis cliquez sur **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="2a396-113">Click **Base plans** and, in hello **Plan** blade, select hello plans you want tooinclude in hello offer, and then click **Select**.</span></span> <span data-ttu-id="2a396-114">Cliquez sur **créer** offre de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="2a396-114">Click **Create** toocreate hello offer.</span></span>

   ![](media/azure-stack-create-offer/image02.png)
4. <span data-ttu-id="2a396-115">Cliquez sur **toutes les ressources**, recherchez votre offre, cliquez sur Nouvelle offre de hello, cliquez sur **changement d’état**, puis cliquez sur **Public**.</span><span class="sxs-lookup"><span data-stu-id="2a396-115">Click **All Resources**, search for your new offer, click on hello new offer, click **Change State**, and then click **Public**.</span></span>

   ![](media/azure-stack-create-offer/image03.png)

<span data-ttu-id="2a396-116">Offres doivent rendre publics pour une vue complète de locataires tooget hello lors de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="2a396-116">Offers must be made public for tenants tooget hello full view when subscribing.</span></span> <span data-ttu-id="2a396-117">Les offres peuvent être :</span><span class="sxs-lookup"><span data-stu-id="2a396-117">Offers can be:</span></span>

* <span data-ttu-id="2a396-118">**Public**: tootenants Visible.</span><span class="sxs-lookup"><span data-stu-id="2a396-118">**Public**: Visible tootenants.</span></span>
* <span data-ttu-id="2a396-119">**Privé**: seuls les administrateurs de cloud toohello visible.</span><span class="sxs-lookup"><span data-stu-id="2a396-119">**Private**: Only visible toohello cloud administrators.</span></span> <span data-ttu-id="2a396-120">Utile lors de plan de hello rédactionnelle ou de l’offre, ou si l’administrateur du cloud hello veut tooapprove chaque abonnement.</span><span class="sxs-lookup"><span data-stu-id="2a396-120">Useful while drafting hello plan or offer, or if hello cloud administrator wants tooapprove every subscription.</span></span>
* <span data-ttu-id="2a396-121">**Mise hors service**: fermé toonew abonnés.</span><span class="sxs-lookup"><span data-stu-id="2a396-121">**Decommissioned**: Closed toonew subscribers.</span></span> <span data-ttu-id="2a396-122">administrateur du cloud Hello, vous pouvez utiliser les abonnements de futures tooprevent mis hors service, mais laisser les abonnés actuels inchangés.</span><span class="sxs-lookup"><span data-stu-id="2a396-122">hello cloud administrator can use decommissioned tooprevent future subscriptions, but leave current subscribers untouched.</span></span>

<span data-ttu-id="2a396-123">Offre de toohello de modifications ne sont pas immédiatement visible toohello client.</span><span class="sxs-lookup"><span data-stu-id="2a396-123">Changes toohello offer are not immediately visible toohello tenant.</span></span> <span data-ttu-id="2a396-124">modifications de hello toosee, vous pouvez avoir nouvel abonnement toologout/connexion toosee hello dans hello « Sélecteur d’abonnement » lorsque la création de groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="2a396-124">toosee hello changes, you might have toologout/login toosee hello new subscription in hello “Subscription picker” when creating resources/resource groups.</span></span>

> [!NOTE]
><span data-ttu-id="2a396-125">Vous pouvez également créer des offres de valeur par défaut, les plans et les quotas à l’aide de PowerShell comme expliqué dans hello [Lisezmoi de l’administrateur du Service Azure pile](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin).</span><span class="sxs-lookup"><span data-stu-id="2a396-125">You can also create default offers, plans, and quotas by using PowerShell as explained in hello [Azure Stack Service Administrator readme](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin).</span></span>
>


## <a name="next-steps"></a><span data-ttu-id="2a396-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2a396-126">Next steps</span></span>
[<span data-ttu-id="2a396-127">S’abonner tooan offre et ensuite configurer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="2a396-127">Subscribe tooan offer and then provision a VM</span></span>](azure-stack-subscribe-plan-provision-vm.md)
