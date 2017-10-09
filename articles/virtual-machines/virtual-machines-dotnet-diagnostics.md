---
title: aaaHow toouse diagnostics Azure dans les Machines virtuelles | Documents Microsoft
description: "À l’aide des données de toogather de diagnostics Windows Azure à partir d’ordinateurs virtuels Azure pour le débogage, la mesure de performances, analyse, l’analyse du trafic et bien plus encore."
services: virtual-machines
documentationcenter: .net
author: davidmu1
manager: 
editor: 
ms.assetid: dfaabc7a-23e7-4af0-8369-f504d2915b3d
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/16/2016
ms.author: davidmu
ms.openlocfilehash: 54cdfd30d7bbbb71af449826e90234faf5ecdf44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a><span data-ttu-id="e3d5e-103">Activation des diagnostics dans Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="e3d5e-103">Enabling Diagnostics in Azure Virtual Machines</span></span>
<span data-ttu-id="e3d5e-104">Consultez la page [Présentation des diagnostics Azure](../monitoring-and-diagnostics/azure-diagnostics.md) pour obtenir des informations sur les diagnostics Azure.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-104">See [Azure Diagnostics Overview](../monitoring-and-diagnostics/azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-tooenable-diagnostics-in-a-virtual-machine"></a><span data-ttu-id="e3d5e-105">Comment tooEnable Diagnostics sur une Machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e3d5e-105">How tooEnable Diagnostics in a Virtual Machine</span></span>
<span data-ttu-id="e3d5e-106">Cette procédure pas à pas explique comment tooremotely installer les Diagnostics tooan machine virtuelle Azure à partir d’un ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-106">This walk through describes how tooremotely install Diagnostics tooan Azure virtual machine from a development computer.</span></span> <span data-ttu-id="e3d5e-107">Vous apprendrez également comment une application qui s’exécute sur cet ordinateur virtuel Azure et émet les données de télémétrie à l’aide de tooimplement hello .NET [EventSource, classe][EventSource Class].</span><span class="sxs-lookup"><span data-stu-id="e3d5e-107">You also learn how tooimplement an application that runs on that Azure virtual machine and emits telemetry data using hello .NET [EventSource Class][EventSource Class].</span></span> <span data-ttu-id="e3d5e-108">Diagnostics Azure est utilisé toocollect hello télémétrie et le stocker dans un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-108">Azure Diagnostics is used toocollect hello telemetry and store it in an Azure storage account.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="e3d5e-109">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="e3d5e-109">Pre-requisites</span></span>
<span data-ttu-id="e3d5e-110">Cette procédure pas à pas suppose que vous avez un abonnement Azure et que vous utilisez Visual Studio 2017 avec hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-110">This walk through assumes you have an Azure subscription and are using Visual Studio 2017 with hello Azure SDK.</span></span> <span data-ttu-id="e3d5e-111">Si vous n’avez pas un abonnement Azure, vous pouvez vous inscrire pour hello [version d’évaluation gratuite][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="e3d5e-111">If you do not have an Azure subscription, you can sign up for hello [Free Trial][Free Trial].</span></span> <span data-ttu-id="e3d5e-112">Assurez-vous que trop[installer et configurer Azure PowerShell version 0.8.7 ou version ultérieure][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="e3d5e-112">Make sure too[Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-virtual-machine"></a><span data-ttu-id="e3d5e-113">Étape 1 : création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e3d5e-113">Step 1: Create a Virtual Machine</span></span>
1. <span data-ttu-id="e3d5e-114">Sur votre ordinateur de développement, lancez Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-114">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="e3d5e-115">Bonjour Visual Studio **l’Explorateur de serveurs** développez **Azure**, avec le bouton droit **virtuels** puis sélectionnez **créer un ordinateur virtuel**.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-115">In hello Visual Studio **Server Explorer** expand **Azure**, right-click **Virtual Machines** then select **Create Virtual Machine**.</span></span>
3. <span data-ttu-id="e3d5e-116">Sélectionnez votre abonnement Azure Bonjour **choisir un abonnement** boîte de dialogue et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-116">Select your Azure subscription in hello **Choose a Subscription** dialog and click **Next**.</span></span>
4. <span data-ttu-id="e3d5e-117">Sélectionnez **Windows Server 2012 R2 Datacenter, juin 2017** Bonjour **sélectionner une Image de Machine virtuelle** boîte de dialogue et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-117">Select **Windows Server 2012 R2 Datacenter, June 2017** in hello **Select a Virtual Machine Image** dialog and click **Next**.</span></span>
5. <span data-ttu-id="e3d5e-118">Bonjour **les paramètres de base de Machine virtuelle**, définissez le nom d’ordinateur virtuel hello trop « wadexample ».</span><span class="sxs-lookup"><span data-stu-id="e3d5e-118">In hello **Virtual Machine Basic Settings**, set hello virtual machine name too"wadexample".</span></span> <span data-ttu-id="e3d5e-119">Définissez votre nom d'utilisateur et votre mot de passe administrateur, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-119">Set your Administrator user name and password and click **Next**.</span></span>
6. <span data-ttu-id="e3d5e-120">Bonjour **paramètres du Service Cloud** boîte de dialogue Créer un nouveau service cloud nommé « wadexampleVM ».</span><span class="sxs-lookup"><span data-stu-id="e3d5e-120">In hello **Cloud Service Settings** dialog create a new cloud service named "wadexampleVM".</span></span> <span data-ttu-id="e3d5e-121">Créez un compte de stockage appelé « wadexample », puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-121">Create a new Storage account named "wadexample" and click **Next**.</span></span>
7. <span data-ttu-id="e3d5e-122">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-122">Click **Create**.</span></span>

