## <a name="view-hello-telemetry"></a>Télémétrie des consultations de hello

Hello framboises Pi envoie désormais une solution d’analyse à distance toohello télémétrie. Vous pouvez afficher les données de télémétrie hello sur le tableau de bord de solution hello. Vous pouvez également envoyer des messages tooyour framboises Pi à partir du tableau de bord de solution hello.

- Accédez à tableau de bord toohello solution.
- Sélectionnez votre appareil dans hello **tooView de périphérique** liste déroulante.
- télémétrie Hello hello framboises Pi affiche sur le tableau de bord hello.

![Afficher les données de télémétrie de hello framboises Pi][img-telemetry-display]

## <a name="initiate-hello-firmware-update"></a>Lancer la mise à jour du microprogramme hello

processus de mise à jour de microprogramme Hello télécharge et installe une version mise à jour de l’application de client de périphérique hello sur hello framboises Pi. Pour plus d’informations sur le processus de mise à jour de microprogramme hello, consultez la description hello du modèle de mise à jour de microprogramme hello dans [vue d’ensemble de gestion des appareils avec IoT Hub][lnk-update-pattern].

Vous lancer le processus de mise à jour de microprogramme hello en appelant une méthode sur l’appareil de hello. Cette méthode est asynchrone et retourne dès que le processus de mise à jour hello commence. Hello périphérique utilise signalé solution de propriétés toonotify hello sur la progression de hello de mise à jour hello.

Pour appeler des méthodes sur votre Pi framboises à partir du tableau de bord de solution hello. Lorsque hello framboises Pi connecte toohello solution d’analyse à distance d’abord, il envoie des informations sur les méthodes hello qu'il prend en charge. 

[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-advanced/telemetry.png
[lnk-update-pattern]: ../articles/iot-hub/iot-hub-device-management-overview.md
