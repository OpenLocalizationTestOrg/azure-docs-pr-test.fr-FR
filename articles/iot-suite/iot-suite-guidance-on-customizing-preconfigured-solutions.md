---
title: "aaaCustomizing préconfiguré solutions | Documents Microsoft"
description: "Explique comment toocustomize hello Azure IoT Suite préconfiguré solutions."
services: 
suite: iot-suite
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4653ae53-4110-4a10-bd6c-7dc034c293a8
ms.service: iot-suite
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 1a8573f5ac6ed944c44459df495446f15174d513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-a-preconfigured-solution"></a>Personnaliser une solution préconfigurée

solutions de Hello préconfiguré fournies avec hello Azure IoT Suite illustrent les services de hello dans hello suite travailler ensemble toodeliver une solution de bout en bout. À partir de ce point de départ, il existe divers emplacements dans lesquels vous pouvez étendre et personnaliser des solutions hello pour des scénarios spécifiques. Hello les sections suivantes décrire ces points de personnalisation courantes.

## <a name="find-hello-source-code"></a>Rechercher du code source de hello

code source de Hello pour les solutions hello préconfiguré est disponible sur GitHub Bonjour suivant référentiels :

* Surveillance à distance : [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)
* Maintenance prédictive : [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)
* Usine connectée : [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)

code source de Hello pour les solutions hello préconfiguré est fournie pratiques et les modèles de hello toodemonstrate aux fonctionnalités de bout en bout hello tooimplement d’une solution IoT à l’aide d’Azure IoT Suite utilisées. Vous trouverez plus d’informations sur la façon toobuild et déployer des solutions hello dans des référentiels GitHub hello.

## <a name="change-hello-preconfigured-rules"></a>Modifier les règles de hello préconfiguré

