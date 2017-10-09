> [!div class="op_single_selector"]
> * [Node.JS](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [C#/Node.js](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a>Introduction

Dans [prise en main jumeaux des appareils IoT Hub][lnk-twin-tutorial], vous avez appris comment tooset les métadonnées de périphérique à partir de votre solution précédent mettre fin à l’aide de *balises*, signaler l’appareil à partir d’une application de périphérique à l’aide de *signalé propriétés*et ces informations à l’aide d’un langage de type SQL de la requête.

Dans ce didacticiel, vous allez apprendre comment toouse hello du double hello appareil *propriétés souhaitée* avec *signalé propriétés*, tooremotely configurer des applications de périphérique. Plus spécifiquement, ce didacticiel montre comment un double de périphérique signalé et propriétés souhaitées activer une configuration à plusieurs étapes d’une application de périphérique et fournissent des hello visibilité toohello solution back end d’état hello de cette opération sur tous les périphériques. Vous trouverez plus d’informations sur le rôle de hello de configurations du périphérique dans [vue d’ensemble de gestion des appareils avec IoT Hub][lnk-dm-overview].

À un niveau élevé, jumeaux de périphérique grâce à hello solution back-end toospecify hello configuration souhaitée pour les appareils hello géré, au lieu d’envoyer des commandes spécifiques. Cela met l’appareil hello responsable de la configuration hello meilleure manière tooupdate sa configuration (très important dans les scénarios IoT où les conditions de périphérique spécifique affectent hello capacité tooimmediately exécuter des commandes spécifiques), tout en permanence reporting toohello solution de retour de fin état actuel de hello et conditions d’erreur potentielle du processus de mise à jour hello. Ce modèle est gestion toohello instrumentale de grands ensembles de périphériques, car elle permet des hello solution back-end toohave une visibilité complète de l’état de hello hello du processus de configuration sur tous les périphériques.

> [!NOTE]
> Pour les scénarios impliquant un contrôle plus interactif des appareils (mise en marche d’un ventilateur à partir d’une application contrôlée par l’utilisateur), envisagez d’utiliser des [méthodes directes][lnk-methods].
> 
> 

Dans ce didacticiel, modifications de back-end de solution hello hello télémétrie configuration d’un appareil cible, à la suite qui, application d’appareil hello suit un processus comportant plusieurs étapes de tooapply une configuration de mise à jour (par exemple, nécessitant un redémarrage de module logiciel, dans lequel ce didacticiel simule avec un simple délai).

Hello solution back-end stocke la configuration de hello dans les propriétés du double hello appareil Bonjour de configuration suivant :

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of hello configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> Étant donné que les configurations peuvent être des objets complexes, elles sont généralement affectés des ID uniques (hachages ou [GUID][lnk-guid]) toosimplify leurs comparaisons.
> 
> 

application Hello signale sa configuration actuelle, mise en miroir de la propriété de hello souhaité **telemetryConfig** Bonjour signalé propriétés :

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

Notez comment hello **telemetryConfig** a une propriété supplémentaire **état**, utilisé l’état de hello tooreport hello mise à jour du processus de configuration.

Lorsqu’une nouvelle configuration souhaitée est reçue, application hello signale une configuration en attente en modifiant les informations de hello :

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of hello pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

Ensuite, à un moment ultérieur, application d’appareil hello signalera réussite de hello ou l’échec de cette opération en mettant à jour hello au-dessus de propriété.
Notez comment hello solution back-end est capable, à tout moment, l’état de hello tooquery hello du processus de configuration sur tous les périphériques hello.

Ce didacticiel vous explique les procédures suivantes :

* Créer une application d’appareil simulé qui reçoit des mises à jour de la configuration de hello solution back-end et des rapports de plusieurs mises à jour en tant que *signalé propriétés* sur la configuration de hello des mises à jour.
* Créer une application back-end que les mises à jour hello souhaitée de configuration d’un périphérique, et puis requêtes hello le processus de mise à jour de configuration.

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier
