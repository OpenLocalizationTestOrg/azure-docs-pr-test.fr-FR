## <a name="view-hello-solution-dashboard"></a>Tableau de bord View hello solution

tableau de bord Hello solution vous permet de solution de hello déployé toomanage. Par exemple, vous pouvez afficher les données de télémétrie, ajouter des appareils et appeler des méthodes.

1. Lorsque l’approvisionnement hello est terminé et vignette hello pour votre solution préconfigurée indique **prêt**, choisissez **lancer** tooopen votre portail de solution de surveillance à distance dans un nouvel onglet.

    ![Lancer la solution de hello préconfiguré][img-launch-solution]

1. Par défaut, portail de solution hello affiche hello *tableau de bord*. Accédez tooother des zones du portail de solution hello à l’aide du menu de hello sur la partie gauche de la page de hello hello.

    ![Tableau de bord de solution préconfigurée de surveillance à distance][img-menu]

## <a name="add-a-device"></a>Ajout d’un appareil

Pour une solution toohello préconfiguré tooconnect des appareils, il doit s’identifier tooIoT concentrateur à l’aide des informations d’identification valides. Vous pouvez récupérer les informations d’identification de périphérique hello à partir du tableau de bord de solution hello. Pour inclure des informations d’identification de périphérique hello dans votre application cliente, plus loin dans ce didacticiel.

tooadd une solution d’analyse à distance tooyour périphérique, hello complet suivant les étapes dans le tableau de bord de solution hello :

1. Dans hello coin inférieur gauche du tableau de bord hello, cliquez sur **ajouter un périphérique**.

   ![Ajout d’un appareil][1]

1. Bonjour **personnalisé appareil** du panneau, cliquez sur **ajouter un nouveau**.

   ![Ajout d’un appareil personnalisé][2]

1. Choisissez **Me laisser définir mon propre ID d'appareil**. Entrez un ID de périphérique tel **device01**, cliquez sur **vérifier l’ID** tooverify vous n’avez pas déjà utilisé le nom de hello dans votre solution, puis cliquez sur **créer** appareil de hello tooprovision.

   ![Ajouter ID d’appareil][3]

1. Rendre un périphérique de hello Remarque informations d’identification (**ID de périphérique**, **nom d’hôte du Hub IoT**, et **clé de périphérique**). Votre application cliente sur hello Intel NUC doit ces toohello tooconnect de valeurs solution de surveillance à distance. Cliquez ensuite sur **Terminé**.

    ![Afficher les informations d’identification d’un appareil][4]

1. Sélectionnez votre appareil dans la liste des appareils hello dans le tableau de bord de solution hello. Ensuite, dans hello **détails de l’appareil** du panneau, cliquez sur **activer le périphérique**. Hello de votre appareil est maintenant **en cours d’exécution**. solution de surveillance à distance Hello peut maintenant recevoir les données de télémétrie à partir de votre appareil et d’appeler des méthodes sur l’appareil de hello.

[img-launch-solution]: media/iot-suite-gateway-kit-view-solution/launch.png
[img-menu]: media/iot-suite-gateway-kit-view-solution/menu.png
[1]: media/iot-suite-gateway-kit-view-solution/suite0.png
[2]: media/iot-suite-gateway-kit-view-solution/suite1.png
[3]: media/iot-suite-gateway-kit-view-solution/suite2.png
[4]: media/iot-suite-gateway-kit-view-solution/suite3.png