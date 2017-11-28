---
title: "Configuration de la mise à niveau d’une application Service Fabric | Microsoft Docs"
description: "Apprenez à configurer les paramètres de mise à niveau d'une application Service Fabric à l'aide de Microsoft Visual Studio."
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
ms.openlocfilehash: 314b29a56e4651222822f40a116af97a7372ff2c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-upgrade-of-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="d8dd3-103">Configuration de la mise à niveau d’une application Service Fabric dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d8dd3-103">Configure the upgrade of a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="d8dd3-104">Les outils Visual Studio pour Azure Service Fabric fournissent une prise en charge des mises à niveau pour la publication vers des clusters locaux ou distants.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-104">Visual Studio tools for Azure Service Fabric provide upgrade support for publishing to local or remote clusters.</span></span> <span data-ttu-id="d8dd3-105">Voici les trois cas dans lesquels vous devriez mettre à niveau votre application vers une version plus récente au lieu de la remplacer durant les tests et le débogage :</span><span class="sxs-lookup"><span data-stu-id="d8dd3-105">There are three scenarios in which you want to upgrade your application to a newer version instead of replacing the application during testing and debugging:</span></span>

* <span data-ttu-id="d8dd3-106">Les données d’application ne sont pas perdues lors de la mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-106">Application data won't be lost during the upgrade.</span></span>
* <span data-ttu-id="d8dd3-107">La disponibilité reste élevée, car le service n’est pas interrompu au cours de la mise à niveau s’il y a suffisamment d’instances de service réparties sur plusieurs domaines de mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-107">Availability remains high so there won't be any service interruption during the upgrade, if there are enough service instances spread across upgrade domains.</span></span>
* <span data-ttu-id="d8dd3-108">Une application peut faire l’objet de tests pendant sa mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-108">Tests can be run against an application while it's being upgraded.</span></span>

## <a name="parameters-needed-to-upgrade"></a><span data-ttu-id="d8dd3-109">Paramètres nécessaires à la mise à niveau</span><span class="sxs-lookup"><span data-stu-id="d8dd3-109">Parameters needed to upgrade</span></span>
<span data-ttu-id="d8dd3-110">Vous avez le choix entre deux types de déploiement : standard ou mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-110">You can choose from two types of deployment: regular or upgrade.</span></span> <span data-ttu-id="d8dd3-111">Un déploiement standard efface les informations relatives à tout déploiement précédent ainsi que les données du cluster, tandis qu’un déploiement de mise à niveau les conserve.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-111">A regular deployment erases any previous deployment information and data on the cluster, while an upgrade deployment preserves it.</span></span> <span data-ttu-id="d8dd3-112">Lorsque vous mettez à niveau une application Service Fabric dans Visual Studio, vous devez fournir les paramètres de mise à niveau de l'application et les stratégies de contrôle d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-112">When you upgrade a Service Fabric application in Visual Studio, you need to provide application upgrade parameters and health check policies.</span></span> <span data-ttu-id="d8dd3-113">Les paramètres de mise à niveau de l’application permettent de contrôler la mise à niveau, tandis que les stratégies de contrôle d’intégrité déterminent si la mise à niveau a réussi.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-113">Application upgrade parameters help control the upgrade, while health check policies determine whether the upgrade was successful.</span></span> <span data-ttu-id="d8dd3-114">Pour en savoir plus, consultez [Mise à niveau d’une application Service Fabric : paramètres de mise à niveau](service-fabric-application-upgrade-parameters.md) .</span><span class="sxs-lookup"><span data-stu-id="d8dd3-114">See [Service Fabric application upgrade: upgrade parameters](service-fabric-application-upgrade-parameters.md) for more details.</span></span>

<span data-ttu-id="d8dd3-115">Il existe trois modes de mise à niveau : *Monitored*, *UnmonitoredAuto* et *UnmonitoredManual*.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-115">There are three upgrade modes: *Monitored*, *UnmonitoredAuto*, and *UnmonitoredManual*.</span></span>

