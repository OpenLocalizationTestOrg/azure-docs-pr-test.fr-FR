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
# <a name="tutorial-connect-logic-app-tooyour-azure-iot-suite-remote-monitoring-preconfigured-solution"></a>Didacticiel : Connecter des solutions d’Azure IoT Suite l’analyse à distance préconfiguré tooyour application logique
Hello [Microsoft Azure IoT Suite] [ lnk-internetofthings] solutions préconfigurées de surveillance à distance est un excellent moyen tooget démarré rapidement avec un ensemble de fonctionnalités de bout en bout qui illustre une solution IoT. Ce didacticiel vous guide tout au long de la surveillance à distance de tooadd application logique tooyour Microsoft Azure IoT Suite des solution préconfigurée. Ces étapes montrent comment prendre votre solution IoT encore davantage en la connectant tooa processus d’entreprise.

*Si vous avez besoin d’une procédure pas à pas sur la solution préconfigurée tooprovision une surveillance à distance, consultez [didacticiel : prise en main des solutions IoT préconfiguré hello][lnk-getstarted].*

Avant de commencer ce didacticiel, vous devez :

* Configurer l’analyse à distance hello préconfiguré solution dans votre abonnement Azure.
* Créer un tooenable de compte SendGrid toosend un message électronique qui déclenche votre processus d’entreprise. Vous pouvez vous inscrire à un compte d’évaluation gratuit sur [SendGrid](https://sendgrid.com/) en cliquant sur **Essai gratuit**. Une fois que vous êtes inscrit pour votre compte d’évaluation gratuite, vous devez toocreate une [clé API](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) dans SendGrid qui accorde des autorisations toosend mail. Vous avez besoin de cette clé API plus loin dans le didacticiel de hello.

toocomplete ce didacticiel, vous avez besoin de Visual Studio 2015 ou Visual Studio 2017 toomodify hello actions hello solution préconfigurée back-end.

En supposant, vous avez déjà configuré votre contrôle à distance de la solution préconfigurée, accédez toohello groupe de ressources pour cette solution Bonjour [portail Azure][lnk-azureportal]. groupe de ressources Hello a hello même nom que celui que hello solution nom que vous avez choisi lorsque vous avez configuré votre solution d’analyse à distance. Dans le groupe de ressources hello, vous pouvez voir hello tous mis en service des ressources Azure pour votre solution à l’exception de hello application Azure Active Directory que vous pouvez trouver Bonjour portail classique Azure. Hello capture d’écran suivante montre un exemple **groupe de ressources** solution préconfigurée de panneau pour une surveillance à distance :

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

toobegin, configuration hello logique application toouse avec hello la solution préconfigurée.

## <a name="set-up-hello-logic-app"></a>Configurer hello logique d’application
1. Cliquez sur **ajouter** haut hello du panneau des ressources de votre groupe Bonjour portail Azure.
2. Recherchez **l’application logique**, sélectionnez-la, puis cliquez sur **Créer**.
3. Remplir hello **nom** et utilisez hello même **abonnement** et **groupe de ressources** que vous avez utilisé lors de la configuration de votre solution d’analyse à distance. Cliquez sur **Créer**.
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. Lorsque votre déploiement est terminé, vous pouvez voir hello Qu'application logique est répertoriée en tant que ressource dans votre groupe de ressources.
5. Cliquez sur le panneau des applications logiques hello application logique toonavigate toohello, sélectionnez hello **application logique vide** hello tooopen de modèle **Concepteur d’applications logique**.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. Sélectionnez **Requête**. Cette action indique qu’une demande HTTP entrante avec une charge utile au format JSON spécifique agit comme un déclencheur.
7. Collez hello après le code dans hello schéma de JSON de corps de la requête :
   
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
   > Vous pouvez copier des URL hello pour valider de hello HTTP une fois que vous avez enregistré hello logique application, mais vous devez d’abord ajouter une action.
   > 
   > 
8. Cliquez sur **+ Nouvelle étape** sous votre déclencheur manuel. Cliquez ensuite sur **Ajouter une action**.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. Recherchez **SendGrid - Send email** (SendGrid - Envoyer un e-mail) et cliquez dessus.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. Entrez un nom pour la connexion de hello, tel que **SendGridConnection**, entrez hello **clé d’API SendGrid** vous avez créé lorsque vous configurez votre compte SendGrid, puis cliquez sur **créer**.
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. Ajouter des adresses de messagerie vous tooboth propre hello **de** et **à** champs. Ajouter **alerte de surveillance à distance [DeviceId]** toohello **sujet** champ. Bonjour **corps du message électronique** champ, ajoutez **[DeviceId] a signalé [measurementName] avec la valeur [measuredValue].** Vous pouvez ajouter **[DeviceId]**, **[measurementName]**, et **[measuredValue]** en cliquant sur Bonjour **vous pouvez insérer des données à partir des précédentes étapes**section.
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. Cliquez sur **enregistrer** dans le menu du haut hello.
13. Cliquez sur hello **demande** déclencheur et copie hello **Http Post toothis URL** valeur. Vous aurez besoin de cette URL plus tard dans ce didacticiel.

> [!NOTE]
> Logic Apps permettent de toorun [différents types d’action] [ lnk-logic-apps-actions] notamment des actions dans Office 365. 
> 
> 

## <a name="set-up-hello-eventprocessor-web-job"></a>Configurer hello EventProcessor de tâche Web
Dans cette section, vous vous connectez votre toohello solution préconfigurée application logique que vous avez créé. toocomplete cette tâche, vous ajoutez hello tootrigger hello application logique toohello action d’URL qui se déclenche lorsqu’une valeur du capteur de périphérique dépasse un seuil.

1. Utiliser git tooclone hello dernière version de votre client de hello [azure-iot-de surveillance à distance référentiel github][lnk-rmgithub]. Par exemple :
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. Dans Visual Studio, ouvrez hello **RemoteMonitoring.sln** à partir de la copie locale de hello du référentiel de hello.
3. Ouvrez hello **ActionRepository.cs** fichier Bonjour **Infrastructure\\référentiel** dossier.
4. Hello de mise à jour **actionIds** dictionnaire avec hello **Http Post toothis URL** vous avez pris note à partir de votre application logique comme suit :
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post toothis URL>" },
        { "Raise Alarm", "<Http Post toothis URL>" }
    };
    ```
5. Enregistrer les modifications de hello dans la solution et quittez Visual Studio.

## <a name="deploy-from-hello-command-line"></a>Déployer à partir de la ligne de commande hello
Dans cette section, vous déployez votre version de mise à jour de hello distant solutions tooreplace hello version de surveillance en cours d’exécution dans Azure.

1. Suite hello [dev configuration] [ lnk-devsetup] tooset d’instructions de votre environnement pour le déploiement.
2. toodeploy localement, suivez hello [déploiement local] [ lnk-localdeploy] obtenir des instructions.
3. toodeploy toohello cloud et mettre à jour votre déploiement de cloud computing existant, suivez hello [déploiement de cloud computing] [ lnk-clouddeploy] obtenir des instructions. Utiliser le nom hello de votre déploiement d’origine en tant que nom du déploiement hello. Par exemple, si le déploiement d’origine de hello a été appelé **demologicapp**, utilisez hello de commande suivante :
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   Lorsque hello générer le script s’exécute, veillez à toouse hello même compte Azure, abonnement, région et instance Active Directory que vous avez utilisé lors de la configuration de solution de hello.

## <a name="see-your-logic-app-in-action"></a>Voir votre application logique en action
Hello solution préconfigurée de surveillance à distance a deux règles définies par défaut lorsque vous configurez une solution. Les deux règles sont sur hello **SampleDevice001** appareil :

* Temperature > 38.00
* Humidity > 48.00

règle de température de Hello déclenche hello **déclencher une alarme** action et hello la règle humidité déclenche hello **SendMessage** action. Si vous avez utilisé hello même URL pour les deux hello actions **ActionRepository** classe vos déclencheurs d’application logique pour une règle. Les deux règles utilisent SendGrid toosend un toohello de messagerie **à** adresse avec les détails de l’alerte de hello.

> [!NOTE]
> Hello application logique continue tootrigger chaque fois que hello seuil est atteint. tooavoid les e-mails inutiles, vous pouvez soit désactiver les règles hello dans votre solution portail ou désactiver hello application logique Bonjour [portail Azure][lnk-azureportal].
> 
> 

En outre tooreceiving e-mails, vous pouvez également voir quand hello logique d’application s’exécute dans le portail de hello :

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez utilisé un processus d’entreprise tooa solution application logique tooconnect hello préconfiguré, vous plus d’informations sur les options de hello pour la personnalisation des solutions de hello préconfiguré :

* [Utiliser la télémétrie dynamique avec hello solution préconfigurée de surveillance à distance][lnk-dynamic]
* [Métadonnées d’informations de périphérique Bonjour solution préconfigurée de surveillance à distance][lnk-devinfo]

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
