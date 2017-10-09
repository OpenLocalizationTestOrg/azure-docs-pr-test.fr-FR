## <a name="view-device-telemetry-in-hello-dashboard"></a>Télémétrie des consultations de périphérique dans le tableau de bord hello
tableau de bord Hello Bonjour permet de solution télémétrie hello tooview tooIoT Hub d’envoi de vos appareils de surveillance à distance.

1. Dans votre navigateur, retour toohello distant solutions tableau de bord, cliquez sur **périphériques** dans hello panneau gauche toonavigate toohello **liste de périphériques**.
2. Bonjour **liste de périphériques**, vous devez voir que hello de votre appareil sont **en cours d’exécution**. Dans le cas contraire, cliquez sur **activer le périphérique** Bonjour **détails de l’appareil** Panneau de configuration.
   
    ![Afficher l’état de l’appareil][18]
3. Cliquez sur **tableau de bord** tooreturn toohello tableau de bord, sélectionnez votre appareil dans hello **tooView de périphérique** tooview de liste déroulante ses données de télémétrie. télémétrie Hello à partir de l’exemple d’application hello est 50 unités pour la température interne, 55 unités pour la température externe et 50 unités de l’humidité.
   
    ![Afficher la télémétrie d’appareil][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a>Appel d’une méthode sur votre appareil
tableau de bord Hello dans la solution d’analyse à distance hello vous permet de méthodes tooinvoke sur vos appareils via IoT Hub. Par exemple, Bonjour solution de surveillance à distance, vous pouvez appeler une toosimulate méthode redémarrage d’un périphérique.

1. Dans hello distant solutions tableau de bord, cliquez sur **périphériques** dans hello panneau gauche toonavigate toohello **liste de périphériques**.
2. Cliquez sur **ID de périphérique** pour votre appareil dans hello **liste de périphériques**.
3. Bonjour **détails de l’appareil** du panneau, cliquez sur **méthodes**.
   
    ![Méthodes d’appareil][13]
4. Bonjour **méthode** liste déroulante, sélectionnez **InitiateFirmwareUpdate**, puis dans **FWPACKAGEURI** entrer une URL factice. Cliquez sur **appeler une méthode** toocall la méthode hello sur le périphérique de hello.
   
    ![Appel d’une méthode d’appareil][14]
   

5. Vous voyez un message dans la console hello votre code de l’appareil en cours d’exécution lorsque le périphérique de hello gère la méthode hello. résultats Hello de méthode hello sont ajoutées toohello historique au portail de solution hello :

    ![Affichage de l’historique des méthodes][img-method-history]

## <a name="next-steps"></a>Étapes suivantes
article de Hello [personnalisation préconfiguré solutions] [ lnk-customize] décrit quelques méthodes que vous pouvez étendre cet exemple. Les extensions incluent l'utilisation de capteurs réels et l'implémentation de commandes supplémentaires.

Vous en apprendrez davantage sur hello [autorisations sur le site de azureiotsuite.com hello][lnk-permissions].

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
