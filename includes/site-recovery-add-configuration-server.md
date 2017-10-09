1. Exécutez le fichier d’installation du programme d’installation unifiée de hello.
2. Dans **avant de commencer**, sélectionnez **installer le serveur de configuration hello et serveur de processus**.

    ![Avant de commencer](./media/site-recovery-add-configuration-server/combined-wiz1.png)

3. Dans **licence de logiciel tiers**, cliquez sur **J’accepte** toodownload et installer MySQL.

    ![Logiciels tiers](./media/site-recovery-add-configuration-server/combined-wiz2.png)
4. Dans **inscription**, sélectionnez la clé d’enregistrement hello vous avez téléchargé à partir du coffre de hello.

    ![Inscription](./media/site-recovery-add-configuration-server/combined-wiz3.png)
5. Dans **paramètres Internet**, spécifiez comment hello fournisseur en cours d’exécution sur le serveur de configuration hello connecte tooAzure Site Recovery via hello Internet.

   a. Si vous souhaitez tooconnect avec proxy hello est actuellement configuré sur l’ordinateur de hello, sélectionnez **tooAzure Site Recovery à l’aide d’un serveur proxy de connexion**.

   b. Si vous souhaitez hello fournisseur tooconnect directement, sélectionnez **vous connecter directement tooAzure Site Recovery sans un serveur proxy**.

   c. Si le proxy existant de hello requiert une authentification, ou si vous souhaitez toouse un proxy personnalisé pour la connexion du fournisseur hello, sélectionnez **se connecter avec les paramètres de proxy personnalisés**.

     * Si vous utilisez un proxy personnalisé, vous avez besoin d’informations d’identification, le port et adresse de hello toospecify.
     * Si vous utilisez un proxy, vous devez avoir déjà hello URL autorisées décrites dans [conditions préalables](#prerequisites).

     ![Pare-feu](./media/site-recovery-add-configuration-server/combined-wiz4.png)
6. Dans **vérification**, le programme d’installation exécute une vérification toomake assurer que l’installation peut exécuter. Si un avertissement s’affiche sur hello **vérification de la synchronisation temporelle globale**, vérifiez cette heure hello sur l’horloge système hello (**Date et heure** paramètres) est identique à hello en tant que le fuseau horaire de hello.

    ![Composants requis](./media/site-recovery-add-configuration-server/combined-wiz5.png)
7. Dans **MySQL Configuration**, créer des informations d’identification d’ouverture de session d’instance toohello MySQL server est installé.

    ![MySQL](./media/site-recovery-add-configuration-server/combined-wiz6.png)
8. Dans **détails de l’environnement**, indiquez si vous souhaitez tooreplicate les ordinateurs virtuels VMware. Si c’est le cas, le programme d’installation vérifie que PowerCLI 6.0 est installé.

    ![MySQL](./media/site-recovery-add-configuration-server/combined-wiz7.png)

9. Dans **l’emplacement d’installation**, sélectionnez où vous souhaitez que les fichiers binaires de tooinstall hello et stockez le cache de hello. lecteur Hello que vous sélectionnez doit avoir au moins 5 Go d’espace disque disponible, mais nous vous recommandons d’un lecteur de cache au moins 600 Go d’espace libre.

    ![Emplacement d’installation](./media/site-recovery-add-configuration-server/combined-wiz8.png)
10. Dans **sélection du réseau**, spécifiez l’écouteur hello (carte réseau et port SSL) sur le serveur de configuration hello envoie et reçoit des données de réplication. Port 9443 est le port par défaut de hello utilisé pour envoyer et recevoir le trafic de réplication, mais vous pouvez modifier cette toosuit de numéro de port les exigences de votre environnement. Dans le port toohello d’addition 9443, nous permet également d’ouvrir le port 443, qui est utilisé par les opérations de réplication tooorchestrate un serveur web. N’utilisez pas le port 443 pour envoyer ou recevoir le trafic de réplication.

    ![Sélection du réseau](./media/site-recovery-add-configuration-server/combined-wiz9.png)


11. Dans **Résumé**, passez en revue les informations hello et cliquez sur **installer**. Une fois l’installation terminée, une phrase secrète est générée. Vous en aurez besoin lorsque vous activerez la réplication. Par conséquent, copiez-la et conservez-la en lieu sûr.

    ![Résumé](./media/site-recovery-add-configuration-server/combined-wiz10.png)

Une fois l’inscription terminée, le serveur de hello s’affiche sur hello **paramètres** > **serveurs** panneau dans le coffre hello.
