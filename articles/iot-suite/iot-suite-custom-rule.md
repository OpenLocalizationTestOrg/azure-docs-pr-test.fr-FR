---
title: "Création d’une règle personnalisée dans Azure IoT Suite | Microsoft Docs"
description: "Comment créer une règle personnalisée dans une solution IoT Suite préconfigurée."
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
ms.openlocfilehash: d58c27234ea05a82aaa3e8d72f70c1449980df09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-custom-rule-in-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="76f8c-103">Création d’une règle personnalisée dans la solution de surveillance à distance préconfigurée</span><span class="sxs-lookup"><span data-stu-id="76f8c-103">Create a custom rule in the remote monitoring preconfigured solution</span></span>

## <a name="introduction"></a><span data-ttu-id="76f8c-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="76f8c-104">Introduction</span></span>

<span data-ttu-id="76f8c-105">Dans les solutions préconfigurées, vous pouvez configurer [des règles qui se déclenchent lorsqu’une valeur de télémétrie d’un périphérique atteint un seuil spécifique][lnk-builtin-rule].</span><span class="sxs-lookup"><span data-stu-id="76f8c-105">In the preconfigured solutions, you can configure [rules that trigger when a telemetry value for a device reaches a specific threshold][lnk-builtin-rule].</span></span> <span data-ttu-id="76f8c-106">La page [Utilisation de la télémétrie dynamique avec la solution préconfigurée de surveillance à distance][lnk-dynamic-telemetry] vous explique comment ajouter des valeurs de télémétrie personnalisées, telles que *ExternalTemperature*, à votre solution.</span><span class="sxs-lookup"><span data-stu-id="76f8c-106">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic-telemetry] describes how you can add custom telemetry values, such as *ExternalTemperature* to your solution.</span></span> <span data-ttu-id="76f8c-107">Cet article vous montre comment créer une règle personnalisée pour les types de télémétrie dynamiques dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="76f8c-107">This article shows you how to create custom rule for dynamic telemetry types in your solution.</span></span>

<span data-ttu-id="76f8c-108">Ce didacticiel utilise un appareil simulé Node.js simple pour générer la télémétrie dynamique à envoyer vers le serveur principal de la solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="76f8c-108">This tutorial uses a simple Node.js simulated device to generate dynamic telemetry to send to the preconfigured solution back end.</span></span> <span data-ttu-id="76f8c-109">Vous ajoutez ensuite des règles personnalisées dans la solution Visual Studio **RemoteMonitoring** et déployez ce serveur principal personnalisé sur votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="76f8c-109">You then add custom rules in the **RemoteMonitoring** Visual Studio solution and deploy this customized back end to your Azure subscription.</span></span>

<span data-ttu-id="76f8c-110">Pour suivre ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="76f8c-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="76f8c-111">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="76f8c-111">An active Azure subscription.</span></span> <span data-ttu-id="76f8c-112">Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="76f8c-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="76f8c-113">Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="76f8c-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="76f8c-114">[Node.js][lnk-node] version 0.12.x ou ultérieure pour créer un appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="76f8c-114">[Node.js][lnk-node] version 0.12.x or later to create a simulated device.</span></span>
* <span data-ttu-id="76f8c-115">Visual Studio 2015 ou Visual Studio 2017 pour modifier le serveur principal de la solution préconfigurée avec vos nouvelles règles.</span><span class="sxs-lookup"><span data-stu-id="76f8c-115">Visual Studio 2015 or Visual Studio 2017 to modify the preconfigured solution back end with your new rules.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

<span data-ttu-id="76f8c-116">Notez le nom de solution que vous avez choisi pour votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="76f8c-116">Make a note of the solution name you chose for your deployment.</span></span> <span data-ttu-id="76f8c-117">Vous aurez besoin de ce nom plus tard dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="76f8c-117">You need this solution name later in this tutorial.</span></span>

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

