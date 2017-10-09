---
title: "aaaCreate une règle personnalisée dans Azure IoT Suite | Documents Microsoft"
description: "Comment toocreate une règle personnalisée dans une Suite de IoT solution préconfigurée."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 6c5bb2ca54f3f17b99ad482e727c8e9fa28d7fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-rule-in-hello-remote-monitoring-preconfigured-solution"></a>Créer une règle personnalisée dans hello solution préconfigurée de surveillance à distance

## <a name="introduction"></a>Introduction

Dans les solutions hello préconfiguré, vous pouvez configurer [les règles qui se déclenchent lorsqu’une télémétrie valeur pour un appareil atteint un seuil spécifique][lnk-builtin-rule]. [Utiliser la télémétrie dynamique avec hello solution préconfigurée de surveillance à distance] [ lnk-dynamic-telemetry] décrit comment vous pouvez ajouter des valeurs de données de télémétrie personnalisées, telles que *ExternalTemperature* tooyour solution. Cet article vous explique comment des types de règle personnalisée de toocreate de télémétrie dynamique dans votre solution.

Ce didacticiel utilise un simple Node.js appareil simulé toogenerate télémétrie dynamique toosend toohello solution préconfigurée back-end. Puis, vous ajoutez des règles personnalisées Bonjour **RemoteMonitoring** solution Visual Studio et déployer ce tooyour back-end personnalisé abonnement Azure.

toocomplete ce didacticiel, vous devez :

* Un abonnement Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes. Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk_free_trial].
* [Node.js] [ lnk-node] version 0.12.x ou ultérieure toocreate un appareil simulé.
* Visual Studio 2015 ou Visual Studio 2017 toomodify hello préconfiguré solution précédent se terminer par vos nouvelles règles.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

Prenez note du nom de la solution hello que vous avez choisie pour votre déploiement. Vous aurez besoin de ce nom plus tard dans ce didacticiel.

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

Vous pouvez arrêter l’application de console hello Node.js lorsque vous avez vérifié qu’il envoie **ExternalTemperature** toohello de télémétrie de solution préconfigurée. Maintenir les fenêtre de console hello étant donné que vous exécutez cette application de console Node.js à nouveau après avoir ajouté des solutions de toohello hello règle personnalisée.

## <a name="rule-storage-locations"></a>Emplacements de stockage des règles

Les informations sur les règles sont conservées dans deux emplacements :

* **DeviceRulesNormalizedTable** – cette table stocke un normalisé référencer toohello les règles définies par le portail de solution hello. Lorsque le portail de solution hello affiche les règles de l’appareil, il interroge cette table pour les définitions de règles hello.
* **DeviceRules** blob – cet objet blob stocke toutes les règles de hello définies pour toutes les inscrits et sont définies comme une exécution de traitements référence toohello d’entrée Analytique de flux de données Azure.
 
Lorsque vous mettez à jour une règle existante ou définissez une nouvelle règle dans le portail de solution hello, table de hello et blob sont mises à jour tooreflect hello modifications. règle Hello définition affichée dans le portail de hello provient du magasin de tables hello et règle hello définition référencée par les tâches de flux de données Analytique hello proviennent d’objet blob de hello. 

## <a name="update-hello-remotemonitoring-visual-studio-solution"></a>Mettre à jour hello RemoteMonitoring Visual Studio solution

Hello étapes suivantes vous montrent comment toomodify hello tooinclude de solution RemoteMonitoring Visual Studio, une règle qui utilise hello **ExternalTemperature** télémétrie envoyé à partir de l’appareil simulé de hello :

1. Si vous n'avez pas déjà fait, hello du clone **azure-iot-de surveillance à distance** emplacement approprié de référentiel tooa sur votre ordinateur local à l’aide de hello Git commande suivante :

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. Dans Visual Studio, ouvrez le fichier de RemoteMonitoring.sln de hello à partir de votre copie locale de hello **azure-iot-de surveillance à distance** référentiel.

3. Ouvrez le fichier hello Infrastructure\Models\DeviceRuleBlobEntity.cs et ajoutez un **ExternalTemperature** propriété comme suit :

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. Dans hello du même fichier, ajoutez une **ExternalTemperatureRuleOutput** propriété comme suit :

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. Ouvrez le fichier de hello Infrastructure\Models\DeviceRuleDataFields.cs et ajoutez les éléments suivants de hello **ExternalTemperature** après hello existant **humidité** propriété :

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. Dans l’hello du même fichier, mettre à jour hello **_availableDataFields** méthode tooinclude **ExternalTemperature** comme suit :

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. Ouvrez le fichier hello Infrastructure\Repository\DeviceRulesRepository.cs et modifier hello **BuildBlobEntityListFromTableRows** méthode comme suit :

    ```csharp
    else if (rule.DataField == DeviceRuleDataFields.Humidity)
    {
        entity.Humidity = rule.Threshold;
        entity.HumidityRuleOutput = rule.RuleOutput;
    }
    else if (rule.DataField == DeviceRuleDataFields.ExternalTemperature)
    {
      entity.ExternalTemperature = rule.Threshold;
      entity.ExternalTemperatureRuleOutput = rule.RuleOutput;
    }
    ```