### <a name="step-2-create-your-application"></a><span data-ttu-id="e3d5e-123">Étape 2 : création d’une application</span><span class="sxs-lookup"><span data-stu-id="e3d5e-123">Step 2: Create your Application</span></span>
1. <span data-ttu-id="e3d5e-124">Sur votre ordinateur de développement, lancez Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-124">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="e3d5e-125">Créez une nouvelle application console Visual C# qui cible .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-125">Create a new Visual C# Console Application that targets .NET Framework 4.5.</span></span> <span data-ttu-id="e3d5e-126">Nommez le projet de hello « WadExampleVM ».</span><span class="sxs-lookup"><span data-stu-id="e3d5e-126">Name hello project "WadExampleVM".</span></span>

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. <span data-ttu-id="e3d5e-128">Remplacez contenu hello de Program.cs par hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-128">Replace hello contents of Program.cs with hello following code.</span></span> <span data-ttu-id="e3d5e-129">Hello classe **SampleEventSourceWriter** implémente les quatre méthodes de journalisation : **SendEnums**, **MessageMethod**, **SetOther** et  **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-129">hello class **SampleEventSourceWriter** implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="e3d5e-130">Hello premier paramètre toohello WriteEvent méthode définit les ID de hello pour les événements respectif hello.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-130">hello first parameter toohello WriteEvent method defines hello ID for hello respective event.</span></span> <span data-ttu-id="e3d5e-131">Hello méthode Run implémente une boucle infinie qui chacun des hello appelle des méthodes de journalisation implémentées dans hello **SampleEventSourceWriter** classe toutes les 10 secondes.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-131">hello Run method implements an infinite loop that calls each of hello logging methods implemented in hello **SampleEventSourceWriter** class every 10 seconds.</span></span>

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums tooint for efficient logging.
         public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
         public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
         public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }
       }

       enum MyColor {
         Red,
         Blue,
         Green
       }

       [Flags]
       enum MyFlags {
         Flag1 = 1,
         Flag2 = 2,
         Flag3 = 4
       }

       class Program
       {
         static void Main(string[] args) {
         Trace.TraceInformation("My application entry point called");

         int value = 0;

         while (true) {
             Thread.Sleep(10000);
             Trace.TraceInformation("Working");

             // Emit several events every time we go through hello loop
             for (int i = 0; i < 6; i++) {
                 SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
             }

             for (int i = 0; i < 3; i++) {
                 SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                 SampleEventSourceWriter.Log.SetOther(true, 123456789);
             }

             if (value == int.MaxValue) value = 0;
             SampleEventSourceWriter.Log.HighFreq(value++);
         }

        }
      }
     }
     ```
4. <span data-ttu-id="e3d5e-132">Enregistrez le fichier de hello et sélectionnez **générer la Solution** de hello **générer** menu toobuild votre code.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-132">Save hello file and select **Build Solution** from hello **Build** menu toobuild your code.</span></span>

### <a name="step-3-deploy-your-application"></a><span data-ttu-id="e3d5e-133">Étape 3 : déploiement de votre application</span><span class="sxs-lookup"><span data-stu-id="e3d5e-133">Step 3: Deploy your Application</span></span>
1. <span data-ttu-id="e3d5e-134">Avec le bouton droit sur hello **WadExampleVM** projet **l’Explorateur de solutions** et choisissez **ouvrir le dossier dans l’Explorateur de fichiers**.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-134">Right-click on hello **WadExampleVM** project in **Solution Explorer** and choose **Open Folder in File Explorer**.</span></span>
2. <span data-ttu-id="e3d5e-135">Accédez toohello *bin\Debug* dossier et copie tous les hello fichiers (WadExampleVM.*)</span><span class="sxs-lookup"><span data-stu-id="e3d5e-135">Navigate toohello *bin\Debug* folder and copy all hello files (WadExampleVM.*)</span></span>
3. <span data-ttu-id="e3d5e-136">Dans **l’Explorateur de serveurs** avec le bouton droit sur l’ordinateur virtuel de hello et choisissez **se connecter à l’aide du Bureau à distance**.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-136">In **Server Explorer** right-click on hello virtual machine and choose **Connect using Remote Desktop**.</span></span>
4. <span data-ttu-id="e3d5e-137">Une fois connecté toohello VM créez un dossier nommé WadExampleVM et collez les fichiers de votre application dans le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-137">Once connected toohello VM create a folder named WadExampleVM and paste your application files into hello folder.</span></span>
5. <span data-ttu-id="e3d5e-138">Lancez l’application hello WadExampleVM.exe.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-138">Launch hello application WadExampleVM.exe.</span></span> <span data-ttu-id="e3d5e-139">Une fenêtre de console vide doit apparaître.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-139">You should see a blank console window.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-and-install-hello-extension"></a><span data-ttu-id="e3d5e-140">Étape 4 : Création de votre configuration de Diagnostics et installer l’Extension de hello</span><span class="sxs-lookup"><span data-stu-id="e3d5e-140">Step 4: Create your Diagnostics configuration and install hello Extension</span></span>
1. <span data-ttu-id="e3d5e-141">Téléchargez l’ordinateur de développement tooyour définition de schéma de hello configuration publique fichier en exécutant hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="e3d5e-141">Download hello public configuration file schema definition tooyour development computer by executing hello following PowerShell command:</span></span>

     <span data-ttu-id="e3d5e-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span><span class="sxs-lookup"><span data-stu-id="e3d5e-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span></span>
2. <span data-ttu-id="e3d5e-143">Ouvrez un nouveau fichier XML dans Visual Studio, soit dans un projet qui est déjà ouvert, soit dans une instance de Visual Studio ne comportant aucun projet ouvert.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-143">Open a new XML file in Visual Studio, either in a project you already have open or in a Visual Studio instance with no open projects.</span></span> <span data-ttu-id="e3d5e-144">Dans Visual Studio, sélectionnez **Ajouter** -> **Nouvel élément…**</span><span class="sxs-lookup"><span data-stu-id="e3d5e-144">In Visual Studio, select **Add** -> **New Item…**</span></span><span data-ttu-id="e3d5e-145"> -> **Éléments Visual C#** -> **Données** -> **Fichier XML**.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-145"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="e3d5e-146">Nom de fichier hello « WadExample.xml »</span><span class="sxs-lookup"><span data-stu-id="e3d5e-146">Name hello file "WadExample.xml"</span></span>
3. <span data-ttu-id="e3d5e-147">Associer hello WadConfig.xsd fichier de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-147">Associate hello WadConfig.xsd with hello configuration file.</span></span> <span data-ttu-id="e3d5e-148">Assurez-vous que la fenêtre de l’éditeur WadExample.xml hello est la fenêtre active hello.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-148">Make sure hello WadExample.xml editor window is hello active window.</span></span> <span data-ttu-id="e3d5e-149">Appuyez sur **F4** tooopen hello **propriétés** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-149">Press **F4** tooopen hello **Properties** window.</span></span> <span data-ttu-id="e3d5e-150">Cliquez sur hello **schémas** propriété Bonjour **propriétés** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-150">Click on hello **Schemas** property in hello **Properties** window.</span></span> <span data-ttu-id="e3d5e-151">Cliquez sur hello **...**</span><span class="sxs-lookup"><span data-stu-id="e3d5e-151">Click hello **…**</span></span> <span data-ttu-id="e3d5e-152">Bonjour **schémas** propriété.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-152">in hello **Schemas** property.</span></span> <span data-ttu-id="e3d5e-153">Cliquez sur hello **ajouter...**</span><span class="sxs-lookup"><span data-stu-id="e3d5e-153">Click hello **Add…**</span></span> <span data-ttu-id="e3d5e-154">bouton et accédez emplacement toohello où vous avez enregistré le fichier XSD de hello et sélectionnez hello WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-154">button and navigate toohello location where you saved hello XSD file and select hello file WadConfig.xsd.</span></span> <span data-ttu-id="e3d5e-155">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-155">Click **OK**.</span></span>
4. <span data-ttu-id="e3d5e-156">Remplacez le contenu hello hello WadExample.xml du fichier de configuration par hello XML suivant, puis enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-156">Replace hello contents of hello WadExample.xml configuration file with hello following XML and save hello file.</span></span> <span data-ttu-id="e3d5e-157">Ce fichier de configuration définit deux toocollect de compteurs de performances : un pour l’utilisation du processeur et l’autre pour l’utilisation de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-157">This configuration file defines a couple performance counters toocollect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="e3d5e-158">Configuration de hello définit ensuite hello quatre événements correspondant méthodes toohello Bonjour SampleEventSourceWriter classe.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-158">Then hello configuration defines hello four events corresponding toohello methods in hello SampleEventSourceWriter class.</span></span>

```
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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a><span data-ttu-id="e3d5e-159">Étape 5 : installation à distance de Diagnostics sur votre machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="e3d5e-159">Step 5: Remotely install Diagnostics on your Azure Virtual Machine</span></span>
<span data-ttu-id="e3d5e-160">Hello applets de commande PowerShell pour gérer les Diagnostics sur une machine virtuelle sont : Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension et Remove-AzureVMDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-160">hello PowerShell cmdlets for managing Diagnostics on a VM are: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension, and Remove-AzureVMDiagnosticsExtension.</span></span>

