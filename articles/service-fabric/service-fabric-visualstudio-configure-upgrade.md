---
title: "mise à niveau de hello aaaConfigure d’une application de Service Fabric | Documents Microsoft"
description: "Découvrez comment tooconfigure hello les paramètres de mise à niveau d’une application de Service Fabric à l’aide de Microsoft Visual Studio."
services: service-fabric
documentationcenter: na
author: mikkelhegn
manager: mfussell
editor: tglee
ms.assetid: 1757ba85-0b7b-4f16-8a23-2ddaa61c86c6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/29/2017
ms.author: mikkelhegn
ms.openlocfilehash: 8ca50aa9d911f3c98f017490c8fe29011e8d80cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-upgrade-of-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="7377e-103">Configurer la mise à niveau hello d’une application de Service Fabric dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7377e-103">Configure hello upgrade of a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="7377e-104">Visual Studio tools pour Azure Service Fabric fournissent la prise en charge de mise à niveau pour la publication toolocal ou des clusters distants.</span><span class="sxs-lookup"><span data-stu-id="7377e-104">Visual Studio tools for Azure Service Fabric provide upgrade support for publishing toolocal or remote clusters.</span></span> <span data-ttu-id="7377e-105">Il existe trois scénarios dans lesquels vous tooupgrade tooa nouvelle version de votre application au lieu de remplacer l’application hello durant les tests et de débogage :</span><span class="sxs-lookup"><span data-stu-id="7377e-105">There are three scenarios in which you want tooupgrade your application tooa newer version instead of replacing hello application during testing and debugging:</span></span>

* <span data-ttu-id="7377e-106">Données d’application ne seront pas perdues pendant la mise à niveau hello.</span><span class="sxs-lookup"><span data-stu-id="7377e-106">Application data won't be lost during hello upgrade.</span></span>
* <span data-ttu-id="7377e-107">Disponibilité reste élevée afin qu’il ne sera pas y avoir toute interruption de service au cours de la mise à niveau de hello, s’il y a que suffisamment d’instances de service réparties sur plusieurs domaines de mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="7377e-107">Availability remains high so there won't be any service interruption during hello upgrade, if there are enough service instances spread across upgrade domains.</span></span>
* <span data-ttu-id="7377e-108">Une application peut faire l’objet de tests pendant sa mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="7377e-108">Tests can be run against an application while it's being upgraded.</span></span>

## <a name="parameters-needed-tooupgrade"></a><span data-ttu-id="7377e-109">Les paramètres nécessaires tooupgrade</span><span class="sxs-lookup"><span data-stu-id="7377e-109">Parameters needed tooupgrade</span></span>
<span data-ttu-id="7377e-110">Vous avez le choix entre deux types de déploiement : standard ou mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="7377e-110">You can choose from two types of deployment: regular or upgrade.</span></span> <span data-ttu-id="7377e-111">Un déploiement régulière efface les données sur le cluster de hello et les informations sur le déploiement précédent pendant un déploiement de mise à niveau conserve.</span><span class="sxs-lookup"><span data-stu-id="7377e-111">A regular deployment erases any previous deployment information and data on hello cluster, while an upgrade deployment preserves it.</span></span> <span data-ttu-id="7377e-112">Lorsque vous mettez à niveau une application de Service Fabric dans Visual Studio, vous devez tooprovide paramètres de mise à niveau l’application et les stratégies de contrôle d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="7377e-112">When you upgrade a Service Fabric application in Visual Studio, you need tooprovide application upgrade parameters and health check policies.</span></span> <span data-ttu-id="7377e-113">Mise à niveau de l’application les paramètres permettent de contrôler la mise à niveau de la hello, tandis que les stratégies de contrôle d’intégrité déterminent si la mise à niveau hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="7377e-113">Application upgrade parameters help control hello upgrade, while health check policies determine whether hello upgrade was successful.</span></span> <span data-ttu-id="7377e-114">Pour en savoir plus, consultez [Mise à niveau d’une application Service Fabric : paramètres de mise à niveau](service-fabric-application-upgrade-parameters.md) .</span><span class="sxs-lookup"><span data-stu-id="7377e-114">See [Service Fabric application upgrade: upgrade parameters](service-fabric-application-upgrade-parameters.md) for more details.</span></span>

