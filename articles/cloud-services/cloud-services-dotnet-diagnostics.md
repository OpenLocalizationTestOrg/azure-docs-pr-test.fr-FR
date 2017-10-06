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
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a>Activation des diagnostics Azure dans Azure Cloud Services
Consultez la page [Présentation des diagnostics Azure](../azure-diagnostics.md) pour obtenir des informations sur les diagnostics Azure.

## <a name="how-tooenable-diagnostics-in-a-worker-role"></a>Comment tooEnable Diagnostics dans un rôle de travail
Cette procédure pas à pas décrit comment un rôle de travail Azure qui émet les données de télémétrie à l’aide de tooimplement hello .NET EventSource (classe). Diagnostics Azure est utilisé toocollect des données de télémétrie hello et stockez-le dans un compte de stockage Azure. Lorsque vous créez un rôle de travail, Visual Studio active automatiquement Diagnostics 1.0 dans le cadre de la solution hello dans Azure SDK pour .NET 2.4 et versions antérieures. Hello instructions suivantes décrivent les processus hello pour la création de rôle de travail hello, la désactivation de Diagnostics 1.0 à partir de la solution de hello et le déploiement de Diagnostics 1.2 ou rôle de travail tooyour 1.3.

### <a name="prerequisites"></a>Composants requis
Cet article suppose que vous avez un abonnement Azure et que vous utilisez Visual Studio avec hello Azure SDK. Si vous n’avez pas un abonnement Azure, vous pouvez vous inscrire pour hello [version d’évaluation gratuite][Free Trial]. Assurez-vous que trop[installer et configurer Azure PowerShell version 0.8.7 ou version ultérieure][Install and configure Azure PowerShell version 0.8.7 or later].

### <a name="step-1-create-a-worker-role"></a>Étape 1 : création d’un rôle de travail
1. Lancez **Visual Studio**.
2. Créer un **Azure Cloud Service** projet à partir de hello **Cloud** modèle qui cible le .NET Framework 4.5.  Nommez le projet hello « WadExample » et cliquez sur Ok.
3. Sélectionnez **Rôle de travail** et cliquez sur Ok. Hello projet sera créé.
4. Dans **l’Explorateur de solutions**, double-cliquez sur hello **WorkerRole1** fichier de propriétés.
5. Bonjour **Configuration** onglet, décochez la case **activer les Diagnostics** toodisable Diagnostics 1.0 (Azure SDK 2.4 et versions antérieur).
6. Générer votre tooverify de solution qui vous comporter aucune erreur.

### <a name="step-2-instrument-your-code"></a>Étape 2 : instrumentalisation de votre code
Remplacez contenu hello de WorkerRole.cs par hello suivant de code. Hello classe SampleEventSourceWriter, héritée de hello [EventSource, classe][EventSource Class], implémente les quatre méthodes de journalisation : **SendEnums**, **MessageMethod** , **SetOther** et **HighFreq**. Hello premier paramètre toohello **WriteEvent** méthode définit l’ID hello pour les événements respectif hello. Hello méthode Run implémente une boucle infinie qui chacun des hello appelle des méthodes de journalisation implémentées dans hello **SampleEventSourceWriter** classe toutes les 10 secondes.

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


### <a name="step-3-deploy-your-worker-role"></a>Étape 3 : déploiement de votre rôle de travail

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. Déployer votre tooAzure de rôle de travail à partir de Visual Studio en sélectionnant hello **WadExample** projet Bonjour l’Explorateur de solutions, puis **publier** de hello **générer** menu.
2. Choisissez votre abonnement.
3. Bonjour **paramètres de publication Microsoft Azure** boîte de dialogue, sélectionnez **créer un nouveau...** .
4. Bonjour **créer un Service Cloud et le compte de stockage** boîte de dialogue, entrez un **nom** (par exemple, « WadExample ») et sélectionnez une région ou un groupe d’affinités.
5. Ensemble hello **environnement** trop**intermédiaire**.
6. Modifiez d’autres **Paramètres** le cas échéant, puis cliquez sur **Publier**.
7. Une fois le déploiement terminé, vérifiez dans hello portail Azure que votre service cloud est dans un **en cours d’exécution** état.

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-hello-extension"></a>Étape 4 : Créer votre fichier de configuration de Diagnostics et installer l’extension de hello
1. Télécharger la définition de schéma de fichier de configuration publique hello en exécutant hello suivant de commande PowerShell :

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. Ajouter un tooyour du fichier XML **WorkerRole1** projet en cliquant sur hello **WorkerRole1** de projet et sélectionnez **ajouter** -> **un nouvel élément...** -> **Éléments Visual C#** -> **Données** -> **Fichier XML**. Nom de fichier de hello « WadExample.xml ».

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. Associer hello WadConfig.xsd fichier de configuration hello. Assurez-vous que la fenêtre de l’éditeur WadExample.xml hello est la fenêtre active hello. Appuyez sur **F4** tooopen hello **propriétés** fenêtre. Cliquez sur hello **schémas** propriété Bonjour **propriétés** fenêtre. Cliquez sur hello **...** Bonjour **schémas** propriété. Cliquez sur hello **ajouter...** bouton et accédez emplacement toohello où vous avez enregistré le fichier XSD de hello et sélectionnez hello WadConfig.xsd. Cliquez sur **OK**.

4. Remplacez le contenu hello hello WadExample.xml du fichier de configuration par hello XML suivant, puis enregistrez le fichier de hello. Ce fichier de configuration définit deux toocollect de compteurs de performances : un pour l’utilisation du processeur et l’autre pour l’utilisation de la mémoire. Configuration de hello définit ensuite hello quatre événements correspondant méthodes toohello Bonjour SampleEventSourceWriter classe.

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

### <a name="step-5-install-diagnostics-on-your-worker-role"></a>Étape 5 : installation de Diagnostics sur votre rôle de travail
Hello applets de commande PowerShell pour gérer les Diagnostics sur un rôle web ou de travail sont : Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension et Remove-AzureServiceDiagnosticsExtension.

1. Ouvrez Azure PowerShell.
2. Exécutez hello script tooinstall Diagnostics sur votre rôle de travail (remplacez *StorageAccountKey* avec la clé de compte de stockage hello pour votre compte de stockage wadexample et *config_path* avec le chemin d’accès de hello toohello *WadExample.xml* fichier) :

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a>Étape 6 : examen de vos données télémétriques
Bonjour Visual Studio **l’Explorateur de serveurs**, accédez de compte de stockage toohello wadexample. Une fois que le service de cloud computing hello s’exécute minutes environ cinq (5), vous devez voir les tables hello **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** et **WADSetOtherTable**. Double-cliquez sur un de télémétrie de hello hello tables tooview qui ont été collectée.

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a>Schéma du fichier de configuration
fichier de configuration des Diagnostics Hello définit des valeurs qui sont des paramètres de configuration de diagnostic tooinitialize utilisé au démarrage de l’agent de diagnostics hello. Consultez hello [dernière référence du schéma](https://msdn.microsoft.com/library/azure/mt634524.aspx) pour les valeurs valides et des exemples.

## <a name="troubleshooting"></a>Résolution des problèmes
Si vous rencontrez des problèmes, consultez la page [Résolution de problèmes des diagnostics Azure](../azure-diagnostics-troubleshooting.md) pour obtenir de l’aide.

## <a name="next-steps"></a>Étapes suivantes
[Afficher la liste des articles diagnostic connexes Azure à une machine virtuelle](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) vous collectez les données de salutation toochange résoudre des problèmes ou en savoir plus sur les diagnostics en général.

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
