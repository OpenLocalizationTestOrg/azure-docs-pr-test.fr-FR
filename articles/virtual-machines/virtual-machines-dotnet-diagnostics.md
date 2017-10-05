---
title: Utilisation des diagnostics Azure dans les Machines Virtuelles | Microsoft Docs
description: "Utilisation des diagnostics Azure pour rassembler des données à partir d’Azure Virtual Machines pour le débogage, la mesure des performances, la surveillance, l’analyse du trafic, etc."
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
ms.openlocfilehash: 8ff6b9825212359617b748aba1c78ed789b130dd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a><span data-ttu-id="2d5b2-103">Activation des diagnostics dans Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="2d5b2-103">Enabling Diagnostics in Azure Virtual Machines</span></span>
<span data-ttu-id="2d5b2-104">Consultez la page [Présentation des diagnostics Azure](../monitoring-and-diagnostics/azure-diagnostics.md) pour obtenir des informations sur les diagnostics Azure.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-104">See [Azure Diagnostics Overview](../monitoring-and-diagnostics/azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-to-enable-diagnostics-in-a-virtual-machine"></a><span data-ttu-id="2d5b2-105">Activation de Diagnostics dans une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="2d5b2-105">How to Enable Diagnostics in a Virtual Machine</span></span>
<span data-ttu-id="2d5b2-106">Cette procédure pas à pas décrit comment installer Diagnostics à distance dans une machine virtuelle Azure à partir d'un ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-106">This walk through describes how to remotely install Diagnostics to an Azure virtual machine from a development computer.</span></span> <span data-ttu-id="2d5b2-107">Vous apprendrez également à implémenter une application qui s’exécute sur cette machine virtuelle Azure et qui émet des données télémétriques à l’aide de la classe [EventSource Class][EventSource Class].NET.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-107">You also learn how to implement an application that runs on that Azure virtual machine and emits telemetry data using the .NET [EventSource Class][EventSource Class].</span></span> <span data-ttu-id="2d5b2-108">Azure Diagnostics est utilisé pour collecter des données télémétriques et les stocker dans un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-108">Azure Diagnostics is used to collect the telemetry and store it in an Azure storage account.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="2d5b2-109">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="2d5b2-109">Pre-requisites</span></span>
<span data-ttu-id="2d5b2-110">Cette procédure pas à pas part du principe que vous disposez d’un abonnement Azure et que vous utilisez Visual Studio 2017 avec le kit de développement logiciel (SDK) Azure.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-110">This walk through assumes you have an Azure subscription and are using Visual Studio 2017 with the Azure SDK.</span></span> <span data-ttu-id="2d5b2-111">Si vous n’avez pas d’abonnement Azure, vous pouvez vous inscrire pour bénéficier d’une [version d’évaluation gratuite][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="2d5b2-111">If you do not have an Azure subscription, you can sign up for the [Free Trial][Free Trial].</span></span> <span data-ttu-id="2d5b2-112">Assurez-vous d’avoir [installé et configuré Azure PowerShell version 0.8.7 ou ultérieure][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="2d5b2-112">Make sure to [Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-virtual-machine"></a><span data-ttu-id="2d5b2-113">Étape 1 : création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="2d5b2-113">Step 1: Create a Virtual Machine</span></span>
1. <span data-ttu-id="2d5b2-114">Sur votre ordinateur de développement, lancez Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-114">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="2d5b2-115">Dans **l’Explorateur de serveurs** de Visual Studio, développez **Azure**, cliquez avec le bouton droit sur **Machines virtuelles**, puis sélectionnez **Créer une machine virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-115">In the Visual Studio **Server Explorer** expand **Azure**, right-click **Virtual Machines** then select **Create Virtual Machine**.</span></span>
3. <span data-ttu-id="2d5b2-116">Sélectionnez votre abonnement Azure dans la boîte de dialogue **Choisir un abonnement** et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-116">Select your Azure subscription in the **Choose a Subscription** dialog and click **Next**.</span></span>
4. <span data-ttu-id="2d5b2-117">Sélectionnez **Windows Server 2012 R2 Datacenter, juin 2017** dans la boîte de dialogue **Sélectionner une image de machine virtuelle**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-117">Select **Windows Server 2012 R2 Datacenter, June 2017** in the **Select a Virtual Machine Image** dialog and click **Next**.</span></span>
5. <span data-ttu-id="2d5b2-118">Dans **Paramètres de base de la machine virtuelle**, définissez le nom de la machine virtuelle sur « wadexample ».</span><span class="sxs-lookup"><span data-stu-id="2d5b2-118">In the **Virtual Machine Basic Settings**, set the virtual machine name to "wadexample".</span></span> <span data-ttu-id="2d5b2-119">Définissez votre nom d'utilisateur et votre mot de passe administrateur, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-119">Set your Administrator user name and password and click **Next**.</span></span>
6. <span data-ttu-id="2d5b2-120">Dans la boîte de dialogue **Paramètres de service cloud** , créez un service cloud appelé « wadexampleVM ».</span><span class="sxs-lookup"><span data-stu-id="2d5b2-120">In the **Cloud Service Settings** dialog create a new cloud service named "wadexampleVM".</span></span> <span data-ttu-id="2d5b2-121">Créez un compte de stockage appelé « wadexample », puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-121">Create a new Storage account named "wadexample" and click **Next**.</span></span>
7. <span data-ttu-id="2d5b2-122">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-122">Click **Create**.</span></span>