<span data-ttu-id="76f8c-118">Vous pouvez arrêter l’application de console Node.js lorsque vous avez vérifié qu’il envoie la télémétrie **ExternalTemperature** à la solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="76f8c-118">You can stop the Node.js console app when you have verified that it is sending **ExternalTemperature** telemetry to the preconfigured solution.</span></span> <span data-ttu-id="76f8c-119">Gardez la fenêtre de console ouverte car vous exécuterez à nouveau cette application de console Node.js après avoir ajouté la règle personnalisée à la solution.</span><span class="sxs-lookup"><span data-stu-id="76f8c-119">Keep the console window open because you run this Node.js console app again after you add the custom rule to the solution.</span></span>

## <a name="rule-storage-locations"></a><span data-ttu-id="76f8c-120">Emplacements de stockage des règles</span><span class="sxs-lookup"><span data-stu-id="76f8c-120">Rule storage locations</span></span>

<span data-ttu-id="76f8c-121">Les informations sur les règles sont conservées dans deux emplacements :</span><span class="sxs-lookup"><span data-stu-id="76f8c-121">Information about rules is persisted in two locations:</span></span>

* <span data-ttu-id="76f8c-122">Table **DeviceRulesNormalizedTable** : cette table stocke une référence normalisée aux règles définies par le portail de la solution.</span><span class="sxs-lookup"><span data-stu-id="76f8c-122">**DeviceRulesNormalizedTable** table – This table stores a normalized reference to the rules defined by the solution portal.</span></span> <span data-ttu-id="76f8c-123">Lorsque le portail de la solution affiche les règles des appareils, il interroge cette table sur les définitions de règles.</span><span class="sxs-lookup"><span data-stu-id="76f8c-123">When the solution portal displays device rules, it queries this table for the rule definitions.</span></span>
* <span data-ttu-id="76f8c-124">Objet blob **DeviceRules** : cet objet blob stocke toutes les règles définies pour tous les appareils inscrits et est défini comme une entrée de référence pour les travaux Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="76f8c-124">**DeviceRules** blob – This blob stores all the rules defined for all registered devices and is defined as a reference input to the Azure Stream Analytics jobs.</span></span>
 
<span data-ttu-id="76f8c-125">Lorsque vous mettez à jour une règle existante ou définissez une nouvelle règle dans le portail de la solution, la table et l’objet blob sont mis à jour pour refléter les modifications.</span><span class="sxs-lookup"><span data-stu-id="76f8c-125">When you update an existing rule or define a new rule in the solution portal, both the table and blob are updated to reflect the changes.</span></span> <span data-ttu-id="76f8c-126">La définition des règles affichée dans le portail provient du magasin de tables et la définition des règles référencée par les travaux Stream Analytics provient de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="76f8c-126">The rule definition displayed in the portal comes from the table store, and the rule definition referenced by the Stream Analytics jobs comes from the blob.</span></span> 

## <a name="update-the-remotemonitoring-visual-studio-solution"></a><span data-ttu-id="76f8c-127">Mise à jour de la solution Visual Studio RemoteMonitoring</span><span class="sxs-lookup"><span data-stu-id="76f8c-127">Update the RemoteMonitoring Visual Studio solution</span></span>

<span data-ttu-id="76f8c-128">Les étapes suivantes vous montrent comment modifier la solution Visual Studio RemoteMonitoring pour inclure une nouvelle règle qui utilise la télémétrie **ExternalTemperature** envoyée depuis l’appareil simulé :</span><span class="sxs-lookup"><span data-stu-id="76f8c-128">The following steps show you how to modify the RemoteMonitoring Visual Studio solution to include a new rule that uses the **ExternalTemperature** telemetry sent from the simulated device:</span></span>

