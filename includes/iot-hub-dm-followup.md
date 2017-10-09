## <a name="customize-and-extend-hello-device-management-actions"></a>Personnaliser et étendre les actions de gestion de périphérique hello

Vos solutions IoT développez ensemble hello défini des modèles de gestion des appareils ou activer les modèles personnalisés à l’aide de la double du périphérique hello et primitives de méthode du cloud sur l’appareil. La réinitialisation des paramètres d’usine, la mise à jour du microprogramme, la mise à jour logicielle, la gestion de l’alimentation, la gestion du réseau et de la connectivité, et le chiffrement des données sont d’autres exemples d’actions de gestion des appareils.

## <a name="device-maintenance-windows"></a>Fenêtres de maintenance d’appareil

En règle générale, vous configurez des actions de tooperform de périphériques à un moment qui réduit les interruptions et les temps d’arrêt. Les fenêtres de maintenance de périphérique sont un modèle couramment utilisés toodefine hello quand un appareil doit mettre à jour sa configuration. Vos solutions principale propriétés hello souhaité de hello appareil double toodefine et d’activer une stratégie sur votre appareil qui permet à une fenêtre de maintenance. Lorsqu’un appareil reçoit la stratégie de fenêtre de maintenance hello, elle peut utiliser hello a signalé la propriété de hello double tooreport hello statut de périphérique de stratégie de hello. Hello principal application peut ensuite utiliser appareil double requêtes tooattest toocompliance de périphériques et de chaque stratégie.

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez utilisé un tootrigger méthode directe une réinitialisation à distance sur un appareil. Vous hello utilisé des propriétés déclarées tooreport hello redémarrer dernière heure à partir de l’appareil de hello et interrogés Bonjour appareil double toodiscover Bonjour redémarrer dernière heure de l’appareil hello du cloud de hello.

toocontinue mise en route avec IoT Hub et les modèles de gestion des appareils tels qu’à distance sur la mise à jour de microprogramme hello air, consultez :

[Didacticiel : Comment toodo un microprogramme mettre à jour][lnk-fwupdate]

toolearn tooextend votre méthode de planification et de solution IoT des appels sur plusieurs appareils, consultez hello [planification et les tâches de diffusion] [ lnk-tutorial-jobs] didacticiel.

toocontinue mise en route avec IoT Hub, consultez [mise en route avec IoT bord][lnk-iot-edge].

[lnk-fwupdate]: ../articles/iot-hub/iot-hub-node-node-firmware-update.md
[lnk-tutorial-jobs]: ../articles/iot-hub/iot-hub-node-node-schedule-jobs.md
[lnk-iot-edge]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md