### <a name="step-2-create-your-application"></a><span data-ttu-id="2d5b2-123">Étape 2 : création d’une application</span><span class="sxs-lookup"><span data-stu-id="2d5b2-123">Step 2: Create your Application</span></span>
1. <span data-ttu-id="2d5b2-124">Sur votre ordinateur de développement, lancez Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-124">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="2d5b2-125">Créez une nouvelle application console Visual C# qui cible .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-125">Create a new Visual C# Console Application that targets .NET Framework 4.5.</span></span> <span data-ttu-id="2d5b2-126">Nommez le projet « WadExampleVM ».</span><span class="sxs-lookup"><span data-stu-id="2d5b2-126">Name the project "WadExampleVM".</span></span>

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. <span data-ttu-id="2d5b2-128">Remplacez le contenu de Program.cs par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-128">Replace the contents of Program.cs with the following code.</span></span> <span data-ttu-id="2d5b2-129">La classe **SampleEventSourceWriter** implémente quatre méthodes de journalisation : **SendEnums**, **MessageMethod**, **SetOther** et **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-129">The class **SampleEventSourceWriter** implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="2d5b2-130">Le premier paramètre de la méthode WriteEvent définit l'ID de l'événement respectif.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-130">The first parameter to the WriteEvent method defines the ID for the respective event.</span></span> <span data-ttu-id="2d5b2-131">La méthode Run implémente une boucle infinie qui appelle chacune des méthodes de journalisation implémentées dans la classe **SampleEventSourceWriter** toutes les 10 secondes.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-131">The Run method implements an infinite loop that calls each of the logging methods implemented in the **SampleEventSourceWriter** class every 10 seconds.</span></span>

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums to int for efficient logging.
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

             // Emit several events every time we go through the loop
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
4. <span data-ttu-id="2d5b2-132">Enregistrez le fichier, puis sélectionnez **Générer la solution** à partir du menu **Générer** pour générer votre code.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-132">Save the file and select **Build Solution** from the **Build** menu to build your code.</span></span>

