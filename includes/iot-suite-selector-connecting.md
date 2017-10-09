> [!div class="op_single_selector"]
> * [C sur Windows](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [C sur Linux](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [Node.JS](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a>Présentation du scénario
Dans ce scénario, vous créez un périphérique qui envoie hello suivant la surveillance à distance de télémétrie toohello [solution préconfigurée][lnk-what-are-preconfig-solutions]:

* Température externe
* Température interne
* Humidité

Par souci de simplicité, code hello sur l’appareil de hello génère des exemples de valeurs, mais nous encourageons exemple hello tooextend par connexion réelle capteurs tooyour appareil et l’envoi de télémétrie réel.

Hello appareil est également en mesure de toorespond toomethods appelée à partir du tableau de bord de solution hello et souhaitée des valeurs de propriété définies dans le tableau de bord de solution hello.

toocomplete ce didacticiel, vous avez besoin d’un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk-free-trial].

## <a name="before-you-start"></a>Avant de commencer
Avant d’écrire du code pour votre appareil, vous devez approvisionner votre solution préconfigurée de surveillance à distance et approvisionner un nouvel appareil personnalisé dans cette solution.

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a>Approvisionner la solution préconfigurée de surveillance à distance
APPAREIL Hello vous créez dans ce didacticiel envoie instance tooan de données de hello [surveillance à distance] [ lnk-remote-monitoring] solution préconfigurée. Si vous n’avez pas déjà configuré hello solution préconfigurée dans votre compte Azure de surveillance à distance, utilisez hello comme suit :

1. Sur hello <https://www.azureiotsuite.com/> , cliquez sur  **+**  toocreate une solution.
2. Cliquez sur **sélectionnez** sur hello **surveillance à distance** panneau toocreate votre solution.
3. Sur hello **créer distant solutions d’analyse** , entrez un **nom de la Solution** de votre choix, sélectionnez hello **région** vous le souhaitez toodeploy à et sélectionnez hello Azure abonnement toowant toouse. Cliquez ensuite sur **Créer la solution**.
4. Attendez que hello processus de configuration est terminée.

> [!WARNING]
> les solutions de Hello préconfiguré utilisent les services Azure facturables. Veillez tooremove hello solution préconfigurée à partir de votre abonnement lorsque vous avez terminé avec lui tooavoid tous les frais inutiles. Vous pouvez supprimer complètement une solution préconfigurée de votre abonnement en visitant hello <https://www.azureiotsuite.com/> page.
> 
> 

Lorsque hello processus pour hello solution de surveillance à distance de configuration est terminée, cliquez sur **lancer** tooopen hello solution tableau de bord dans votre navigateur.

![Tableau de bord de solution][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a>Configurer votre appareil dans la solution de surveillance à distance de hello
> [!NOTE]
> Si vous avez déjà approvisionné un appareil dans votre solution, vous pouvez ignorer cette étape. Vous avez besoin d’informations d’identification de périphérique tooknow hello lorsque vous créez l’application cliente de hello.
> 
> 

Pour une solution toohello préconfiguré tooconnect des appareils, il doit s’identifier tooIoT concentrateur à l’aide des informations d’identification valides. Vous pouvez récupérer les informations d’identification de périphérique hello à partir du tableau de bord de solution hello. Pour inclure des informations d’identification de périphérique hello dans votre application cliente, plus loin dans ce didacticiel.

tooadd une solution d’analyse à distance tooyour périphérique, hello complet suivant les étapes dans le tableau de bord de solution hello :

1. Dans hello coin inférieur gauche du tableau de bord hello, cliquez sur **ajouter un périphérique**.
   
   ![Ajout d’un appareil][1]
2. Bonjour **personnalisé appareil** du panneau, cliquez sur **ajouter un nouveau**.
   
   ![Ajout d’un appareil personnalisé][2]
3. Choisissez **Me laisser définir mon propre ID d'appareil**. Entrez un ID de périphérique tel **mydevice**, cliquez sur **vérifier l’ID** tooverify ce nom n’est pas déjà en cours d’utilisation, puis cliquez sur **créer** appareil de hello tooprovision.
   
   ![Ajouter ID d’appareil][3]
4. Rendre un périphérique de hello de note les informations d’identification (ID de périphérique, nom d’hôte du Hub IoT et clé de périphérique). Votre application cliente doit ces toohello tooconnect de valeurs solution de surveillance à distance. Cliquez ensuite sur **Terminé**.
   
    ![Afficher les informations d’identification d’un appareil][4]
5. Sélectionnez votre appareil dans la liste des appareils hello dans le tableau de bord de solution hello. Ensuite, dans hello **détails de l’appareil** du panneau, cliquez sur **activer le périphérique**. Hello de votre appareil est maintenant **en cours d’exécution**. solution de surveillance à distance Hello peut maintenant recevoir les données de télémétrie à partir de votre appareil et d’appeler des méthodes sur l’appareil de hello.

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/