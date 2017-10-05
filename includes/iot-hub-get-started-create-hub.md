## <a name="create-an-iot-hub"></a>Créer un hub IoT
Créez un IoT Hub pour que votre application de périphérique simulé puisse se connecter. Les étapes suivantes vous montrent comment exécuter cette tâche à l’aide du portail Azure.

1. Connectez-vous au [portail Azure][lnk-portal].
1. Dans la barre de lancement, cliquez sur **Nouveau** > **Internet des objets** > **Azure IoT Hub**.
   
    ![Barre de lancement du portail Azure][1]
1. Dans le panneau **IoT hub** , choisissez la configuration de votre concentrateur IoT.
   
    ![Panneau IoT Hub][2]
   
   1. Dans la zone **Nom** , saisissez un nom pour identifier votre hub IoT. Une fois le **Nom** validé et disponible, une coche verte apparaît dans la case **Nom**.
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. Sélectionnez une [tarification et un niveau de mise à l’échelle][lnk-pricing]. Ce didacticiel ne nécessite pas un niveau spécifique. Pour ce didacticiel, utilisez le niveau F1 gratuit.
   1. Dans **Groupe de ressources**, créez un groupe de ressources ou sélectionnez un groupe existant. Pour plus d’informations, consultez [Utilisation des groupes de ressources pour gérer vos ressources Azure][lnk-resource-groups].
   1. Dans **Emplacement**, sélectionnez l’emplacement destiné à héberger votre concentrateur IoT. Pour ce didacticiel, choisissez l’emplacement le plus proche.
1. Une fois que vous avez choisi les options de configuration de votre hub IoT, cliquez sur **Créer**.  La création du hub IoT par Azure peut prendre plusieurs minutes. Pour vérifier l’état d’avancement de l’opération, vous pouvez consulter le tableau d’accueil ou le panneau Notifications.
   
    ![Nouveau statut IoT Hub][3]
1. Lorsque l’IoT hub a été créé avec succès, cliquez sur la nouvelle vignette représentant votre IoT hub dans le portail Azure pour ouvrir le panneau du nouveau IoT Hub. Notez la valeur **Hostname**, puis cliquez sur **Stratégies d’accès partagé**.
   
    ![Nouveau panneau IoT Hub][4]
1. Dans le panneau **Stratégies d’accès partagé**, cliquez sur la stratégie **iothubowner**, puis copiez et notez la chaîne de connexion IoT Hub dans le panneau **iothubowner**. Consultez la rubrique [Access Control][lnk-access-control] du « Guide du développeur IoT Hub » pour plus d’informations.
   
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