## <a name="rebuild-and-redeploy-hello-solution"></a>Régénérer et redéployer les solutions de hello.

Vous pouvez désormais déployer la solution de mise à jour de hello tooyour abonnement Azure.

1. Ouvrez une invite de commandes avec élévation de privilèges et accédez racine toohello de votre copie locale du référentiel de hello azure-iot-de surveillance à distance.

2. toodeploy votre solution de mise à jour, exécutez hello suivant de commande en remplaçant **{nom du déploiement}** avec nom hello de votre déploiement de solutions préconfigurées que vous avez notée précédemment :

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-hello-stream-analytics-job"></a>Mettre à jour de la tâche de flux de données Analytique hello

Lorsque le déploiement de hello est terminé, vous pouvez mettre à jour hello flux Analytique toouse hello nouvelle règle définitions des travaux.

1. Bonjour portail Azure, accédez à groupe de ressources toohello qui contient des ressources de votre solution préconfigurée. Ce groupe de ressources a hello même nom que vous avez spécifié pour hello solution pendant le déploiement de hello.

2. Accédez toohello {nom du déploiement}-travail de l’Analytique des flux de règles. 

3. Cliquez sur **arrêter** tâche de flux de données Analytique hello toostop de s’exécuter. (Vous devez attendre hello toostop de travail de diffusion en continu avant de pouvoir modifier la requête de hello.)

4. Cliquez sur **Requête**. Modifier hello de hello requête tooinclude **sélectionnez** instruction pour **ExternalTemperature**. Hello exemple suivant montre hello complet de la requête avec hello nouveau **sélectionnez** instruction :

    ```
    WITH AlarmsData AS 
    (
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Temperature' as ReadingType,
         Stream.Temperature as Reading,
         Ref.Temperature as Threshold,
         Ref.TemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Humidity' as ReadingType,
         Stream.Humidity as Reading,
         Ref.Humidity as Threshold,
         Ref.HumidityRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'ExternalTemperature' as ReadingType,
         Stream.ExternalTemperature as Reading,
         Ref.ExternalTemperature as Threshold,
         Ref.ExternalTemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.ExternalTemperature IS NOT null AND Stream.ExternalTemperature > Ref.ExternalTemperature
    )
     
    SELECT *
    INTO DeviceRulesMonitoring
    FROM AlarmsData
     
    SELECT *
    INTO DeviceRulesHub
    FROM AlarmsData
    ```

5. Cliquez sur **enregistrer** toochange hello mis à jour la requête de la règle.

6. Cliquez sur **Démarrer** tâche de flux de données Analytique hello toostart à nouveau d’exécuter.

## <a name="add-your-new-rule-in-hello-dashboard"></a>Ajouter votre nouvelle règle dans le tableau de bord hello

Vous pouvez maintenant ajouter hello **ExternalTemperature** périphérique tooa de règle dans le tableau de bord de solution hello.

1. Accédez portal de solution toohello.

2. Accédez toohello **périphériques** Panneau de configuration.

3. Recherchez hello personnalisé périphérique vous avez créé qui envoie **ExternalTemperature** télémétrie et hello **détails de l’appareil** du panneau, cliquez sur **ajouter une règle**.

4. Sélectionnez **ExternalTemperature** dans **Champ de données**.

5. Définissez **seuil** too56. Cliquez ensuite sur **Enregistrer et afficher les règles**.

6. Retourner l’historique de toohello du tableau de bord tooview hello alarme.

7. Dans la fenêtre de console hello vous reste ouvert, démarrer l’envoi de toobegin d’une application hello Node.js console **ExternalTemperature** les données de télémétrie.

8. Notez que hello **alarme historique** tableau présente les nouvelles alertes lors de la nouvelle règle de hello est déclenchée.
 
## <a name="additional-information"></a>Informations supplémentaires

Opérateur de hello modification  **>**  est plus complexe et dépasse hello les étapes décrites dans ce didacticiel. Tout opérateur vous le souhaitez, vous pouvez modifier toouse de tâche de flux de données Analytique hello, reflétant l’opérateur dans le portail de solution hello est une tâche plus complexe. 

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez vu comment toocreate des règles personnalisées, vous pouvez en savoir plus sur les solutions hello préconfiguré :

- [Solution de Azure IoT Suite l’analyse à distance préconfiguré tooyour application logique de connexion][lnk-logic-app]
- [Solution préconfigurée de métadonnées informations de périphérique dans le contrôle à distance hello][lnk-devinfo].

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md