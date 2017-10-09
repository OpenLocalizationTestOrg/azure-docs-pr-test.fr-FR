# <a name="make-a-remote-connection-tooa-kubernetes-dcos-or-docker-swarm-cluster"></a>Création d’un cluster de Kubernetes, contrôleur de domaine/système d’exploitation ou Docker Swarm de tooa connexion à distance
Après avoir créé un cluster du Service de conteneur Azure, vous devez tooconnect toohello cluster toodeploy et gérez des charges de travail. Cet article décrit comment tooconnect toohello master VM de hello de cluster à partir d’un ordinateur distant. 

les clusters Kubernetes, contrôleur de domaine/système d’exploitation et Docker Swarm Hello fournissent des points de terminaison HTTP localement. Kubernetes, ce point de terminaison est en toute sécurité exposée sur hello internet, et vous pouvez y accéder en exécutant hello `kubectl` outil de ligne de commande à partir de n’importe quel ordinateur connecté à internet. 

Pour le contrôleur de domaine/système d’exploitation et Docker Swarm, nous vous recommandons de créer un tunnel SSH (secure shell) à partir de votre système de gestion de cluster toohello ordinateur local. Une fois hello tunnel établi, vous pouvez exécuter des commandes qui utilisent des points de terminaison HTTP hello et interface d’orchestrator vue hello web (si disponible) de votre système local. 

## <a name="prerequisites"></a>Composants requis

* Un cluster Kubernetes, DC/OS ou Docker Swarm [déployé dans Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).
* SSH RSA fichier de clé privée, correspondant toohello toohello ajouté de clé publique cluster pendant le déploiement. Ces commandes partent du principe que clé SSH privée de hello est `$HOME/.ssh/id_rsa` sur votre ordinateur. Pour plus d’informations, consultez ces instructions pour [macOS et Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) ou [Windows](../articles/virtual-machines/linux/ssh-from-windows.md). Si vous ne fonctionne pas hello connexion SSH, vous devrez peut-être trop [réinitialiser vos clés SSH](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).

## <a name="connect-tooa-kubernetes-cluster"></a>Se connecter tooa Kubernetes cluster

Suivez ces étapes tooinstall et configurer `kubectl` sur votre ordinateur.

> [!NOTE] 
> Sur Linux ou macOS, vous devrez peut-être les commandes de hello toorun dans cette section à l’aide de `sudo`.
> 

### <a name="install-kubectl"></a>Installer kubectl
Une façon tooinstall cet outil est toouse hello `az acs kubernetes install-cli` commande Azure CLI 2.0. toorun cette commande, assurez-vous que vous [installé](/cli/azure/install-az-cli2) hello dernière Azure CLI 2.0 et consigné dans tooan compte Azure (`az login`).

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

Ou bien, vous pouvez télécharger hello dernières `kubectl` client directement à partir de hello [Kubernetes libère page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md). Pour plus d’informations, consultez [Installation et configuration de kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).

### <a name="download-cluster-credentials"></a>Télécharger des informations d’identification du cluster
Une fois que vous avez `kubectl` installé, vous avez besoin d’informations d’identification tooyour ordinateur de toocopy hello cluster. Informations d’identification de toodo monodirectionnelle get hello est avec hello `az acs kubernetes get-credentials` commande. Passez le nom hello hello du groupe de ressources et le nom hello de ressource de service de conteneur hello :

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

Cette commande télécharge les informations d’identification du cluster hello trop`$HOME/.kube/config`, où `kubectl` attend qu’il toobe situé.

Vous pouvez également utiliser `scp` toosecurely copiez le fichier hello de `$HOME/.kube/config` sur l’ordinateur local hello master virtuelle tooyour. Par exemple :

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

Si vous êtes sous Windows, vous pouvez utiliser l’interpréteur de commandes sur Ubuntu sur Windows, client de copie de fichiers sécurisé PuTTy hello ou un outil similaire.

### <a name="use-kubectl"></a>Utiliser kubectl

Une fois que vous avez `kubectl` configuré, tester la connexion de hello en répertoriant les nœuds hello dans votre cluster :

```bash
kubectl get nodes
```

Vous pouvez essayer d’autres commandes `kubectl`. Par exemple, vous pouvez afficher hello Kubernetes le tableau de bord. Tout d’abord, exécutez un proxy de serveur de l’API de Kubernetes toohello :

