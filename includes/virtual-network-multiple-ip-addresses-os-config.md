## <span data-ttu-id="de53c-101"><a name="os-config"></a>Ajouter le système d’exploitation VM IP adresses tooa</span><span class="sxs-lookup"><span data-stu-id="de53c-101"><a name="os-config"></a>Add IP addresses tooa VM operating system</span></span>

<span data-ttu-id="de53c-102">Se connecter et connexion tooa machine virtuelle que vous avez créé avec plusieurs adresses IP privées.</span><span class="sxs-lookup"><span data-stu-id="de53c-102">Connect and login tooa VM you created with multiple private IP addresses.</span></span> <span data-ttu-id="de53c-103">Vous devez ajouter manuellement tous les hello des adresses IP privées (y compris hello principal) que vous avez ajouté toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="de53c-103">You must manually add all hello private IP addresses (including hello primary) that you added toohello VM.</span></span> <span data-ttu-id="de53c-104">Hello complète pour votre système d’exploitation de machine virtuelle comme suit :</span><span class="sxs-lookup"><span data-stu-id="de53c-104">Complete hello following steps for your VM operating system:</span></span>

### <a name="windows"></a><span data-ttu-id="de53c-105">Windows</span><span class="sxs-lookup"><span data-stu-id="de53c-105">Windows</span></span>

1. <span data-ttu-id="de53c-106">Tapez *ipconfig /all*à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="de53c-106">From a command prompt, type *ipconfig /all*.</span></span>  <span data-ttu-id="de53c-107">Vous ne voyez que hello *principal* une adresse IP privée (via DHCP).</span><span class="sxs-lookup"><span data-stu-id="de53c-107">You only see hello *Primary* private IP address (through DHCP).</span></span>
2. <span data-ttu-id="de53c-108">Type *ncpa.cpl* Bonjour de hello invite de commandes tooopen **des connexions réseau** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="de53c-108">Type *ncpa.cpl* in hello command prompt tooopen hello **Network connections** window.</span></span>
3. <span data-ttu-id="de53c-109">Ouvrez les propriétés de hello pour l’adaptateur approprié hello : **connexion au réseau Local**.</span><span class="sxs-lookup"><span data-stu-id="de53c-109">Open hello properties for hello appropriate adapter: **Local Area Connection**.</span></span>
4. <span data-ttu-id="de53c-110">Double-cliquez sur Internet Protocol version 4 (IPv4).</span><span class="sxs-lookup"><span data-stu-id="de53c-110">Double-click Internet Protocol version 4 (IPv4).</span></span>
5. <span data-ttu-id="de53c-111">Sélectionnez **hello utilisation adresse IP suivante** et entrez hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="de53c-111">Select **Use hello following IP address** and enter hello following values:</span></span>

    * <span data-ttu-id="de53c-112">**Adresse IP**: entrez hello *principal* adresse IP privée</span><span class="sxs-lookup"><span data-stu-id="de53c-112">**IP address**: Enter hello *Primary* private IP address</span></span>
    * <span data-ttu-id="de53c-113">**Masque de sous-réseau**: définissez cette option en fonction de votre sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="de53c-113">**Subnet mask**: Set based on your subnet.</span></span> <span data-ttu-id="de53c-114">Par exemple, si hello sous-réseau est un /24 sous-réseau puis le sous-réseau de hello masque est 255.255.255.0.</span><span class="sxs-lookup"><span data-stu-id="de53c-114">For example, if hello subnet is a /24 subnet then hello subnet mask is 255.255.255.0.</span></span>
    * <span data-ttu-id="de53c-115">**Passerelle par défaut**: hello la première adresse IP de sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="de53c-115">**Default gateway**: hello first IP address in hello subnet.</span></span> <span data-ttu-id="de53c-116">Si votre sous-réseau est 10.0.0.0/24, adresse IP de passerelle hello est 10.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="de53c-116">If your subnet is 10.0.0.0/24, then hello gateway IP address is 10.0.0.1.</span></span>
    * <span data-ttu-id="de53c-117">Cliquez sur **hello utilisation suivant des adresses de serveur DNS** et entrez hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="de53c-117">Click **Use hello following DNS server addresses** and enter hello following values:</span></span>
        * <span data-ttu-id="de53c-118">**Serveur DNS préféré** : saisissez 168.63.129.16 si vous n’utilisez pas votre propre serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="de53c-118">**Preferred DNS server**: If you are not using your own DNS server, enter 168.63.129.16.</span></span>  <span data-ttu-id="de53c-119">Si vous utilisez votre propre serveur DNS, entrez l’adresse IP de hello pour votre serveur.</span><span class="sxs-lookup"><span data-stu-id="de53c-119">If you are using your own DNS server, enter hello IP address for your server.</span></span>
    * <span data-ttu-id="de53c-120">Cliquez sur hello **avancé** bouton et ajouter des adresses IP supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="de53c-120">Click hello **Advanced** button and add additional IP addresses.</span></span> <span data-ttu-id="de53c-121">Ajouter chaque hello secondaire des adresses IP privées répertoriés dans l’étape 8 toohello carte réseau avec hello même sous-réseau spécifié pour l’adresse IP principale hello.</span><span class="sxs-lookup"><span data-stu-id="de53c-121">Add each of hello secondary private IP addresses listed in step 8 toohello NIC with hello same subnet specified for hello primary IP address.</span></span>
        >[!WARNING] 
        ><span data-ttu-id="de53c-122">Si vous ne suivez pas les étapes hello ci-dessus correctement, vous risquez de perdre connectivité tooyour machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="de53c-122">If you do not follow hello steps above correctly, you may lose connectivity tooyour VM.</span></span> <span data-ttu-id="de53c-123">Vérifiez les informations de hello tapées à l’étape 5 sont correctes avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="de53c-123">Ensure hello information entered for step 5 is accurate before proceeding.</span></span>

    * <span data-ttu-id="de53c-124">Cliquez sur **OK** tooclose les paramètres TCP/IP de hello, puis **OK** tooclose à nouveau les paramètres de carte hello.</span><span class="sxs-lookup"><span data-stu-id="de53c-124">Click **OK** tooclose out hello TCP/IP settings and then **OK** again tooclose hello adapter settings.</span></span> <span data-ttu-id="de53c-125">Votre connexion RDP est rétablie.</span><span class="sxs-lookup"><span data-stu-id="de53c-125">Your RDP connection is re-established.</span></span>

6. <span data-ttu-id="de53c-126">Tapez *ipconfig /all*à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="de53c-126">From a command prompt, type *ipconfig /all*.</span></span> <span data-ttu-id="de53c-127">Toutes les adresses IP que vous avez ajoutées sont affichées et le protocole DHCP est désactivé.</span><span class="sxs-lookup"><span data-stu-id="de53c-127">All IP addresses you added are shown and DHCP is turned off.</span></span>


### <a name="validation-windows"></a><span data-ttu-id="de53c-128">Validation (Windows)</span><span class="sxs-lookup"><span data-stu-id="de53c-128">Validation (Windows)</span></span>

<span data-ttu-id="de53c-129">tooensure toohello tooconnect en mesure d’internet à partir de votre configuration IP secondaire via hello qu'adresse IP publique associée, une fois que vous avez ajouté correctement à l’aide des étapes ci-dessus, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="de53c-129">tooensure you are able tooconnect toohello internet from your secondary IP configuration via hello public IP associated it, once you have added it correctly using steps above, use hello following command:</span></span>

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="de53c-130">Pour les configurations IP secondaires, vous pouvez uniquement effectuer un ping toohello Internet si la configuration de hello possède une adresse IP publique associée.</span><span class="sxs-lookup"><span data-stu-id="de53c-130">For secondary IP configurations, you can only ping toohello Internet if hello configuration has a public IP address associated with it.</span></span> <span data-ttu-id="de53c-131">Pour les configurations IP principales, une adresse IP publique n’est pas requis tooping toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="de53c-131">For primary IP configurations, a public IP address is not required tooping toohello Internet.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="de53c-132">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="de53c-132">Linux (Ubuntu)</span></span>

