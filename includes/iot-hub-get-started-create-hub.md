## <a name="create-an-iot-hub"></a>Créer un hub IoT
Créez un hub IoT pour votre tooconnect d’application appareil simulé à. Hello étapes suivantes vous montrent comment toocomplete cette tâche à l’aide de hello portail Azure.

1. Connectez-vous à toohello [portail Azure][lnk-portal].
1. Bonjour Jumpbar, cliquez sur **nouveau** > **Internet of Things** > **IoT Hub**.
   
    ![Barre de lancement du portail Azure][1]
1. Bonjour **IoT hub** panneau, choisissez configuration hello pour votre hub IoT.
   
    ![Panneau IoT Hub][2]
   
   1. Bonjour **nom** , entrez un nom pour votre hub IoT. Si hello **nom** n’est valide et disponible, une coche verte s’affiche dans hello **nom** boîte.
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. Sélectionnez une [tarification et un niveau de mise à l’échelle][lnk-pricing]. Ce didacticiel ne nécessite pas un niveau spécifique. Pour ce didacticiel, utilisez le gratuit F1 hello.
   1. Dans **Groupe de ressources**, créez un groupe de ressources ou sélectionnez un groupe existant. Pour plus d’informations, consultez [à l’aide de la ressource groupes toomanage vos ressources Azure][lnk-resource-groups].
   1. Dans **emplacement**, sélectionnez hello emplacement toohost votre hub IoT. Pour ce didacticiel, choisissez l’emplacement le plus proche.
1. Une fois que vous avez choisi les options de configuration de votre hub IoT, cliquez sur **Créer**.  Il peut prendre quelques minutes pour Azure toocreate votre hub IoT. état de hello toocheck, vous pouvez surveiller progression hello sur hello tableau d’accueil ou dans le panneau de configuration de Notifications hello.
   
    ![Nouveau statut IoT Hub][3]
1. Lorsque le hub IoT de hello a été créé avec succès, cliquez sur hello nouvelle vignette représentant votre hub IoT dans Panneau de hello hello tooopen portail Azure pour le nouveau concentrateur de IoT hello. Prenez note de hello **nom d’hôte**, puis cliquez sur **les stratégies d’accès partagé**.
   
    ![Nouveau panneau IoT Hub][4]
1. Bonjour **les stratégies d’accès partagé** panneau, cliquez sur hello **iothubowner** stratégie, puis copiez et prenez note de hello chaîne de connexion de IoT Hub Bonjour **iothubowner** panneau. Pour plus d’informations, consultez [le contrôle d’accès] [ lnk-access-control] Bonjour « Guide du développeur IoT Hub ».
   
    ![Panneau des stratégies d’accès partagées][5]

<!-- Images. -->
[1]: ./media/iot-hub-get-started-create-hub/create-iot-hub1.png
[2]: ./media/iot-hub-get-started-create-hub/create-iot-hub2.png
[3]: ./media/iot-hub-get-started-create-hub/create-iot-hub3.png
[4]: ./media/iot-hub-get-started-create-hub/create-iot-hub4.png
[5]: ./media/iot-hub-get-started-create-hub/create-iot-hub5.png

<!-- Links -->
[lnk-resource-groups]: ../articles/azure-resource-manager/resource-group-portal.md
[lnk-portal]: https://portal.azure.com/
[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-access-control]: ../articles/iot-hub/iot-hub-devguide-security.md