### <a name="step-3-deploy-your-application"></a><span data-ttu-id="2d5b2-133">Étape 3 : déploiement de votre application</span><span class="sxs-lookup"><span data-stu-id="2d5b2-133">Step 3: Deploy your Application</span></span>
1. <span data-ttu-id="2d5b2-134">Cliquez avec le bouton droit sur le projet **WadExampleVM** dans **l’Explorateur de solutions**, puis choisissez **Ouvrir un dossier dans l’Explorateur de fichiers**.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-134">Right-click on the **WadExampleVM** project in **Solution Explorer** and choose **Open Folder in File Explorer**.</span></span>
2. <span data-ttu-id="2d5b2-135">Naviguez vers le dossier *bin\Debug* et copiez tous les fichiers (WadExampleVM.*)</span><span class="sxs-lookup"><span data-stu-id="2d5b2-135">Navigate to the *bin\Debug* folder and copy all the files (WadExampleVM.*)</span></span>
3. <span data-ttu-id="2d5b2-136">Dans **l’Explorateur de serveurs**, cliquez avec le bouton droit sur la machine virtuelle, puis sélectionnez **Se connecter à l’aide du Bureau à distance**.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-136">In **Server Explorer** right-click on the virtual machine and choose **Connect using Remote Desktop**.</span></span>
4. <span data-ttu-id="2d5b2-137">Une fois connecté à la machine virtuelle, créez un dossier nommé WadExampleVM, puis collez vos fichiers d'application dans le dossier.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-137">Once connected to the VM create a folder named WadExampleVM and paste your application files into the folder.</span></span>
5. <span data-ttu-id="2d5b2-138">Lancez l'application WadExampleVM.exe.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-138">Launch the application WadExampleVM.exe.</span></span> <span data-ttu-id="2d5b2-139">Une fenêtre de console vide doit apparaître.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-139">You should see a blank console window.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-and-install-the-extension"></a><span data-ttu-id="2d5b2-140">Étape 4 : création de votre configuration Diagnostics et installation de l’extension</span><span class="sxs-lookup"><span data-stu-id="2d5b2-140">Step 4: Create your Diagnostics configuration and install the Extension</span></span>
1. <span data-ttu-id="2d5b2-141">Téléchargez la définition de schéma de fichier de configuration publique sur votre ordinateur de développement en exécutant la commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="2d5b2-141">Download the public configuration file schema definition to your development computer by executing the following PowerShell command:</span></span>

     <span data-ttu-id="2d5b2-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span><span class="sxs-lookup"><span data-stu-id="2d5b2-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span></span>
2. <span data-ttu-id="2d5b2-143">Ouvrez un nouveau fichier XML dans Visual Studio, soit dans un projet qui est déjà ouvert, soit dans une instance de Visual Studio ne comportant aucun projet ouvert.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-143">Open a new XML file in Visual Studio, either in a project you already have open or in a Visual Studio instance with no open projects.</span></span> <span data-ttu-id="2d5b2-144">Dans Visual Studio, sélectionnez **Ajouter** -> **Nouvel élément…**</span><span class="sxs-lookup"><span data-stu-id="2d5b2-144">In Visual Studio, select **Add** -> **New Item…**</span></span><span data-ttu-id="2d5b2-145"> -> **Éléments Visual C#** -> **Données** -> **Fichier XML**.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-145"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="2d5b2-146">Nommez le fichier « WadExample.xml ».</span><span class="sxs-lookup"><span data-stu-id="2d5b2-146">Name the file "WadExample.xml"</span></span>
3. <span data-ttu-id="2d5b2-147">Associez le fichier WadConfig.xsd avec le fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-147">Associate the WadConfig.xsd with the configuration file.</span></span> <span data-ttu-id="2d5b2-148">Assurez-vous que la fenêtre de l'éditeur WadExample.xml est la fenêtre active.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-148">Make sure the WadExample.xml editor window is the active window.</span></span> <span data-ttu-id="2d5b2-149">Appuyez sur **F4** pour ouvrir la fenêtre **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-149">Press **F4** to open the **Properties** window.</span></span> <span data-ttu-id="2d5b2-150">Cliquez sur la propriété **Schémas** dans la fenêtre **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-150">Click on the **Schemas** property in the **Properties** window.</span></span> <span data-ttu-id="2d5b2-151">Cliquez sur **…**</span><span class="sxs-lookup"><span data-stu-id="2d5b2-151">Click the **…**</span></span> <span data-ttu-id="2d5b2-152">in the **Schémas** .</span><span class="sxs-lookup"><span data-stu-id="2d5b2-152">in the **Schemas** property.</span></span> <span data-ttu-id="2d5b2-153">Cliquez sur **Ajouter…**</span><span class="sxs-lookup"><span data-stu-id="2d5b2-153">Click the **Add…**</span></span> <span data-ttu-id="2d5b2-154">et naviguez jusqu’à l’emplacement où vous avez enregistré le fichier XSD, puis sélectionnez le fichier WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-154">button and navigate to the location where you saved the XSD file and select the file WadConfig.xsd.</span></span> <span data-ttu-id="2d5b2-155">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-155">Click **OK**.</span></span>
4. <span data-ttu-id="2d5b2-156">Remplacez le contenu du fichier de configuration WadExample.xml par le XML suivant, puis enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-156">Replace the contents of the WadExample.xml configuration file with the following XML and save the file.</span></span> <span data-ttu-id="2d5b2-157">Ce fichier de configuration définit deux compteurs de performances à collecter : un pour l'utilisation du processeur et l'autre pour l'utilisation de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-157">This configuration file defines a couple performance counters to collect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="2d5b2-158">Ensuite, la configuration définit les quatre événements correspondant aux méthodes de la classe SampleEventSourceWriter.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-158">Then the configuration defines the four events corresponding to the methods in the SampleEventSourceWriter class.</span></span>

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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a><span data-ttu-id="2d5b2-159">Étape 5 : installation à distance de Diagnostics sur votre machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="2d5b2-159">Step 5: Remotely install Diagnostics on your Azure Virtual Machine</span></span>
<span data-ttu-id="2d5b2-160">Les applets de commande PowerShell pour la gestion de Diagnostics sur une machine virtuelle sont : Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension et Remove-AzureVMDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-160">The PowerShell cmdlets for managing Diagnostics on a VM are: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension, and Remove-AzureVMDiagnosticsExtension.</span></span>

