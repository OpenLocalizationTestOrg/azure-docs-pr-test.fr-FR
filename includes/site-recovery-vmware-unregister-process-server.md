Hello étapes toounregister un serveur de processus diffère selon l’état de la connexion avec hello serveur de Configuration.

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a>Annuler l’inscription d’un serveur de traitement qui se trouve dans un état connecté

1. Accédez à distance au serveur de processus hello en tant qu’administrateur.
2. Lancez hello **le panneau de configuration** et ouvrez **programmes > désinstaller un programme**
3. Désinstaller un programme par le nom de hello **serveur/processus de Configuration de Microsoft Azure Site Recovery**
4. Une fois l’étape 3 terminée, vous pouvez désinstaller **Dépendances du serveur de configuration/traitement Microsoft Azure Site Recovery**

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a>Annuler l’inscription d’un serveur de traitement qui se trouve dans un état déconnecté

> [!WARNING]
> Hello utilisation étapes ci-dessous doit être utilisé s’il n’existe aucun moyen toorevive hello virtuels sur le hello serveur de processus a été installé.

1. Ouvrez une session sur le serveur de configuration tooyour en tant qu’administrateur.
2. Ouvrez une invite de commandes d’administration et de parcourir le répertoire de toohello `%ProgramData%\ASR\home\svsystems\bin`.
3. Maintenant, exécutez les commandes hello.

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. Cela effacera détails hello hello du serveur de processus à partir du système de hello.
