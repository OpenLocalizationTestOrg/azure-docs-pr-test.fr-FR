---
title: aaaEnable Azure Application Insights Profiler sur une ressource de Services de cloud computing | Documents Microsoft
description: "Découvrez comment tooset de profileur hello sur une application ASP.NET hébergée par une ressource de Services de cloud computing Azure."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: b9ac3bca513bf4518f44780389a9f2945f6ccc98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a><span data-ttu-id="c3a6a-103">Activer Application Insights Profiler pour une ressource Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="c3a6a-103">Enable Application Insights Profiler on an Azure Cloud Services resource</span></span>

<span data-ttu-id="c3a6a-104">Cette procédure pas à pas montre comment tooenable Azure Application Insights Profiler une application ASP.NET hébergée par une ressource de Services de cloud computing Azure.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-104">This walkthrough demonstrates how tooenable Azure Application Insights Profiler on an ASP.NET application hosted by an Azure Cloud Services resource.</span></span> <span data-ttu-id="c3a6a-105">prise en charge pour les Machines virtuelles Azure, les machines virtuelles identiques et Azure Service Fabric sont des exemples de Hello.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-105">hello examples include support for Azure Virtual Machines, virtual machine scale sets, and Azure Service Fabric.</span></span> <span data-ttu-id="c3a6a-106">exemples Hello s’appuient sur des modèles qui prennent en charge le modèle de déploiement du Gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-106">hello examples all rely on templates that support hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="c3a6a-107">Pour plus d’informations sur le modèle de déploiement hello, passez en revue [Azure Resource Manager et déploiement classique : comprendre les modèles de déploiement et état de vos ressources de hello](/azure-resource-manager/resource-manager-deployment-model).</span><span class="sxs-lookup"><span data-stu-id="c3a6a-107">For more information about hello deployment model, review [Azure Resource Manager vs. classic deployment: Understand deployment models and hello state of your resources](/azure-resource-manager/resource-manager-deployment-model).</span></span>

## <a name="overview"></a><span data-ttu-id="c3a6a-108">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="c3a6a-108">Overview</span></span>

<span data-ttu-id="c3a6a-109">Hello suivant le diagramme illustre le fonctionne de générateur de profils hello pour les ressources des Services de cloud computing Azure.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-109">hello following diagram illustrates how hello profiler works for Azure Cloud Services resources.</span></span> <span data-ttu-id="c3a6a-110">Il utilise une machine virtuelle Azure comme exemple.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-110">It uses an Azure virtual machine as an example.</span></span>

<span data-ttu-id="c3a6a-111">![Vue d’ensemble](./media/enable-profiler-compute/overview.png) toocollect concernant le traitement et l’affichage sur hello portail Azure, vous devez installer le composant d’Agent de Diagnostics hello pour les ressources des Services de cloud computing Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-111">![Overview](./media/enable-profiler-compute/overview.png) toocollect information for processing and display on hello Azure portal, you must install hello Diagnostics Agent component for hello Azure Cloud Services resources.</span></span> <span data-ttu-id="c3a6a-112">Hello reste de la procédure pas à pas hello fournit des conseils sur la façon de tooinstall et configurer hello Agent de Diagnostics tooenable Application Insights Profiler.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-112">hello rest of hello walkthrough provides guidance on how tooinstall and configure hello Diagnostics Agent tooenable Application Insights Profiler.</span></span>

## <a name="prerequisites-for-hello-walkthrough"></a><span data-ttu-id="c3a6a-113">Configuration requise pour la procédure pas à pas hello</span><span class="sxs-lookup"><span data-stu-id="c3a6a-113">Prerequisites for hello walkthrough</span></span>

* <span data-ttu-id="c3a6a-114">Un modèle de gestionnaire de ressources de déploiement qui installe les agents de profileur hello sur hello machines virtuelles ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) ou mettre à l’échelle de jeux ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span><span class="sxs-lookup"><span data-stu-id="c3a6a-114">A deployment Resource Manager template that installs hello profiler agents on hello VMs ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) or scale sets ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span></span>

