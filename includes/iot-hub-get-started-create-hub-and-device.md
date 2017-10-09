## <a name="create-an-iot-hub"></a>Créer un hub IoT

1. Bonjour [portail Azure](https://portal.azure.com/), cliquez sur **nouveau** > **Internet of Things** > **IoT Hub**.

   ![Créez un hub IoT Bonjour portail Azure](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. Bonjour **IoT hub** volet, entrez hello informations pour votre hub IoT suivantes :

     **Nom**: entrez le nom hello de votre hub IoT. Si le nom hello que vous entrez est valide, une coche verte s’affiche.

     **Niveau de tarification et de mise à l’échelle**: hello sélectionnez **F1 - libre** couche. Cette option suffit pour cette démonstration. Pour plus d’informations, consultez hello [niveau de tarification et de mise à l’échelle](https://azure.microsoft.com/pricing/details/iot-hub/).

     **Groupe de ressources**: création d’un ressource groupe toohost hello IoT hub ou utilisez-en un existant. Pour plus d’informations, consultez [groupes de ressources de l’utilisation toomanage vos ressources Azure](../articles/azure-resource-manager/resource-group-portal.md).

     **Emplacement**: sélectionnez hello plus proche tooyou emplacement où hub IoT de hello est créé.

     **Code confidentiel toodashboard**: sélectionnez cette option pour le hub de IoT tooyour accéder facilement à partir du tableau de bord hello.

   ![Entrez les informations toocreate votre IoT hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. Cliquez sur **Créer**. Votre IoT hub peut prendre quelques minutes toocreate. Vous pouvez consulter la progression dans hello **Notifications** volet.

   ![Voir les notifications de progression de votre IoT Hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. Une fois votre hub IoT est créé, cliquez dessus dans le tableau de bord hello. Prenez note de hello **nom d’hôte**, puis cliquez sur **les stratégies d’accès partagé**.

   ![Obtenir le nom d’hôte hello de votre hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. Bonjour **les stratégies d’accès partagé** volet, cliquez sur hello **iothubowner** stratégie, puis copie et noté de hello **chaîne de connexion** de votre hub IoT. Pour plus d’informations, consultez [tooIoT d’accès contrôle Hub](../articles/iot-hub/iot-hub-devguide-security.md).

> [!NOTE] 
Vous n’aurez pas besoin de cette chaîne de connexion iothubowner pour ce didacticiel d’installation. Toutefois, vous devrez il pour certaines des didacticiels hello sur différents scénarios IoT après avoir terminé cette installation.

   ![Obtention de la chaîne de connexion de votre IoT Hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-hello-iot-hub-for-your-device"></a>Inscrire un appareil dans hello IoT hub pour votre appareil

1. Bonjour [portail Azure](https://portal.azure.com/), ouvrez votre hub IoT.

2. Cliquez sur **Explorateur d’appareils**.
3. Dans le volet de l’Explorateur de l’appareil hello, cliquez sur **ajouter** tooadd un IoT hub de périphérique tooyour. Puis la hello suivant :

   **ID de périphérique**: hello de saisir de nouveau périphérique de hello. Les ID d’appareil respectent la casse.

   **Type d’authentification** : sélectionnez **Clé symétrique**.

   **Générer automatiquement les clés** : cochez cette case.

   **Connecter l’appareil tooIoT Hub**: cliquez sur **activer**.

   ![Ajouter un périphérique dans hello Explorateur de l’appareil de votre hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. Cliquez sur **Enregistrer**.
5. Après la création de l’appareil de hello, d’ouvrir l’unité de hello Bonjour **appareil Explorer** volet.
6. Prenez note de clé primaire de hello hello de chaîne de connexion.

   ![Obtenir la chaîne de connexion de périphérique hello](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
