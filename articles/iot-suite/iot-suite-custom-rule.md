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
# <a name="create-a-custom-rule-in-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="71867-103">Créer une règle personnalisée dans hello solution préconfigurée de surveillance à distance</span><span class="sxs-lookup"><span data-stu-id="71867-103">Create a custom rule in hello remote monitoring preconfigured solution</span></span>

## <a name="introduction"></a><span data-ttu-id="71867-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="71867-104">Introduction</span></span>

<span data-ttu-id="71867-105">Dans les solutions hello préconfiguré, vous pouvez configurer [les règles qui se déclenchent lorsqu’une télémétrie valeur pour un appareil atteint un seuil spécifique][lnk-builtin-rule].</span><span class="sxs-lookup"><span data-stu-id="71867-105">In hello preconfigured solutions, you can configure [rules that trigger when a telemetry value for a device reaches a specific threshold][lnk-builtin-rule].</span></span> <span data-ttu-id="71867-106">[Utiliser la télémétrie dynamique avec hello solution préconfigurée de surveillance à distance] [ lnk-dynamic-telemetry] décrit comment vous pouvez ajouter des valeurs de données de télémétrie personnalisées, telles que *ExternalTemperature* tooyour solution.</span><span class="sxs-lookup"><span data-stu-id="71867-106">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic-telemetry] describes how you can add custom telemetry values, such as *ExternalTemperature* tooyour solution.</span></span> <span data-ttu-id="71867-107">Cet article vous explique comment des types de règle personnalisée de toocreate de télémétrie dynamique dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="71867-107">This article shows you how toocreate custom rule for dynamic telemetry types in your solution.</span></span>

<span data-ttu-id="71867-108">Ce didacticiel utilise un simple Node.js appareil simulé toogenerate télémétrie dynamique toosend toohello solution préconfigurée back-end.</span><span class="sxs-lookup"><span data-stu-id="71867-108">This tutorial uses a simple Node.js simulated device toogenerate dynamic telemetry toosend toohello preconfigured solution back end.</span></span> <span data-ttu-id="71867-109">Puis, vous ajoutez des règles personnalisées Bonjour **RemoteMonitoring** solution Visual Studio et déployer ce tooyour back-end personnalisé abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="71867-109">You then add custom rules in hello **RemoteMonitoring** Visual Studio solution and deploy this customized back end tooyour Azure subscription.</span></span>

<span data-ttu-id="71867-110">toocomplete ce didacticiel, vous devez :</span><span class="sxs-lookup"><span data-stu-id="71867-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="71867-111">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="71867-111">An active Azure subscription.</span></span> <span data-ttu-id="71867-112">Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="71867-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="71867-113">Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="71867-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="71867-114">[Node.js] [ lnk-node] version 0.12.x ou ultérieure toocreate un appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="71867-114">[Node.js][lnk-node] version 0.12.x or later toocreate a simulated device.</span></span>
* <span data-ttu-id="71867-115">Visual Studio 2015 ou Visual Studio 2017 toomodify hello préconfiguré solution précédent se terminer par vos nouvelles règles.</span><span class="sxs-lookup"><span data-stu-id="71867-115">Visual Studio 2015 or Visual Studio 2017 toomodify hello preconfigured solution back end with your new rules.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

<span data-ttu-id="71867-116">Prenez note du nom de la solution hello que vous avez choisie pour votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="71867-116">Make a note of hello solution name you chose for your deployment.</span></span> <span data-ttu-id="71867-117">Vous aurez besoin de ce nom plus tard dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="71867-117">You need this solution name later in this tutorial.</span></span>

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

<span data-ttu-id="71867-118">Vous pouvez arrêter l’application de console hello Node.js lorsque vous avez vérifié qu’il envoie **ExternalTemperature** toohello de télémétrie de solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="71867-118">You can stop hello Node.js console app when you have verified that it is sending **ExternalTemperature** telemetry toohello preconfigured solution.</span></span> <span data-ttu-id="71867-119">Maintenir les fenêtre de console hello étant donné que vous exécutez cette application de console Node.js à nouveau après avoir ajouté des solutions de toohello hello règle personnalisée.</span><span class="sxs-lookup"><span data-stu-id="71867-119">Keep hello console window open because you run this Node.js console app again after you add hello custom rule toohello solution.</span></span>

## <a name="rule-storage-locations"></a><span data-ttu-id="71867-120">Emplacements de stockage des règles</span><span class="sxs-lookup"><span data-stu-id="71867-120">Rule storage locations</span></span>

<span data-ttu-id="71867-121">Les informations sur les règles sont conservées dans deux emplacements :</span><span class="sxs-lookup"><span data-stu-id="71867-121">Information about rules is persisted in two locations:</span></span>