* <span data-ttu-id="d8dd3-116">Une mise à niveau Monitored automatise la mise à niveau et le contrôle d’intégrité de l’application.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-116">A Monitored upgrade automates the upgrade and application health check.</span></span>
* <span data-ttu-id="d8dd3-117">Une mise à niveau UnmonitoredAuto automatise la mise à niveau, mais ignore le contrôle d’intégrité de l’application.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-117">An UnmonitoredAuto upgrade automates the upgrade, but skips the application health check.</span></span>
* <span data-ttu-id="d8dd3-118">Quand vous effectuez une mise à niveau UnmonitoredManual, vous devez mettre à niveau manuellement chaque domaine de mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-118">When you do an UnmonitoredManual upgrade, you need to manually upgrade each upgrade domain.</span></span>

<span data-ttu-id="d8dd3-119">Chaque mode de mise à niveau nécessite différents jeux de paramètres.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-119">Each upgrade mode requires different sets of parameters.</span></span> <span data-ttu-id="d8dd3-120">Pour en savoir plus sur les options de mise à niveau disponibles, consultez [Paramètres de mise à niveau d’application](service-fabric-application-upgrade-parameters.md) .</span><span class="sxs-lookup"><span data-stu-id="d8dd3-120">See [Application upgrade parameters](service-fabric-application-upgrade-parameters.md) to learn more about the available upgrade options.</span></span>

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="d8dd3-121">Mise à niveau d’une application Service Fabric dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d8dd3-121">Upgrade a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="d8dd3-122">Si vous utilisez les outils Service Fabric de Visual Studio pour mettre à niveau une application Service Fabric, vous pouvez préciser si le processus de publication doit être une mise à niveau plutôt qu’un déploiement standard en cochant la case **Mettre à niveau l’application** .</span><span class="sxs-lookup"><span data-stu-id="d8dd3-122">If you’re using the Visual Studio Service Fabric tools to upgrade a Service Fabric application, you can specify a publish process to be an upgrade rather than a regular deployment by checking the **Upgrade the application** check box.</span></span>

### <a name="to-configure-the-upgrade-parameters"></a><span data-ttu-id="d8dd3-123">Pour configurer les paramètres de mise à niveau</span><span class="sxs-lookup"><span data-stu-id="d8dd3-123">To configure the upgrade parameters</span></span>
1. <span data-ttu-id="d8dd3-124">Cliquez sur le bouton **Paramètres** en regard de la case à cocher.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-124">Click the **Settings** button next to the check box.</span></span> <span data-ttu-id="d8dd3-125">La boîte de dialogue **Modifier les paramètres de mise à niveau** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-125">The **Edit Upgrade Parameters** dialog box appears.</span></span> <span data-ttu-id="d8dd3-126">La boîte de dialogue **Modifier les paramètres de mise à niveau** prend en charge les modes de mise à niveau Monitored, UnmonitoredAuto et UnmonitoredManual.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-126">The **Edit Upgrade Parameters** dialog box supports the Monitored, UnmonitoredAuto, and UnmonitoredManual upgrade modes.</span></span>
2. <span data-ttu-id="d8dd3-127">Sélectionnez le mode de mise à niveau que vous souhaitez utiliser, puis remplissez la grille de paramètres.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-127">Select the upgrade mode that you want to use and then fill out the parameter grid.</span></span>

    <span data-ttu-id="d8dd3-128">Chaque paramètre a des valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-128">Each parameter has default values.</span></span> <span data-ttu-id="d8dd3-129">Le paramètre facultatif *DefaultServiceTypeHealthPolicy* accepte une entrée de table de hachage.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-129">The optional parameter *DefaultServiceTypeHealthPolicy* takes a hash table input.</span></span> <span data-ttu-id="d8dd3-130">Voici un exemple du format d'entrée de table de hachage pour *DefaultServiceTypeHealthPolicy*:</span><span class="sxs-lookup"><span data-stu-id="d8dd3-130">Here’s an example of the hash table input format for *DefaultServiceTypeHealthPolicy*:</span></span>

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    <span data-ttu-id="d8dd3-131">*ServiceTypeHealthPolicyMap* est un autre paramètre facultatif qui acceptant une entrée de table de hachage au format suivant :</span><span class="sxs-lookup"><span data-stu-id="d8dd3-131">*ServiceTypeHealthPolicyMap* is another optional parameter that takes a hash table input in the following format:</span></span>

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    <span data-ttu-id="d8dd3-132">Voici un exemple concret :</span><span class="sxs-lookup"><span data-stu-id="d8dd3-132">Here's a real-life example:</span></span>

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. <span data-ttu-id="d8dd3-133">Si vous sélectionnez le mode de mise à niveau UnmonitoredManual, vous devrez démarrer manuellement une console PowerShell pour continuer et terminer le processus de mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-133">If you select UnmonitoredManual upgrade mode, you must manually start a PowerShell console to continue and finish the upgrade process.</span></span> <span data-ttu-id="d8dd3-134">Pour en savoir plus sur le fonctionnement de la mise à niveau manuelle, consultez [Mise à niveau d’une application Service Fabric : rubriques avancées](service-fabric-application-upgrade-advanced.md) .</span><span class="sxs-lookup"><span data-stu-id="d8dd3-134">Refer to [Service Fabric application upgrade: advanced topics](service-fabric-application-upgrade-advanced.md) to learn how manual upgrade works.</span></span>