<span data-ttu-id="7377e-115">Il existe trois modes de mise à niveau : *Monitored*, *UnmonitoredAuto* et *UnmonitoredManual*.</span><span class="sxs-lookup"><span data-stu-id="7377e-115">There are three upgrade modes: *Monitored*, *UnmonitoredAuto*, and *UnmonitoredManual*.</span></span>

* <span data-ttu-id="7377e-116">Une mise à niveau analysées automatise la mise à niveau hello et application du contrôle d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="7377e-116">A Monitored upgrade automates hello upgrade and application health check.</span></span>
* <span data-ttu-id="7377e-117">Une mise à niveau UnmonitoredAuto automatise la mise à niveau hello, mais ignore hello intégrité d’application.</span><span class="sxs-lookup"><span data-stu-id="7377e-117">An UnmonitoredAuto upgrade automates hello upgrade, but skips hello application health check.</span></span>
* <span data-ttu-id="7377e-118">Lorsque vous effectuez une mise à niveau UnmonitoredManual, vous devez toomanually mise à niveau de chaque domaine de mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="7377e-118">When you do an UnmonitoredManual upgrade, you need toomanually upgrade each upgrade domain.</span></span>

<span data-ttu-id="7377e-119">Chaque mode de mise à niveau nécessite différents jeux de paramètres.</span><span class="sxs-lookup"><span data-stu-id="7377e-119">Each upgrade mode requires different sets of parameters.</span></span> <span data-ttu-id="7377e-120">Consultez [paramètres de mise à niveau l’Application](service-fabric-application-upgrade-parameters.md) toolearn plus d’informations sur les options de mise à niveau disponibles hello.</span><span class="sxs-lookup"><span data-stu-id="7377e-120">See [Application upgrade parameters](service-fabric-application-upgrade-parameters.md) toolearn more about hello available upgrade options.</span></span>

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="7377e-121">Mise à niveau d’une application Service Fabric dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7377e-121">Upgrade a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="7377e-122">Si vous utilisez hello Visual Studio Service Fabric tools tooupgrade une application de Service Fabric, vous pouvez spécifier une mise à niveau au lieu d’un déploiement régulière un toobe de processus de publication en vérifiant hello **mise à niveau d’application hello** vérifier zone.</span><span class="sxs-lookup"><span data-stu-id="7377e-122">If you’re using hello Visual Studio Service Fabric tools tooupgrade a Service Fabric application, you can specify a publish process toobe an upgrade rather than a regular deployment by checking hello **Upgrade hello application** check box.</span></span>

### <a name="tooconfigure-hello-upgrade-parameters"></a><span data-ttu-id="7377e-123">paramètres de mise à niveau tooconfigure hello</span><span class="sxs-lookup"><span data-stu-id="7377e-123">tooconfigure hello upgrade parameters</span></span>
1. <span data-ttu-id="7377e-124">Cliquez sur hello **paramètres** bouton toohello case à cocher.</span><span class="sxs-lookup"><span data-stu-id="7377e-124">Click hello **Settings** button next toohello check box.</span></span> <span data-ttu-id="7377e-125">Hello **modifier les paramètres de mise à niveau** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7377e-125">hello **Edit Upgrade Parameters** dialog box appears.</span></span> <span data-ttu-id="7377e-126">Hello **modifier les paramètres de mise à niveau** boîte de dialogue prend en charge les modes mise à niveau de hello surveillés, UnmonitoredAuto et UnmonitoredManual.</span><span class="sxs-lookup"><span data-stu-id="7377e-126">hello **Edit Upgrade Parameters** dialog box supports hello Monitored, UnmonitoredAuto, and UnmonitoredManual upgrade modes.</span></span>
2. <span data-ttu-id="7377e-127">Sélectionnez hello le mode de mise à niveau que vous souhaitez toouse et puis remplissez à la grille de paramètres hello.</span><span class="sxs-lookup"><span data-stu-id="7377e-127">Select hello upgrade mode that you want toouse and then fill out hello parameter grid.</span></span>

    <span data-ttu-id="7377e-128">Chaque paramètre a des valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="7377e-128">Each parameter has default values.</span></span> <span data-ttu-id="7377e-129">paramètre facultatif de Hello *DefaultServiceTypeHealthPolicy* prend une entrée de table de hachage.</span><span class="sxs-lookup"><span data-stu-id="7377e-129">hello optional parameter *DefaultServiceTypeHealthPolicy* takes a hash table input.</span></span> <span data-ttu-id="7377e-130">Voici un exemple de format d’entrée de la table de hachage d’hello pour *DefaultServiceTypeHealthPolicy*:</span><span class="sxs-lookup"><span data-stu-id="7377e-130">Here’s an example of hello hash table input format for *DefaultServiceTypeHealthPolicy*:</span></span>

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    <span data-ttu-id="7377e-131">*ServiceTypeHealthPolicyMap* est un autre paramètre facultatif qui accepte une entrée de table de hachage Bonjour suivant format :</span><span class="sxs-lookup"><span data-stu-id="7377e-131">*ServiceTypeHealthPolicyMap* is another optional parameter that takes a hash table input in hello following format:</span></span>

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    <span data-ttu-id="7377e-132">Voici un exemple concret :</span><span class="sxs-lookup"><span data-stu-id="7377e-132">Here's a real-life example:</span></span>

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. <span data-ttu-id="7377e-133">Si vous sélectionnez le mode de mise à niveau UnmonitoredManual, vous devez manuellement un toocontinue de console PowerShell et terminer le processus de mise à niveau hello.</span><span class="sxs-lookup"><span data-stu-id="7377e-133">If you select UnmonitoredManual upgrade mode, you must manually start a PowerShell console toocontinue and finish hello upgrade process.</span></span> <span data-ttu-id="7377e-134">Consultez trop[mise à niveau de Service Fabric application : rubriques avancées](service-fabric-application-upgrade-advanced.md) toolearn manuel Mise à niveau fonctionne.</span><span class="sxs-lookup"><span data-stu-id="7377e-134">Refer too[Service Fabric application upgrade: advanced topics](service-fabric-application-upgrade-advanced.md) toolearn how manual upgrade works.</span></span>

