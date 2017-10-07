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
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a>Activer Application Insights Profiler pour une ressource Azure Cloud Services

Cette procédure pas à pas montre comment tooenable Azure Application Insights Profiler une application ASP.NET hébergée par une ressource de Services de cloud computing Azure. prise en charge pour les Machines virtuelles Azure, les machines virtuelles identiques et Azure Service Fabric sont des exemples de Hello. exemples Hello s’appuient sur des modèles qui prennent en charge le modèle de déploiement du Gestionnaire de ressources Azure hello. Pour plus d’informations sur le modèle de déploiement hello, passez en revue [Azure Resource Manager et déploiement classique : comprendre les modèles de déploiement et état de vos ressources de hello](/azure-resource-manager/resource-manager-deployment-model).

## <a name="overview"></a>Vue d'ensemble

Hello suivant le diagramme illustre le fonctionne de générateur de profils hello pour les ressources des Services de cloud computing Azure. Il utilise une machine virtuelle Azure comme exemple.

![Vue d’ensemble](./media/enable-profiler-compute/overview.png) toocollect concernant le traitement et l’affichage sur hello portail Azure, vous devez installer le composant d’Agent de Diagnostics hello pour les ressources des Services de cloud computing Azure hello. Hello reste de la procédure pas à pas hello fournit des conseils sur la façon de tooinstall et configurer hello Agent de Diagnostics tooenable Application Insights Profiler.

## <a name="prerequisites-for-hello-walkthrough"></a>Configuration requise pour la procédure pas à pas hello

* Un modèle de gestionnaire de ressources de déploiement qui installe les agents de profileur hello sur hello machines virtuelles ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) ou mettre à l’échelle de jeux ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).

* Une instance Application Insights activée pour le profilage. Pour obtenir des instructions, consultez [activer le profil hello](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).

* Ressource de Services de cloud computing Azure de cible de .NET framework 4.6.1 ou version ultérieure installée sur hello.

## <a name="create-a-resource-group-in-your-azure-subscription"></a>Créer un groupe de ressources dans votre abonnement Azure
Bonjour à l’exemple suivant montre comment toocreate une ressource de groupe à l’aide d’un script PowerShell :

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-hello-resource-group"></a>Créer une ressource Application Insights dans le groupe de ressources hello
Sur hello **Application Insights** panneau, entrez les informations de hello pour votre ressource, comme indiqué dans cet exemple : 