1. <span data-ttu-id="de53c-133">Ouvrez une fenêtre de terminal.</span><span class="sxs-lookup"><span data-stu-id="de53c-133">Open a terminal window.</span></span>
2. <span data-ttu-id="de53c-134">Assurez-vous que vous êtes hello racine utilisateur.</span><span class="sxs-lookup"><span data-stu-id="de53c-134">Make sure you are hello root user.</span></span> <span data-ttu-id="de53c-135">Si vous n’êtes pas le cas, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="de53c-135">If you are not, enter hello following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="de53c-136">Mettre à jour le fichier de configuration hello d’interface de réseau hello (en supposant « eth0 »).</span><span class="sxs-lookup"><span data-stu-id="de53c-136">Update hello configuration file of hello network interface (assuming ‘eth0’).</span></span>

    * <span data-ttu-id="de53c-137">Gardez à l’élément de ligne existante hello pour dhcp.</span><span class="sxs-lookup"><span data-stu-id="de53c-137">Keep hello existing line item for dhcp.</span></span> <span data-ttu-id="de53c-138">l’adresse IP principale Hello configuration reste telle qu’elle était précédemment.</span><span class="sxs-lookup"><span data-stu-id="de53c-138">hello primary IP address remains configured as it was previously.</span></span>
    * <span data-ttu-id="de53c-139">Ajoutez une configuration pour une adresse IP statique supplémentaire avec hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="de53c-139">Add a configuration for an additional static IP address with hello following commands:</span></span>

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    <span data-ttu-id="de53c-140">Un fichier .cfg doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="de53c-140">You should see a .cfg file.</span></span>
4. <span data-ttu-id="de53c-141">Fichier de hello ouvert.</span><span class="sxs-lookup"><span data-stu-id="de53c-141">Open hello file.</span></span> <span data-ttu-id="de53c-142">Vous devez voir hello lignes à fin hello du fichier de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="de53c-142">You should see hello following lines at hello end of hello file:</span></span>

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. <span data-ttu-id="de53c-143">Ajoutez hello lignes suivantes après lignes hello qui existent dans ce fichier :</span><span class="sxs-lookup"><span data-stu-id="de53c-143">Add hello following lines after hello lines that exist in this file:</span></span>

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. <span data-ttu-id="de53c-144">Enregistrer le fichier de hello à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="de53c-144">Save hello file by using hello following command:</span></span>

    ```bash
    :wq
    ```

7. <span data-ttu-id="de53c-145">Réinitialiser l’interface de réseau hello avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="de53c-145">Reset hello network interface with hello following command:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="de53c-146">Exécutez ifdown et ifup Bonjour même ligne si vous utilisez une connexion à distance.</span><span class="sxs-lookup"><span data-stu-id="de53c-146">Run both ifdown and ifup in hello same line if using a remote connection.</span></span>
    >

8. <span data-ttu-id="de53c-147">Vérifiez l’adresse hello est ajoutée à interface de réseau toohello avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="de53c-147">Verify hello IP address is added toohello network interface with hello following command:</span></span>

    ```bash
    ip addr list eth0
    ```

    <span data-ttu-id="de53c-148">Vous devez voir hello IP adresse que vous avez ajoutés en tant que partie de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="de53c-148">You should see hello IP address you added as part of hello list.</span></span>

### <a name="linux-redhat-centos-and-others"></a><span data-ttu-id="de53c-149">Linux (Redhat, CentOS, etc.)</span><span class="sxs-lookup"><span data-stu-id="de53c-149">Linux (Redhat, CentOS, and others)</span></span>

1. <span data-ttu-id="de53c-150">Ouvrez une fenêtre de terminal.</span><span class="sxs-lookup"><span data-stu-id="de53c-150">Open a terminal window.</span></span>
2. <span data-ttu-id="de53c-151">Assurez-vous que vous êtes hello racine utilisateur.</span><span class="sxs-lookup"><span data-stu-id="de53c-151">Make sure you are hello root user.</span></span> <span data-ttu-id="de53c-152">Si vous n’êtes pas le cas, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="de53c-152">If you are not, enter hello following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="de53c-153">Entrez votre mot de passe et suivez les instructions qui s’affichent.</span><span class="sxs-lookup"><span data-stu-id="de53c-153">Enter your password and follow instructions as prompted.</span></span> <span data-ttu-id="de53c-154">Une fois l’utilisateur racine de hello, accédez dossier scripts de réseau toohello avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="de53c-154">Once you are hello root user, navigate toohello network scripts folder with hello following command:</span></span>

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. <span data-ttu-id="de53c-155">Hello de la liste des fichiers associés à l’ifcfg à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="de53c-155">List hello related ifcfg files using hello following command:</span></span>

    ```bash
    ls ifcfg-*
    ```

    <span data-ttu-id="de53c-156">Vous devez voir *ifcfg-eth0* comme l’un des fichiers de hello.</span><span class="sxs-lookup"><span data-stu-id="de53c-156">You should see *ifcfg-eth0* as one of hello files.</span></span>

5. <span data-ttu-id="de53c-157">tooadd une adresse IP, créez un fichier de configuration pour qu’il comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="de53c-157">tooadd an IP address, create a configuration file for it as shown below.</span></span> <span data-ttu-id="de53c-158">Notez qu’un fichier doit être créé pour chaque configuration IP.</span><span class="sxs-lookup"><span data-stu-id="de53c-158">Note that one file must be created for each IP configuration.</span></span>

    ```bash
    touch ifcfg-eth0:0
    ```

