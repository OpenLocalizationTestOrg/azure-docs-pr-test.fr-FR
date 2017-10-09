## <a name="create-a-device-identity"></a>Création d’une identité d’appareil

Dans cette section, vous utilisez hello [portail Azure] [ lnk-azure-portal] toocreate une identité d’appareil dans le Registre des identités hello dans votre hub IoT. Un appareil ne peut pas se connecter à tooIoT concentrateur sauf si elle possède une entrée dans le Registre des identités hello. Pour plus d’informations, voir section « Registre des identités » hello hello [guide du développeur IoT Hub][lnk-devguide-identity]. Hello **appareil Explorer** Bonjour portail vous permet de générer un ID d’appareil unique et une clé que votre appareil peut utiliser tooidentify lui-même quand il connecte tooIoT Hub. Les ID d’appareil respectent la casse.

1. Assurez-vous que vous êtes connecté dans toohello [portail Azure][lnk-azure-portal].

1. Bonjour Jumpbar, cliquez sur **toutes les ressources** et recherchez votre ressource de hub IoT.

    ![Accédez tooyour Iot hub][img-find-iothub]

1. Lorsque votre ressource de hub IoT est ouverte, cliquez sur hello **appareil Explorer** d’outils, puis cliquez sur **ajouter** haut hello. Fournir le nom hello pour votre nouveau périphérique, tel que **myDeviceId**, puis cliquez sur **enregistrer**.

    ![Créer une identité d’appareil sur le portail][img-create-device]

   Cela permet de créer une identité d’appareil pour votre IoT Hub.

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. Bonjour **appareil Explorer**de liste de périphériques, cliquez sur le périphérique de hello qui vient d’être créé et prenez note de hello **chaîne de connexion---clé primaire**. 

    ![Chaîne de connexion de l’appareil][img-connection-string]

> [!NOTE]
> Hello Registre des identités IoT Hub stocke uniquement toohello IoT hub de périphérique identités tooenable un accès sécurisé. Il stocke toouse ID et les clés de périphérique en tant qu’informations d’identification de sécurité et un indicateur activée/désactivée que vous pouvez utiliser l’accès toodisable pour un périphérique. Si votre application doit toostore autres métadonnées spécifiques au périphérique, elle doit utiliser un magasin spécifique à l’application. Pour plus d’informations, reportez-vous au [Guide du développeur IoT Hub][lnk-devguide-identity].

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md

