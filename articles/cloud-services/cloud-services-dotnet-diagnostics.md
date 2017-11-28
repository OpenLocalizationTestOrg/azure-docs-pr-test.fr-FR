---
title: aaaHow toouse Azure diagnostics (.NET) avec les Services de cloud computing | Documents Microsoft
description: "À l’aide des diagnostics Azure toogather données à partir d’Azure cloud Services pour le débogage, mesurer les performances, analyse, l’analyse du trafic et bien plus encore."
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
ms.openlocfilehash: 1525eac1e85955d8f05aa21a9805e0a80d0e4bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a><span data-ttu-id="39e2e-103">Activation des diagnostics Azure dans Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="39e2e-103">Enabling Azure Diagnostics in Azure Cloud Services</span></span>
<span data-ttu-id="39e2e-104">Consultez la page [Présentation des diagnostics Azure](../azure-diagnostics.md) pour obtenir des informations sur les diagnostics Azure.</span><span class="sxs-lookup"><span data-stu-id="39e2e-104">See [Azure Diagnostics Overview](../azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-tooenable-diagnostics-in-a-worker-role"></a><span data-ttu-id="39e2e-105">Comment tooEnable Diagnostics dans un rôle de travail</span><span class="sxs-lookup"><span data-stu-id="39e2e-105">How tooEnable Diagnostics in a Worker Role</span></span>
<span data-ttu-id="39e2e-106">Cette procédure pas à pas décrit comment un rôle de travail Azure qui émet les données de télémétrie à l’aide de tooimplement hello .NET EventSource (classe).</span><span class="sxs-lookup"><span data-stu-id="39e2e-106">This walkthrough describes how tooimplement an Azure worker role that emits telemetry data using hello .NET EventSource class.</span></span> <span data-ttu-id="39e2e-107">Diagnostics Azure est utilisé toocollect des données de télémétrie hello et stockez-le dans un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="39e2e-107">Azure Diagnostics is used toocollect hello telemetry data and store it in an Azure storage account.</span></span> <span data-ttu-id="39e2e-108">Lorsque vous créez un rôle de travail, Visual Studio active automatiquement Diagnostics 1.0 dans le cadre de la solution hello dans Azure SDK pour .NET 2.4 et versions antérieures.</span><span class="sxs-lookup"><span data-stu-id="39e2e-108">When creating a worker role, Visual Studio automatically enables Diagnostics 1.0 as part of hello solution in Azure SDKs for .NET 2.4 and earlier.</span></span> <span data-ttu-id="39e2e-109">Hello instructions suivantes décrivent les processus hello pour la création de rôle de travail hello, la désactivation de Diagnostics 1.0 à partir de la solution de hello et le déploiement de Diagnostics 1.2 ou rôle de travail tooyour 1.3.</span><span class="sxs-lookup"><span data-stu-id="39e2e-109">hello following instructions describe hello process for creating hello worker role, disabling Diagnostics 1.0 from hello solution, and deploying Diagnostics 1.2 or 1.3 tooyour worker role.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="39e2e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="39e2e-110">Prerequisites</span></span>
<span data-ttu-id="39e2e-111">Cet article suppose que vous avez un abonnement Azure et que vous utilisez Visual Studio avec hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="39e2e-111">This article assumes you have an Azure subscription and are using Visual Studio with hello Azure SDK.</span></span> <span data-ttu-id="39e2e-112">Si vous n’avez pas un abonnement Azure, vous pouvez vous inscrire pour hello [version d’évaluation gratuite][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="39e2e-112">If you do not have an Azure subscription, you can sign up for hello [Free Trial][Free Trial].</span></span> <span data-ttu-id="39e2e-113">Assurez-vous que trop[installer et configurer Azure PowerShell version 0.8.7 ou version ultérieure][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="39e2e-113">Make sure too[Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-worker-role"></a><span data-ttu-id="39e2e-114">Étape 1 : création d’un rôle de travail</span><span class="sxs-lookup"><span data-stu-id="39e2e-114">Step 1: Create a Worker Role</span></span>
1. <span data-ttu-id="39e2e-115">Lancez **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="39e2e-115">Launch **Visual Studio**.</span></span>
2. <span data-ttu-id="39e2e-116">Créer un **Azure Cloud Service** projet à partir de hello **Cloud** modèle qui cible le .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="39e2e-116">Create an **Azure Cloud Service** project from hello **Cloud** template that targets .NET Framework 4.5.</span></span>  <span data-ttu-id="39e2e-117">Nommez le projet hello « WadExample » et cliquez sur Ok.</span><span class="sxs-lookup"><span data-stu-id="39e2e-117">Name hello project "WadExample" and click Ok.</span></span>
3. <span data-ttu-id="39e2e-118">Sélectionnez **Rôle de travail** et cliquez sur Ok.</span><span class="sxs-lookup"><span data-stu-id="39e2e-118">Select **Worker Role** and click Ok.</span></span> <span data-ttu-id="39e2e-119">Hello projet sera créé.</span><span class="sxs-lookup"><span data-stu-id="39e2e-119">hello project will be created.</span></span>
4. <span data-ttu-id="39e2e-120">Dans **l’Explorateur de solutions**, double-cliquez sur hello **WorkerRole1** fichier de propriétés.</span><span class="sxs-lookup"><span data-stu-id="39e2e-120">In **Solution Explorer**, double-click hello **WorkerRole1** properties file.</span></span>
5. <span data-ttu-id="39e2e-121">Bonjour **Configuration** onglet, décochez la case **activer les Diagnostics** toodisable Diagnostics 1.0 (Azure SDK 2.4 et versions antérieur).</span><span class="sxs-lookup"><span data-stu-id="39e2e-121">In hello **Configuration** tab, un-check **Enable Diagnostics** toodisable Diagnostics 1.0 (Azure SDK 2.4 and earlier).</span></span>
6. <span data-ttu-id="39e2e-122">Générer votre tooverify de solution qui vous comporter aucune erreur.</span><span class="sxs-lookup"><span data-stu-id="39e2e-122">Build your solution tooverify that you have no errors.</span></span>

### <a name="step-2-instrument-your-code"></a><span data-ttu-id="39e2e-123">Étape 2 : instrumentalisation de votre code</span><span class="sxs-lookup"><span data-stu-id="39e2e-123">Step 2: Instrument your code</span></span>
<span data-ttu-id="39e2e-124">Remplacez contenu hello de WorkerRole.cs par hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="39e2e-124">Replace hello contents of WorkerRole.cs with hello following code.</span></span> <span data-ttu-id="39e2e-125">Hello classe SampleEventSourceWriter, héritée de hello [EventSource, classe][EventSource Class], implémente les quatre méthodes de journalisation : **SendEnums**, **MessageMethod** , **SetOther** et **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="39e2e-125">hello class SampleEventSourceWriter, inherited from hello [EventSource Class][EventSource Class], implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="39e2e-126">Hello premier paramètre toohello **WriteEvent** méthode définit l’ID hello pour les événements respectif hello.</span><span class="sxs-lookup"><span data-stu-id="39e2e-126">hello first parameter toohello **WriteEvent** method defines hello ID for hello respective event.</span></span> <span data-ttu-id="39e2e-127">Hello méthode Run implémente une boucle infinie qui chacun des hello appelle des méthodes de journalisation implémentées dans hello **SampleEventSourceWriter** classe toutes les 10 secondes.</span><span class="sxs-lookup"><span data-stu-id="39e2e-127">hello Run method implements an infinite loop that calls each of hello logging methods implemented in hello **SampleEventSourceWriter** class every 10 seconds.</span></span>

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
        public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); }// Cast enums tooint for efficient logging.
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

                // Emit several events every time we go through hello loop
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
            // Set hello maximum number of concurrent connections
            ServicePointManager.DefaultConnectionLimit = 12;

            // For information on handling configuration changes
            // see hello MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.

            return base.OnStart();
        }
    }
}
```


### <a name="step-3-deploy-your-worker-role"></a><span data-ttu-id="39e2e-128">Étape 3 : déploiement de votre rôle de travail</span><span class="sxs-lookup"><span data-stu-id="39e2e-128">Step 3: Deploy your Worker Role</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. <span data-ttu-id="39e2e-129">Déployer votre tooAzure de rôle de travail à partir de Visual Studio en sélectionnant hello **WadExample** projet Bonjour l’Explorateur de solutions, puis **publier** de hello **générer** menu.</span><span class="sxs-lookup"><span data-stu-id="39e2e-129">Deploy your worker role tooAzure from within Visual Studio by selecting hello **WadExample** project in hello Solution Explorer then **Publish** from hello **Build** menu.</span></span>
2. <span data-ttu-id="39e2e-130">Choisissez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="39e2e-130">Choose your subscription.</span></span>
3. <span data-ttu-id="39e2e-131">Bonjour **paramètres de publication Microsoft Azure** boîte de dialogue, sélectionnez **créer un nouveau...** .</span><span class="sxs-lookup"><span data-stu-id="39e2e-131">In hello **Microsoft Azure Publish Settings** dialog, select **Create New…**.</span></span>
4. <span data-ttu-id="39e2e-132">Bonjour **créer un Service Cloud et le compte de stockage** boîte de dialogue, entrez un **nom** (par exemple, « WadExample ») et sélectionnez une région ou un groupe d’affinités.</span><span class="sxs-lookup"><span data-stu-id="39e2e-132">In hello **Create Cloud Service and Storage Account** dialog, enter a **Name** (for example, "WadExample") and select a region or affinity group.</span></span>
5. <span data-ttu-id="39e2e-133">Ensemble hello **environnement** trop**intermédiaire**.</span><span class="sxs-lookup"><span data-stu-id="39e2e-133">Set hello **Environment** too**Staging**.</span></span>
6. <span data-ttu-id="39e2e-134">Modifiez d’autres **Paramètres** le cas échéant, puis cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="39e2e-134">Modify any other **Settings** as appropriate and click **Publish**.</span></span>
7. <span data-ttu-id="39e2e-135">Une fois le déploiement terminé, vérifiez dans hello portail Azure que votre service cloud est dans un **en cours d’exécution** état.</span><span class="sxs-lookup"><span data-stu-id="39e2e-135">After deployment has completed, verify in hello Azure portal that your cloud service is in a **Running** state.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-hello-extension"></a><span data-ttu-id="39e2e-136">Étape 4 : Créer votre fichier de configuration de Diagnostics et installer l’extension de hello</span><span class="sxs-lookup"><span data-stu-id="39e2e-136">Step 4: Create your Diagnostics configuration file and install hello extension</span></span>
1. <span data-ttu-id="39e2e-137">Télécharger la définition de schéma de fichier de configuration publique hello en exécutant hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="39e2e-137">Download hello public configuration file schema definition by executing hello following PowerShell command:</span></span>

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. <span data-ttu-id="39e2e-138">Ajouter un tooyour du fichier XML **WorkerRole1** projet en cliquant sur hello **WorkerRole1** de projet et sélectionnez **ajouter** -> **un nouvel élément...**</span><span class="sxs-lookup"><span data-stu-id="39e2e-138">Add an XML file tooyour **WorkerRole1** project by right-clicking on hello **WorkerRole1** project and select **Add** -> **New Item…**</span></span><span data-ttu-id="39e2e-139"> -> **Éléments Visual C#** -> **Données** -> **Fichier XML**.</span><span class="sxs-lookup"><span data-stu-id="39e2e-139"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="39e2e-140">Nom de fichier de hello « WadExample.xml ».</span><span class="sxs-lookup"><span data-stu-id="39e2e-140">Name hello file "WadExample.xml".</span></span>

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. <span data-ttu-id="39e2e-142">Associer hello WadConfig.xsd fichier de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="39e2e-142">Associate hello WadConfig.xsd with hello configuration file.</span></span> <span data-ttu-id="39e2e-143">Assurez-vous que la fenêtre de l’éditeur WadExample.xml hello est la fenêtre active hello.</span><span class="sxs-lookup"><span data-stu-id="39e2e-143">Make sure hello WadExample.xml editor window is hello active window.</span></span> <span data-ttu-id="39e2e-144">Appuyez sur **F4** tooopen hello **propriétés** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="39e2e-144">Press **F4** tooopen hello **Properties** window.</span></span> <span data-ttu-id="39e2e-145">Cliquez sur hello **schémas** propriété Bonjour **propriétés** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="39e2e-145">Click hello **Schemas** property in hello **Properties** window.</span></span> <span data-ttu-id="39e2e-146">Cliquez sur hello **...**</span><span class="sxs-lookup"><span data-stu-id="39e2e-146">Click hello **…**</span></span> <span data-ttu-id="39e2e-147">Bonjour **schémas** propriété.</span><span class="sxs-lookup"><span data-stu-id="39e2e-147">in hello **Schemas** property.</span></span> <span data-ttu-id="39e2e-148">Cliquez sur hello **ajouter...**</span><span class="sxs-lookup"><span data-stu-id="39e2e-148">Click hello **Add…**</span></span> <span data-ttu-id="39e2e-149">bouton et accédez emplacement toohello où vous avez enregistré le fichier XSD de hello et sélectionnez hello WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="39e2e-149">button and navigate toohello location where you saved hello XSD file and select hello file WadConfig.xsd.</span></span> <span data-ttu-id="39e2e-150">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="39e2e-150">Click **OK**.</span></span>

4. <span data-ttu-id="39e2e-151">Remplacez le contenu hello hello WadExample.xml du fichier de configuration par hello XML suivant, puis enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="39e2e-151">Replace hello contents of hello WadExample.xml configuration file with hello following XML and save hello file.</span></span> <span data-ttu-id="39e2e-152">Ce fichier de configuration définit deux toocollect de compteurs de performances : un pour l’utilisation du processeur et l’autre pour l’utilisation de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="39e2e-152">This configuration file defines a couple performance counters toocollect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="39e2e-153">Configuration de hello définit ensuite hello quatre événements correspondant méthodes toohello Bonjour SampleEventSourceWriter classe.</span><span class="sxs-lookup"><span data-stu-id="39e2e-153">Then hello configuration defines hello four events corresponding toohello methods in hello SampleEventSourceWriter class.</span></span>

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

### <a name="step-5-install-diagnostics-on-your-worker-role"></a><span data-ttu-id="39e2e-154">Étape 5 : installation de Diagnostics sur votre rôle de travail</span><span class="sxs-lookup"><span data-stu-id="39e2e-154">Step 5: Install Diagnostics on your Worker Role</span></span>
<span data-ttu-id="39e2e-155">Hello applets de commande PowerShell pour gérer les Diagnostics sur un rôle web ou de travail sont : Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension et Remove-AzureServiceDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="39e2e-155">hello PowerShell cmdlets for managing Diagnostics on a web or worker role are: Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension, and Remove-AzureServiceDiagnosticsExtension.</span></span>

1. <span data-ttu-id="39e2e-156">Ouvrez Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="39e2e-156">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="39e2e-157">Exécutez hello script tooinstall Diagnostics sur votre rôle de travail (remplacez *StorageAccountKey* avec la clé de compte de stockage hello pour votre compte de stockage wadexample et *config_path* avec le chemin d’accès de hello toohello *WadExample.xml* fichier) :</span><span class="sxs-lookup"><span data-stu-id="39e2e-157">Execute hello script tooinstall Diagnostics on your worker role (replace *StorageAccountKey* with hello storage account key for your wadexample storage account and *config_path* with hello path toohello *WadExample.xml* file):</span></span>

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="39e2e-158">Étape 6 : examen de vos données télémétriques</span><span class="sxs-lookup"><span data-stu-id="39e2e-158">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="39e2e-159">Bonjour Visual Studio **l’Explorateur de serveurs**, accédez de compte de stockage toohello wadexample.</span><span class="sxs-lookup"><span data-stu-id="39e2e-159">In hello Visual Studio **Server Explorer**, navigate toohello wadexample storage account.</span></span> <span data-ttu-id="39e2e-160">Une fois que le service de cloud computing hello s’exécute minutes environ cinq (5), vous devez voir les tables hello **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** et **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="39e2e-160">After hello cloud service has been running about five (5) minutes, you should see hello tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="39e2e-161">Double-cliquez sur un de télémétrie de hello hello tables tooview qui ont été collectée.</span><span class="sxs-lookup"><span data-stu-id="39e2e-161">Double-click one of hello tables tooview hello telemetry that has been collected.</span></span>

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="39e2e-163">Schéma du fichier de configuration</span><span class="sxs-lookup"><span data-stu-id="39e2e-163">Configuration File Schema</span></span>
<span data-ttu-id="39e2e-164">fichier de configuration des Diagnostics Hello définit des valeurs qui sont des paramètres de configuration de diagnostic tooinitialize utilisé au démarrage de l’agent de diagnostics hello.</span><span class="sxs-lookup"><span data-stu-id="39e2e-164">hello Diagnostics configuration file defines values that are used tooinitialize diagnostic configuration settings when hello diagnostics agent starts.</span></span> <span data-ttu-id="39e2e-165">Consultez hello [dernière référence du schéma](https://msdn.microsoft.com/library/azure/mt634524.aspx) pour les valeurs valides et des exemples.</span><span class="sxs-lookup"><span data-stu-id="39e2e-165">See hello [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="39e2e-166">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="39e2e-166">Troubleshooting</span></span>
<span data-ttu-id="39e2e-167">Si vous rencontrez des problèmes, consultez la page [Résolution de problèmes des diagnostics Azure](../azure-diagnostics-troubleshooting.md) pour obtenir de l’aide.</span><span class="sxs-lookup"><span data-stu-id="39e2e-167">If you have trouble, see [Troubleshooting Azure Diagnostics](../azure-diagnostics-troubleshooting.md) for help with common problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39e2e-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="39e2e-168">Next Steps</span></span>
<span data-ttu-id="39e2e-169">[Afficher la liste des articles diagnostic connexes Azure à une machine virtuelle](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) vous collectez les données de salutation toochange résoudre des problèmes ou en savoir plus sur les diagnostics en général.</span><span class="sxs-lookup"><span data-stu-id="39e2e-169">[See a list of related Azure virtual-machine diagnostic articles](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) toochange hello data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