* <span data-ttu-id="71867-122">**DeviceRulesNormalizedTable** – cette table stocke un normalisé référencer toohello les règles définies par le portail de solution hello.</span><span class="sxs-lookup"><span data-stu-id="71867-122">**DeviceRulesNormalizedTable** table – This table stores a normalized reference toohello rules defined by hello solution portal.</span></span> <span data-ttu-id="71867-123">Lorsque le portail de solution hello affiche les règles de l’appareil, il interroge cette table pour les définitions de règles hello.</span><span class="sxs-lookup"><span data-stu-id="71867-123">When hello solution portal displays device rules, it queries this table for hello rule definitions.</span></span>
* <span data-ttu-id="71867-124">**DeviceRules** blob – cet objet blob stocke toutes les règles de hello définies pour toutes les inscrits et sont définies comme une exécution de traitements référence toohello d’entrée Analytique de flux de données Azure.</span><span class="sxs-lookup"><span data-stu-id="71867-124">**DeviceRules** blob – This blob stores all hello rules defined for all registered devices and is defined as a reference input toohello Azure Stream Analytics jobs.</span></span>
 
<span data-ttu-id="71867-125">Lorsque vous mettez à jour une règle existante ou définissez une nouvelle règle dans le portail de solution hello, table de hello et blob sont mises à jour tooreflect hello modifications.</span><span class="sxs-lookup"><span data-stu-id="71867-125">When you update an existing rule or define a new rule in hello solution portal, both hello table and blob are updated tooreflect hello changes.</span></span> <span data-ttu-id="71867-126">règle Hello définition affichée dans le portail de hello provient du magasin de tables hello et règle hello définition référencée par les tâches de flux de données Analytique hello proviennent d’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="71867-126">hello rule definition displayed in hello portal comes from hello table store, and hello rule definition referenced by hello Stream Analytics jobs comes from hello blob.</span></span> 

## <a name="update-hello-remotemonitoring-visual-studio-solution"></a><span data-ttu-id="71867-127">Mettre à jour hello RemoteMonitoring Visual Studio solution</span><span class="sxs-lookup"><span data-stu-id="71867-127">Update hello RemoteMonitoring Visual Studio solution</span></span>

<span data-ttu-id="71867-128">Hello étapes suivantes vous montrent comment toomodify hello tooinclude de solution RemoteMonitoring Visual Studio, une règle qui utilise hello **ExternalTemperature** télémétrie envoyé à partir de l’appareil simulé de hello :</span><span class="sxs-lookup"><span data-stu-id="71867-128">hello following steps show you how toomodify hello RemoteMonitoring Visual Studio solution tooinclude a new rule that uses hello **ExternalTemperature** telemetry sent from hello simulated device:</span></span>

1. <span data-ttu-id="71867-129">Si vous n'avez pas déjà fait, hello du clone **azure-iot-de surveillance à distance** emplacement approprié de référentiel tooa sur votre ordinateur local à l’aide de hello Git commande suivante :</span><span class="sxs-lookup"><span data-stu-id="71867-129">If you have not already done so, clone hello **azure-iot-remote-monitoring** repository tooa suitable location on your local machine using hello following Git command:</span></span>

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. <span data-ttu-id="71867-130">Dans Visual Studio, ouvrez le fichier de RemoteMonitoring.sln de hello à partir de votre copie locale de hello **azure-iot-de surveillance à distance** référentiel.</span><span class="sxs-lookup"><span data-stu-id="71867-130">In Visual Studio, open hello RemoteMonitoring.sln file from your local copy of hello **azure-iot-remote-monitoring** repository.</span></span>

3. <span data-ttu-id="71867-131">Ouvrez le fichier hello Infrastructure\Models\DeviceRuleBlobEntity.cs et ajoutez un **ExternalTemperature** propriété comme suit :</span><span class="sxs-lookup"><span data-stu-id="71867-131">Open hello file Infrastructure\Models\DeviceRuleBlobEntity.cs and add an **ExternalTemperature** property as follows:</span></span>

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. <span data-ttu-id="71867-132">Dans hello du même fichier, ajoutez une **ExternalTemperatureRuleOutput** propriété comme suit :</span><span class="sxs-lookup"><span data-stu-id="71867-132">In hello same file, add an **ExternalTemperatureRuleOutput** property as follows:</span></span>

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. <span data-ttu-id="71867-133">Ouvrez le fichier de hello Infrastructure\Models\DeviceRuleDataFields.cs et ajoutez les éléments suivants de hello **ExternalTemperature** après hello existant **humidité** propriété :</span><span class="sxs-lookup"><span data-stu-id="71867-133">Open hello file Infrastructure\Models\DeviceRuleDataFields.cs and add hello following **ExternalTemperature** property after hello existing **Humidity** property:</span></span>

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. <span data-ttu-id="71867-134">Dans l’hello du même fichier, mettre à jour hello **_availableDataFields** méthode tooinclude **ExternalTemperature** comme suit :</span><span class="sxs-lookup"><span data-stu-id="71867-134">In hello same file, update hello **_availableDataFields** method tooinclude **ExternalTemperature** as follows:</span></span>

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. <span data-ttu-id="71867-135">Ouvrez le fichier hello Infrastructure\Repository\DeviceRulesRepository.cs et modifier hello **BuildBlobEntityListFromTableRows** méthode comme suit :</span><span class="sxs-lookup"><span data-stu-id="71867-135">Open hello file Infrastructure\Repository\DeviceRulesRepository.cs and modify hello **BuildBlobEntityListFromTableRows** method as follows:</span></span>

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