## <a name="upgrade-an-application-by-using-powershell"></a><span data-ttu-id="7377e-135">Mettre à niveau une application à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="7377e-135">Upgrade an application by using PowerShell</span></span>
<span data-ttu-id="7377e-136">Vous pouvez utiliser les applets de commande de PowerShell tooupgrade une application de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7377e-136">You can use PowerShell cmdlets tooupgrade a Service Fabric application.</span></span> <span data-ttu-id="7377e-137">Pour plus d’informations, consultez [Didacticiel sur la mise à niveau d’une application Service Fabric](service-fabric-application-upgrade-tutorial.md) et [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx).</span><span class="sxs-lookup"><span data-stu-id="7377e-137">See [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md) and [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) for detailed information.</span></span>

## <a name="specify-a-health-check-policy-in-hello-application-manifest-file"></a><span data-ttu-id="7377e-138">Spécifier une stratégie de contrôle d’intégrité dans le fichier manifeste d’application hello</span><span class="sxs-lookup"><span data-stu-id="7377e-138">Specify a health check policy in hello application manifest file</span></span>
<span data-ttu-id="7377e-139">Chaque service dans une application de Service Fabric peut avoir ses propres paramètres de stratégie de contrôle d’intégrité qui remplacent les valeurs par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="7377e-139">Every service in a Service Fabric application can have its own health policy parameters that override hello default values.</span></span> <span data-ttu-id="7377e-140">Vous pouvez fournir ces valeurs de paramètre dans le fichier manifeste d’application hello.</span><span class="sxs-lookup"><span data-stu-id="7377e-140">You can provide these parameter values in hello application manifest file.</span></span>

<span data-ttu-id="7377e-141">Hello suivant montre comment tooapply un contrôle d’intégrité unique vérifier la stratégie pour chaque service dans le manifeste de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="7377e-141">hello following example shows how tooapply a unique health check policy for each service in hello application manifest.</span></span>

```xml
<Policies>
    <HealthPolicy ConsiderWarningAsError="false" MaxPercentUnhealthyDeployedApplications="20">
        <DefaultServiceTypeHealthPolicy MaxPercentUnhealthyServices="20"               
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />
        <ServiceTypeHealthPolicy ServiceTypeName="ServiceTypeName1"
                MaxPercentUnhealthyServices="20"
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />      
    </HealthPolicy>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="7377e-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7377e-142">Next steps</span></span>
<span data-ttu-id="7377e-143">Pour plus d'informations sur le déploiement d'une application, consultez la page [Déploiement d’une application existante dans Azure Service Fabric](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="7377e-143">For more information about deploying an application, see [Deploy an existing application in Azure Service Fabric](service-fabric-deploy-existing-app.md).</span></span>