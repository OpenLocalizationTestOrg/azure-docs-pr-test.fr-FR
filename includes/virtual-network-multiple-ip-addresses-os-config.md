## <a name="os-config"></a>Ajouter le système d’exploitation VM IP adresses tooa

Se connecter et connexion tooa machine virtuelle que vous avez créé avec plusieurs adresses IP privées. Vous devez ajouter manuellement tous les hello des adresses IP privées (y compris hello principal) que vous avez ajouté toohello machine virtuelle. Hello complète pour votre système d’exploitation de machine virtuelle comme suit :

### <a name="windows"></a>Windows

1. Tapez *ipconfig /all*à l’invite de commandes.  Vous ne voyez que hello *principal* une adresse IP privée (via DHCP).
2. Type *ncpa.cpl* Bonjour de hello invite de commandes tooopen **des connexions réseau** fenêtre.
3. Ouvrez les propriétés de hello pour l’adaptateur approprié hello : **connexion au réseau Local**.
4. Double-cliquez sur Internet Protocol version 4 (IPv4).
5. Sélectionnez **hello utilisation adresse IP suivante** et entrez hello valeurs suivantes :

    * **Adresse IP**: entrez hello *principal* adresse IP privée
    * **Masque de sous-réseau**: définissez cette option en fonction de votre sous-réseau. Par exemple, si hello sous-réseau est un /24 sous-réseau puis le sous-réseau de hello masque est 255.255.255.0.
    * **Passerelle par défaut**: hello la première adresse IP de sous-réseau de hello. Si votre sous-réseau est 10.0.0.0/24, adresse IP de passerelle hello est 10.0.0.1.
    * Cliquez sur **hello utilisation suivant des adresses de serveur DNS** et entrez hello valeurs suivantes :
        * **Serveur DNS préféré** : saisissez 168.63.129.16 si vous n’utilisez pas votre propre serveur DNS.  Si vous utilisez votre propre serveur DNS, entrez l’adresse IP de hello pour votre serveur.
    * Cliquez sur hello **avancé** bouton et ajouter des adresses IP supplémentaires. Ajouter chaque hello secondaire des adresses IP privées répertoriés dans l’étape 8 toohello carte réseau avec hello même sous-réseau spécifié pour l’adresse IP principale hello.
        >[!WARNING] 
        >Si vous ne suivez pas les étapes hello ci-dessus correctement, vous risquez de perdre connectivité tooyour machine virtuelle. Vérifiez les informations de hello tapées à l’étape 5 sont correctes avant de continuer.

    * Cliquez sur **OK** tooclose les paramètres TCP/IP de hello, puis **OK** tooclose à nouveau les paramètres de carte hello. Votre connexion RDP est rétablie.

6. Tapez *ipconfig /all*à l’invite de commandes. Toutes les adresses IP que vous avez ajoutées sont affichées et le protocole DHCP est désactivé.


### <a name="validation-windows"></a>Validation (Windows)

tooensure toohello tooconnect en mesure d’internet à partir de votre configuration IP secondaire via hello qu'adresse IP publique associée, une fois que vous avez ajouté correctement à l’aide des étapes ci-dessus, utilisez hello de commande suivante :

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
>Pour les configurations IP secondaires, vous pouvez uniquement effectuer un ping toohello Internet si la configuration de hello possède une adresse IP publique associée. Pour les configurations IP principales, une adresse IP publique n’est pas requis tooping toohello Internet.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)

1. Ouvrez une fenêtre de terminal.
2. Assurez-vous que vous êtes hello racine utilisateur. Si vous n’êtes pas le cas, entrez hello de commande suivante :

    ```bash
    sudo -i
    ```

3. Mettre à jour le fichier de configuration hello d’interface de réseau hello (en supposant « eth0 »).

    * Gardez à l’élément de ligne existante hello pour dhcp. l’adresse IP principale Hello configuration reste telle qu’elle était précédemment.
    * Ajoutez une configuration pour une adresse IP statique supplémentaire avec hello suivant de commandes :

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    Un fichier .cfg doit s’afficher.
4. Fichier de hello ouvert. Vous devez voir hello lignes à fin hello du fichier de hello suivantes :

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. Ajoutez hello lignes suivantes après lignes hello qui existent dans ce fichier :

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. Enregistrer le fichier de hello à l’aide de hello de commande suivante :

    ```bash
    :wq
    ```

7. Réinitialiser l’interface de réseau hello avec hello de commande suivante :

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > Exécutez ifdown et ifup Bonjour même ligne si vous utilisez une connexion à distance.
    >

8. Vérifiez l’adresse hello est ajoutée à interface de réseau toohello avec hello de commande suivante :

    ```bash
    ip addr list eth0
    ```

    Vous devez voir hello IP adresse que vous avez ajoutés en tant que partie de la liste de hello.

### <a name="linux-redhat-centos-and-others"></a>Linux (Redhat, CentOS, etc.)

1. Ouvrez une fenêtre de terminal.
2. Assurez-vous que vous êtes hello racine utilisateur. Si vous n’êtes pas le cas, entrez hello de commande suivante :

    ```bash
    sudo -i
    ```

3. Entrez votre mot de passe et suivez les instructions qui s’affichent. Une fois l’utilisateur racine de hello, accédez dossier scripts de réseau toohello avec hello de commande suivante :

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. Hello de la liste des fichiers associés à l’ifcfg à l’aide de hello de commande suivante :

    ```bash
    ls ifcfg-*
    ```

    Vous devez voir *ifcfg-eth0* comme l’un des fichiers de hello.

5. tooadd une adresse IP, créez un fichier de configuration pour qu’il comme indiqué ci-dessous. Notez qu’un fichier doit être créé pour chaque configuration IP.

    ```bash
    touch ifcfg-eth0:0
    ```

6. Ouvrez hello *ifcfg-eth0:0* fichier avec hello de commande suivante :

    ```bash
    vi ifcfg-eth0:0
    ```

7. Ajoutez le fichier de contenu toohello, *eth0:0* dans ce cas, par hello commande suivante. Être tooupdate que les informations en fonction de votre adresse IP.

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. Enregistrer le fichier de hello avec hello de commande suivante :

    ```bash
    :wq
    ```

9. Redémarrez les services réseau hello et assurez-vous que les modifications de hello sont réussies par hello suivant les commandes en cours d’exécution :

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    Vous devez voir hello IP adresse que vous avez ajouté, *eth0:0*, dans la liste hello retournée.

### <a name="validation-linux"></a>Validation (Linux)

tooensure vous êtes en mesure de tooconnect toohello internet à partir de votre configuration IP secondaire via l’adresse IP publique hello associé, utilisez hello de commande suivante :

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
>Pour les configurations IP secondaires, vous pouvez uniquement effectuer un ping toohello Internet si la configuration de hello possède une adresse IP publique associée. Pour les configurations IP principales, une adresse IP publique n’est pas requis tooping toohello Internet.

Pour les machines virtuelles Linux, lors de la tentative de connexion sortante de toovalidate à partir d’une carte réseau secondaire, vous devrez peut-être tooadd les itinéraires appropriés. Il existe plusieurs façons toodo cela. Reportez-vous à la documentation appropriée pour votre distribution Linux. suivant de Hello s’agit-il d’une méthode tooaccomplish :

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- Être tooreplace que :
    - **10.0.0.5** avec hello privé adresse qui a une adresse IP publique adresse IP tooit associé
    - **10.0.0.1** passerelle par défaut de tooyour
    - **eth2** nom toohello de votre carte réseau secondaire
