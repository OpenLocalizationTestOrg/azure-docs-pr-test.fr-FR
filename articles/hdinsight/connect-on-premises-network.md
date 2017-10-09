---
title: "réseau local de tooyour Microsoft aaaConnect HDInsight - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toocreate un HDInsight de cluster dans un réseau virtuel Azure et connectez-la tooyour sur réseau local. Découvrez comment tooconfigure la résolution de noms entre HDInsight et votre réseau local à l’aide d’un serveur DNS personnalisé."
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a3adf0e3df7726d8e6566d723700506baaf89a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-hdinsight-tooyour-on-premise-network"></a>Connexion réseau locale de tooyour HDInsight

Découvrez comment tooconnect HDInsight tooyour local réseau à l’aide de réseaux virtuels Azure et une passerelle VPN. Ce document fournit des informations de planification concernant :

* À l’aide de HDInsight dans un réseau virtuel Azure qui se connecte tooyour sur site réseau.

* Configuration de la résolution de nom DNS entre le réseau virtuel de hello et votre réseau local.

* Configuration réseau sécurité groupes toorestrict internet access tooHDInsight.

* Ports fournis par HDInsight sur un réseau virtuel de hello.

## <a name="create-hello-virtual-network-configuration"></a>Créer la configuration du réseau virtuel hello

> [!IMPORTANT]
> Si vous recherchez des instructions étape par étape sur la connexion HDInsight tooyour locale réseau à l’aide d’un réseau virtuel Azure, consultez hello [réseau de se connecter de HDInsight tooyour locale](connect-on-premises-network.md) document.

Toolearn les documents suivants de hello utilisation comment toocreate un réseau virtuel Azure qui est connecté tooyour local réseau :
    