## <a name="upgrade-an-application-by-using-powershell"></a><span data-ttu-id="d8dd3-135">Mettre à niveau une application à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8dd3-135">Upgrade an application by using PowerShell</span></span>
<span data-ttu-id="d8dd3-136">Vous pouvez utiliser les applets de commande PowerShell pour mettre à niveau une application Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-136">You can use PowerShell cmdlets to upgrade a Service Fabric application.</span></span> <span data-ttu-id="d8dd3-137">Pour plus d’informations, consultez [Didacticiel sur la mise à niveau d’une application Service Fabric](service-fabric-application-upgrade-tutorial.md) et [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8dd3-137">See [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md) and [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) for detailed information.</span></span>

## <a name="specify-a-health-check-policy-in-the-application-manifest-file"></a><span data-ttu-id="d8dd3-138">Spécifier une stratégie de contrôle d’intégrité dans le fichier manifeste d’application</span><span class="sxs-lookup"><span data-stu-id="d8dd3-138">Specify a health check policy in the application manifest file</span></span>
<span data-ttu-id="d8dd3-139">Chaque service d’une application Service Fabric peut avoir ses propres paramètres de stratégie de contrôle d'intégrité, qui remplacent alors les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-139">Every service in a Service Fabric application can have its own health policy parameters that override the default values.</span></span> <span data-ttu-id="d8dd3-140">Vous pouvez définir les valeurs de ces paramètres dans le fichier manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-140">You can provide these parameter values in the application manifest file.</span></span>

<span data-ttu-id="d8dd3-141">L'exemple suivant montre comment appliquer une stratégie de contrôle d'intégrité unique pour chaque service du manifeste d'application.</span><span class="sxs-lookup"><span data-stu-id="d8dd3-141">The following example shows how to apply a unique health check policy for each service in the application manifest.</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="d8dd3-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d8dd3-142">Next steps</span></span>
<span data-ttu-id="d8dd3-143">Pour plus d'informations sur le déploiement d'une application, consultez la page [Déploiement d’une application existante dans Azure Service Fabric](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="d8dd3-143">For more information about deploying an application, see [Deploy an existing application in Azure Service Fabric](service-fabric-deploy-existing-app.md).</span></span>