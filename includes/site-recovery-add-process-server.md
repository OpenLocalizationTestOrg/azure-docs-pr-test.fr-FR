1. Lancez hello Azure Site Recovery UnifiedSetup.exe
2. Dans **avant de commencer**, sélectionnez **ajouter tooscale de serveurs de processus supplémentaire déploiement**.

  ![Ajouter un serveur de traitement](./media/site-recovery-add-process-server/ps-page-1.png)

3. Dans **détails du serveur de Configuration**, spécifiez l’adresse IP de hello du serveur de Configuration de hello et hello phrase secrète.

  ![Ajouter un serveur de traitement 2](./media/site-recovery-add-process-server/ps-page-2.png)
4. Dans **paramètres Internet**, spécifiez comment hello fournisseur en cours d’exécution sur le serveur de Configuration de hello connecte tooAzure Site Recovery via hello Internet.

  ![Ajouter un serveur de traitement 3](./media/site-recovery-add-process-server/ps-page-3.png)

   * Si vous souhaitez tooconnect avec proxy hello est actuellement configuré sur l’ordinateur de hello, sélectionnez **se connecter avec des paramètres proxy existants**.
   * Si vous souhaitez hello fournisseur tooconnect directement, sélectionnez **se connecter directement sans proxy**.
   * Si le proxy existant de hello requiert une authentification, ou si vous souhaitez toouse un proxy personnalisé pour la connexion du fournisseur hello, sélectionnez **se connecter avec les paramètres de proxy personnalisés**.

     * Si vous utilisez un proxy personnalisé, vous avez besoin d’informations d’identification, le port et adresse de hello toospecify.
     * Si vous utilisez un proxy, vous devez ont déjà accès toohello service URL autorisées.

5. Dans **vérification**, le programme d’installation exécute une vérification toomake assurer que l’installation peut exécuter. Si un avertissement s’affiche sur hello **vérification de la synchronisation temporelle globale**, vérifiez cette heure hello sur l’horloge système hello (**Date et heure** paramètres) est identique à hello en tant que le fuseau horaire de hello.

     ![Ajouter un serveur de traitement 4](./media/site-recovery-add-process-server/ps-page-4.png)

6. Dans **détails de l’environnement**, indiquez si vous souhaitez tooreplicate les ordinateurs virtuels VMware. Si c’est le cas, le programme d’installation vérifie que PowerCLI 6.0 est installé.

     ![Ajouter un serveur de traitement 5](./media/site-recovery-add-process-server/ps-page-5.png)

7. Dans **l’emplacement d’installation**, sélectionnez où vous souhaitez que les fichiers binaires de tooinstall hello et stockez le cache de hello. lecteur Hello que vous sélectionnez doit avoir au moins 5 Go d’espace disque disponible, mais nous vous recommandons d’un lecteur de cache au moins 600 Go d’espace libre.
     ![Ajouter un serveur de traitement 5](./media/site-recovery-add-process-server/ps-page-6.png)

8. Dans **sélection du réseau**, spécifiez l’écouteur hello (carte réseau et port SSL) sur le serveur de Configuration, hello envoie et reçoit des données de réplication. Port 9443 est le port par défaut de hello utilisé pour envoyer et recevoir le trafic de réplication, mais vous pouvez modifier cette toosuit de numéro de port les exigences de votre environnement. Dans le port toohello d’addition 9443, nous permet également d’ouvrir le port 443, qui est utilisé par les opérations de réplication tooorchestrate un serveur web. N’utilisez pas le port 443 pour envoyer ou recevoir le trafic de réplication.

     ![Ajouter un serveur de traitement 6](./media/site-recovery-add-process-server/ps-page-7.png)
9. Dans **Résumé**, passez en revue les informations hello et cliquez sur **installer**. Une fois l’installation terminée, une phrase secrète est générée. Vous en aurez besoin lorsque vous activerez la réplication. Par conséquent, copiez-la et conservez-la en lieu sûr.

     ![Ajouter un serveur de traitement 7](./media/site-recovery-add-process-server/ps-page-8.png)
