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
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a>Activation des diagnostics dans Azure Virtual Machines
Consultez la page [Présentation des diagnostics Azure](../monitoring-and-diagnostics/azure-diagnostics.md) pour obtenir des informations sur les diagnostics Azure.

## <a name="how-tooenable-diagnostics-in-a-virtual-machine"></a>Comment tooEnable Diagnostics sur une Machine virtuelle
Cette procédure pas à pas explique comment tooremotely installer les Diagnostics tooan machine virtuelle Azure à partir d’un ordinateur de développement. Vous apprendrez également comment une application qui s’exécute sur cet ordinateur virtuel Azure et émet les données de télémétrie à l’aide de tooimplement hello .NET [EventSource, classe][EventSource Class]. Diagnostics Azure est utilisé toocollect hello télémétrie et le stocker dans un compte de stockage Azure.

### <a name="pre-requisites"></a>Conditions préalables
Cette procédure pas à pas suppose que vous avez un abonnement Azure et que vous utilisez Visual Studio 2017 avec hello Azure SDK. Si vous n’avez pas un abonnement Azure, vous pouvez vous inscrire pour hello [version d’évaluation gratuite][Free Trial]. Assurez-vous que trop[installer et configurer Azure PowerShell version 0.8.7 ou version ultérieure][Install and configure Azure PowerShell version 0.8.7 or later].

### <a name="step-1-create-a-virtual-machine"></a>Étape 1 : création d’une machine virtuelle
1. Sur votre ordinateur de développement, lancez Visual Studio 2017.
2. Bonjour Visual Studio **l’Explorateur de serveurs** développez **Azure**, avec le bouton droit **virtuels** puis sélectionnez **créer un ordinateur virtuel**.
3. Sélectionnez votre abonnement Azure Bonjour **choisir un abonnement** boîte de dialogue et cliquez sur **suivant**.
4. Sélectionnez **Windows Server 2012 R2 Datacenter, juin 2017** Bonjour **sélectionner une Image de Machine virtuelle** boîte de dialogue et cliquez sur **suivant**.
5. Bonjour **les paramètres de base de Machine virtuelle**, définissez le nom d’ordinateur virtuel hello trop « wadexample ». Définissez votre nom d'utilisateur et votre mot de passe administrateur, puis cliquez sur **Suivant**.
6. Bonjour **paramètres du Service Cloud** boîte de dialogue Créer un nouveau service cloud nommé « wadexampleVM ». Créez un compte de stockage appelé « wadexample », puis cliquez sur **Suivant**.
7. Cliquez sur **Create**.

### <a name="step-2-create-your-application"></a>Étape 2 : création d’une application
1. Sur votre ordinateur de développement, lancez Visual Studio 2017.
2. Créez une nouvelle application console Visual C# qui cible .NET Framework 4.5. Nommez le projet de hello « WadExampleVM ».

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. Remplacez contenu hello de Program.cs par hello suivant de code. Hello classe **SampleEventSourceWriter** implémente les quatre méthodes de journalisation : **SendEnums**, **MessageMethod**, **SetOther** et  **HighFreq**. Hello premier paramètre toohello WriteEvent méthode définit les ID de hello pour les événements respectif hello. Hello méthode Run implémente une boucle infinie qui chacun des hello appelle des méthodes de journalisation implémentées dans hello **SampleEventSourceWriter** classe toutes les 10 secondes.

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
4. Enregistrez le fichier de hello et sélectionnez **générer la Solution** de hello **générer** menu toobuild votre code.

### <a name="step-3-deploy-your-application"></a>Étape 3 : déploiement de votre application
1. Avec le bouton droit sur hello **WadExampleVM** projet **l’Explorateur de solutions** et choisissez **ouvrir le dossier dans l’Explorateur de fichiers**.
2. Accédez toohello *bin\Debug* dossier et copie tous les hello fichiers (WadExampleVM.*)
3. Dans **l’Explorateur de serveurs** avec le bouton droit sur l’ordinateur virtuel de hello et choisissez **se connecter à l’aide du Bureau à distance**.
4. Une fois connecté toohello VM créez un dossier nommé WadExampleVM et collez les fichiers de votre application dans le dossier de hello.
5. Lancez l’application hello WadExampleVM.exe. Une fenêtre de console vide doit apparaître.