![Panneau Application Insights](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-hello-azure-resource-manager-template"></a>Appliquer une clé d’instrumentation Application Insights dans le modèle de gestionnaire de ressources Azure hello

1. Si vous n’avez pas encore téléchargé le modèle de hello, téléchargez-le à partir de [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).

2. Trouver la clé d’Application Insights hello.
   
   ![Emplacement de clé de hello](./media/enable-profiler-compute/copyaikey.png)

3. Remplacez la valeur de modèle hello.
   
   ![Valeur de modèle de hello remplacé](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-toohost-hello-web-application"></a>Créer une application web de machine virtuelle Azure toohost hello
1. Créer un mot de passe de chaîne sécurisée toosave hello.

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. Déployer le modèle de gestionnaire de ressources Azure hello.

   Modifier le répertoire hello dans hello PowerShell console toohello dossier qui contient votre modèle de gestionnaire de ressources. modèle de hello toodeploy, exécutez hello de commande suivante :

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

Une fois le script de hello s’exécute correctement, vous devez trouver un ordinateur virtuel nommé **MyWindowsVM** dans votre groupe de ressources.

## <a name="configure-web-deploy-on-hello-vm"></a>Configurer Web Deploy sur hello machine virtuelle
Assurez-vous que l’extension Web Deploy est activée sur votre machine virtuelle pour pouvoir publier votre application web à partir de Visual Studio.

tooinstall Web Deploy sur un ordinateur virtuel manuellement via WebPI, consultez [installation et configuration de Web Deploy sur IIS 8.0 ou version ultérieure](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later). Pour obtenir un exemple de procédure tooautomate l’installation de Web Deploy à l’aide d’un modèle Azure Resource Manager, consultez [créer, configurer et déployer un tooan d’application web Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).

Si vous déployez une application ASP.NET MVC, consultez tooServer Manager, sélectionnez **Ajout de rôles et fonctionnalités** > **serveur Web (IIS)** > **Web Server**  >  **Développement d’applications**et activer ASP.NET 4.5 sur votre serveur.

![Ajouter ASP.NET](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-hello-azure-application-insights-sdk-for-your-project"></a>Installer hello Kit de développement logiciel Azure Application Insights pour votre projet
1. Ouvrez votre application web ASP.NET dans Visual Studio.

2. Droit hello projet, puis sélectionnez **ajouter** > **Services connectés**.

3. Sélectionnez **Application Insights**.

4. Suivez les instructions de hello sur la page de hello. Sélectionnez la ressource Application Insights hello que vous avez créé précédemment.

5. Sélectionnez hello **inscrire** bouton.


## <a name="publish-hello-project-tooan-azure-vm"></a>Publier hello projet tooan machine virtuelle Azure
Il existe plusieurs façons toopublish un tooan application Azure VM. Une façon consiste toouse Visual Studio 2017.

1. Droit hello projet, puis sélectionnez **publier**.

2. Sélectionnez **des Machines virtuelles Microsoft Azure** comme hello cible de publication et suivez les étapes de hello.

   ![Publish-FromVS](./media/enable-profiler-compute/publishtoVM.png)

3. Exécutez un test de charge sur votre application. Vous devez voir les résultats sur la page Web du portail hello Application Insights instance.


## <a name="enable-hello-profiler"></a>Activer le Générateur de profils hello
1. Accédez tooyour Application Insights **performances** panneau et sélectionnez **configurer**.
   
   ![Icône Configurer](./media/enable-profiler-compute/enableprofiler1.png)
 
2. Sélectionnez **Activer le profileur**.
   
   ![Icône Activer le profileur](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-tooyour-application"></a>Ajouter une application de tooyour de test de performances
Afin de nous permettre de collecter certaines toobe de données exemple affichée dans le Générateur de profils Application Insights, procédez comme suit :

1. Parcourir la ressource Application Insights toohello que vous avez créé précédemment. 

2. Accédez toohello **disponibilité** panneau et ajoutez un test de performances qui envoie l’URL d’application web demandes tooyour. 

   ![Ajouter un test de performance](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a>Afficher vos données de performances

1. Attendez 10-15 minutes pour toocollect de profileur hello et analyser les données de hello. 

2. Accédez toohello **performances** lame dans votre ressource Application Insights et le mode de fonctionne de votre application lorsqu’il est sous charge.

   ![Affichage des données de performance](./media/enable-profiler-compute/aiperformance.png)

3. Icône hello sélectionnez sous **exemples** tooopen hello **vue Trace** panneau.

   ![Ouvrir le panneau d’affichage de la Trace hello](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a>Utiliser un modèle existant

1. Recherchez la déclaration de ressource hello Diagnostics Azure dans votre modèle de déploiement.
   
   Si vous n’avez pas une déclaration, vous pouvez en créer un qui ressemble à la déclaration de hello Bonjour l’exemple suivant. Vous pouvez mettre à jour modèle hello hello [site Web de l’Explorateur de ressources Azure](https://resources.azure.com).

2. Éditeur de hello de modification à partir de `Microsoft.Azure.Diagnostics` trop`AIP.Diagnostics.Test`.

3. Pour `typeHandlerVersion`, utilisez `0.0`.

4. Assurez-vous que `autoUpgradeMinorVersion` est défini trop`true`.

5. Ajouter hello nouvelle `ApplicationInsightsProfiler` instance récepteur Bonjour `WadCfg` objet de paramètres, comme indiqué dans hello l’exemple suivant :

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

## <a name="enable-hello-profiler-on-virtual-machine-scale-sets"></a>Activer le profileur hello sur des machines virtuelles identiques
toosee comment tooenable hello profiler, télécharger hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) modèle. Appliquer hello modifications dans une ressource d’extension de machine virtuelle modèle toohello diagnostics pour l’ensemble d’échelle de machine virtuelle hello.

Assurez-vous que chaque instance dans l’ensemble d’échelle hello a toohello d’accès internet. Hello Agent Profiler peut alors envoyer des exemples de hello collectée Insights tooApplication pour l’affichage et analyse.

## <a name="enable-hello-profiler-on-service-fabric-applications"></a>Activer le profileur hello sur les applications de Service Fabric
1. Hello configurer l’infrastructure du Service cluster toohave hello extension Azure Diagnostics qui installe hello Agent Profiler.

2. Installer hello Application Insights SDK dans le projet de hello et configurer la clé d’Application Insights hello.

3. Ajouter des données de télémétrie application code tooinstrument.

### <a name="provision-hello-service-fabric-cluster-toohave-hello-azure-diagnostics-extension-that-installs-hello-profiler-agent"></a>Configurer Bonjour Service Fabric cluster toohave Bonjour extension Azure Diagnostics qui installe hello Agent Profiler
Un cluster Service Fabric peut être sécurisé ou non sécurisé. Vous pouvez définir un toobe de cluster de passerelle non sécurisées afin qu’il ne nécessite pas un certificat pour l’accès. Les clusters qui hébergent les données et la logique métier doivent être sécurisés. Vous pouvez activer le profileur hello sur des clusters Service Fabric sécurisées et non sécurisées. Cette procédure pas à pas utilise un cluster non sécurisées comme un tooexplain exemple quelles modifications sont requises tooenable hello profiler. Vous pouvez configurer un cluster sécurisé Bonjour identique.

1. Téléchargez le fichier [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json). Comme pour les machines virtuelles et les groupes de machines virtuelles identiques, remplacez `Application_Insights_Key` par votre clé Application Insights :

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

2. Déployer le modèle de hello à l’aide d’un script PowerShell :

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-hello-application-insights-sdk-in-hello-project-and-configure-hello-application-insights-key"></a>Installer hello Application Insights SDK dans le projet de hello et configurer la clé d’Application Insights hello
Installer hello Application Insights SDK à partir de hello [package NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/). Assurez-vous que vous installez une version stable, 2.3 ou ultérieure. 

Pour plus d’informations sur la configuration d’Application Insights dans vos projets, voir [Utilisation de Service Fabric avec Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).

### <a name="add-application-code-tooinstrument-telemetry"></a>Ajouter des données de télémétrie application code tooinstrument
1. Pour tout type de code que vous souhaitez tooinstrument, ajouter une à l’aide de l’instruction autour de lui. 

   Dans l’exemple suivant de hello, hello `RunAsync` méthode est effectue un travail et hello `telemetryClient` classe capture les données de télémétrie hello après son démarrage. événement de Hello requiert un nom unique dans l’application hello.

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

2. Déployer votre cluster de Service Fabric application toohello. Attendez hello application toorun pendant 10 minutes. Pour un meilleur effet, vous pouvez exécuter un test de charge sur l’application hello. Du portail de l’Application Insights accédez toohello **performances** panneau et vous devez voir exemples de traces de profilage s’affichent.

<!---
Commenting out these sections for now
## Enable hello Profiler on Cloud Services applications
[TODO]
## Enable hello Profiler on classic Azure Virtual Machines
[TODO]
## Enable hello Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a>Étapes suivantes

- Trouvez de l’aide pour résoudre les problèmes rencontrés avec le profileur en consultant l’article [Résolution des problèmes de profileur](app-insights-profiler.md#troubleshooting).

- En savoir plus sur le profileur hello dans [Application Insights Profiler](app-insights-profiler.md).