## <a name="rebuild-and-redeploy-hello-solution"></a><span data-ttu-id="71867-136">Régénérer et redéployer les solutions de hello.</span><span class="sxs-lookup"><span data-stu-id="71867-136">Rebuild and redeploy hello solution.</span></span>

<span data-ttu-id="71867-137">Vous pouvez désormais déployer la solution de mise à jour de hello tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="71867-137">You can now deploy hello updated solution tooyour Azure subscription.</span></span>

1. <span data-ttu-id="71867-138">Ouvrez une invite de commandes avec élévation de privilèges et accédez racine toohello de votre copie locale du référentiel de hello azure-iot-de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="71867-138">Open an elevated command prompt and navigate toohello root of your local copy of hello azure-iot-remote-monitoring repository.</span></span>

2. <span data-ttu-id="71867-139">toodeploy votre solution de mise à jour, exécutez hello suivant de commande en remplaçant **{nom du déploiement}** avec nom hello de votre déploiement de solutions préconfigurées que vous avez notée précédemment :</span><span class="sxs-lookup"><span data-stu-id="71867-139">toodeploy your updated solution, run hello following command substituting **{deployment name}** with hello name of your preconfigured solution deployment that you noted previously:</span></span>

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-hello-stream-analytics-job"></a><span data-ttu-id="71867-140">Mettre à jour de la tâche de flux de données Analytique hello</span><span class="sxs-lookup"><span data-stu-id="71867-140">Update hello Stream Analytics job</span></span>

<span data-ttu-id="71867-141">Lorsque le déploiement de hello est terminé, vous pouvez mettre à jour hello flux Analytique toouse hello nouvelle règle définitions des travaux.</span><span class="sxs-lookup"><span data-stu-id="71867-141">When hello deployment is complete, you can update hello Stream Analytics job toouse hello new rule definitions.</span></span>

1. <span data-ttu-id="71867-142">Bonjour portail Azure, accédez à groupe de ressources toohello qui contient des ressources de votre solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="71867-142">In hello Azure portal, navigate toohello resource group that contains your preconfigured solution resources.</span></span> <span data-ttu-id="71867-143">Ce groupe de ressources a hello même nom que vous avez spécifié pour hello solution pendant le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="71867-143">This resource group has hello same name you specified for hello solution during hello deployment.</span></span>

2. <span data-ttu-id="71867-144">Accédez toohello {nom du déploiement}-travail de l’Analytique des flux de règles.</span><span class="sxs-lookup"><span data-stu-id="71867-144">Navigate toohello {deployment name}-Rules Stream Analytics job.</span></span> 

3. <span data-ttu-id="71867-145">Cliquez sur **arrêter** tâche de flux de données Analytique hello toostop de s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="71867-145">Click **Stop** toostop hello Stream Analytics job from running.</span></span> <span data-ttu-id="71867-146">(Vous devez attendre hello toostop de travail de diffusion en continu avant de pouvoir modifier la requête de hello.)</span><span class="sxs-lookup"><span data-stu-id="71867-146">(You must wait for hello streaming job toostop before you can edit hello query).</span></span>

4. <span data-ttu-id="71867-147">Cliquez sur **Requête**.</span><span class="sxs-lookup"><span data-stu-id="71867-147">Click **Query**.</span></span> <span data-ttu-id="71867-148">Modifier hello de hello requête tooinclude **sélectionnez** instruction pour **ExternalTemperature**.</span><span class="sxs-lookup"><span data-stu-id="71867-148">Edit hello query tooinclude hello **SELECT** statement for **ExternalTemperature**.</span></span> <span data-ttu-id="71867-149">Hello exemple suivant montre hello complet de la requête avec hello nouveau **sélectionnez** instruction :</span><span class="sxs-lookup"><span data-stu-id="71867-149">hello following sample shows hello complete query with hello new **SELECT** statement:</span></span>

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

5. <span data-ttu-id="71867-150">Cliquez sur **enregistrer** toochange hello mis à jour la requête de la règle.</span><span class="sxs-lookup"><span data-stu-id="71867-150">Click **Save** toochange hello updated rule query.</span></span>