1. <span data-ttu-id="e3d5e-161">Sur votre ordinateur de développement, ouvrez Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-161">On your developer computer, open Azure PowerShell.</span></span>
2. <span data-ttu-id="e3d5e-162">Exécuter l’installation de tooremotely script hello Diagnostics sur votre machine virtuelle (remplacez `<user>` avec votre nom d’utilisateur active.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-162">Execute hello script tooremotely install Diagnostics on your VM (Replace `<user>` with your user directory name.</span></span> <span data-ttu-id="e3d5e-163">Remplacez `<StorageAccountKey>` par la clé de compte de stockage hello pour votre compte de stockage wadexamplevm) :</span><span class="sxs-lookup"><span data-stu-id="e3d5e-163">Replace `<StorageAccountKey>` with hello storage account key for your wadexamplevm storage account):</span></span>
```
     $storage_name = "wadexamplevm"
     $key = "<StorageAccountKey>"
     $config_path="c:\users\<user>\documents\visual studio 2017\Projects\WadExampleVM\WadExampleVM\WadExample.xml"
     $service_name="wadexamplevm"
     $vm_name="WadExample"
     $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
     $VM1 = Get-AzureVM -ServiceName $service_name -Name $vm_name
     $VM2 = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $config_path -Version "1.*" -VM $VM1 -StorageContext $storageContext
     $VM3 = Update-AzureVM -ServiceName $service_name -Name $vm_name -VM $VM2.VM
```
### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="e3d5e-164">Étape 6 : examen de vos données télémétriques</span><span class="sxs-lookup"><span data-stu-id="e3d5e-164">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="e3d5e-165">Bonjour Visual Studio **l’Explorateur de serveurs** accédez compte de stockage toohello wadexample.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-165">In hello Visual Studio **Server Explorer** navigate toohello wadexample storage account.</span></span> <span data-ttu-id="e3d5e-166">Après avoir hello machine virtuelle a été exécuté environ 5 minutes, vous devez voir les tables hello **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**,  **WADPerformanceCountersTable** et **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-166">After hello VM has been running about 5 minutes you should see hello tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="e3d5e-167">Double-cliquez sur l’un de télémétrie de hello hello tables tooview qui ont été collectée.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-167">Double-click on one of hello tables tooview hello telemetry that has been collected.</span></span>

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="e3d5e-169">Schéma du fichier de configuration</span><span class="sxs-lookup"><span data-stu-id="e3d5e-169">Configuration file schema</span></span>
<span data-ttu-id="e3d5e-170">fichier de configuration des Diagnostics Hello définit des valeurs qui sont des paramètres de configuration de diagnostic tooinitialize utilisé au démarrage de l’agent de diagnostics hello.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-170">hello Diagnostics configuration file defines values that are used tooinitialize diagnostic configuration settings when hello diagnostics agent starts.</span></span> <span data-ttu-id="e3d5e-171">Consultez hello [dernière référence du schéma](https://msdn.microsoft.com/library/azure/mt634524.aspx) pour les valeurs valides et des exemples.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-171">See hello [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e3d5e-172">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="e3d5e-172">Troubleshooting</span></span>
<span data-ttu-id="e3d5e-173">Pour plus d'informations, voir [Dépannage des diagnostics Azure](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) .</span><span class="sxs-lookup"><span data-stu-id="e3d5e-173">See [Troubleshooting Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3d5e-174">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e3d5e-174">Next steps</span></span>
<span data-ttu-id="e3d5e-175">[Pour afficher la liste de la machine virtuelle de Azure Diagnostics relatifs](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) vous collectez les données de salutation toochange résoudre des problèmes ou en savoir plus sur les diagnostics en général.</span><span class="sxs-lookup"><span data-stu-id="e3d5e-175">[See a list of virtual machine related Azure Diagnostics articles](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) toochange hello data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