1. <span data-ttu-id="76f8c-129">Si vous ne l'avez pas déjà fait, clonez le référentiel **azure-iot-remote-monitoring** dans un emplacement approprié sur votre ordinateur local à l’aide de la commande Git suivante :</span><span class="sxs-lookup"><span data-stu-id="76f8c-129">If you have not already done so, clone the **azure-iot-remote-monitoring** repository to a suitable location on your local machine using the following Git command:</span></span>

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. <span data-ttu-id="76f8c-130">Dans Visual Studio, ouvrez le fichier RemoteMonitoring.sln à partir de votre copie locale du référentiel **azure-iot-remote-monitoring**.</span><span class="sxs-lookup"><span data-stu-id="76f8c-130">In Visual Studio, open the RemoteMonitoring.sln file from your local copy of the **azure-iot-remote-monitoring** repository.</span></span>

3. <span data-ttu-id="76f8c-131">Ouvrez le fichier Infrastructure\Models\DeviceRuleBlobEntity.cs et ajoutez une propriété **ExternalTemperature** comme suit :</span><span class="sxs-lookup"><span data-stu-id="76f8c-131">Open the file Infrastructure\Models\DeviceRuleBlobEntity.cs and add an **ExternalTemperature** property as follows:</span></span>

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. <span data-ttu-id="76f8c-132">Dans le même fichier, ajoutez une propriété **ExternalTemperatureRuleOutput** comme suit :</span><span class="sxs-lookup"><span data-stu-id="76f8c-132">In the same file, add an **ExternalTemperatureRuleOutput** property as follows:</span></span>

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. <span data-ttu-id="76f8c-133">Ouvrez le fichier Infrastructure\Models\DeviceRuleDataFields.cs et ajoutez la propriété **ExternalTemperature** suivante après la propriété **Humidity** existante :</span><span class="sxs-lookup"><span data-stu-id="76f8c-133">Open the file Infrastructure\Models\DeviceRuleDataFields.cs and add the following **ExternalTemperature** property after the existing **Humidity** property:</span></span>

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. <span data-ttu-id="76f8c-134">Dans le même fichier, mettez à jour la méthode **_availableDataFields** pour inclure **ExternalTemperature** comme suit :</span><span class="sxs-lookup"><span data-stu-id="76f8c-134">In the same file, update the **_availableDataFields** method to include **ExternalTemperature** as follows:</span></span>

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. <span data-ttu-id="76f8c-135">Ouvrez le fichier Infrastructure\Repository\DeviceRulesRepository.cs et modifiez la méthode **BuildBlobEntityListFromTableRows** comme suit :</span><span class="sxs-lookup"><span data-stu-id="76f8c-135">Open the file Infrastructure\Repository\DeviceRulesRepository.cs and modify the **BuildBlobEntityListFromTableRows** method as follows:</span></span>

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

## <a name="rebuild-and-redeploy-the-solution"></a><span data-ttu-id="76f8c-136">Procédez maintenant à la régénération et au redéploiement de la solution.</span><span class="sxs-lookup"><span data-stu-id="76f8c-136">Rebuild and redeploy the solution.</span></span>

<span data-ttu-id="76f8c-137">Vous pouvez maintenant déployer la solution mise à jour sur votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="76f8c-137">You can now deploy the updated solution to your Azure subscription.</span></span>

1. <span data-ttu-id="76f8c-138">Ouvrez une invite de commandes avec élévation de privilèges et accédez à la racine de votre copie locale du référentiel azure-iot-remote-monitoring.</span><span class="sxs-lookup"><span data-stu-id="76f8c-138">Open an elevated command prompt and navigate to the root of your local copy of the azure-iot-remote-monitoring repository.</span></span>

2. <span data-ttu-id="76f8c-139">Pour déployer votre solution mise à jour, exécutez la commande suivante en remplaçant **{deployment name}** par le nom du déploiement de votre solution préconfigurée que vous avez noté précédemment :</span><span class="sxs-lookup"><span data-stu-id="76f8c-139">To deploy your updated solution, run the following command substituting **{deployment name}** with the name of your preconfigured solution deployment that you noted previously:</span></span>

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-the-stream-analytics-job"></a><span data-ttu-id="76f8c-140">Mise à jour du travail Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="76f8c-140">Update the Stream Analytics job</span></span>

