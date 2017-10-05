---
title: Utilisation des diagnostics (.NET) Azure avec Cloud Services | Microsoft Docs
description: "Utilisation des diagnostics Azure pour rassembler des données à partir d’Azure Cloud Services pour le débogage, la mesure des performances, la surveillance, l’analyse du trafic, etc."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 89623a0e-4e78-4b67-a446-7d19a35a44be
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/22/2017
ms.author: robb
ms.openlocfilehash: 333d2f26ce043a167fb84858c8327cb39e868ffa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a><span data-ttu-id="28c85-103">Activation des diagnostics Azure dans Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="28c85-103">Enabling Azure Diagnostics in Azure Cloud Services</span></span>
<span data-ttu-id="28c85-104">Consultez la page [Présentation des diagnostics Azure](../azure-diagnostics.md) pour obtenir des informations sur les diagnostics Azure.</span><span class="sxs-lookup"><span data-stu-id="28c85-104">See [Azure Diagnostics Overview](../azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-to-enable-diagnostics-in-a-worker-role"></a><span data-ttu-id="28c85-105">Activation de Diagnostics dans un rôle de travail</span><span class="sxs-lookup"><span data-stu-id="28c85-105">How to Enable Diagnostics in a Worker Role</span></span>
<span data-ttu-id="28c85-106">Cette procédure pas à pas décrit comment mettre en oeuvre un rôle de travail Azure qui émet des données télémétriques à l'aide de la classe EventSource .NET.</span><span class="sxs-lookup"><span data-stu-id="28c85-106">This walkthrough describes how to implement an Azure worker role that emits telemetry data using the .NET EventSource class.</span></span> <span data-ttu-id="28c85-107">Azure Diagnostics est utilisé pour collecter des données télémétriques et les stocker dans un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="28c85-107">Azure Diagnostics is used to collect the telemetry data and store it in an Azure storage account.</span></span> <span data-ttu-id="28c85-108">Lors de la création d'un rôle de travail, Visual Studio active automatiquement Diagnostics 1.0 dans le cadre de la solution dans les Kits de développement logiciel (SDK) pour .NET 2.4 et versions antérieures.</span><span class="sxs-lookup"><span data-stu-id="28c85-108">When creating a worker role, Visual Studio automatically enables Diagnostics 1.0 as part of the solution in Azure SDKs for .NET 2.4 and earlier.</span></span> <span data-ttu-id="28c85-109">Les instructions suivantes décrivent le processus de création d'un rôle de travail, de désactivation de Diagnostics 1.0 de la solution, et de déploiement de Diagnostics 1.2 ou 1.3 sur votre rôle de travail.</span><span class="sxs-lookup"><span data-stu-id="28c85-109">The following instructions describe the process for creating the worker role, disabling Diagnostics 1.0 from the solution, and deploying Diagnostics 1.2 or 1.3 to your worker role.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="28c85-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="28c85-110">Prerequisites</span></span>
<span data-ttu-id="28c85-111">Cet article part du principe que vous disposez d’un abonnement Azure et que vous utilisez Visual Studio avec le Kit de développement logiciel (SDK) Azure.</span><span class="sxs-lookup"><span data-stu-id="28c85-111">This article assumes you have an Azure subscription and are using Visual Studio with the Azure SDK.</span></span> <span data-ttu-id="28c85-112">Si vous n’avez pas d’abonnement Azure, vous pouvez vous inscrire pour bénéficier d’une [version d’évaluation gratuite][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="28c85-112">If you do not have an Azure subscription, you can sign up for the [Free Trial][Free Trial].</span></span> <span data-ttu-id="28c85-113">Assurez-vous d’avoir [installé et configuré Azure PowerShell version 0.8.7 ou ultérieure][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="28c85-113">Make sure to [Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-worker-role"></a><span data-ttu-id="28c85-114">Étape 1 : création d’un rôle de travail</span><span class="sxs-lookup"><span data-stu-id="28c85-114">Step 1: Create a Worker Role</span></span>
1. <span data-ttu-id="28c85-115">Lancez **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="28c85-115">Launch **Visual Studio**.</span></span>
2. <span data-ttu-id="28c85-116">Créez un projet **Azure Cloud Services** à partir du modèle **Cloud** qui cible .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="28c85-116">Create an **Azure Cloud Service** project from the **Cloud** template that targets .NET Framework 4.5.</span></span>  <span data-ttu-id="28c85-117">Nommez le projet « WadExample » et cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="28c85-117">Name the project "WadExample" and click Ok.</span></span>
3. <span data-ttu-id="28c85-118">Sélectionnez **Rôle de travail** et cliquez sur Ok.</span><span class="sxs-lookup"><span data-stu-id="28c85-118">Select **Worker Role** and click Ok.</span></span> <span data-ttu-id="28c85-119">Le projet est créé.</span><span class="sxs-lookup"><span data-stu-id="28c85-119">The project will be created.</span></span>
4. <span data-ttu-id="28c85-120">Dans **Explorateur de solutions**, double-cliquez sur le fichier de propriétés **WorkerRole1**.</span><span class="sxs-lookup"><span data-stu-id="28c85-120">In **Solution Explorer**, double-click the **WorkerRole1** properties file.</span></span>
5. <span data-ttu-id="28c85-121">Dans l’onglet **Configuration**, décochez **Activer Diagnostics** pour désactiver Diagnostics 1.0 (Kit de développement Azure 2.4 et versions antérieures).</span><span class="sxs-lookup"><span data-stu-id="28c85-121">In the **Configuration** tab, un-check **Enable Diagnostics** to disable Diagnostics 1.0 (Azure SDK 2.4 and earlier).</span></span>
6. <span data-ttu-id="28c85-122">Générez votre solution pour vérifier que vous n'avez pas d'erreurs.</span><span class="sxs-lookup"><span data-stu-id="28c85-122">Build your solution to verify that you have no errors.</span></span>

### <a name="step-2-instrument-your-code"></a><span data-ttu-id="28c85-123">Étape 2 : instrumentalisation de votre code</span><span class="sxs-lookup"><span data-stu-id="28c85-123">Step 2: Instrument your code</span></span>
<span data-ttu-id="28c85-124">Remplacez le contenu de WorkerRole.cs par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="28c85-124">Replace the contents of WorkerRole.cs with the following code.</span></span> <span data-ttu-id="28c85-125">La classe SampleEventSourceWriter, héritée de la classe [EventSource][EventSource Class], implémente quatre méthodes de journalisation : **SendEnums**, **MessageMethod**, **SetOther** et **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="28c85-125">The class SampleEventSourceWriter, inherited from the [EventSource Class][EventSource Class], implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="28c85-126">Le premier paramètre de la méthode **WriteEvent** définit l’ID de l’événement respectif.</span><span class="sxs-lookup"><span data-stu-id="28c85-126">The first parameter to the **WriteEvent** method defines the ID for the respective event.</span></span> <span data-ttu-id="28c85-127">La méthode Run implémente une boucle infinie qui appelle chacune des méthodes de journalisation implémentées dans la classe **SampleEventSourceWriter** toutes les 10 secondes.</span><span class="sxs-lookup"><span data-stu-id="28c85-127">The Run method implements an infinite loop that calls each of the logging methods implemented in the **SampleEventSourceWriter** class every 10 seconds.</span></span>

```csharp
using Microsoft.WindowsAzure.ServiceRuntime;
using System;
using System.Diagnostics;
using System.Diagnostics.Tracing;
using System.Net;
using System.Threading;

namespace WorkerRole1
{
    sealed class SampleEventSourceWriter : EventSource
    {
        public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
        public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); }// Cast enums to int for efficient logging.
        public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
        public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
        public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }

    }

    enum MyColor
    {
        Red,
        Blue,
        Green
    }

    [Flags]
    enum MyFlags
    {
        Flag1 = 1,
        Flag2 = 2,
        Flag3 = 4
    }

    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
            // This is a sample worker implementation. Replace with your logic.
            Trace.TraceInformation("WorkerRole1 entry point called");

            int value = 0;

            while (true)
            {
                Thread.Sleep(10000);
                Trace.TraceInformation("Working");

                // Emit several events every time we go through the loop
                for (int i = 0; i < 6; i++)
                {
                    SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
                }

                for (int i = 0; i < 3; i++)
                {
                    SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                    SampleEventSourceWriter.Log.SetOther(true, 123456789);
                }

                if (value == int.MaxValue) value = 0;
                SampleEventSourceWriter.Log.HighFreq(value++);
            }
        }

        public override bool OnStart()
        {
            // Set the maximum number of concurrent connections
            ServicePointManager.DefaultConnectionLimit = 12;

            // For information on handling configuration changes
            // see the MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.

            return base.OnStart();
        }
    }
}
```


### <a name="step-3-deploy-your-worker-role"></a><span data-ttu-id="28c85-128">Étape 3 : déploiement de votre rôle de travail</span><span class="sxs-lookup"><span data-stu-id="28c85-128">Step 3: Deploy your Worker Role</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. <span data-ttu-id="28c85-129">Déployez votre rôle de travail vers Azure à partir de Visual Studio en sélectionnant le projet **WadExample** dans l’Explorateur de solutions, puis **Publier** à partir du menu **Générer**.</span><span class="sxs-lookup"><span data-stu-id="28c85-129">Deploy your worker role to Azure from within Visual Studio by selecting the **WadExample** project in the Solution Explorer then **Publish** from the **Build** menu.</span></span>
2. <span data-ttu-id="28c85-130">Choisissez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="28c85-130">Choose your subscription.</span></span>
3. <span data-ttu-id="28c85-131">Dans la boîte de dialogue **Paramètres de publication Microsoft Azure**, sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="28c85-131">In the **Microsoft Azure Publish Settings** dialog, select **Create New…**.</span></span>
4. <span data-ttu-id="28c85-132">Dans la boîte de dialogue **Créer un service cloud et un compte de stockage**, saisissez un **Nom** (par exemple « WadExample »), puis sélectionnez une région ou un groupe d’affinités.</span><span class="sxs-lookup"><span data-stu-id="28c85-132">In the **Create Cloud Service and Storage Account** dialog, enter a **Name** (for example, "WadExample") and select a region or affinity group.</span></span>
5. <span data-ttu-id="28c85-133">Définissez l’**Environnement** sur **Intermédiaire**.</span><span class="sxs-lookup"><span data-stu-id="28c85-133">Set the **Environment** to **Staging**.</span></span>
6. <span data-ttu-id="28c85-134">Modifiez d’autres **Paramètres** le cas échéant, puis cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="28c85-134">Modify any other **Settings** as appropriate and click **Publish**.</span></span>
7. <span data-ttu-id="28c85-135">Une fois le déploiement terminé, vérifiez dans le portail Azure Classic que votre service cloud est en cours d’ **Exécution** .</span><span class="sxs-lookup"><span data-stu-id="28c85-135">After deployment has completed, verify in the Azure portal that your cloud service is in a **Running** state.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-the-extension"></a><span data-ttu-id="28c85-136">Étape 4 : création de votre fichier de configuration Diagnostics et installation de l’extension</span><span class="sxs-lookup"><span data-stu-id="28c85-136">Step 4: Create your Diagnostics configuration file and install the extension</span></span>
1. <span data-ttu-id="28c85-137">Téléchargez la définition de schéma de fichier de configuration publique en exécutant la commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="28c85-137">Download the public configuration file schema definition by executing the following PowerShell command:</span></span>

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. <span data-ttu-id="28c85-138">Ajouter un fichier XML à votre **WorkerRole1** projet en cliquant sur le **WorkerRole1** de projet et sélectionnez **ajouter** -> **un nouvel élément...**</span><span class="sxs-lookup"><span data-stu-id="28c85-138">Add an XML file to your **WorkerRole1** project by right-clicking on the **WorkerRole1** project and select **Add** -> **New Item…**</span></span><span data-ttu-id="28c85-139"> -> **Éléments Visual C#** -> **Données** -> **Fichier XML**.</span><span class="sxs-lookup"><span data-stu-id="28c85-139"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="28c85-140">Nommez le fichier « WadExample.xml ».</span><span class="sxs-lookup"><span data-stu-id="28c85-140">Name the file "WadExample.xml".</span></span>

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. <span data-ttu-id="28c85-142">Associez le fichier WadConfig.xsd avec le fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="28c85-142">Associate the WadConfig.xsd with the configuration file.</span></span> <span data-ttu-id="28c85-143">Assurez-vous que la fenêtre de l'éditeur WadExample.xml est la fenêtre active.</span><span class="sxs-lookup"><span data-stu-id="28c85-143">Make sure the WadExample.xml editor window is the active window.</span></span> <span data-ttu-id="28c85-144">Appuyez sur **F4** pour ouvrir la fenêtre **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="28c85-144">Press **F4** to open the **Properties** window.</span></span> <span data-ttu-id="28c85-145">Cliquez sur la propriété **Schémas** dans la fenêtre **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="28c85-145">Click the **Schemas** property in the **Properties** window.</span></span> <span data-ttu-id="28c85-146">Cliquez sur **…**</span><span class="sxs-lookup"><span data-stu-id="28c85-146">Click the **…**</span></span> <span data-ttu-id="28c85-147">in the **Schémas** .</span><span class="sxs-lookup"><span data-stu-id="28c85-147">in the **Schemas** property.</span></span> <span data-ttu-id="28c85-148">Cliquez sur **Ajouter…**</span><span class="sxs-lookup"><span data-stu-id="28c85-148">Click the **Add…**</span></span> <span data-ttu-id="28c85-149">et naviguez jusqu’à l’emplacement où vous avez enregistré le fichier XSD, puis sélectionnez le fichier WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="28c85-149">button and navigate to the location where you saved the XSD file and select the file WadConfig.xsd.</span></span> <span data-ttu-id="28c85-150">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="28c85-150">Click **OK**.</span></span>

4. <span data-ttu-id="28c85-151">Remplacez le contenu du fichier de configuration WadExample.xml par le XML suivant, puis enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="28c85-151">Replace the contents of the WadExample.xml configuration file with the following XML and save the file.</span></span> <span data-ttu-id="28c85-152">Ce fichier de configuration définit deux compteurs de performances à collecter : un pour l'utilisation du processeur et l'autre pour l'utilisation de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="28c85-152">This configuration file defines a couple performance counters to collect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="28c85-153">Ensuite, la configuration définit les quatre événements correspondant aux méthodes de la classe SampleEventSourceWriter.</span><span class="sxs-lookup"><span data-stu-id="28c85-153">Then the configuration defines the four events corresponding to the methods in the SampleEventSourceWriter class.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="25000">
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT1M" unit="bytes"/>
      </PerformanceCounters>
      <EtwProviders>
        <EtwEventSourceProviderConfiguration provider="SampleEventSourceWriter" scheduledTransferPeriod="PT5M">
          <Event id="1" eventDestination="EnumsTable"/>
          <Event id="2" eventDestination="MessageTable"/>
          <Event id="3" eventDestination="SetOtherTable"/>
          <Event id="4" eventDestination="HighFreqTable"/>
          <DefaultEvents eventDestination="DefaultTable" />
        </EtwEventSourceProviderConfiguration>
      </EtwProviders>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```

### <a name="step-5-install-diagnostics-on-your-worker-role"></a><span data-ttu-id="28c85-154">Étape 5 : installation de Diagnostics sur votre rôle de travail</span><span class="sxs-lookup"><span data-stu-id="28c85-154">Step 5: Install Diagnostics on your Worker Role</span></span>
<span data-ttu-id="28c85-155">Les applets de commande PowerShell pour la gestion de Diagnostics sur un rôle Web ou de travail sont : Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension et Remove-AzureServiceDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="28c85-155">The PowerShell cmdlets for managing Diagnostics on a web or worker role are: Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension, and Remove-AzureServiceDiagnosticsExtension.</span></span>

1. <span data-ttu-id="28c85-156">Ouvrez Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="28c85-156">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="28c85-157">Exécutez le script pour installer Diagnostics sur votre rôle de travail (remplacez *StorageAccountKey* par la clé du compte de stockage de votre compte de stockage wadexample) et *config_path* par le chemin du fichier *WadExample.xml*) :</span><span class="sxs-lookup"><span data-stu-id="28c85-157">Execute the script to install Diagnostics on your worker role (replace *StorageAccountKey* with the storage account key for your wadexample storage account and *config_path* with the path to the *WadExample.xml* file):</span></span>

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="28c85-158">Étape 6 : examen de vos données télémétriques</span><span class="sxs-lookup"><span data-stu-id="28c85-158">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="28c85-159">Dans l' **Explorateur de serveurs** de Visual Studio, naviguez jusqu'au compte de stockage wadexample.</span><span class="sxs-lookup"><span data-stu-id="28c85-159">In the Visual Studio **Server Explorer**, navigate to the wadexample storage account.</span></span> <span data-ttu-id="28c85-160">Une fois que le service cloud a été exécuté pendant environ cinq (5) minutes, vous devriez voir les tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** et **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="28c85-160">After the cloud service has been running about five (5) minutes, you should see the tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="28c85-161">Double-cliquez sur l'une des tables pour afficher les données télémétriques qui ont été collectées.</span><span class="sxs-lookup"><span data-stu-id="28c85-161">Double-click one of the tables to view the telemetry that has been collected.</span></span>

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="28c85-163">Schéma du fichier de configuration</span><span class="sxs-lookup"><span data-stu-id="28c85-163">Configuration File Schema</span></span>
<span data-ttu-id="28c85-164">Le fichier de configuration des diagnostics définit les valeurs qui sont utilisées pour initialiser les paramètres de configuration de diagnostic lorsque l’agent de diagnostics démarre.</span><span class="sxs-lookup"><span data-stu-id="28c85-164">The Diagnostics configuration file defines values that are used to initialize diagnostic configuration settings when the diagnostics agent starts.</span></span> <span data-ttu-id="28c85-165">Consultez la [dernière référence de schéma](https://msdn.microsoft.com/library/azure/mt634524.aspx) pour obtenir les valeurs valides et des exemples.</span><span class="sxs-lookup"><span data-stu-id="28c85-165">See the [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="28c85-166">Résolution de problèmes</span><span class="sxs-lookup"><span data-stu-id="28c85-166">Troubleshooting</span></span>
<span data-ttu-id="28c85-167">Si vous rencontrez des problèmes, consultez la page [Résolution de problèmes des diagnostics Azure](../azure-diagnostics-troubleshooting.md) pour obtenir de l’aide.</span><span class="sxs-lookup"><span data-stu-id="28c85-167">If you have trouble, see [Troubleshooting Azure Diagnostics](../azure-diagnostics-troubleshooting.md) for help with common problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28c85-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="28c85-168">Next Steps</span></span>
<span data-ttu-id="28c85-169">[Consultez la liste des articles connexes sur les diagnostics relatifs aux machines virtuelles Azure ](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) pour modifier les données que vous collectez, résoudre des problèmes ou pour en savoir plus sur les diagnostics en général.</span><span class="sxs-lookup"><span data-stu-id="28c85-169">[See a list of related Azure virtual-machine diagnostic articles](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) to change the data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
