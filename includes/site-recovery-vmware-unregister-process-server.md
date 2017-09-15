<span data-ttu-id="6d8d3-101">Les étapes d’annulation de l’inscription d’un serveur de traitement diffèrent en fonction de son état de connexion avec le serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="6d8d3-101">The steps to unregister a process server differs depending on its connection status with the Configuration Server.</span></span>

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a><span data-ttu-id="6d8d3-102">Annuler l’inscription d’un serveur de traitement qui se trouve dans un état connecté</span><span class="sxs-lookup"><span data-stu-id="6d8d3-102">Unregister a process server that is in a connected state</span></span>

1. <span data-ttu-id="6d8d3-103">Accédez à distance au serveur de traitement en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6d8d3-103">Remote into the process server as an Administrator.</span></span>
2. <span data-ttu-id="6d8d3-104">Démarrez le **Panneau de configuration** et ouvrez **Programmes > Désinstaller un programme**</span><span class="sxs-lookup"><span data-stu-id="6d8d3-104">Launch the **Control Panel** and open **Programs > Uninstall a program**</span></span>
3. <span data-ttu-id="6d8d3-105">Désinstallez le programme nommé **Serveur de configuration/traitement Microsoft Azure Site Recovery**</span><span class="sxs-lookup"><span data-stu-id="6d8d3-105">Uninstall a program by the name **Microsoft Azure Site Recovery Configuration/Process Server**</span></span>
4. <span data-ttu-id="6d8d3-106">Une fois l’étape 3 terminée, vous pouvez désinstaller **Dépendances du serveur de configuration/traitement Microsoft Azure Site Recovery**</span><span class="sxs-lookup"><span data-stu-id="6d8d3-106">Once step 3 is completed, you can uninstall **Microsoft Azure Site Recovery Configuration/Process Server Dependencies**</span></span>

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a><span data-ttu-id="6d8d3-107">Annuler l’inscription d’un serveur de traitement qui se trouve dans un état déconnecté</span><span class="sxs-lookup"><span data-stu-id="6d8d3-107">Unregister a process server that is in a disconnected state</span></span>

> [!WARNING]
> <span data-ttu-id="6d8d3-108">Utilisez les étapes ci-dessous s’il n’existe aucun moyen de réactiver la machine virtuelle sur laquelle le serveur de traitement a été installé.</span><span class="sxs-lookup"><span data-stu-id="6d8d3-108">Use the below steps should be used if there is no way to revive the virtual machine on which the Process Server was installed.</span></span>

1. <span data-ttu-id="6d8d3-109">Connectez-vous à votre serveur de configuration en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6d8d3-109">Log on to your configuration server as an Administrator.</span></span>
2. <span data-ttu-id="6d8d3-110">Ouvrez une invite de commande d’administration et accédez au répertoire `%ProgramData%\ASR\home\svsystems\bin`.</span><span class="sxs-lookup"><span data-stu-id="6d8d3-110">Open an Administrative command prompt and browse to the directory `%ProgramData%\ASR\home\svsystems\bin`.</span></span>
3. <span data-ttu-id="6d8d3-111">Ensuite, exécutez la commande.</span><span class="sxs-lookup"><span data-stu-id="6d8d3-111">Now run the command.</span></span>

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. <span data-ttu-id="6d8d3-112">Cette opération vide les informations du serveur de traitement du système.</span><span class="sxs-lookup"><span data-stu-id="6d8d3-112">This will purge the details of the process server from the system.</span></span>