<span data-ttu-id="76f8c-141">Lorsque le déploiement est terminé, vous pouvez mettre à jour le travail Stream Analytics pour utiliser les nouvelles définitions de règles.</span><span class="sxs-lookup"><span data-stu-id="76f8c-141">When the deployment is complete, you can update the Stream Analytics job to use the new rule definitions.</span></span>

1. <span data-ttu-id="76f8c-142">Dans le portail Azure, accédez au groupe de ressources contenant les ressources de votre solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="76f8c-142">In the Azure portal, navigate to the resource group that contains your preconfigured solution resources.</span></span> <span data-ttu-id="76f8c-143">Ce groupe de ressources possède le même nom que vous avez spécifié pour la solution lors du déploiement.</span><span class="sxs-lookup"><span data-stu-id="76f8c-143">This resource group has the same name you specified for the solution during the deployment.</span></span>

2. <span data-ttu-id="76f8c-144">Accédez au travail Stream Analytics {deployment name}-Rules.</span><span class="sxs-lookup"><span data-stu-id="76f8c-144">Navigate to the {deployment name}-Rules Stream Analytics job.</span></span> 

3. <span data-ttu-id="76f8c-145">Cliquez sur **Arrêter** pour arrêter l’exécution du travail Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="76f8c-145">Click **Stop** to stop the Stream Analytics job from running.</span></span> <span data-ttu-id="76f8c-146">(Vous devez attendre l’arrêt du travail de diffusion avant de pouvoir modifier la requête).</span><span class="sxs-lookup"><span data-stu-id="76f8c-146">(You must wait for the streaming job to stop before you can edit the query).</span></span>

4. <span data-ttu-id="76f8c-147">Cliquez sur **Requête**.</span><span class="sxs-lookup"><span data-stu-id="76f8c-147">Click **Query**.</span></span> <span data-ttu-id="76f8c-148">Modifiez la requête afin d’inclure l’instruction **SELECT** pour **ExternalTemperature**.</span><span class="sxs-lookup"><span data-stu-id="76f8c-148">Edit the query to include the **SELECT** statement for **ExternalTemperature**.</span></span> <span data-ttu-id="76f8c-149">L’exemple suivant montre la requête complète avec la nouvelle instruction **SELECT** :</span><span class="sxs-lookup"><span data-stu-id="76f8c-149">The following sample shows the complete query with the new **SELECT** statement:</span></span>

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

5. <span data-ttu-id="76f8c-150">Cliquez sur **Enregistrer** pour modifier la requête de la règle mise à jour.</span><span class="sxs-lookup"><span data-stu-id="76f8c-150">Click **Save** to change the updated rule query.</span></span>

6. <span data-ttu-id="76f8c-151">Cliquez sur **Démarrer** pour redémarrer le travail Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="76f8c-151">Click **Start** to start the Stream Analytics job running again.</span></span>

## <a name="add-your-new-rule-in-the-dashboard"></a><span data-ttu-id="76f8c-152">Ajout de votre nouvelle règle dans le tableau de bord</span><span class="sxs-lookup"><span data-stu-id="76f8c-152">Add your new rule in the dashboard</span></span>

<span data-ttu-id="76f8c-153">Vous pouvez maintenant ajouter la règle **ExternalTemperature** à un appareil dans le tableau de bord de la solution.</span><span class="sxs-lookup"><span data-stu-id="76f8c-153">You can now add the **ExternalTemperature** rule to a device in the solution dashboard.</span></span>

1. <span data-ttu-id="76f8c-154">Accédez au portail de la solution.</span><span class="sxs-lookup"><span data-stu-id="76f8c-154">Navigate to the solution portal.</span></span>

