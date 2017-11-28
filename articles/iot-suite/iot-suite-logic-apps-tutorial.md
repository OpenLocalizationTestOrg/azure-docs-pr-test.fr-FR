---
title: aaaAzure IoT Suite et Logic Apps | Documents Microsoft
description: "Un didacticiel sur la façon de toohook des Logic Apps tooAzure IoT Suite pour les processus d’entreprise."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4629a7af-56ca-4b21-a769-5fa18bc3ab07
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: corywink
ms.openlocfilehash: 6ef7311ac38f4e2ddb032cff0fb73591da5f76c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-connect-logic-app-tooyour-azure-iot-suite-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="f0604-103">Didacticiel : Connecter des solutions d’Azure IoT Suite l’analyse à distance préconfiguré tooyour application logique</span><span class="sxs-lookup"><span data-stu-id="f0604-103">Tutorial: Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution</span></span>
<span data-ttu-id="f0604-104">Hello [Microsoft Azure IoT Suite] [ lnk-internetofthings] solutions préconfigurées de surveillance à distance est un excellent moyen tooget démarré rapidement avec un ensemble de fonctionnalités de bout en bout qui illustre une solution IoT.</span><span class="sxs-lookup"><span data-stu-id="f0604-104">hello [Microsoft Azure IoT Suite][lnk-internetofthings] remote monitoring preconfigured solution is a great way tooget started quickly with an end-to-end feature set that exemplifies an IoT solution.</span></span> <span data-ttu-id="f0604-105">Ce didacticiel vous guide tout au long de la surveillance à distance de tooadd application logique tooyour Microsoft Azure IoT Suite des solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="f0604-105">This tutorial walks you through how tooadd Logic App tooyour Microsoft Azure IoT Suite remote monitoring preconfigured solution.</span></span> <span data-ttu-id="f0604-106">Ces étapes montrent comment prendre votre solution IoT encore davantage en la connectant tooa processus d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="f0604-106">These steps demonstrate how you can take your IoT solution even further by connecting it tooa business process.</span></span>

<span data-ttu-id="f0604-107">*Si vous avez besoin d’une procédure pas à pas sur la solution préconfigurée tooprovision une surveillance à distance, consultez [didacticiel : prise en main des solutions IoT préconfiguré hello][lnk-getstarted].*</span><span class="sxs-lookup"><span data-stu-id="f0604-107">*If you’re looking for a walkthrough on how tooprovision a remote monitoring preconfigured solution, see [Tutorial: Get started with hello IoT preconfigured solutions][lnk-getstarted].*</span></span>

<span data-ttu-id="f0604-108">Avant de commencer ce didacticiel, vous devez :</span><span class="sxs-lookup"><span data-stu-id="f0604-108">Before you start this tutorial, you should:</span></span>