* <span data-ttu-id="c3a6a-115">Une instance Application Insights activée pour le profilage.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-115">An Application Insights instance enabled for profiling.</span></span> <span data-ttu-id="c3a6a-116">Pour obtenir des instructions, consultez [activer le profil hello](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span><span class="sxs-lookup"><span data-stu-id="c3a6a-116">For instructions, see [Enable hello profile](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span></span>

* <span data-ttu-id="c3a6a-117">Ressource de Services de cloud computing Azure de cible de .NET framework 4.6.1 ou version ultérieure installée sur hello.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-117">.NET Framework 4.6.1 or later installed on hello target Azure Cloud Services resource.</span></span>

## <a name="create-a-resource-group-in-your-azure-subscription"></a><span data-ttu-id="c3a6a-118">Créer un groupe de ressources dans votre abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="c3a6a-118">Create a resource group in your Azure subscription</span></span>
<span data-ttu-id="c3a6a-119">Bonjour à l’exemple suivant montre comment toocreate une ressource de groupe à l’aide d’un script PowerShell :</span><span class="sxs-lookup"><span data-stu-id="c3a6a-119">hello following example demonstrates how toocreate a resource group by using a PowerShell script:</span></span>

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-hello-resource-group"></a><span data-ttu-id="c3a6a-120">Créer une ressource Application Insights dans le groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="c3a6a-120">Create an Application Insights resource in hello resource group</span></span>
<span data-ttu-id="c3a6a-121">Sur hello **Application Insights** panneau, entrez les informations de hello pour votre ressource, comme indiqué dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="c3a6a-121">On hello **Application Insights** blade, enter hello information for your resource, as shown in this example:</span></span> 