2. <span data-ttu-id="76f8c-155">Accédez au volet **Appareils**.</span><span class="sxs-lookup"><span data-stu-id="76f8c-155">Navigate to the **Devices** panel.</span></span>

3. <span data-ttu-id="76f8c-156">Recherchez l’appareil personnalisé que vous avez créé qui envoie la télémétrie **ExternalTemperature**, et dans le volet **Informations sur l’appareil**, cliquez sur **Ajouter une règle**.</span><span class="sxs-lookup"><span data-stu-id="76f8c-156">Locate the custom device you created that sends **ExternalTemperature** telemetry and on the **Device Details** panel, click **Add Rule**.</span></span>

4. <span data-ttu-id="76f8c-157">Sélectionnez **ExternalTemperature** dans **Champ de données**.</span><span class="sxs-lookup"><span data-stu-id="76f8c-157">Select **ExternalTemperature** in **Data Field**.</span></span>

5. <span data-ttu-id="76f8c-158">Définissez le **Seuil** sur 56.</span><span class="sxs-lookup"><span data-stu-id="76f8c-158">Set **Threshold** to 56.</span></span> <span data-ttu-id="76f8c-159">Cliquez ensuite sur **Enregistrer et afficher les règles**.</span><span class="sxs-lookup"><span data-stu-id="76f8c-159">Then click **Save and view rules**.</span></span>

6. <span data-ttu-id="76f8c-160">Retournez au tableau de bord pour afficher l’historique des alertes.</span><span class="sxs-lookup"><span data-stu-id="76f8c-160">Return to the dashboard to view the alarm history.</span></span>

7. <span data-ttu-id="76f8c-161">Dans la fenêtre de console que vous avez laissée ouverte, démarrez l’application de console Node.js pour commencer l’envoi des données de télémétrie **ExternalTemperature**.</span><span class="sxs-lookup"><span data-stu-id="76f8c-161">In the console window you left open, start the Node.js console app to begin sending **ExternalTemperature** telemetry data.</span></span>

8. <span data-ttu-id="76f8c-162">Notez que la table **Historique des alertes** affiche les nouvelles alertes lorsque la nouvelle règle est déclenchée.</span><span class="sxs-lookup"><span data-stu-id="76f8c-162">Notice that the **Alarm History** table shows new alarms when the new rule is triggered.</span></span>
 
## <a name="additional-information"></a><span data-ttu-id="76f8c-163">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="76f8c-163">Additional information</span></span>

<span data-ttu-id="76f8c-164">La modification de l’opérateur **>** est plus complexe et dépasse le cadre de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="76f8c-164">Changing the operator **>** is more complex and goes beyond the steps outlined in this tutorial.</span></span> <span data-ttu-id="76f8c-165">Alors que vous pouvez modifier le travail Stream Analytics pour utiliser l’opérateur souhaité, l’action de refléter cet opérateur dans le portail de la solution représente une tâche plus complexe.</span><span class="sxs-lookup"><span data-stu-id="76f8c-165">While you can change the Stream Analytics job to use whatever operator you like, reflecting that operator in the solution portal is a more complex task.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="76f8c-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="76f8c-166">Next steps</span></span>
<span data-ttu-id="76f8c-167">Maintenant que vous avez vu comment créer des règles personnalisées, vous pouvez en apprendre plus sur les solutions préconfigurées :</span><span class="sxs-lookup"><span data-stu-id="76f8c-167">Now that you've seen how to create custom rules, you can learn more about the preconfigured solutions:</span></span>

- <span data-ttu-id="76f8c-168">[Connecter Logic App à la solution préconfigurée de surveillance à distance Azure IoT Suite][lnk-logic-app]</span><span class="sxs-lookup"><span data-stu-id="76f8c-168">[Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logic-app]</span></span>
- <span data-ttu-id="76f8c-169">[Métadonnées relatives aux informations d’appareil dans la solution préconfigurée de surveillance à distance][lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="76f8c-169">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md