Hello solution d’analyse à distance inclut trois [Analytique de flux de données Azure](https://azure.microsoft.com/services/stream-analytics/) travaux toohandle les informations de périphérique, la télémétrie et logique des règles dans les solutions hello.

Hello trois flux de travaux de l’analytique et leur syntaxe sont décrites en détail dans hello [surveillance à distance préconfiguré procédure pas à pas de solution](iot-suite-remote-monitoring-sample-walkthrough.md). 

Vous pouvez modifier ces travaux directement tooalter hello logique, ou ajouter une logique spécifique tooyour scénario. Vous pouvez trouver hello les tâches de flux de données Analytique comme suit :

1. Accédez trop[portail Azure](https://portal.azure.com).
2. Recherchez le groupe de ressources toohello avec le même nom que votre solution IoT de hello. 
3. Sélectionnez hello Analytique de flux de données Azure tâche toomodify. 
4. Tâche d’arrêt de hello en sélectionnant **arrêter** dans l’ensemble de hello de commandes. 
5. Modifier les sorties, les requêtes et les entrées de hello.
   
    Une simple modification est la requête de hello toochange pour hello **règles** travail toouse un **« < »** au lieu d’un **» > «**. portail de solution Hello affiche toujours **» > «** lorsque vous modifiez une règle, mais notez comment le comportement de hello est retournée en raison de modifications toohello Bonjour sous-jacent du travail.
6. Démarrer le travail de hello

> [!NOTE]
> tableau de bord analyse Hello à distance dépend des données spécifiques, toute modification des travaux de hello peut causer toofail du tableau de bord hello.

## <a name="add-your-own-rules"></a>Ajout de vos propres règles

En outre toochanging hello préconfiguré les travaux de l’Analytique des flux de données Azure, vous pouvez utiliser les nouveaux travaux de hello tooadd portail Azure ou ajouter de nouveaux travaux de tooexisting de requêtes.

## <a name="customize-devices"></a>Personnalisation des appareils

Une des activités extension les plus courantes hello travaille avec un scénario tooyour spécifique de périphériques. Il existe plusieurs méthodes pour travailler avec des appareils, Ces méthodes incluent la modification d’un toomatch appareil simulé votre scénario ou à l’aide de hello [IoT appareil SDK] [ IoT Device SDK] tooconnect votre solution de toohello périphérique physique.

Pour une unité de tooadding guide pas à pas, consultez hello [Iot Suite connexion appareils](iot-suite-connecting-devices.md) article et hello [exemple du Kit de développement logiciel C de surveillance à distance](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring). Cet exemple est conçu toowork avec hello solution préconfigurée de surveillance à distance.

### <a name="create-your-own-simulated-device"></a>Création de votre propre appareil simulé

Inclus dans hello [code source de la solution de surveillance à distance](https://github.com/Azure/azure-iot-remote-monitoring), est un simulateur .NET. Ce simulateur est hello une configuré comme partie de la solution de hello et que vous pouvez modifier toosend différentes métadonnées, données de télémétrie et répondre de méthodes et les commandes de toodifferent.

Simulateur préconfigurées de Hello Bonjour solution préconfigurée de surveillance à distance simule un périphérique de refroidissement qui émet les données de télémétrie température et humidité. Vous pouvez modifier le simulateur hello Bonjour [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) projeter le moment où vous avez dupliquée référentiel GitHub de hello.

### <a name="available-locations-for-simulated-devices"></a>Emplacements disponibles pour les appareils simulés

ensemble des emplacements par défaut de Hello est en Seattle Way, Redmond, Washington, États-Unis d’Amérique. Vous pouvez modifier ces emplacements dans [SampleDeviceFactory.cs][lnk-sample-device-factory].

### <a name="add-a-desired-property-update-handler-toohello-simulator"></a>Ajouter un simulateur de toohello Gestionnaire de propriétés souhaitées mise à jour

Vous pouvez définir une valeur pour une propriété spécifique pour un périphérique dans le portail de solution hello. Il incombe hello de demande de modification de propriété hello appareil toohandle hello lors de l’appareil de hello récupère la valeur de propriété de hello souhaité. prise en charge de tooadd pour une modification de valeur de propriété via une propriété de votre choix, vous devez tooadd un simulateur toohello de gestionnaire.

Simulateur de Hello contient des gestionnaires pour hello **SetPointTemp** et **TelemetryInterval** propriétés que vous pouvez mettre à jour en définissant souhaitée des valeurs dans le portail de solution hello.

exemple Hello présente Gestionnaire hello pour hello **SetPointTemp** souhaité propriété Bonjour **CoolerDevice** classe :

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

Cette méthode met à jour le point de données de télémétrie hello température hello de rapports change différé tooIoT Hub en définissant une propriété signalée.

Vous pouvez ajouter vos propres gestionnaires pour vos propres propriétés en suivant le modèle hello Bonjour précédent exemple.

Vous devez également lier Gestionnaire de toohello hello propriété souhaitée comme indiqué dans hello hello de l’exemple suivant **CoolerDevice** constructeur :

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

Notez que **SetPointTempPropertyName** est une constante définie en tant que « Config.SetPointTemp ».

### <a name="add-support-for-a-new-method-toohello-simulator"></a>Ajouter la prise en charge pour un nouveau simulateur de toohello (méthode)

Vous pouvez personnaliser hello simulateur tooadd prise en charge pour un nouveau [(méthode) (méthode directe)][lnk-direct-methods]. Les deux principales étapes requises sont les suivantes :

- Simulateur de Hello doit le signaler hello IoT hub dans solution hello préconfiguré avec les détails de la méthode hello.
- Simulateur de Hello doit inclure l’appel de méthode de code toohandle hello lorsque vous l’appelez à partir de hello **détails de l’appareil** Panneau de configuration dans l’Explorateur de solutions hello ou via un travail.

Hello surveillance à distance préconfiguré solution utilise *signalé propriétés* toosend les détails du concentrateur de tooIoT méthodes prises en charge. Hello solution back-end conserve une liste de toutes les méthodes hello pris en charge par chaque périphérique, ainsi que l’historique des appels de méthode. Vous pouvez afficher ces informations sur les périphériques et appeler des méthodes dans le portail de solution hello.

toonotify hello IoT hub qu’un périphérique prend en charge une méthode, les appareils hello doivent ajouter les détails de hello méthode toohello **SupportedMethods** nœud Bonjour signalé propriétés :

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

signature de méthode Hello a hello suivant le format : `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`. Par exemple, toospecify hello **InitiateFirmwareUpdate** méthode attend un paramètre de chaîne nommé **FwPackageURI**, utilisez hello après la signature de méthode :

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

Pour obtenir la liste des types de paramètres pris en charge, consultez hello **CommandTypes** classe dans le projet d’Infrastructure hello.

toodelete une méthode, définissez trop de signature de méthode hello`null` Bonjour signalé propriétés.

> [!NOTE]
> Hello back-end solution met à jour uniquement les informations sur les méthodes prises en charge lorsqu’il reçoit un *les informations de périphérique* message à partir de l’appareil de hello.

Hello suivant l’exemple de code à partir de hello **SampleDeviceFactory** classe Bonjour commun projet montre comment tooadd liste méthode toohello de **SupportedMethods** Bonjour signalé propriétés envoyées par hello périphérique :

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' toospecifiy hello URI of hello firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

Cet extrait de code ajoute les détails de hello **InitiateFirmwareUpdate** méthode notamment toodisplay de texte dans le portail de solution hello et les détails de hello nécessaire les paramètres de méthode.

Simulateur de Hello envoie des propriétés déclarées, y compris la liste hello des méthodes prises en charge, tooIoT Hub au démarrage du simulateur de hello.

Ajouter un code de simulateur Gestionnaire toohello pour chaque méthode, qu'il prend en charge. Vous pouvez voir les gestionnaires existants de hello Bonjour **CoolerDevice** classe dans le projet de Simulator.WebJob hello. exemple Hello présente Gestionnaire hello pour **InitiateFirmwareUpdate** méthode :

```csharp
public async Task<MethodResponse> OnInitiateFirmwareUpdate(MethodRequest methodRequest, object userContext)
{
    if (_deviceManagementTask != null && !_deviceManagementTask.IsCompleted)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "Device is busy"
        }, 409));
    }

    try
    {
        var operation = new FirmwareUpdate(methodRequest);
        _deviceManagementTask = operation.Run(Transport).ContinueWith(async task =>
        {
            // after firmware completed, we reset telemetry
            var telemetry = _telemetryController as ITelemetryWithTemperatureMeanValue;
            if (telemetry != null)
            {
                telemetry.TemperatureMeanValue = 34.5;
            }

            await UpdateReportedTemperatureMeanValue();
        });

        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "FirmwareUpdate accepted",
            Uri = operation.Uri
        }));
    }
    catch (Exception ex)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = ex.Message
        }, 400));
    }
}
```

Noms de gestionnaire de méthode doivent commencer par `On` suivi nom hello de méthode hello. Hello **methodRequest** paramètre contient tous les paramètres transmis avec l’appel de méthode hello de hello solution back-end. valeur de retour Hello doit être de type **tâche&lt;MethodResponse&gt;**. Hello **BuildMethodResponse** méthode utilitaire vous permet de créer la valeur de retour hello.

À l’intérieur du Gestionnaire de méthode hello, vous pouvez :

- Démarrer une tâche asynchrone.
- Extraire les propriétés souhaitées hello *double de l’appareil* dans IoT Hub.
- Mettre à jour une seule propriété signalée à l’aide de hello **SetReportedPropertyAsync** méthode Bonjour **CoolerDevice** classe.
- Mettre à jour plusieurs propriétés déclarées en créant un **TwinCollection** instance et hello appelant **Transport.UpdateReportedPropertiesAsync** (méthode).

Hello précédent exemple de mise à jour de microprogramme exécute hello comme suit :

- Vérifications hello périphérique est la demande de mise à jour du microprogramme tooaccept en mesure de hello.
- Lance l’opération de mise à jour de microprogramme hello de façon asynchrone et réinitialise les données de télémétrie hello lorsque hello est terminée.
- Immédiatement retourne hello « FirmwareUpdate accepté » demande de message tooindicate hello a été acceptée par le périphérique de hello.

### <a name="build-and-use-your-own-physical-device"></a>Création et utilisation de votre propre appareil (physique)

Hello [kits de développement logiciel Azure IoT](https://github.com/Azure/azure-iot-sdks) fournissent des bibliothèques pour la connexion de nombreux types d’appareils (systèmes d’exploitation et langues) dans les solutions IoT.

## <a name="modify-dashboard-limits"></a>Modification des limites de tableau de bord

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a>Nombre d’appareils affichés dans la liste déroulante du tableau de bord

valeur par défaut Hello est 200. Vous pouvez modifier cette valeur dans [DashboardController.cs][lnk-dashboard-controller].

### <a name="number-of-pins-toodisplay-in-bing-map-control"></a>Nombre de toodisplay des codes confidentiels dans un contrôle de carte Bing

valeur par défaut Hello est 200. Vous pouvez modifier cette valeur dans [TelemetryApiController.cs][lnk-telemetry-api-controller-01].

### <a name="time-period-of-telemetry-graph"></a>Période de temps du graphique de télémétrie

valeur par défaut Hello est de 10 minutes. Vous pouvez modifier cette valeur dans [TelemetryApiController.cs][lnk-telemetry-api-controller-02].

## <a name="manually-set-up-application-roles"></a>Configuration manuelle des rôles d’application

Hello procédure suivante décrit comment tooadd **Admin** et **ReadOnly** tooa de rôles d’application de solution préconfigurée. Notez que les solutions préconfigurées déjà mis en service à partir du site de azureiotsuite.com hello incluent hello **Admin** et **ReadOnly** rôles.

Membres de hello **ReadOnly** rôle peut voir hello le tableau de bord et de la liste des appareils hello, mais ne sont pas autorisées tooadd périphériques, modifier les attributs de périphérique ou les commandes de l’envoi.  Membres de hello **Admin** rôle possèdent un accès complet des fonctionnalités de hello de tooall dans la solution de hello.

1. Accédez toohello [portail Azure classic][lnk-classic-portal].
2. Sélectionnez **Active Directory**.
3. Cliquez sur nom hello client AAD de hello que vous avez utilisé lors de la configuration de votre solution.
4. Cliquez sur **Applications**.
5. Cliquez sur nom hello application hello qui correspond au nom de votre solution préconfigurée. Si vous ne voyez pas votre application dans la liste de hello, sélectionnez **Applications que ma société possède** Bonjour **afficher** liste déroulante et cliquez sur hello case à cocher.
6. Au bas de hello de page de hello, cliquez sur **gérer manifeste** , puis **télécharger le manifeste**.
7. Cette procédure télécharge un ordinateur local de .json fichier tooyour. Ouvrez ce fichier pour le modifier dans un éditeur de texte de votre choix.
8. Sur hello troisième ligne du fichier .json de hello, vous pouvez voir :

   ```json
   "appRoles" : [],
   ```
   Remplacez cette ligne hello suivant de code :

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access toohello application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access toodevice information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. Enregistrez le fichier de mise à jour .json de hello (vous pouvez remplacer les fichiers existants hello).
10. Bonjour portail Azure classic, bas hello de page de hello, sélectionnez **gérer manifeste** puis **télécharger le manifeste** tooupload hello .json enregistré à l’étape précédente de hello.
11. Vous avez maintenant ajouté hello **Admin** et **ReadOnly** application tooyour de rôles.
12. tooassign un de ces utilisateurs tooa de rôles dans votre annuaire, consultez [autorisations sur le site de azureiotsuite.com hello][lnk-permissions].

## <a name="feedback"></a>Commentaires

Avez-vous une personnalisation que vous aimeriez toosee traitée dans ce document ? Ajouter des suggestions de fonctionnalités trop[User Voice](https://feedback.azure.com/forums/321918-azure-iot), ou un commentaire sur cet article. 

## <a name="next-steps"></a>Étapes suivantes

toolearn savoir plus sur les options hello pour la personnalisation des solutions de hello préconfiguré, consultez :

* [Solution de Azure IoT Suite l’analyse à distance préconfiguré tooyour application logique de connexion][lnk-logicapp]
* [Utiliser la télémétrie dynamique avec hello solution préconfigurée de surveillance à distance][lnk-dynamic]
* [Métadonnées d’informations de périphérique Bonjour solution préconfigurée de surveillance à distance][lnk-devinfo]
* [Personnaliser l’interconnexion hello fabrique solution affiche les données à partir de vos serveurs OPC UA][lnk-cf-customize]

[lnk-logicapp]: iot-suite-logic-apps-tutorial.md
[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[IoT Device SDK]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-permissions]: iot-suite-permissions.md
[lnk-dashboard-controller]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/Controllers/DashboardController.cs#L27
[lnk-telemetry-api-controller-01]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L27
[lnk-telemetry-api-controller-02]: https://github.com/Azure/azure-iot-remote-monitoring/blob/e7003339f73e21d3930f71ceba1e74fb5c0d9ea0/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L25 
[lnk-sample-device-factory]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Common/Factory/SampleDeviceFactory.cs#L40
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-cf-customize]: iot-suite-connected-factory-customize.md