![Panneau Application Insights](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-hello-azure-resource-manager-template"></a><span data-ttu-id="c3a6a-123">Appliquer une clé d’instrumentation Application Insights dans le modèle de gestionnaire de ressources Azure hello</span><span class="sxs-lookup"><span data-stu-id="c3a6a-123">Apply an Application Insights instrumentation key in hello Azure Resource Manager template</span></span>

1. <span data-ttu-id="c3a6a-124">Si vous n’avez pas encore téléchargé le modèle de hello, téléchargez-le à partir de [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span><span class="sxs-lookup"><span data-stu-id="c3a6a-124">If you haven't downloaded hello template yet, download it from [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span></span>

2. <span data-ttu-id="c3a6a-125">Trouver la clé d’Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-125">Find hello Application Insights key.</span></span>
   
   ![Emplacement de clé de hello](./media/enable-profiler-compute/copyaikey.png)

3. <span data-ttu-id="c3a6a-127">Remplacez la valeur de modèle hello.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-127">Replace hello template value.</span></span>
   
   ![Valeur de modèle de hello remplacé](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-toohost-hello-web-application"></a><span data-ttu-id="c3a6a-129">Créer une application web de machine virtuelle Azure toohost hello</span><span class="sxs-lookup"><span data-stu-id="c3a6a-129">Create an Azure VM toohost hello web application</span></span>
1. <span data-ttu-id="c3a6a-130">Créer un mot de passe de chaîne sécurisée toosave hello.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-130">Create a secure string toosave hello password.</span></span>

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. <span data-ttu-id="c3a6a-131">Déployer le modèle de gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-131">Deploy hello Azure Resource Manager template.</span></span>

   <span data-ttu-id="c3a6a-132">Modifier le répertoire hello dans hello PowerShell console toohello dossier qui contient votre modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-132">Change hello directory in hello PowerShell console toohello folder that contains your Resource Manager template.</span></span> <span data-ttu-id="c3a6a-133">modèle de hello toodeploy, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c3a6a-133">toodeploy hello template, run hello following command:</span></span>

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

<span data-ttu-id="c3a6a-134">Une fois le script de hello s’exécute correctement, vous devez trouver un ordinateur virtuel nommé **MyWindowsVM** dans votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-134">After hello script runs successfully, you should find a VM named **MyWindowsVM** in your resource group.</span></span>

## <a name="configure-web-deploy-on-hello-vm"></a><span data-ttu-id="c3a6a-135">Configurer Web Deploy sur hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c3a6a-135">Configure Web Deploy on hello VM</span></span>
<span data-ttu-id="c3a6a-136">Assurez-vous que l’extension Web Deploy est activée sur votre machine virtuelle pour pouvoir publier votre application web à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-136">Make sure that Web Deploy is enabled on your VM so you can publish your web application from Visual Studio.</span></span>

<span data-ttu-id="c3a6a-137">tooinstall Web Deploy sur un ordinateur virtuel manuellement via WebPI, consultez [installation et configuration de Web Deploy sur IIS 8.0 ou version ultérieure](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span><span class="sxs-lookup"><span data-stu-id="c3a6a-137">tooinstall Web Deploy on a VM manually via WebPI, see [Installing and Configuring Web Deploy on IIS 8.0 or Later](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span></span> <span data-ttu-id="c3a6a-138">Pour obtenir un exemple de procédure tooautomate l’installation de Web Deploy à l’aide d’un modèle Azure Resource Manager, consultez [créer, configurer et déployer un tooan d’application web Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span><span class="sxs-lookup"><span data-stu-id="c3a6a-138">For an example of how tooautomate installing Web Deploy by using an Azure Resource Manager template, see [Create, configure, and deploy a web application tooan Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span></span>

<span data-ttu-id="c3a6a-139">Si vous déployez une application ASP.NET MVC, consultez tooServer Manager, sélectionnez **Ajout de rôles et fonctionnalités** > **serveur Web (IIS)** > **Web Server**  >  **Développement d’applications**et activer ASP.NET 4.5 sur votre serveur.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-139">If you are deploying an ASP.NET MVC application, go tooServer Manager, select **Add Roles and Features** > **Web Server (IIS)** > **Web Server** > **Application Development**, and enable ASP.NET 4.5 on your server.</span></span>

![Ajouter ASP.NET](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-hello-azure-application-insights-sdk-for-your-project"></a><span data-ttu-id="c3a6a-141">Installer hello Kit de développement logiciel Azure Application Insights pour votre projet</span><span class="sxs-lookup"><span data-stu-id="c3a6a-141">Install hello Azure Application Insights SDK for your project</span></span>
1. <span data-ttu-id="c3a6a-142">Ouvrez votre application web ASP.NET dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-142">Open your ASP.NET web application in Visual Studio.</span></span>

2. <span data-ttu-id="c3a6a-143">Droit hello projet, puis sélectionnez **ajouter** > **Services connectés**.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-143">Right-click hello project and select **Add** > **Connected Services**.</span></span>

3. <span data-ttu-id="c3a6a-144">Sélectionnez **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-144">Select **Application Insights**.</span></span>

4. <span data-ttu-id="c3a6a-145">Suivez les instructions de hello sur la page de hello.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-145">Follow hello instructions on hello page.</span></span> <span data-ttu-id="c3a6a-146">Sélectionnez la ressource Application Insights hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-146">Select hello Application Insights resource that you created earlier.</span></span>

5. <span data-ttu-id="c3a6a-147">Sélectionnez hello **inscrire** bouton.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-147">Select hello **Register** button.</span></span>


## <a name="publish-hello-project-tooan-azure-vm"></a><span data-ttu-id="c3a6a-148">Publier hello projet tooan machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="c3a6a-148">Publish hello project tooan Azure VM</span></span>
<span data-ttu-id="c3a6a-149">Il existe plusieurs façons toopublish un tooan application Azure VM.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-149">There are several ways toopublish an application tooan Azure VM.</span></span> <span data-ttu-id="c3a6a-150">Une façon consiste toouse Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-150">One way is toouse Visual Studio 2017.</span></span>

1. <span data-ttu-id="c3a6a-151">Droit hello projet, puis sélectionnez **publier**.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-151">Right-click hello project and select **Publish**.</span></span>

2. <span data-ttu-id="c3a6a-152">Sélectionnez **des Machines virtuelles Microsoft Azure** comme hello cible de publication et suivez les étapes de hello.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-152">Select **Microsoft Azure Virtual Machines** as hello publish target and follow hello steps.</span></span>

   ![Publish-FromVS](./media/enable-profiler-compute/publishtoVM.png)

3. <span data-ttu-id="c3a6a-154">Exécutez un test de charge sur votre application.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-154">Run a load test against your application.</span></span> <span data-ttu-id="c3a6a-155">Vous devez voir les résultats sur la page Web du portail hello Application Insights instance.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-155">You should see results on hello Application Insights instance portal webpage.</span></span>


## <a name="enable-hello-profiler"></a><span data-ttu-id="c3a6a-156">Activer le Générateur de profils hello</span><span class="sxs-lookup"><span data-stu-id="c3a6a-156">Enable hello profiler</span></span>
1. <span data-ttu-id="c3a6a-157">Accédez tooyour Application Insights **performances** panneau et sélectionnez **configurer**.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-157">Go tooyour Application Insights **Performance** blade and select **Configure**.</span></span>
   
   ![Icône Configurer](./media/enable-profiler-compute/enableprofiler1.png)
 
2. <span data-ttu-id="c3a6a-159">Sélectionnez **Activer le profileur**.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-159">Select **Enable Profiler**.</span></span>
   
   ![Icône Activer le profileur](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-tooyour-application"></a><span data-ttu-id="c3a6a-161">Ajouter une application de tooyour de test de performances</span><span class="sxs-lookup"><span data-stu-id="c3a6a-161">Add a performance test tooyour application</span></span>
<span data-ttu-id="c3a6a-162">Afin de nous permettre de collecter certaines toobe de données exemple affichée dans le Générateur de profils Application Insights, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c3a6a-162">Follow these steps so we can collect some sample data toobe displayed in Application Insights Profiler:</span></span>

1. <span data-ttu-id="c3a6a-163">Parcourir la ressource Application Insights toohello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-163">Browse toohello Application Insights resource that you created earlier.</span></span> 

2. <span data-ttu-id="c3a6a-164">Accédez toohello **disponibilité** panneau et ajoutez un test de performances qui envoie l’URL d’application web demandes tooyour.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-164">Go toohello **Availability** blade and add a performance test that sends web requests tooyour application URL.</span></span> 

   ![Ajouter un test de performance](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a><span data-ttu-id="c3a6a-166">Afficher vos données de performances</span><span class="sxs-lookup"><span data-stu-id="c3a6a-166">View your performance data</span></span>

1. <span data-ttu-id="c3a6a-167">Attendez 10-15 minutes pour toocollect de profileur hello et analyser les données de hello.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-167">Wait 10-15 minutes for hello profiler toocollect and analyze hello data.</span></span> 

2. <span data-ttu-id="c3a6a-168">Accédez toohello **performances** lame dans votre ressource Application Insights et le mode de fonctionne de votre application lorsqu’il est sous charge.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-168">Go toohello **Performance** blade in your Application Insights resource and view how your application is performing when it's under load.</span></span>

   ![Affichage des données de performance](./media/enable-profiler-compute/aiperformance.png)

3. <span data-ttu-id="c3a6a-170">Icône hello sélectionnez sous **exemples** tooopen hello **vue Trace** panneau.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-170">Select hello icon under **Examples** tooopen hello **Trace View** blade.</span></span>

   ![Ouvrir le panneau d’affichage de la Trace hello](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a><span data-ttu-id="c3a6a-172">Utiliser un modèle existant</span><span class="sxs-lookup"><span data-stu-id="c3a6a-172">Work with an existing template</span></span>

1. <span data-ttu-id="c3a6a-173">Recherchez la déclaration de ressource hello Diagnostics Azure dans votre modèle de déploiement.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-173">Locate hello Azure Diagnostics resource declaration in your deployment template.</span></span>
   
   <span data-ttu-id="c3a6a-174">Si vous n’avez pas une déclaration, vous pouvez en créer un qui ressemble à la déclaration de hello Bonjour l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-174">If you don't have a declaration, you can create one that resembles hello declaration in hello following example.</span></span> <span data-ttu-id="c3a6a-175">Vous pouvez mettre à jour modèle hello hello [site Web de l’Explorateur de ressources Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c3a6a-175">You can update hello template from hello [Azure Resource Explorer website](https://resources.azure.com).</span></span>

2. <span data-ttu-id="c3a6a-176">Éditeur de hello de modification à partir de `Microsoft.Azure.Diagnostics` trop`AIP.Diagnostics.Test`.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-176">Change hello publisher from `Microsoft.Azure.Diagnostics` too`AIP.Diagnostics.Test`.</span></span>

3. <span data-ttu-id="c3a6a-177">Pour `typeHandlerVersion`, utilisez `0.0`.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-177">For `typeHandlerVersion`, use `0.0`.</span></span>

4. <span data-ttu-id="c3a6a-178">Assurez-vous que `autoUpgradeMinorVersion` est défini trop`true`.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-178">Make sure that `autoUpgradeMinorVersion` is set too`true`.</span></span>

5. <span data-ttu-id="c3a6a-179">Ajouter hello nouvelle `ApplicationInsightsProfiler` instance récepteur Bonjour `WadCfg` objet de paramètres, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="c3a6a-179">Add hello new `ApplicationInsightsProfiler` sink instance in hello `WadCfg` settings object, as shown in hello following example:</span></span>

```
"resources": [
        {
          "type": "extensions",
          "name": "Microsoft.Insights.VMDiagnosticsSettings",
          "apiVersion": "2016-03-30",
          "properties": {
            "publisher": "AIP.Diagnostics.Test",
            "type": "IaaSDiagnostics",
            "typeHandlerVersion": "0.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "WadCfg": {
                "SinksConfig": {
                  "Sink": [
                    {
                      "name": "Give a descriptive short name. E.g.: MyApplicationInsightsProfilerSink",
                      "ApplicationInsightsProfiler": "Enter hello Application Insights instance instrumentation key guid here"
                    }
                  ]
                },
                "DiagnosticMonitorConfiguration": {
                    ...
                }
                ...
              }
              ...
            }
            ...
          }
          ...
]
```

## <a name="enable-hello-profiler-on-virtual-machine-scale-sets"></a><span data-ttu-id="c3a6a-180">Activer le profileur hello sur des machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="c3a6a-180">Enable hello profiler on virtual machine scale sets</span></span>
<span data-ttu-id="c3a6a-181">toosee comment tooenable hello profiler, télécharger hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) modèle.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-181">toosee how tooenable hello profiler, download hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) template.</span></span> <span data-ttu-id="c3a6a-182">Appliquer hello modifications dans une ressource d’extension de machine virtuelle modèle toohello diagnostics pour l’ensemble d’échelle de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-182">Apply hello same changes in a VM template toohello diagnostics extension resource for hello virtual machine scale set.</span></span>

<span data-ttu-id="c3a6a-183">Assurez-vous que chaque instance dans l’ensemble d’échelle hello a toohello d’accès internet.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-183">Make sure that each instance in hello scale set has access toohello internet.</span></span> <span data-ttu-id="c3a6a-184">Hello Agent Profiler peut alors envoyer des exemples de hello collectée Insights tooApplication pour l’affichage et analyse.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-184">hello Profiler Agent can then send hello collected samples tooApplication Insights for display and analysis.</span></span>

## <a name="enable-hello-profiler-on-service-fabric-applications"></a><span data-ttu-id="c3a6a-185">Activer le profileur hello sur les applications de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c3a6a-185">Enable hello profiler on Service Fabric applications</span></span>
1. <span data-ttu-id="c3a6a-186">Hello configurer l’infrastructure du Service cluster toohave hello extension Azure Diagnostics qui installe hello Agent Profiler.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-186">Provision hello Service Fabric cluster toohave hello Azure Diagnostics extension that installs hello Profiler Agent.</span></span>

2. <span data-ttu-id="c3a6a-187">Installer hello Application Insights SDK dans le projet de hello et configurer la clé d’Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-187">Install hello Application Insights SDK in hello project and configure hello Application Insights key.</span></span>

3. <span data-ttu-id="c3a6a-188">Ajouter des données de télémétrie application code tooinstrument.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-188">Add application code tooinstrument telemetry.</span></span>

### <a name="provision-hello-service-fabric-cluster-toohave-hello-azure-diagnostics-extension-that-installs-hello-profiler-agent"></a><span data-ttu-id="c3a6a-189">Configurer Bonjour Service Fabric cluster toohave Bonjour extension Azure Diagnostics qui installe hello Agent Profiler</span><span class="sxs-lookup"><span data-stu-id="c3a6a-189">Provision hello Service Fabric cluster toohave hello Azure Diagnostics extension that installs hello Profiler Agent</span></span>
<span data-ttu-id="c3a6a-190">Un cluster Service Fabric peut être sécurisé ou non sécurisé.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-190">A Service Fabric cluster can be secure or non-secure.</span></span> <span data-ttu-id="c3a6a-191">Vous pouvez définir un toobe de cluster de passerelle non sécurisées afin qu’il ne nécessite pas un certificat pour l’accès.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-191">You can set one gateway cluster toobe non-secure so it doesn't require a certificate for access.</span></span> <span data-ttu-id="c3a6a-192">Les clusters qui hébergent les données et la logique métier doivent être sécurisés.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-192">Clusters that host business logic and data should be secure.</span></span> <span data-ttu-id="c3a6a-193">Vous pouvez activer le profileur hello sur des clusters Service Fabric sécurisées et non sécurisées.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-193">You can enable hello profiler on both secure and non-secure Service Fabric clusters.</span></span> <span data-ttu-id="c3a6a-194">Cette procédure pas à pas utilise un cluster non sécurisées comme un tooexplain exemple quelles modifications sont requises tooenable hello profiler.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-194">This walkthrough uses a non-secure cluster as an example tooexplain what changes are required tooenable hello profiler.</span></span> <span data-ttu-id="c3a6a-195">Vous pouvez configurer un cluster sécurisé Bonjour identique.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-195">You can provision a secure cluster in hello same way.</span></span>

1. <span data-ttu-id="c3a6a-196">Téléchargez le fichier [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span><span class="sxs-lookup"><span data-stu-id="c3a6a-196">Download [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span></span> <span data-ttu-id="c3a6a-197">Comme pour les machines virtuelles et les groupes de machines virtuelles identiques, remplacez `Application_Insights_Key` par votre clé Application Insights :</span><span class="sxs-lookup"><span data-stu-id="c3a6a-197">As you did for VMs and virtual machine scale sets, replace `Application_Insights_Key` with your Application Insights key:</span></span>

   ```
   "publisher": "AIP.Diagnostics.Test",
                 "settings": {
                   "WadCfg": {
                     "SinksConfig": {
                       "Sink": [
                         {
                           "name": "MyApplicationInsightsProfilerSinkVMSS",
                           "ApplicationInsightsProfiler": "[Application_Insights_Key]"
                         }
                       ]
                     },
   ```

2. <span data-ttu-id="c3a6a-198">Déployer le modèle de hello à l’aide d’un script PowerShell :</span><span class="sxs-lookup"><span data-stu-id="c3a6a-198">Deploy hello template by using a PowerShell script:</span></span>

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-hello-application-insights-sdk-in-hello-project-and-configure-hello-application-insights-key"></a><span data-ttu-id="c3a6a-199">Installer hello Application Insights SDK dans le projet de hello et configurer la clé d’Application Insights hello</span><span class="sxs-lookup"><span data-stu-id="c3a6a-199">Install hello Application Insights SDK in hello project and configure hello Application Insights key</span></span>
<span data-ttu-id="c3a6a-200">Installer hello Application Insights SDK à partir de hello [package NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="c3a6a-200">Install hello Application Insights SDK from hello [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="c3a6a-201">Assurez-vous que vous installez une version stable, 2.3 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-201">Make sure that you install a stable version, 2.3 or later.</span></span> 

<span data-ttu-id="c3a6a-202">Pour plus d’informations sur la configuration d’Application Insights dans vos projets, voir [Utilisation de Service Fabric avec Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span><span class="sxs-lookup"><span data-stu-id="c3a6a-202">For information about configuring Application Insights in your projects, see [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span></span>

### <a name="add-application-code-tooinstrument-telemetry"></a><span data-ttu-id="c3a6a-203">Ajouter des données de télémétrie application code tooinstrument</span><span class="sxs-lookup"><span data-stu-id="c3a6a-203">Add application code tooinstrument telemetry</span></span>
1. <span data-ttu-id="c3a6a-204">Pour tout type de code que vous souhaitez tooinstrument, ajouter une à l’aide de l’instruction autour de lui.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-204">For any piece of code that you want tooinstrument, add a using statement around it.</span></span> 

   <span data-ttu-id="c3a6a-205">Dans l’exemple suivant de hello, hello `RunAsync` méthode est effectue un travail et hello `telemetryClient` classe capture les données de télémétrie hello après son démarrage.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-205">In hello following  example, hello `RunAsync` method is doing some work, and hello `telemetryClient` class captures hello telemetry after it starts.</span></span> <span data-ttu-id="c3a6a-206">événement de Hello requiert un nom unique dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-206">hello event needs a unique name across hello application.</span></span>

   ```
   protected override async Task RunAsync(CancellationToken cancellationToken)
       {
           // TODO: Replace hello following sample code with your own logic
           //       or remove this RunAsync override if it's not needed in your service.

           while (true)
           {
               using( var operation = telemetryClient.StartOperation<RequestTelemetry>("[Insert_Event_Unique_Name]"))
               {
                   cancellationToken.ThrowIfCancellationRequested();

                   ++this.iterations;

                   ServiceEventSource.Current.ServiceMessage(this.Context, "Working-{0}", this.iterations);

                   await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
               }

           }
       }
   ```

2. <span data-ttu-id="c3a6a-207">Déployer votre cluster de Service Fabric application toohello.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-207">Deploy your application toohello Service Fabric cluster.</span></span> <span data-ttu-id="c3a6a-208">Attendez hello application toorun pendant 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-208">Wait for hello app toorun for 10 minutes.</span></span> <span data-ttu-id="c3a6a-209">Pour un meilleur effet, vous pouvez exécuter un test de charge sur l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-209">For better effect, you can run a load test on hello app.</span></span> <span data-ttu-id="c3a6a-210">Du portail de l’Application Insights accédez toohello **performances** panneau et vous devez voir exemples de traces de profilage s’affichent.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-210">Go toohello Application Insights portal's **Performance** blade, and you should see examples of profiling traces appear.</span></span>

<!---
Commenting out these sections for now
## Enable hello Profiler on Cloud Services applications
[TODO]
## Enable hello Profiler on classic Azure Virtual Machines
[TODO]
## Enable hello Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a><span data-ttu-id="c3a6a-211">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c3a6a-211">Next steps</span></span>

- <span data-ttu-id="c3a6a-212">Trouvez de l’aide pour résoudre les problèmes rencontrés avec le profileur en consultant l’article [Résolution des problèmes de profileur](app-insights-profiler.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="c3a6a-212">Find help with troubleshooting profiler issues in [Profiler troubleshooting](app-insights-profiler.md#troubleshooting).</span></span>

- <span data-ttu-id="c3a6a-213">En savoir plus sur le profileur hello dans [Application Insights Profiler](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="c3a6a-213">Read more about hello profiler in [Application Insights Profiler](app-insights-profiler.md).</span></span>