1. <span data-ttu-id="2d5b2-161">Sur votre ordinateur de développement, ouvrez Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-161">On your developer computer, open Azure PowerShell.</span></span>
2. <span data-ttu-id="2d5b2-162">Exécutez le script pour installer Diagnostics à distance sur votre machine virtuelle (remplacez `<user>` par le nom de votre répertoire utilisateur).</span><span class="sxs-lookup"><span data-stu-id="2d5b2-162">Execute the script to remotely install Diagnostics on your VM (Replace `<user>` with your user directory name.</span></span> <span data-ttu-id="2d5b2-163">Remplacez `<StorageAccountKey>` par la clé de votre compte de stockage wadexamplevm) :</span><span class="sxs-lookup"><span data-stu-id="2d5b2-163">Replace `<StorageAccountKey>` with the storage account key for your wadexamplevm storage account):</span></span>
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
### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="2d5b2-164">Étape 6 : examen de vos données télémétriques</span><span class="sxs-lookup"><span data-stu-id="2d5b2-164">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="2d5b2-165">Dans l' **Explorateur de serveurs** de Visual Studio, naviguez jusqu'au compte de stockage wadexample.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-165">In the Visual Studio **Server Explorer** navigate to the wadexample storage account.</span></span> <span data-ttu-id="2d5b2-166">Après environ cinq minutes d’exécution de la machine virtuelle, vous devriez voir les tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** et **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-166">After the VM has been running about 5 minutes you should see the tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="2d5b2-167">Double-cliquez sur l'une des tables pour afficher les données télémétriques qui ont été collectées.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-167">Double-click on one of the tables to view the telemetry that has been collected.</span></span>

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="2d5b2-169">Schéma du fichier de configuration</span><span class="sxs-lookup"><span data-stu-id="2d5b2-169">Configuration file schema</span></span>
<span data-ttu-id="2d5b2-170">Le fichier de configuration des diagnostics définit les valeurs qui sont utilisées pour initialiser les paramètres de configuration de diagnostic lorsque l’agent de diagnostics démarre.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-170">The Diagnostics configuration file defines values that are used to initialize diagnostic configuration settings when the diagnostics agent starts.</span></span> <span data-ttu-id="2d5b2-171">Consultez la [dernière référence de schéma](https://msdn.microsoft.com/library/azure/mt634524.aspx) pour obtenir les valeurs valides et des exemples.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-171">See the [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2d5b2-172">Résolution de problèmes</span><span class="sxs-lookup"><span data-stu-id="2d5b2-172">Troubleshooting</span></span>
<span data-ttu-id="2d5b2-173">Pour plus d'informations, voir [Dépannage des diagnostics Azure](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) .</span><span class="sxs-lookup"><span data-stu-id="2d5b2-173">See [Troubleshooting Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d5b2-174">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2d5b2-174">Next steps</span></span>
<span data-ttu-id="2d5b2-175">[Consultez la liste des articles sur les diagnostics Azure relatifs aux machines virtuelles](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) pour modifier les données que vous collectez, résoudre des problèmes ou pour en savoir plus sur les diagnostics en général.</span><span class="sxs-lookup"><span data-stu-id="2d5b2-175">[See a list of virtual machine related Azure Diagnostics articles](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) to change the data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