6. <span data-ttu-id="71867-151">Cliquez sur **Démarrer** tâche de flux de données Analytique hello toostart à nouveau d’exécuter.</span><span class="sxs-lookup"><span data-stu-id="71867-151">Click **Start** toostart hello Stream Analytics job running again.</span></span>

## <a name="add-your-new-rule-in-hello-dashboard"></a><span data-ttu-id="71867-152">Ajouter votre nouvelle règle dans le tableau de bord hello</span><span class="sxs-lookup"><span data-stu-id="71867-152">Add your new rule in hello dashboard</span></span>

<span data-ttu-id="71867-153">Vous pouvez maintenant ajouter hello **ExternalTemperature** périphérique tooa de règle dans le tableau de bord de solution hello.</span><span class="sxs-lookup"><span data-stu-id="71867-153">You can now add hello **ExternalTemperature** rule tooa device in hello solution dashboard.</span></span>

1. <span data-ttu-id="71867-154">Accédez portal de solution toohello.</span><span class="sxs-lookup"><span data-stu-id="71867-154">Navigate toohello solution portal.</span></span>

2. <span data-ttu-id="71867-155">Accédez toohello **périphériques** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="71867-155">Navigate toohello **Devices** panel.</span></span>

3. <span data-ttu-id="71867-156">Recherchez hello personnalisé périphérique vous avez créé qui envoie **ExternalTemperature** télémétrie et hello **détails de l’appareil** du panneau, cliquez sur **ajouter une règle**.</span><span class="sxs-lookup"><span data-stu-id="71867-156">Locate hello custom device you created that sends **ExternalTemperature** telemetry and on hello **Device Details** panel, click **Add Rule**.</span></span>

4. <span data-ttu-id="71867-157">Sélectionnez **ExternalTemperature** dans **Champ de données**.</span><span class="sxs-lookup"><span data-stu-id="71867-157">Select **ExternalTemperature** in **Data Field**.</span></span>

5. <span data-ttu-id="71867-158">Définissez **seuil** too56.</span><span class="sxs-lookup"><span data-stu-id="71867-158">Set **Threshold** too56.</span></span> <span data-ttu-id="71867-159">Cliquez ensuite sur **Enregistrer et afficher les règles**.</span><span class="sxs-lookup"><span data-stu-id="71867-159">Then click **Save and view rules**.</span></span>

6. <span data-ttu-id="71867-160">Retourner l’historique de toohello du tableau de bord tooview hello alarme.</span><span class="sxs-lookup"><span data-stu-id="71867-160">Return toohello dashboard tooview hello alarm history.</span></span>

7. <span data-ttu-id="71867-161">Dans la fenêtre de console hello vous reste ouvert, démarrer l’envoi de toobegin d’une application hello Node.js console **ExternalTemperature** les données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="71867-161">In hello console window you left open, start hello Node.js console app toobegin sending **ExternalTemperature** telemetry data.</span></span>

8. <span data-ttu-id="71867-162">Notez que hello **alarme historique** tableau présente les nouvelles alertes lors de la nouvelle règle de hello est déclenchée.</span><span class="sxs-lookup"><span data-stu-id="71867-162">Notice that hello **Alarm History** table shows new alarms when hello new rule is triggered.</span></span>
 
## <a name="additional-information"></a><span data-ttu-id="71867-163">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="71867-163">Additional information</span></span>

<span data-ttu-id="71867-164">Opérateur de hello modification  **>**  est plus complexe et dépasse hello les étapes décrites dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="71867-164">Changing hello operator **>** is more complex and goes beyond hello steps outlined in this tutorial.</span></span> <span data-ttu-id="71867-165">Tout opérateur vous le souhaitez, vous pouvez modifier toouse de tâche de flux de données Analytique hello, reflétant l’opérateur dans le portail de solution hello est une tâche plus complexe.</span><span class="sxs-lookup"><span data-stu-id="71867-165">While you can change hello Stream Analytics job toouse whatever operator you like, reflecting that operator in hello solution portal is a more complex task.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="71867-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="71867-166">Next steps</span></span>
<span data-ttu-id="71867-167">Maintenant que vous avez vu comment toocreate des règles personnalisées, vous pouvez en savoir plus sur les solutions hello préconfiguré :</span><span class="sxs-lookup"><span data-stu-id="71867-167">Now that you've seen how toocreate custom rules, you can learn more about hello preconfigured solutions:</span></span>

- <span data-ttu-id="71867-168">[Solution de Azure IoT Suite l’analyse à distance préconfiguré tooyour application logique de connexion][lnk-logic-app]</span><span class="sxs-lookup"><span data-stu-id="71867-168">[Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logic-app]</span></span>
- <span data-ttu-id="71867-169">[Solution préconfigurée de métadonnées informations de périphérique dans le contrôle à distance hello][lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="71867-169">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md