### <a name="step-4-create-your-diagnostics-configuration-and-install-hello-extension"></a>Étape 4 : Création de votre configuration de Diagnostics et installer l’Extension de hello
1. Téléchargez l’ordinateur de développement tooyour définition de schéma de hello configuration publique fichier en exécutant hello suivant de commande PowerShell :

     (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
2. Ouvrez un nouveau fichier XML dans Visual Studio, soit dans un projet qui est déjà ouvert, soit dans une instance de Visual Studio ne comportant aucun projet ouvert. Dans Visual Studio, sélectionnez **Ajouter** -> **Nouvel élément…** -> **Éléments Visual C#** -> **Données** -> **Fichier XML**. Nom de fichier hello « WadExample.xml »
3. Associer hello WadConfig.xsd fichier de configuration hello. Assurez-vous que la fenêtre de l’éditeur WadExample.xml hello est la fenêtre active hello. Appuyez sur **F4** tooopen hello **propriétés** fenêtre. Cliquez sur hello **schémas** propriété Bonjour **propriétés** fenêtre. Cliquez sur hello **...** Bonjour **schémas** propriété. Cliquez sur hello **ajouter...** bouton et accédez emplacement toohello où vous avez enregistré le fichier XSD de hello et sélectionnez hello WadConfig.xsd. Cliquez sur **OK**.
4. Remplacez le contenu hello hello WadExample.xml du fichier de configuration par hello XML suivant, puis enregistrez le fichier de hello. Ce fichier de configuration définit deux toocollect de compteurs de performances : un pour l’utilisation du processeur et l’autre pour l’utilisation de la mémoire. Configuration de hello définit ensuite hello quatre événements correspondant méthodes toohello Bonjour SampleEventSourceWriter classe.

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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a>Étape 5 : installation à distance de Diagnostics sur votre machine virtuelle Azure
Hello applets de commande PowerShell pour gérer les Diagnostics sur une machine virtuelle sont : Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension et Remove-AzureVMDiagnosticsExtension.

1. Sur votre ordinateur de développement, ouvrez Azure PowerShell.
2. Exécuter l’installation de tooremotely script hello Diagnostics sur votre machine virtuelle (remplacez `<user>` avec votre nom d’utilisateur active. Remplacez `<StorageAccountKey>` par la clé de compte de stockage hello pour votre compte de stockage wadexamplevm) :
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
### <a name="step-6-look-at-your-telemetry-data"></a>Étape 6 : examen de vos données télémétriques
Bonjour Visual Studio **l’Explorateur de serveurs** accédez compte de stockage toohello wadexample. Après avoir hello machine virtuelle a été exécuté environ 5 minutes, vous devez voir les tables hello **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**,  **WADPerformanceCountersTable** et **WADSetOtherTable**. Double-cliquez sur l’un de télémétrie de hello hello tables tooview qui ont été collectée.

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a>Schéma du fichier de configuration
fichier de configuration des Diagnostics Hello définit des valeurs qui sont des paramètres de configuration de diagnostic tooinitialize utilisé au démarrage de l’agent de diagnostics hello. Consultez hello [dernière référence du schéma](https://msdn.microsoft.com/library/azure/mt634524.aspx) pour les valeurs valides et des exemples.

## <a name="troubleshooting"></a>Résolution des problèmes
Pour plus d'informations, voir [Dépannage des diagnostics Azure](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) .

## <a name="next-steps"></a>Étapes suivantes
[Pour afficher la liste de la machine virtuelle de Azure Diagnostics relatifs](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) vous collectez les données de salutation toochange résoudre des problèmes ou en savoir plus sur les diagnostics en général.

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