6. <span data-ttu-id="de53c-159">Ouvrez hello *ifcfg-eth0:0* fichier avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="de53c-159">Open hello *ifcfg-eth0:0* file with hello following command:</span></span>

    ```bash
    vi ifcfg-eth0:0
    ```

7. <span data-ttu-id="de53c-160">Ajoutez le fichier de contenu toohello, *eth0:0* dans ce cas, par hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="de53c-160">Add content toohello file, *eth0:0* in this case, with hello following command.</span></span> <span data-ttu-id="de53c-161">Être tooupdate que les informations en fonction de votre adresse IP.</span><span class="sxs-lookup"><span data-stu-id="de53c-161">Be sure tooupdate information based on your IP address.</span></span>

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. <span data-ttu-id="de53c-162">Enregistrer le fichier de hello avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="de53c-162">Save hello file with hello following command:</span></span>

    ```bash
    :wq
    ```

9. <span data-ttu-id="de53c-163">Redémarrez les services réseau hello et assurez-vous que les modifications de hello sont réussies par hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="de53c-163">Restart hello network services and make sure hello changes are successful by running hello following commands:</span></span>

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    <span data-ttu-id="de53c-164">Vous devez voir hello IP adresse que vous avez ajouté, *eth0:0*, dans la liste hello retournée.</span><span class="sxs-lookup"><span data-stu-id="de53c-164">You should see hello IP address you added, *eth0:0*, in hello list returned.</span></span>

### <a name="validation-linux"></a><span data-ttu-id="de53c-165">Validation (Linux)</span><span class="sxs-lookup"><span data-stu-id="de53c-165">Validation (Linux)</span></span>

<span data-ttu-id="de53c-166">tooensure vous êtes en mesure de tooconnect toohello internet à partir de votre configuration IP secondaire via l’adresse IP publique hello associé, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="de53c-166">tooensure you are able tooconnect toohello internet from your secondary IP configuration via hello public IP associated it, use hello following command:</span></span>

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="de53c-167">Pour les configurations IP secondaires, vous pouvez uniquement effectuer un ping toohello Internet si la configuration de hello possède une adresse IP publique associée.</span><span class="sxs-lookup"><span data-stu-id="de53c-167">For secondary IP configurations, you can only ping toohello Internet if hello configuration has a public IP address associated with it.</span></span> <span data-ttu-id="de53c-168">Pour les configurations IP principales, une adresse IP publique n’est pas requis tooping toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="de53c-168">For primary IP configurations, a public IP address is not required tooping toohello Internet.</span></span>

<span data-ttu-id="de53c-169">Pour les machines virtuelles Linux, lors de la tentative de connexion sortante de toovalidate à partir d’une carte réseau secondaire, vous devrez peut-être tooadd les itinéraires appropriés.</span><span class="sxs-lookup"><span data-stu-id="de53c-169">For Linux VMs, when trying toovalidate outbound connectivity from a secondary NIC, you may need tooadd appropriate routes.</span></span> <span data-ttu-id="de53c-170">Il existe plusieurs façons toodo cela.</span><span class="sxs-lookup"><span data-stu-id="de53c-170">There are many ways toodo this.</span></span> <span data-ttu-id="de53c-171">Reportez-vous à la documentation appropriée pour votre distribution Linux.</span><span class="sxs-lookup"><span data-stu-id="de53c-171">Please see appropriate documentation for your Linux distribution.</span></span> <span data-ttu-id="de53c-172">suivant de Hello s’agit-il d’une méthode tooaccomplish :</span><span class="sxs-lookup"><span data-stu-id="de53c-172">hello following is one method tooaccomplish this:</span></span>

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- <span data-ttu-id="de53c-173">Être tooreplace que :</span><span class="sxs-lookup"><span data-stu-id="de53c-173">Be sure tooreplace:</span></span>
    - <span data-ttu-id="de53c-174">**10.0.0.5** avec hello privé adresse qui a une adresse IP publique adresse IP tooit associé</span><span class="sxs-lookup"><span data-stu-id="de53c-174">**10.0.0.5** with hello private IP address that has a public IP address associated tooit</span></span>
    - <span data-ttu-id="de53c-175">**10.0.0.1** passerelle par défaut de tooyour</span><span class="sxs-lookup"><span data-stu-id="de53c-175">**10.0.0.1** tooyour default gateway</span></span>
    - <span data-ttu-id="de53c-176">**eth2** nom toohello de votre carte réseau secondaire</span><span class="sxs-lookup"><span data-stu-id="de53c-176">**eth2** toohello name of your secondary NIC</span></span>
