---
title: "Mise à l’échelle d’un service cloud Azure dans Windows PowerShell | Microsoft Docs"
description: "(classique) Découvrez comment utiliser PowerShell pour mettre à l’échelle un rôle web ou un rôle de travail dans Azure."
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: ee37dd8c-6714-4c61-adb8-03d6bbf76c9a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: mmccrory
ms.openlocfilehash: a7ae8ff202d403dff19b8c9a6a09492235db27ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-scale-a-cloud-service-in-powershell"></a><span data-ttu-id="040db-103">Mise à l’échelle d’un service cloud dans PowerShell</span><span class="sxs-lookup"><span data-stu-id="040db-103">How to scale a cloud service in PowerShell</span></span>

<span data-ttu-id="040db-104">Vous pouvez utiliser Windows PowerShell à pour mettre à l’échelle un rôle web ou un rôle de travail en ajoutant ou supprimant des instances.</span><span class="sxs-lookup"><span data-stu-id="040db-104">You can use Windows PowerShell to scale a web role or worker role in or out by adding or removing instances.</span></span>  

## <a name="log-in-to-azure"></a><span data-ttu-id="040db-105">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="040db-105">Log in to Azure</span></span>

<span data-ttu-id="040db-106">Avant de pouvoir effectuer des opérations sur votre abonnement via PowerShell, vous devez vous connecter :</span><span class="sxs-lookup"><span data-stu-id="040db-106">Before you can perform any operations on your subscription through PowerShell, you must log in:</span></span>

```powershell
Add-AzureAccount
```

<span data-ttu-id="040db-107">Si vous avez plusieurs abonnements associés à votre compte, vous devrez peut-être modifier l’abonnement actuel en fonction de l’emplacement de votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="040db-107">If you have multiple subscriptions associated with your account, you may need to change the current subscription depending on where your cloud service resides.</span></span> <span data-ttu-id="040db-108">Pour vérifier l’abonnement actuel, exécutez :</span><span class="sxs-lookup"><span data-stu-id="040db-108">To check the current subscription, run:</span></span>

```powershell
Get-AzureSubscription -Current
```

<span data-ttu-id="040db-109">Si vous devez modifier l’abonnement en cours, exécutez :</span><span class="sxs-lookup"><span data-stu-id="040db-109">If you need to change the current subscription, run:</span></span>

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-the-current-instance-count-for-your-role"></a><span data-ttu-id="040db-110">Vérifiez le nombre d’instances actuel pour votre rôle</span><span class="sxs-lookup"><span data-stu-id="040db-110">Check the current instance count for your role</span></span>

<span data-ttu-id="040db-111">Pour vérifier l’état actuel de votre rôle, exécutez :</span><span class="sxs-lookup"><span data-stu-id="040db-111">To check the current state of your role, run:</span></span>

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

<span data-ttu-id="040db-112">Vous devriez obtenir des informations sur le rôle, y compris la version actuelle de son système d’exploitation et le nombre d’instances.</span><span class="sxs-lookup"><span data-stu-id="040db-112">You should get back information about the role, including its current OS version and instance count.</span></span> <span data-ttu-id="040db-113">Dans ce cas, le rôle a une seule instance.</span><span class="sxs-lookup"><span data-stu-id="040db-113">In this case, the role has a single instance.</span></span>

![Informations sur le rôle](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-the-role-by-adding-more-instances"></a><span data-ttu-id="040db-115">Augmentation de la taille du rôle en ajoutant des instances</span><span class="sxs-lookup"><span data-stu-id="040db-115">Scale out the role by adding more instances</span></span>

<span data-ttu-id="040db-116">Pour augmenter la taille de votre rôle, passez le nombre souhaité d’instances en tant que paramètre **Count** paramètre à l’applet de commande **Set-AzureRole** :</span><span class="sxs-lookup"><span data-stu-id="040db-116">To scale out your role, pass the desired number of instances as the **Count** parameter to the **Set-AzureRole** cmdlet:</span></span>

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

<span data-ttu-id="040db-117">L’applet de commande se bloque momentanément pendant que les nouvelles instances sont configurées et démarrées.</span><span class="sxs-lookup"><span data-stu-id="040db-117">The cmdlet blocks momentarily while the new instances are provisioned and started.</span></span> <span data-ttu-id="040db-118">Pendant ce temps, si vous ouvrez une fenêtre PowerShell et appelez **Get-AzureRole** comme présenté précédemment, vous verrez le nouveau nombre d’instances cibles.</span><span class="sxs-lookup"><span data-stu-id="040db-118">During this time, if you open a new PowerShell window and call **Get-AzureRole** as shown earlier, you will see the new target instance count.</span></span> <span data-ttu-id="040db-119">Et si vous examinez l’état du rôle dans le portail, vous devriez voir la nouvelle instance démarrer :</span><span class="sxs-lookup"><span data-stu-id="040db-119">And if you inspect the role status in the portal, you should see the new instance starting up:</span></span>

![Instance de machine virtuelle en cours de démarrage dans le portail](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

<span data-ttu-id="040db-121">Une fois les nouvelles instances démarrées, l’applet de commande renvoie correctement :</span><span class="sxs-lookup"><span data-stu-id="040db-121">Once the new instances have started, the cmdlet will return successfully:</span></span>

![Augmentation du nombre d’instances du rôle réussie](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-the-role-by-removing-instances"></a><span data-ttu-id="040db-123">Diminution de la taille du rôle en supprimant des instances</span><span class="sxs-lookup"><span data-stu-id="040db-123">Scale in the role by removing instances</span></span>

<span data-ttu-id="040db-124">Vous pouvez diminuer la taille d’un rôle en supprimant des instances de la même façon.</span><span class="sxs-lookup"><span data-stu-id="040db-124">You can scale in a role by removing instances in the same way.</span></span> <span data-ttu-id="040db-125">Définissez le paramètre **Count** paramètre sur **Set-AzureRole** pour le nombre d’instances que vous souhaitez avoir une fois l’opération de mise à l’échelle terminée.</span><span class="sxs-lookup"><span data-stu-id="040db-125">Set the **Count** parameter on **Set-AzureRole** to the number of instances you want to have after the scale in operation is complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="040db-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="040db-126">Next steps</span></span>

<span data-ttu-id="040db-127">Il n’est pas possible de configurer la mise à l’échelle automatique pour les services cloud à partir de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="040db-127">It is not possible to configure auto-scale for cloud services from PowerShell.</span></span> <span data-ttu-id="040db-128">Pour ce faire, consultez [Mise à l’échelle automatique d’un service cloud](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="040db-128">To do that, see [How to auto scale a cloud service](cloud-services-how-to-scale-portal.md).</span></span>
