<span data-ttu-id="4812e-101">Hello étapes toounregister un serveur de processus diffère selon l’état de la connexion avec hello serveur de Configuration.</span><span class="sxs-lookup"><span data-stu-id="4812e-101">hello steps toounregister a process server differs depending on its connection status with hello Configuration Server.</span></span>

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a><span data-ttu-id="4812e-102">Annuler l’inscription d’un serveur de traitement qui se trouve dans un état connecté</span><span class="sxs-lookup"><span data-stu-id="4812e-102">Unregister a process server that is in a connected state</span></span>

1. <span data-ttu-id="4812e-103">Accédez à distance au serveur de processus hello en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="4812e-103">Remote into hello process server as an Administrator.</span></span>
2. <span data-ttu-id="4812e-104">Lancez hello **le panneau de configuration** et ouvrez **programmes > désinstaller un programme**</span><span class="sxs-lookup"><span data-stu-id="4812e-104">Launch hello **Control Panel** and open **Programs > Uninstall a program**</span></span>
3. <span data-ttu-id="4812e-105">Désinstaller un programme par le nom de hello **serveur/processus de Configuration de Microsoft Azure Site Recovery**</span><span class="sxs-lookup"><span data-stu-id="4812e-105">Uninstall a program by hello name **Microsoft Azure Site Recovery Configuration/Process Server**</span></span>
4. <span data-ttu-id="4812e-106">Une fois l’étape 3 terminée, vous pouvez désinstaller **Dépendances du serveur de configuration/traitement Microsoft Azure Site Recovery**</span><span class="sxs-lookup"><span data-stu-id="4812e-106">Once step 3 is completed, you can uninstall **Microsoft Azure Site Recovery Configuration/Process Server Dependencies**</span></span>

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a><span data-ttu-id="4812e-107">Annuler l’inscription d’un serveur de traitement qui se trouve dans un état déconnecté</span><span class="sxs-lookup"><span data-stu-id="4812e-107">Unregister a process server that is in a disconnected state</span></span>

> [!WARNING]
> <span data-ttu-id="4812e-108">Hello utilisation étapes ci-dessous doit être utilisé s’il n’existe aucun moyen toorevive hello virtuels sur le hello serveur de processus a été installé.</span><span class="sxs-lookup"><span data-stu-id="4812e-108">Use hello below steps should be used if there is no way toorevive hello virtual machine on which hello Process Server was installed.</span></span>

1. <span data-ttu-id="4812e-109">Ouvrez une session sur le serveur de configuration tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="4812e-109">Log on tooyour configuration server as an Administrator.</span></span>
2. <span data-ttu-id="4812e-110">Ouvrez une invite de commandes d’administration et de parcourir le répertoire de toohello `%ProgramData%\ASR\home\svsystems\bin`.</span><span class="sxs-lookup"><span data-stu-id="4812e-110">Open an Administrative command prompt and browse toohello directory `%ProgramData%\ASR\home\svsystems\bin`.</span></span>
3. <span data-ttu-id="4812e-111">Maintenant, exécutez les commandes hello.</span><span class="sxs-lookup"><span data-stu-id="4812e-111">Now run hello command.</span></span>

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. <span data-ttu-id="4812e-112">Cela effacera détails hello hello du serveur de processus à partir du système de hello.</span><span class="sxs-lookup"><span data-stu-id="4812e-112">This will purge hello details of hello process server from hello system.</span></span>