* [À l’aide de hello portail Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [Utilisation de Microsoft Azure PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [Utilisation de l’interface de ligne de commande Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a>Configurer la résolution de noms

tooallow HDInsight et les ressources dans toocommunicate de réseau hello joint par nom, vous devez effectuer hello suivant des actions :

* Créer un serveur DNS personnalisé Bonjour réseau virtuel Azure.

* Configurer hello réseau virtuel toouse hello serveur DNS personnalisé au lieu de la valeur par défaut de hello Azure récursive résolveur.

* Configurer le transfert entre un serveur DNS personnalisé hello et votre serveur DNS sur local.

Cette configuration permet de hello suivant de comportement :

* Les requêtes de noms de domaine complet qui ont le suffixe DNS de hello __pour le réseau virtuel de hello__ sont transférés à un serveur DNS personnalisé toohello. un serveur DNS personnalisé Hello transfère ensuite ces toohello demandes Azure récursive programme de résolution, qui retourne l’adresse IP de hello.

* Toutes les autres demandes sont transférés de serveur DNS de local toohello. Y compris les requêtes pour les ressources internet publics tels que microsoft.com sont transférés serveurDNS toohello local pour la résolution de nom.

Bonjour suivant schéma, lignes vertes sont des requêtes pour les ressources qui se terminent par le suffixe DNS de hello du réseau virtuel de hello. Lignes bleues sont des requêtes pour les ressources d’un réseau local de hello ou hello internet public.

![Diagramme de résolution des requêtes DNS dans configuration hello utilisée dans ce document](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a>Créer un serveur DNS personnalisé

> [!IMPORTANT]
> Vous devez créer et configurer le serveur DNS de hello avant d’installer HDInsight dans le réseau virtuel de hello.

toocreate un VM Linux qui utilise hello [lier](https://www.isc.org/downloads/bind/) logiciel DNS, hello utilisation comme suit :

> [!NOTE]
> Hello étapes suivantes utilisent hello [portail Azure](https://portal.azure.com) toocreate une Machine virtuelle Azure. Pour les autres façons toocreate une machine virtuelle, consultez hello [créer un ordinateur virtuel - CLI d’Azure](../virtual-machines/linux/quick-create-cli.md) et [créer un ordinateur virtuel - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documents.

1. À partir de hello [portail Azure](https://portal.azure.com), sélectionnez  __+__ , __de calcul__, et __Ubuntu Server 16.04 LTS__.

    ![Créer une machine virtuelle Ubuntu](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. À partir de hello __notions de base__ section, entrez hello informations suivantes :

    * __Nom__ : nom convivial identifiant cette machine virtuelle. Par exemple, __DNSProxy__.
    * __Nom d’utilisateur__: nom hello Hello SSH compte.
    * __La clé publique SSH__ ou __mot de passe__: hello la méthode d’authentification pour hello SSH compte. Nous recommandons d’utiliser des clés publiques, car elles sont plus sécurisées. Pour plus d’informations, consultez hello [créer et utiliser des clés SSH pour les machines virtuelles Linux](../virtual-machines/linux/mac-create-ssh-keys.md) document.
    * __Groupe de ressources__: sélectionnez __utiliser l’existante__, puis sélectionnez le groupe de ressources hello contient hello de réseau virtuel créé précédemment.
    * __Emplacement__: sélectionnez hello même emplacement que le réseau virtuel de hello.

    ![Configuration de base de machine virtuelle](./media/connect-on-premises-network/vm-basics.png)

    Conservez les autres entrées de hello valeurs par défaut, puis sélectionnez __OK__.

3. À partir de hello __choisir une taille__ section, la taille de machine virtuelle sélectionnez hello. Pour ce didacticiel, sélectionnez hello plus petit et plus bas coût option. toocontinue, utilisez hello __sélectionnez__ bouton.

4. À partir de hello __paramètres__ section, entrez hello informations suivantes :

    * __Réseau virtuel__: sélectionnez hello réseau virtuel que vous avez créé précédemment.

    * __Sous-réseau__: sélectionnez le sous-réseau hello par défaut pour le réseau virtuel de hello. Faire __pas__ sélectionnez hello sous-réseau utilisé par la passerelle VPN de hello.

    * __Compte de stockage des diagnostics__ : sélectionnez ou créez un compte de stockage.

    ![Paramètres de réseau virtuel](./media/connect-on-premises-network/virtual-network-settings.png)

    Conservez hello autres entrées hello valeur par défaut, puis sélectionnez __OK__ toocontinue.

5. À partir de hello __achat__ section, sélectionnez hello __achat__ bouton toocreate hello virtual machine.

6. Une fois que l’ordinateur virtuel de hello a été créé, son __vue d’ensemble__ s’affiche. Dans la liste hello hello gauche, sélectionnez __propriétés__. Enregistrer hello __adresse IP publique__ et __adresse IP privée__ valeurs. Il va être utilisé dans la section suivante de hello.

    ![Adresses IP publique et privée](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a>Installer et configurer Bind (logiciel DNS)

1. Utiliser SSH tooconnect toohello __adresse IP publique__ de machine virtuelle de hello. Bonjour à l’exemple suivant établit une connexion virtuels tooa à 40.68.254.142 :

    ```bash
    ssh sshuser@40.68.254.142
    ```

    Remplacez `sshuser` par hello SSH compte d’utilisateur que vous avez spécifié lors de la création du cluster de hello.

    > [!NOTE]
    > Il existe une multitude de hello tooobtain de façons `ssh` utilitaire. Sur Linux, Unix et macOS, il est fourni en tant que partie du système d’exploitation de hello. Si vous utilisez Windows, considérez l’une des options suivantes de hello :
    >
    > * [Azure Cloud Shell](../cloud-shell/quickstart.md)
    > * [Bash sur Ubuntu sur Windows 10](https://msdn.microsoft.com/commandline/wsl/about)
    > * [Git (https://git-scm.com/)](https://git-scm.com/)
    > * [OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. tooinstall Bind, utilisez hello suivant les commandes à partir de la session SSH hello :

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. tooconfigure liaison tooforward nom résolution demandes tooyour local serveur DNS, utilisez hello après le texte en tant que contenu hello Hello `/etc/bind/named.conf.options` fichier :

        acl goodclients {
            10.0.0.0/16; # Replace with hello IP address range of hello virtual network
            10.1.0.0/16; # Replace with hello IP address range of hello on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with hello IP address of hello on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform tooRFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > Remplacez les valeurs de hello en hello `goodclients` section avec une plage d’adresses IP hello du réseau virtuel de hello et réseau local. Cette section définit les adresses hello qui accepte les demandes de ce serveur DNS.
    >
    > Remplacez hello `192.168.0.1` entrée Bonjour `forwarders` section avec l’adresse IP de hello du serveur DNS local. Cette tooyour de demandes DNS entrée itinéraires locaux serveur DNS pour la résolution.

    tooedit ce fichier, hello utilisez commande suivante :

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    fichier de hello toosave, utilisez __Ctrl + X__, __Y__, puis __entrée__.

4. À partir de la session SSH hello, utilisez hello de commande suivante :

    ```bash
    hostname -f
    ```

    Cette commande retourne un toohello similaire valeur suit texte :

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    Hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` texte est hello __suffixe DNS__ pour ce réseau virtuel. Enregistrez cette valeur, car vous l’utiliserez plus tard.

5. Liaison tooconfigure tooresolve les noms DNS pour les ressources réseau virtuel de hello, utilisez hello après le texte en tant que contenu hello Hello `/etc/bind/named.conf.local` fichier :

        // Replace hello following with hello DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # hello Azure recursive resolver
        };

    > [!IMPORTANT]
    > Vous devez remplacer hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` avec le suffixe DNS de hello vous extrait précédemment.

    tooedit ce fichier, hello utilisez commande suivante :

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    fichier de hello toosave, utilisez __Ctrl + X__, __Y__, puis __entrée__.

6. toostart Bind, utilisez hello de commande suivante :

    ```bash
    sudo service bind9 restart
    ```

7. tooverify lier peut résoudre les noms de hello de ressources de votre réseau local, hello utilisation suivant de commandes :

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > Remplacez `dns.mynetwork.net` avec le nom de domaine complet (FQDN) hello d’une ressource de votre réseau local.
    >
    > Remplacez `10.0.0.4` avec hello __adresse IP interne__ de votre serveur DNS personnalisé dans le réseau virtuel de hello.

    réponse de Hello apparaît toohello similaire après le texte :

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-hello-virtual-network-toouse-hello-custom-dns-server"></a>Configurer hello réseau virtuel toouse hello serveur DNS personnalisé

tooconfigure hello réseau virtuel toouse hello serveur DNS personnalisé au lieu de hello Azure récursive, programme de résolution, utiliser hello comme suit :

1. Bonjour [portail Azure](https://portal.azure.com), sélectionnez le réseau virtuel de hello, puis sélectionnez __serveurs DNS__.

2. Sélectionnez __personnalisé__, puis entrez hello __adresse IP interne__ d’un serveur DNS personnalisé hello. Enfin, sélectionnez __Enregistrer__.

    ![Définir un serveur DNS personnalisé hello pour le réseau de hello](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-hello-on-premises-dns-server"></a>Configurer hello locale DNS server

Dans la section précédente de hello, vous configuré hello personnalisé DNS server tooforward demandes toohello sur serveur DNS local. Ensuite, vous devez configurer hello locale DNS tooforward demandes toohello personnalisé serveur DNS.

Pour savoir comment tooconfigure votre serveur DNS, consultez la documentation de votre logiciel de serveur DNS hello. Recherchez la procédure hello tooconfigure un __redirecteur conditionnel__.

Un redirecteur conditionnel transfère uniquement les demandes relatives à un suffixe DNS spécifique. Dans ce cas, vous devez configurer un redirecteur le suffixe DNS du réseau virtuel de hello hello. Demandes de ce suffixe doivent être transférés à adresse IP de toohello d’un serveur DNS personnalisé hello. 

Hello texte suivant est un exemple de configuration de redirecteur conditionnel pour hello **lier** logiciel DNS :

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello custom DNS server's internal IP address
    };

Pour plus d’informations sur l’utilisation de DNS sur **Windows Server 2016**, consultez hello [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentation...

Une fois que vous avez configuré le serveur DNS de local hello, vous pouvez utiliser `nslookup` de tooverify de réseau local hello que vous pouvez résoudre les noms dans le réseau virtuel de hello. l’exemple suivant de Hello 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

Cet exemple utilise hello serveur DNS local 196.168.0.4 nom de hello tooresolve d’un serveur DNS personnalisé hello. Remplacez adresse hello hello un pour le serveur DNS de local hello. Remplacez hello `dnsproxy` adresse avec le nom de domaine complet de hello du serveur DNS personnalisé de hello.

## <a name="optional-control-network-traffic"></a>Facultatif : contrôler le trafic réseau

Vous pouvez utiliser des groupes de sécurité réseau (NSG) ou le trafic réseau de toocontrol itinéraires définis par l’utilisateur (UDR). Groupes de sécurité réseau permettent de toofilter entrant et sortant du trafic et autoriser ou refuser le trafic de hello. UDRs vous toocontrol le flux de trafic entre les ressources de réseau virtuel de hello, hello internet et hello réseau local.

> [!WARNING]
> HDInsight requiert un accès entrant à partir d’adresses IP spécifiques Bonjour Azure cloud et un accès sortant non restreint. Lorsque vous utilisez des groupes de sécurité réseau ou UDRs toocontrol du trafic, vous devez effectuer hello comme suit :
>
> 1. Recherche des adresses IP hello pour l’emplacement hello qui contient votre réseau virtuel. Pour obtenir la liste des adresses IP requises par emplacement, consultez [Adresses IP requises](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).
>
> 2. Autoriser le trafic entrant à partir d’adresses IP de hello.
>
>    * __Groupe de sécurité réseau__: autoriser __entrant__ le trafic sur le port __443__ de hello __Internet__.
>    * __UDR__: ensemble hello __tronçon suivant__ type de hello itinéraire too__Internet__.

Pour obtenir un exemple d’utilisation de Azure PowerShell ou hello CLI d’Azure toocreate groupes de sécurité réseau, consultez hello [HDInsight d’étendre les réseaux virtuels Azure](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.

## <a name="create-hello-hdinsight-cluster"></a>Créer le cluster HDInsight de hello

> [!WARNING]
> Vous devez configurer un serveur DNS personnalisé hello avant d’installer HDInsight dans le réseau virtuel de hello.

Hello d’utiliser les étapes Bonjour [créer un cluster HDInsight à l’aide de hello portail Azure](./hdinsight-hadoop-create-linux-clusters-portal.md) document toocreate un cluster HDInsight.

> [!WARNING]
> * Lors de la création du cluster, vous devez choisir l’emplacement hello qui contient votre réseau virtuel.
>
> * Bonjour __paramètres avancés__ partie de la configuration, vous devez sélectionner le réseau virtuel de hello et sous-réseau que vous avez créé précédemment.

## <a name="connecting-toohdinsight"></a>Connexion tooHDInsight

La plupart des documentation sur HDInsight suppose que vous avez des cluster toohello d’accès sur hello internet. Par exemple, que vous pouvez vous connecter à cluster toohello à https://CLUSTERNAME.azurehdinsight.net. Cette adresse utilise la passerelle publique hello, qui n’est pas disponible si vous avez utilisé des groupes de sécurité réseau ou d’accès toorestrict UDRs hello internet.

toodirectly connecter tooHDInsight via le réseau virtuel de hello, utilisez hello comme suit :

1. noms de domaine complet interne toodiscover hello hello HDInsight des nœuds de cluster, utilisez une des méthodes suivantes de hello :

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

2. toodetermine hello port un service disponible, consultez hello [Ports utilisés par les services de Hadoop dans HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.

    > [!IMPORTANT]
    > Certains services hébergés sur les nœuds principaux hello sont uniquement actifs sur un seul nœud à la fois. Si vous essayez d’accéder à un service sur un seul nœud principal et il échoue, basculez toohello autre nœud principal.
    >
    > Par exemple, Ambari n’est actif que sur un nœud principal à la fois. Si vous essayez d’accéder à Ambari sur un seul nœud principal et retourne une erreur 404, puis elle s’exécute sur hello autre nœud principal.

## <a name="next-steps"></a>Étapes suivantes

* Pour plus d’informations sur l’utilisation de HDInsight dans un réseau virtuel, consultez [Étendre HDInsight à l’aide de réseaux virtuels Azure](./hdinsight-extend-hadoop-virtual-network.md).

* Pour plus d’informations sur les réseaux virtuels Azure, consultez hello [vue d’ensemble du réseau virtuel Azure](../virtual-network/virtual-networks-overview.md).

* Pour plus d’informations sur les groupes de sécurité réseau, consultez [Groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md).

* Pour plus d’informations sur les routages par l’utilisateur, consultez [Routage définis par l’utilisateur et transfert IP](../virtual-network/virtual-networks-udr-overview.md).