* <span data-ttu-id="f0604-109">Configurer l’analyse à distance hello préconfiguré solution dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f0604-109">Provision hello remote monitoring preconfigured solution in your Azure subscription.</span></span>
* <span data-ttu-id="f0604-110">Créer un tooenable de compte SendGrid toosend un message électronique qui déclenche votre processus d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="f0604-110">Create a SendGrid account tooenable you toosend an email that triggers your business process.</span></span> <span data-ttu-id="f0604-111">Vous pouvez vous inscrire à un compte d’évaluation gratuit sur [SendGrid](https://sendgrid.com/) en cliquant sur **Essai gratuit**.</span><span class="sxs-lookup"><span data-stu-id="f0604-111">You can sign up for a free trial account at [SendGrid](https://sendgrid.com/) by clicking **Try for Free**.</span></span> <span data-ttu-id="f0604-112">Une fois que vous êtes inscrit pour votre compte d’évaluation gratuite, vous devez toocreate une [clé API](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) dans SendGrid qui accorde des autorisations toosend mail.</span><span class="sxs-lookup"><span data-stu-id="f0604-112">After you have registered for your free trial account, you need toocreate an [API key](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid that grants permissions toosend mail.</span></span> <span data-ttu-id="f0604-113">Vous avez besoin de cette clé API plus loin dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="f0604-113">You need this API key later in hello tutorial.</span></span>

<span data-ttu-id="f0604-114">toocomplete ce didacticiel, vous avez besoin de Visual Studio 2015 ou Visual Studio 2017 toomodify hello actions hello solution préconfigurée back-end.</span><span class="sxs-lookup"><span data-stu-id="f0604-114">toocomplete this tutorial, you need Visual Studio 2015 or Visual Studio 2017 toomodify hello actions in hello preconfigured solution back end.</span></span>

<span data-ttu-id="f0604-115">En supposant, vous avez déjà configuré votre contrôle à distance de la solution préconfigurée, accédez toohello groupe de ressources pour cette solution Bonjour [portail Azure][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="f0604-115">Assuming you’ve already provisioned your remote monitoring preconfigured solution, navigate toohello resource group for that solution in hello [Azure portal][lnk-azureportal].</span></span> <span data-ttu-id="f0604-116">groupe de ressources Hello a hello même nom que celui que hello solution nom que vous avez choisi lorsque vous avez configuré votre solution d’analyse à distance.</span><span class="sxs-lookup"><span data-stu-id="f0604-116">hello resource group has hello same name as hello solution name you chose when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="f0604-117">Dans le groupe de ressources hello, vous pouvez voir hello tous mis en service des ressources Azure pour votre solution à l’exception de hello application Azure Active Directory que vous pouvez trouver Bonjour portail classique Azure.</span><span class="sxs-lookup"><span data-stu-id="f0604-117">In hello resource group, you can see all hello provisioned Azure resources for your solution except for hello Azure Active Directory application that you can find in hello Azure Classic Portal.</span></span> <span data-ttu-id="f0604-118">Hello capture d’écran suivante montre un exemple **groupe de ressources** solution préconfigurée de panneau pour une surveillance à distance :</span><span class="sxs-lookup"><span data-stu-id="f0604-118">hello following screenshot shows an example **Resource group** blade for a remote monitoring preconfigured solution:</span></span>

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

<span data-ttu-id="f0604-119">toobegin, configuration hello logique application toouse avec hello la solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="f0604-119">toobegin, set up hello logic app toouse with hello preconfigured solution.</span></span>

## <a name="set-up-hello-logic-app"></a><span data-ttu-id="f0604-120">Configurer hello logique d’application</span><span class="sxs-lookup"><span data-stu-id="f0604-120">Set up hello Logic App</span></span>
1. <span data-ttu-id="f0604-121">Cliquez sur **ajouter** haut hello du panneau des ressources de votre groupe Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f0604-121">Click **Add** at hello top of your resource group blade in hello Azure portal.</span></span>
2. <span data-ttu-id="f0604-122">Recherchez **l’application logique**, sélectionnez-la, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f0604-122">Search for **Logic App**, select it and then click **Create**.</span></span>
3. <span data-ttu-id="f0604-123">Remplir hello **nom** et utilisez hello même **abonnement** et **groupe de ressources** que vous avez utilisé lors de la configuration de votre solution d’analyse à distance.</span><span class="sxs-lookup"><span data-stu-id="f0604-123">Fill out hello **Name** and use hello same **Subscription** and **Resource group** that you used when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="f0604-124">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f0604-124">Click **Create**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. <span data-ttu-id="f0604-125">Lorsque votre déploiement est terminé, vous pouvez voir hello Qu'application logique est répertoriée en tant que ressource dans votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f0604-125">When your deployment completes, you can see hello Logic App is listed as a resource in your resource group.</span></span>
5. <span data-ttu-id="f0604-126">Cliquez sur le panneau des applications logiques hello application logique toonavigate toohello, sélectionnez hello **application logique vide** hello tooopen de modèle **Concepteur d’applications logique**.</span><span class="sxs-lookup"><span data-stu-id="f0604-126">Click hello Logic App toonavigate toohello Logic App blade, select hello **Blank Logic App** template tooopen hello **Logic Apps Designer**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. <span data-ttu-id="f0604-127">Sélectionnez **Requête**.</span><span class="sxs-lookup"><span data-stu-id="f0604-127">Select **Request**.</span></span> <span data-ttu-id="f0604-128">Cette action indique qu’une demande HTTP entrante avec une charge utile au format JSON spécifique agit comme un déclencheur.</span><span class="sxs-lookup"><span data-stu-id="f0604-128">This action specifies that an incoming HTTP request with a specific JSON formatted payload acts as a trigger.</span></span>
7. <span data-ttu-id="f0604-129">Collez hello après le code dans hello schéma de JSON de corps de la requête :</span><span class="sxs-lookup"><span data-stu-id="f0604-129">Paste hello following code into hello Request Body JSON Schema:</span></span>
   
    ```json
    {
      "$schema": "http://json-schema.org/draft-04/schema#",
      "id": "/",
      "properties": {
        "DeviceId": {
          "id": "DeviceId",
          "type": "string"
        },
        "measuredValue": {
          "id": "measuredValue",
          "type": "integer"
        },
        "measurementName": {
          "id": "measurementName",
          "type": "string"
        }
      },
      "required": [
        "DeviceId",
        "measurementName",
        "measuredValue"
      ],
      "type": "object"
    }
    ```
   
   > [!NOTE]
   > <span data-ttu-id="f0604-130">Vous pouvez copier des URL hello pour valider de hello HTTP une fois que vous avez enregistré hello logique application, mais vous devez d’abord ajouter une action.</span><span class="sxs-lookup"><span data-stu-id="f0604-130">You can copy hello URL for hello HTTP post after you save hello logic app, but first you must add an action.</span></span>
   > 
   > 
8. <span data-ttu-id="f0604-131">Cliquez sur **+ Nouvelle étape** sous votre déclencheur manuel.</span><span class="sxs-lookup"><span data-stu-id="f0604-131">Click **+ New step** under your manual trigger.</span></span> <span data-ttu-id="f0604-132">Cliquez ensuite sur **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="f0604-132">Then click **Add an action**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. <span data-ttu-id="f0604-133">Recherchez **SendGrid - Send email** (SendGrid - Envoyer un e-mail) et cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="f0604-133">Search for **SendGrid - Send email** and click it.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. <span data-ttu-id="f0604-134">Entrez un nom pour la connexion de hello, tel que **SendGridConnection**, entrez hello **clé d’API SendGrid** vous avez créé lorsque vous configurez votre compte SendGrid, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="f0604-134">Enter a name for hello connection, such as **SendGridConnection**, enter hello **SendGrid API Key** you created when you set up your SendGrid account, and click **Create**.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. <span data-ttu-id="f0604-135">Ajouter des adresses de messagerie vous tooboth propre hello **de** et **à** champs.</span><span class="sxs-lookup"><span data-stu-id="f0604-135">Add email addresses you own tooboth hello **From** and **To** fields.</span></span> <span data-ttu-id="f0604-136">Ajouter **alerte de surveillance à distance [DeviceId]** toohello **sujet** champ.</span><span class="sxs-lookup"><span data-stu-id="f0604-136">Add **Remote monitoring alert [DeviceId]** toohello **Subject** field.</span></span> <span data-ttu-id="f0604-137">Bonjour **corps du message électronique** champ, ajoutez **[DeviceId] a signalé [measurementName] avec la valeur [measuredValue].**</span><span class="sxs-lookup"><span data-stu-id="f0604-137">In hello **Email Body** field, add **Device [DeviceId] has reported [measurementName] with value [measuredValue].**</span></span> <span data-ttu-id="f0604-138">Vous pouvez ajouter **[DeviceId]**, **[measurementName]**, et **[measuredValue]** en cliquant sur Bonjour **vous pouvez insérer des données à partir des précédentes étapes**section.</span><span class="sxs-lookup"><span data-stu-id="f0604-138">You can add **[DeviceId]**, **[measurementName]**, and **[measuredValue]** by clicking in hello **You can insert data from previous steps** section.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. <span data-ttu-id="f0604-139">Cliquez sur **enregistrer** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="f0604-139">Click **Save** in hello top menu.</span></span>
13. <span data-ttu-id="f0604-140">Cliquez sur hello **demande** déclencheur et copie hello **Http Post toothis URL** valeur.</span><span class="sxs-lookup"><span data-stu-id="f0604-140">Click hello **Request** trigger and copy hello **Http Post toothis URL** value.</span></span> <span data-ttu-id="f0604-141">Vous aurez besoin de cette URL plus tard dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f0604-141">You need this URL later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="f0604-142">Logic Apps permettent de toorun [différents types d’action] [ lnk-logic-apps-actions] notamment des actions dans Office 365.</span><span class="sxs-lookup"><span data-stu-id="f0604-142">Logic Apps enable you toorun [many different types of action][lnk-logic-apps-actions] including actions in Office 365.</span></span> 
> 
> 

## <a name="set-up-hello-eventprocessor-web-job"></a><span data-ttu-id="f0604-143">Configurer hello EventProcessor de tâche Web</span><span class="sxs-lookup"><span data-stu-id="f0604-143">Set up hello EventProcessor Web Job</span></span>
<span data-ttu-id="f0604-144">Dans cette section, vous vous connectez votre toohello solution préconfigurée application logique que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="f0604-144">In this section, you connect your preconfigured solution toohello Logic App you created.</span></span> <span data-ttu-id="f0604-145">toocomplete cette tâche, vous ajoutez hello tootrigger hello application logique toohello action d’URL qui se déclenche lorsqu’une valeur du capteur de périphérique dépasse un seuil.</span><span class="sxs-lookup"><span data-stu-id="f0604-145">toocomplete this task, you add hello URL tootrigger hello Logic App toohello action that fires when a device sensor value exceeds a threshold.</span></span>

1. <span data-ttu-id="f0604-146">Utiliser git tooclone hello dernière version de votre client de hello [azure-iot-de surveillance à distance référentiel github][lnk-rmgithub].</span><span class="sxs-lookup"><span data-stu-id="f0604-146">Use your git client tooclone hello latest version of hello [azure-iot-remote-monitoring github repository][lnk-rmgithub].</span></span> <span data-ttu-id="f0604-147">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f0604-147">For example:</span></span>
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. <span data-ttu-id="f0604-148">Dans Visual Studio, ouvrez hello **RemoteMonitoring.sln** à partir de la copie locale de hello du référentiel de hello.</span><span class="sxs-lookup"><span data-stu-id="f0604-148">In Visual Studio, open hello **RemoteMonitoring.sln** from hello local copy of hello repository.</span></span>
3. <span data-ttu-id="f0604-149">Ouvrez hello **ActionRepository.cs** fichier Bonjour **Infrastructure\\référentiel** dossier.</span><span class="sxs-lookup"><span data-stu-id="f0604-149">Open hello **ActionRepository.cs** file in hello **Infrastructure\\Repository** folder.</span></span>
4. <span data-ttu-id="f0604-150">Hello de mise à jour **actionIds** dictionnaire avec hello **Http Post toothis URL** vous avez pris note à partir de votre application logique comme suit :</span><span class="sxs-lookup"><span data-stu-id="f0604-150">Update hello **actionIds** dictionary with hello **Http Post toothis URL** you noted from your Logic App as follows:</span></span>
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post toothis URL>" },
        { "Raise Alarm", "<Http Post toothis URL>" }
    };
    ```
5. <span data-ttu-id="f0604-151">Enregistrer les modifications de hello dans la solution et quittez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f0604-151">Save hello changes in solution and exit Visual Studio.</span></span>

## <a name="deploy-from-hello-command-line"></a><span data-ttu-id="f0604-152">Déployer à partir de la ligne de commande hello</span><span class="sxs-lookup"><span data-stu-id="f0604-152">Deploy from hello command line</span></span>
<span data-ttu-id="f0604-153">Dans cette section, vous déployez votre version de mise à jour de hello distant solutions tooreplace hello version de surveillance en cours d’exécution dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f0604-153">In this section, you deploy your updated version of hello remote monitoring solution tooreplace hello version currently running in Azure.</span></span>

1. <span data-ttu-id="f0604-154">Suite hello [dev configuration] [ lnk-devsetup] tooset d’instructions de votre environnement pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="f0604-154">Following hello [dev set-up][lnk-devsetup] instructions tooset up your environment for deployment.</span></span>
2. <span data-ttu-id="f0604-155">toodeploy localement, suivez hello [déploiement local] [ lnk-localdeploy] obtenir des instructions.</span><span class="sxs-lookup"><span data-stu-id="f0604-155">toodeploy locally, follow hello [local deployment][lnk-localdeploy] instructions.</span></span>
3. <span data-ttu-id="f0604-156">toodeploy toohello cloud et mettre à jour votre déploiement de cloud computing existant, suivez hello [déploiement de cloud computing] [ lnk-clouddeploy] obtenir des instructions.</span><span class="sxs-lookup"><span data-stu-id="f0604-156">toodeploy toohello cloud and update your existing cloud deployment, follow hello [cloud deployment][lnk-clouddeploy] instructions.</span></span> <span data-ttu-id="f0604-157">Utiliser le nom hello de votre déploiement d’origine en tant que nom du déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="f0604-157">Use hello name of your original deployment as hello deployment name.</span></span> <span data-ttu-id="f0604-158">Par exemple, si le déploiement d’origine de hello a été appelé **demologicapp**, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f0604-158">For example if hello original deployment was called **demologicapp**, use hello following command:</span></span>
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   <span data-ttu-id="f0604-159">Lorsque hello générer le script s’exécute, veillez à toouse hello même compte Azure, abonnement, région et instance Active Directory que vous avez utilisé lors de la configuration de solution de hello.</span><span class="sxs-lookup"><span data-stu-id="f0604-159">When hello build script runs, be sure toouse hello same Azure account, subscription, region, and Active Directory instance you used when you provisioned hello solution.</span></span>

## <a name="see-your-logic-app-in-action"></a><span data-ttu-id="f0604-160">Voir votre application logique en action</span><span class="sxs-lookup"><span data-stu-id="f0604-160">See your Logic App in action</span></span>
<span data-ttu-id="f0604-161">Hello solution préconfigurée de surveillance à distance a deux règles définies par défaut lorsque vous configurez une solution.</span><span class="sxs-lookup"><span data-stu-id="f0604-161">hello remote monitoring preconfigured solution has two rules set up by default when you provision a solution.</span></span> <span data-ttu-id="f0604-162">Les deux règles sont sur hello **SampleDevice001** appareil :</span><span class="sxs-lookup"><span data-stu-id="f0604-162">Both rules are on hello **SampleDevice001** device:</span></span>

* <span data-ttu-id="f0604-163">Temperature > 38.00</span><span class="sxs-lookup"><span data-stu-id="f0604-163">Temperature > 38.00</span></span>
* <span data-ttu-id="f0604-164">Humidity > 48.00</span><span class="sxs-lookup"><span data-stu-id="f0604-164">Humidity > 48.00</span></span>

<span data-ttu-id="f0604-165">règle de température de Hello déclenche hello **déclencher une alarme** action et hello la règle humidité déclenche hello **SendMessage** action.</span><span class="sxs-lookup"><span data-stu-id="f0604-165">hello temperature rule triggers hello **Raise Alarm** action and hello Humidity rule triggers hello **SendMessage** action.</span></span> <span data-ttu-id="f0604-166">Si vous avez utilisé hello même URL pour les deux hello actions **ActionRepository** classe vos déclencheurs d’application logique pour une règle.</span><span class="sxs-lookup"><span data-stu-id="f0604-166">Assuming you used hello same URL for both actions hello **ActionRepository** class, your logic app triggers for either rule.</span></span> <span data-ttu-id="f0604-167">Les deux règles utilisent SendGrid toosend un toohello de messagerie **à** adresse avec les détails de l’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="f0604-167">Both rules use SendGrid toosend an email toohello **To** address with details of hello alert.</span></span>

> [!NOTE]
> <span data-ttu-id="f0604-168">Hello application logique continue tootrigger chaque fois que hello seuil est atteint.</span><span class="sxs-lookup"><span data-stu-id="f0604-168">hello Logic App continues tootrigger every time hello threshold is met.</span></span> <span data-ttu-id="f0604-169">tooavoid les e-mails inutiles, vous pouvez soit désactiver les règles hello dans votre solution portail ou désactiver hello application logique Bonjour [portail Azure][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="f0604-169">tooavoid unnecessary emails, you can either disable hello rules in your solution portal or disable hello Logic App in hello [Azure portal][lnk-azureportal].</span></span>
> 
> 

<span data-ttu-id="f0604-170">En outre tooreceiving e-mails, vous pouvez également voir quand hello logique d’application s’exécute dans le portail de hello :</span><span class="sxs-lookup"><span data-stu-id="f0604-170">In addition tooreceiving emails, you can also see when hello Logic App runs in hello portal:</span></span>

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a><span data-ttu-id="f0604-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f0604-171">Next steps</span></span>
<span data-ttu-id="f0604-172">Maintenant que vous avez utilisé un processus d’entreprise tooa solution application logique tooconnect hello préconfiguré, vous plus d’informations sur les options de hello pour la personnalisation des solutions de hello préconfiguré :</span><span class="sxs-lookup"><span data-stu-id="f0604-172">Now that you've used a Logic App tooconnect hello preconfigured solution tooa business process, you can learn more about hello options for customizing hello preconfigured solutions:</span></span>

* <span data-ttu-id="f0604-173">[Utiliser la télémétrie dynamique avec hello solution préconfigurée de surveillance à distance][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="f0604-173">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="f0604-174">[Métadonnées d’informations de périphérique Bonjour solution préconfigurée de surveillance à distance][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="f0604-174">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo]</span></span>

[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk-internetofthings]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-getstarted]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-azureportal]: https://portal.azure.com
[lnk-logic-apps-actions]: ../connectors/apis-list.md
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-devsetup]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/dev-setup.md
[lnk-localdeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/local-deployment.md
[lnk-clouddeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
