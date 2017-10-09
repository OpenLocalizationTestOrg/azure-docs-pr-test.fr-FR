## <a name="view-hello-telemetry"></a>Télémétrie des consultations de hello

Hello framboises Pi envoie désormais une solution d’analyse à distance toohello télémétrie. Vous pouvez afficher les données de télémétrie hello sur le tableau de bord de solution hello. Vous pouvez également envoyer des messages tooyour framboises Pi à partir du tableau de bord de solution hello.

- Accédez à tableau de bord toohello solution.
- Sélectionnez votre appareil dans hello **tooView de périphérique** liste déroulante.
- télémétrie Hello hello framboises Pi affiche sur le tableau de bord hello.

![Afficher les données de télémétrie de hello framboises Pi][img-telemetry-display]

## <a name="act-on-hello-device"></a>Agir sur les appareils hello

À partir du tableau de bord hello solution, vous pouvez appeler des méthodes sur votre Pi framboises. Lorsque hello framboises Pi connecte à une solution d’analyse à distance toohello, il envoie des informations sur les méthodes hello qu'il prend en charge.

- Dans le tableau de bord hello solution, cliquez sur **périphériques** toovisit hello **périphériques** page. Sélectionnez votre Pi framboises Bonjour **liste des appareils**. Ensuite, choisissez **Méthodes** :

    ![Liste des appareils dans le tableau de bord][img-list-devices]

- Sur hello **appeler une méthode** choisissez **LightBlink** Bonjour **méthode** liste déroulante.

- Choisissez **InvokeMethod**. Hello DEL connecté toohello que framboises Pi clignote à plusieurs reprises. application Hello sur hello framboises Pi envoie un tableau de bord d’accusé de réception différé toohello solution :

    ![Afficher l’historique de la méthode][img-method-history]

- Vous pouvez basculer les DEL hello et désactiver à l’aide de hello **ChangeLightStatus** méthode avec un **LightStatusValue** défini trop**1** pour sur ou **0** pour désactiver.

> [!WARNING]
> Si vous laissez hello solution en cours d’exécution dans votre compte Azure de surveillance à distance, vous êtes facturé pour hello exécution. Pour plus d’informations sur la réduction de la consommation lors hello s’exécute la solution de surveillance à distance, consultez [configuration Azure IoT Suite préconfiguré des solutions à des fins de démonstration][lnk-demo-config]. Supprimer la solution de hello préconfiguré à partir de votre compte Azure lorsque vous avez terminé.


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md