---
title: aaaScale un service cloud Azure dans Windows PowerShell | Documents Microsoft
description: "(classique) Découvrez comment toouse PowerShell tooscale un rôle web ou un rôle de travail ou arrière dans Azure."
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
ms.openlocfilehash: cfac6660e84f8ae24e4e9bdd5bf2016fb9cd7045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-a-cloud-service-in-powershell"></a><span data-ttu-id="bbe91-103">Comment tooscale un cloud service dans PowerShell</span><span class="sxs-lookup"><span data-stu-id="bbe91-103">How tooscale a cloud service in PowerShell</span></span>

<span data-ttu-id="bbe91-104">Vous pouvez utiliser Windows PowerShell tooscale un rôle web ou un rôle de travail ou en ajoutant ou supprimant des instances.</span><span class="sxs-lookup"><span data-stu-id="bbe91-104">You can use Windows PowerShell tooscale a web role or worker role in or out by adding or removing instances.</span></span>  

## <a name="log-in-tooazure"></a><span data-ttu-id="bbe91-105">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="bbe91-105">Log in tooAzure</span></span>

<span data-ttu-id="bbe91-106">Avant de pouvoir effectuer des opérations sur votre abonnement via PowerShell, vous devez vous connecter :</span><span class="sxs-lookup"><span data-stu-id="bbe91-106">Before you can perform any operations on your subscription through PowerShell, you must log in:</span></span>

```powershell
Add-AzureAccount
```

<span data-ttu-id="bbe91-107">Si vous avez plusieurs abonnements associés à votre compte, vous devrez peut-être toochange hello abonnement en fonction de l’emplacement de votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="bbe91-107">If you have multiple subscriptions associated with your account, you may need toochange hello current subscription depending on where your cloud service resides.</span></span> <span data-ttu-id="bbe91-108">toocheck hello abonnement actuel exécuter :</span><span class="sxs-lookup"><span data-stu-id="bbe91-108">toocheck hello current subscription, run:</span></span>

```powershell
Get-AzureSubscription -Current
```

<span data-ttu-id="bbe91-109">Si vous avez besoin d’abonnement toochange hello, exécutez :</span><span class="sxs-lookup"><span data-stu-id="bbe91-109">If you need toochange hello current subscription, run:</span></span>

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-hello-current-instance-count-for-your-role"></a><span data-ttu-id="bbe91-110">Vérifier le nombre d’instances actuelles hello pour votre rôle.</span><span class="sxs-lookup"><span data-stu-id="bbe91-110">Check hello current instance count for your role</span></span>

<span data-ttu-id="bbe91-111">état actuel de hello toocheck de votre rôle, exécutez :</span><span class="sxs-lookup"><span data-stu-id="bbe91-111">toocheck hello current state of your role, run:</span></span>

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

<span data-ttu-id="bbe91-112">Vous devez obtenir des informations sur le rôle hello, y compris son décompte de version et l’instance actuelle du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="bbe91-112">You should get back information about hello role, including its current OS version and instance count.</span></span> <span data-ttu-id="bbe91-113">Dans ce cas, le rôle de hello a une seule instance.</span><span class="sxs-lookup"><span data-stu-id="bbe91-113">In this case, hello role has a single instance.</span></span>

![Plus d’informations sur le rôle de hello](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-hello-role-by-adding-more-instances"></a><span data-ttu-id="bbe91-115">Rôle de hello faire évoluer en ajoutant plusieurs instances</span><span class="sxs-lookup"><span data-stu-id="bbe91-115">Scale out hello role by adding more instances</span></span>

<span data-ttu-id="bbe91-116">tooscale à votre rôle, passe hello nombre souhaité d’instances comme hello **nombre** paramètre toohello **Set-AzureRole** applet de commande :</span><span class="sxs-lookup"><span data-stu-id="bbe91-116">tooscale out your role, pass hello desired number of instances as hello **Count** parameter toohello **Set-AzureRole** cmdlet:</span></span>

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

<span data-ttu-id="bbe91-117">blocs d’applet de commande Hello momentanément lors de nouvelles instances de hello sont configurés et démarrés.</span><span class="sxs-lookup"><span data-stu-id="bbe91-117">hello cmdlet blocks momentarily while hello new instances are provisioned and started.</span></span> <span data-ttu-id="bbe91-118">Pendant ce temps, si vous ouvrez une nouvelle fenêtre PowerShell et appel **Get-AzureRole** comme indiqué précédemment, vous verrez le nombre d’instances hello nouvelle cible.</span><span class="sxs-lookup"><span data-stu-id="bbe91-118">During this time, if you open a new PowerShell window and call **Get-AzureRole** as shown earlier, you will see hello new target instance count.</span></span> <span data-ttu-id="bbe91-119">Et si vous Inspectez le statut du rôle hello dans le portail de hello, vous devez voir hello nouvelle instance démarre :</span><span class="sxs-lookup"><span data-stu-id="bbe91-119">And if you inspect hello role status in hello portal, you should see hello new instance starting up:</span></span>

![Instance de machine virtuelle en cours de démarrage dans le portail](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

<span data-ttu-id="bbe91-121">Une fois les nouvelles instances de hello ont démarré, applet de commande hello retournera correctement :</span><span class="sxs-lookup"><span data-stu-id="bbe91-121">Once hello new instances have started, hello cmdlet will return successfully:</span></span>

![Augmentation du nombre d’instances du rôle réussie](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-hello-role-by-removing-instances"></a><span data-ttu-id="bbe91-123">Mettre à l’échelle dans le rôle de hello en supprimant des instances</span><span class="sxs-lookup"><span data-stu-id="bbe91-123">Scale in hello role by removing instances</span></span>

<span data-ttu-id="bbe91-124">Vous pouvez faire évoluer dans un rôle en supprimant des instances de hello identique.</span><span class="sxs-lookup"><span data-stu-id="bbe91-124">You can scale in a role by removing instances in hello same way.</span></span> <span data-ttu-id="bbe91-125">Ensemble hello **nombre** paramètre sur **Set-AzureRole** toohello nombre d’instances souhaitées toohave après la mise à l’échelle de hello dans l’opération est terminée.</span><span class="sxs-lookup"><span data-stu-id="bbe91-125">Set hello **Count** parameter on **Set-AzureRole** toohello number of instances you want toohave after hello scale in operation is complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbe91-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bbe91-126">Next steps</span></span>

<span data-ttu-id="bbe91-127">Il n’est pas possible de tooconfigure à l’échelle automatique pour les services de cloud à partir de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bbe91-127">It is not possible tooconfigure auto-scale for cloud services from PowerShell.</span></span> <span data-ttu-id="bbe91-128">toodo qui, consultez [comment tooauto l’échelle un service cloud](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bbe91-128">toodo that, see [How tooauto scale a cloud service](cloud-services-how-to-scale-portal.md).</span></span>