```bash
kubectl proxy
```

Hello Kubernetes UI est désormais disponible à l’adresse : `http://localhost:8001/ui`.

Pour plus d’informations, consultez hello [Kubernetes de démarrage rapide](http://kubernetes.io/docs/user-guide/quick-start/).

## <a name="connect-tooa-dcos-or-swarm-cluster"></a>Connecter le cluster de contrôleur de domaine/système d’exploitation ou essaim tooa

toouse hello contrôleur de domaine/système d’exploitation et les clusters Docker Swarm déployées par le Service de conteneur Azure, suivez ces instructions de toocreate un tunnel SSH à partir de votre système local de Windows, Mac OS ou Linux. 

> [!NOTE]
> Ces instructions se concentrent sur le tunnel du trafic TCP via SSH. Vous pouvez également démarrer une session SSH interactive avec l’un des systèmes de gestion de cluster interne hello, mais nous ne recommandons pas cela. Le fait de travailler directement sur un système interne risque de provoquer des modifications de configuration accidentelles.  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a>Créer un tunnel SSH sur Linux ou macOS
Hello première chose que vous effectuez lorsque vous créez un tunnel SSH sur Linux ou macOS est toolocate hello nom DNS public de masques d’équilibrage de la charge hello. Procédez comme suit :


1. Bonjour [portail Azure](https://portal.azure.com), parcourir le groupe de ressources toohello contenant votre cluster de service de conteneur. Développez le groupe de ressources hello afin que chaque ressource est affichée. 

2. Cliquez sur hello **service de conteneur** ressource, puis cliquez sur **vue d’ensemble**. Hello **Master FQDN** Hello cluster apparaît sous **Essentials**. Enregistrez ce nom pour pouvoir l’utiliser ultérieurement. 

    ![Nom DNS public](./media/container-service-connect/pubdns.png)

    Vous pouvez également exécuter hello `az acs show` commande sur votre service de conteneur. Recherchez hello **profil : nom de domaine complet principal** propriété dans la sortie de la commande hello.

3. Ouvrez un interpréteur de commandes et exécutez hello `ssh` commande en spécifiant hello valeurs suivantes : 

    **LOCAL_PORT** est le port TCP hello côté service de hello de tooconnect de tunnel hello pour. Pour essaim, définissez cette too2375. Pour le contrôleur de domaine/système d’exploitation, définissez cette too80. 
    **REMOTE_PORT** port hello du point de terminaison hello que vous souhaitez tooexpose. Pour Swarm, utilisez le port 2375. Pour DC/OS, utilisez le port 80.  
    **Nom d’utilisateur** est le nom d’utilisateur hello qui a été fourni lors du déploiement de cluster de hello.  
    **DNSPREFIX** est le préfixe du DNS hello que vous avez fourni lors du déploiement de cluster de hello.  
    **RÉGION** est la région de hello dans lequel se trouve votre groupe de ressources.  
    **PATH_TO_PRIVATE_KEY** [facultatif] est hello chemin d’accès toohello clé privée qui correspond la clé publique de toohello vous avez fourni lors de la création de cluster de hello. Utilisez cette option avec hello `-i` indicateur.

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > Hello port de connexion SSH est 2200 et pas hello port standard 22. Dans un cluster avec plusieurs machines virtuelles principal, il s’agit de hello connexion port toohello premier masque de machine virtuelle.
  > 

  commande Hello retourne sans sortie.

Consultez les exemples de hello pour le contrôleur de domaine/système d’exploitation et essaim Bonjour les sections suivantes.    

### <a name="dcos-tunnel"></a>Tunnel DC/OS
tooopen un tunnel pour les points de terminaison de contrôleur de domaine/système d’exploitation, exécutez une commande hello suivante :

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> Vérifiez qu’aucun autre processus local n’est lié au port 80. Si nécessaire, vous pouvez spécifier un port local autre que le port 80, tel que le port 8080. Toutefois, certains liens de l’interface utilisateur web risquent de ne pas fonctionner si vous utilisez ce port.
>

Vous pouvez désormais accéder aux points de terminaison hello contrôleur de domaine/système d’exploitation à partir de votre système local via hello (en supposant que le port local 80) des URL suivantes :

* DC/OS : `http://localhost:80/`
* Marathon : `http://localhost:80/marathon`
* Mesos : `http://localhost:80/mesos`

De même, vous pouvez atteindre les API rest de hello pour chaque application via ce tunnel.

### <a name="swarm-tunnel"></a>Tunnel Swarm
tooopen un point de terminaison tunnel toohello essaim, exécuter une commande hello suivante :

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> Vérifiez qu’aucun autre processus local n’est lié au port 2375. Par exemple, si vous exécutez localement démon Docker de hello, elle est définie par le port de toouse par défaut 2375. Si nécessaire, vous pouvez spécifier un port local autre que le port 2375.
>

Vous pouvez désormais accéder aux cluster de Docker Swarm hello à l’aide d’une interface de ligne hello Docker (CLI Docker) sur votre système local. Pour obtenir des instructions d’installation, consultez [Installation de Docker](https://docs.docker.com/engine/installation/).

Définissez votre toohello de variable environnement DOCKER_HOST port local que vous avez configuré pour un tunnel de hello. 

```bash
export DOCKER_HOST=:2375
```

Exécutez les commandes Docker ce cluster Docker Swarm de tunnel toohello. Par exemple :

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a>Créer un tunnel SSH sur Windows
Il existe plusieurs options de création des tunnels SSH sous Windows. Si vous exécutez un interpréteur de commandes sur Ubuntu sur Windows ou un outil similaire, vous pouvez suivre les instructions tunneling SSH hello indiquées plus haut dans cet article pour macOS et Linux. En guise d’alternative sur Windows, cette section décrit comment tunnel de hello toouse toocreate PuTTY.

1. [Télécharger PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour système Windows.

2. Exécutez l’application hello.

3. Entrez un nom d’hôte qui se compose de nom d’utilisateur admin hello cluster et hello nom DNS public du premier masque hello de cluster de hello. Hello **nom d’hôte** ressemble trop`azureuser@PublicDNSName`. Entrez 2200 pour hello **Port**.

    ![Configuration PuTTY 1](./media/container-service-connect/putty1.png)

4. Sélectionnez **SSH > Auth**. Ajoutez un chemin d’accès tooyour fichier de clé privée (format .ppk) pour l’authentification. Vous pouvez utiliser un outil tel que [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate ce fichier à partir de hello cluster de hello toocreate utilisé clé SSH.

    ![Configuration PuTTY 2](./media/container-service-connect/putty2.png)

5. Sélectionnez **SSH > Tunnels** configurez hello transféré les ports qui suit :

    * **Port source :** utilisez 80 pour DC/OS et 2375 pour Swarm.
    * **Destination :** utilisez localhost:80 pour DC/OS ou localhost:2375 pour Swarm.

    Hello, l’exemple suivant est configuré pour le contrôleur de domaine/système d’exploitation, mais il ressemblera pour Docker Swarm.

    > [!NOTE]
    > Le port 80 ne doit pas être en cours d’utilisation lors de la création de ce tunnel.
    > 

    ![Configuration PuTTY 3](./media/container-service-connect/putty3.png)

6. Lorsque vous avez terminé, cliquez sur **Session > Enregistrer** configuration de la connexion toosave hello.

7. tooconnect toohello PuTTY de session, cliquez sur **ouvrir**. Lorsque vous vous connectez, vous pouvez voir la configuration du port hello dans le journal des événements PuTTY hello.

    ![Journal des événements PuTTY](./media/container-service-connect/putty4.png)

Une fois que vous avez configuré le tunnel de hello pour le contrôleur de domaine/système d’exploitation, vous pouvez accéder à hello relatives des points de terminaison à :

* DC/OS : `http://localhost/`
* Marathon : `http://localhost/marathon`
* Mesos : `http://localhost/mesos`

Une fois que vous avez configuré le tunnel de hello pour Docker Swarm, ouvrez votre tooconfigure de paramètres Windows une variable d’environnement nommée `DOCKER_HOST` avec la valeur `:2375`. Ensuite, vous pouvez accéder cluster essaim de hello via hello Docker CLI.

## <a name="next-steps"></a>Étapes suivantes
Déployer et gérer des conteneurs dans votre cluster :

* [Gestion des conteneurs avec Kubernetes](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [Gestion de conteneur via l’API REST](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [Travailler avec hello Service de conteneur Azure et Docker Swarm](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

