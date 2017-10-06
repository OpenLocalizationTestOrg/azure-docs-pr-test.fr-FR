---
title: aaaUse SSH avec Hadoop - Azure HDInsight | Documents Microsoft
description: "Vous pouvez accéder à un cluster HDInsight à l’aide de SSH (Secure Shell). Ce document fournit des informations sur la connexion tooHDInsight à l’aide de hello ssh et les commandes de scp à partir de clients Windows, Linux, Unix ou macOS."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: commandes hadoop dans linux,commandes hadoop linux,hadoop macos,ssh hadoop,cluster ssh hadoop
ms.assetid: a6a16405-a4a7-4151-9bbf-ab26972216c5
ms.service: hdinsight
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: ac9e70ce3c70693c1b81c9514ba4fd47686070ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toohdinsight-hadoop-using-ssh"></a>Se connecter tooHDInsight (Hadoop) à l’aide de SSH

Découvrez comment toouse [Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) toosecurely connecter tooHadoop sur Azure HDInsight. 

HDInsight peut utiliser Linux (Ubuntu) en tant que système d’exploitation de hello pour les nœuds de cluster Hadoop de hello. Hello tableau ci-dessous contient informations d’adresse et le port hello nécessaires lors de la connexion basée sur les tooLinux HDInsight, à l’aide d’un client SSH :

| Adresse | Port | Se connecte au... |
| ----- | ----- | ----- |
| `<clustername>-ed-ssh.azurehdinsight.net` | 22 | Nœud de périmètre (R Server sur HDInsight) |
| `<edgenodename>.<clustername>-ssh.azurehdinsight.net` | 22 | Nœud de périmètre (n’importe quel autre type de cluster, si un nœud de périmètre existe) |
| `<clustername>-ssh.azurehdinsight.net` | 22 | Nœud principal primaire |
| `<clustername>-ssh.azurehdinsight.net` | 23 | Nœud principal secondaire |

> [!NOTE]
> Remplacez `<edgenodename>` par nom de hello du nœud de périmètre hello.
>
> Remplacez `<clustername>` avec nom hello de votre cluster.
>
> Si votre cluster contient un nœud, il est recommandé que vous __se connectent toujours de nœud de périmètre toohello__ à l’aide de SSH. les nœuds principaux Hello hébergent des services de contrôle d’intégrité critique toohello de Hadoop. nœud de périmètre Hello s’exécute uniquement à ce que vous mettez sur celui-ci.
>
> Pour plus d’informations sur l’utilisation des nœuds de périmètre, consultez [Utiliser des nœuds de périmètre vides dans HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node).

## <a name="ssh-clients"></a>Clients SSH

Les systèmes Linux, Unix et macOS fournissent hello `ssh` et `scp` commandes. Hello `ssh` client est couramment utilisé toocreate une session de ligne de commande à distance avec un système Unix ou de Linux. Hello `scp` client est utilisé toosecurely copier les fichiers entre le système à distance de votre client et hello.

Microsoft Windows ne fournit pas de clients SSH par défaut. Hello `ssh` et `scp` les clients sont disponibles pour Windows via hello suivant des packages :

* [Azure Cloud Shell](../cloud-shell/quickstart.md): hello Cloud Shell fournit un environnement de l’interpréteur de commandes dans votre navigateur et fournit hello `ssh`, `scp`et d’autres commandes Linux courantes.

* [Bash sur Ubuntu sur Windows 10](https://msdn.microsoft.com/commandline/wsl/about): hello `ssh` et `scp` commandes sont disponibles via hello Bash sur la ligne de commande Windows.

* [GIT (https://git-scm.com/)](https://git-scm.com/): hello `ssh` et `scp` commandes sont disponibles via la ligne de commande GitBash hello.

* [Bureau de GitHub (https://desktop.github.com/)](https://desktop.github.com/) hello `ssh` et `scp` commandes sont disponibles via la ligne de commande GitHub Shell de hello. Bureau de GitHub peut être configuré toouse Bash, hello invite de commandes Windows, ou de PowerShell en tant que ligne de commande hello pour hello interpréteur de commandes Git.

* [OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): équipe de PowerShell hello consiste à porter OpenSSH tooWindows et fournit des versions de test.

    > [!WARNING]
    > package d’OpenSSH Hello inclut le composant de serveur SSH hello, `sshd`. Ce composant démarre un serveur SSH sur votre système, ce qui permet à d’autres tooconnect tooit. Ne pas configurer ce composant ou ouvrir le port 22 sauf si vous souhaitez toohost un serveur SSH sur votre système. Il n’est pas requis toocommunicate avec HDInsight.

Il existe également plusieurs clients SSH graphiques, tels que [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) et [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/). Bien que ces clients soient utilisés tooconnect tooHDInsight, processus hello de connexion est différent de celui à l’aide de hello `ssh` utilitaire. Pour plus d’informations, consultez la documentation hello du client hello graphique que vous utilisez.

## <a id="sshkey"></a>Authentification : clés SSH

Utilisent SSH clés [cryptographie à clé publique](https://en.wikipedia.org/wiki/Public-key_cryptography) tooauthenticate SSH sessions. Clés SSH sont plus sûres que les mots de passe et fournissent un cluster Hadoop de facilement toosecure accès tooyour.

Si votre compte SSH est sécurisé à l’aide d’une clé, hello doit fournir hello correspondant à une clé privée lors de la connexion :

* La plupart des clients peut être configurée toouse un __clé par défaut__. Par exemple, hello `ssh` client recherche d’une clé privée à `~/.ssh/id_rsa` sur les environnements Linux et Unix.

* Vous pouvez spécifier hello __clé privée de chemin d’accès tooa__. Avec hello `ssh` client, hello `-i` paramètre est la clé de tooprivate du chemin d’accès utilisé toospecify hello. Par exemple, `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`.

* Si vous avez __plusieurs clés privées__ à utiliser avec différents serveurs, envisagez d’utiliser un utilitaire tel que [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent). Hello `ssh-agent` utilitaire peut être toouse de clé select hello tooautomatically utilisé lors de l’établissement d’une session SSH.

> [!IMPORTANT]
>
> Si vous sécurisez votre clé privée avec un mot de passe, vous devez entrer la phrase secrète de hello lors de l’utilisation de clé de hello. Utilitaires comme `ssh-agent` peut mettre en cache un mot de passe hello pour votre commodité.

### <a name="create-an-ssh-key-pair"></a>Création d’une paire de clés SSH

Hello d’utilisation `ssh-keygen` toocreate fichiers clés publiques et privées de commandes. Hello commande suivante génère une paire de clés RSA 2048 bits qui peut être utilisée avec HDInsight :

    ssh-keygen -t rsa -b 2048

Vous êtes invité pour plus d’informations pendant le processus de création de la clé hello. Par exemple, où les clés hello sont stockés si toouse une phrase secrète. Après la fin du processus de hello, deux fichiers sont créés ; une clé publique et une clé privée.

* Hello __clé publique__ est toocreate utilisé un cluster HDInsight. clé publique de Hello possède une extension `.pub`.

* Hello __clé privée__ est tooauthenticate utilisé votre cluster HDInsight de toohello client.

> [!IMPORTANT]
> Vous pouvez sécuriser vos clés à l’aide d’une phrase secrète. Une phrase secrète est effectivement un mot de passe sur votre clé privée. Même si quelqu'un obtient votre clé privée, ils doivent avoir la clé de hello toouse hello phrase secrète.

### <a name="create-hdinsight-using-hello-public-key"></a>Créer HDInsight à l’aide de la clé publique de hello

| Méthode de création | Comment toouse hello clé publique |
| ------- | ------- |
| **Portail Azure** | Décochez la case __utiliser le même mot de passe en tant que compte de connexion de cluster__, puis sélectionnez __clé publique__ comme type d’authentification SSH de hello. Enfin, sélectionnez le fichier de clé publique hello ou collez le contenu de texte hello du fichier de hello Bonjour __la clé publique SSH__ champ.</br>![Boîte de dialogue de clé publique SSH lors de la création du cluster HDInsight](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png) |
| **Azure PowerShell** | Hello d’utilisation `-SshPublicKey` paramètre Hello `New-AzureRmHdinsightCluster` applet de commande et passez contenu hello de clé publique de hello sous forme de chaîne.|
| **Azure CLI 1.0** | Hello d’utilisation `--sshPublicKey` paramètre Hello `azure hdinsight cluster create` commande et passer le contenu hello de clé publique de hello sous forme de chaîne. |
| **Modèle Resource Manager** | Pour obtenir un exemple d’utilisation des clés SSH avec un modèle, consultez [Deploy HDInsight on Linux (w/ Azure Storage, SSH key)](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/) (Déployer HDInsight sur Linux (avec Stockage Azure, clé SSH). Hello `publicKeys` élément Bonjour [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) fichier est utilisé toopass hello clés tooAzure lors de la création du cluster de hello. |

## <a id="sshpassword"></a>Authentification : mot de passe

Les comptes SSH peuvent être sécurisés à l’aide d’un mot de passe. Lorsque vous vous connectez tooHDInsight à l’aide de SSH, vous êtes mot de passe hello tooenter demandées.

> [!WARNING]
> Il est déconseillé d’utiliser l’authentification par mot de passe pour SSH. Les mots de passe peuvent être devinés et sont vulnérables toobrute les attaques de force. Nous vous recommandons plutôt d’utiliser des [clés SSH pour l’authentification](#sshkey).

### <a name="create-hdinsight-using-a-password"></a>Créer un cluster HDInsight à l’aide d’un mot de passe

| Méthode de création | Comment toospecify hello mot de passe |
| --------------- | ---------------- |
| **Portail Azure** | Par défaut, hello compte d’utilisateur SSH a hello même mot de passe en tant que compte de connexion de cluster hello. toouse un autre mot de passe, décochez la case __utiliser le même mot de passe en tant que compte de connexion de cluster__, puis entrez le mot de passe hello Bonjour __mot de passe SSH__ champ.</br>![Boîte de dialogue de mot de passe SSH lors de la création du cluster HDInsight](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)|
| **Azure PowerShell** | Hello d’utilisation `--SshCredential` paramètre Hello `New-AzureRmHdinsightCluster` applet de commande et passer un `PSCredential` objet qui contient le nom du compte utilisateur hello SSH et le mot de passe. |
| **Azure CLI 1.0** | Hello d’utilisation `--sshPassword` paramètre Hello `azure hdinsight cluster create` commande et fournir la valeur de mot de passe hello. |
| **Modèle Resource Manager** | Pour obtenir un exemple d’utilisation d’un mot de passe avec un modèle, consultez [Deploy HDInsight cluster with Storage and SSH password](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/) (Déployer un cluster HDInsight avec Stockage Azure et un mot de passe SSH). Hello `linuxOperatingSystemProfile` élément Bonjour [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) fichier est utilisé toopass hello SSH compte nom et mot de passe tooAzure lors de la création du cluster de hello.|

### <a name="change-hello-ssh-password"></a>Mot de passe de modification hello SSH

Pour plus d’informations sur la modification de hello SSH mot de passe utilisateur, consultez hello __modifier les mots de passe__ section Hello [HDInsight de gérer](hdinsight-administer-use-portal-linux.md#change-passwords) document.

## <a id="domainjoined"></a>Authentification : HDInsight joint à un domaine

Si vous utilisez un __appartenant au domaine le cluster HDInsight__, vous devez utiliser hello `kinit` commande après vous être connecté avec SSH. Cette commande vous invite à un utilisateur de domaine et le mot de passe et s’authentifie votre session avec le domaine d’Active Directory de Azure hello associé hello cluster.

Pour plus d’informations, consultez la section [Configurer des clusters HDInsight joints à un domaine (version préliminaire)](hdinsight-domain-joined-configure.md).

## <a name="connect-toonodes"></a>Se connecter toonodes

Hello nœuds principal et le nœud de périmètre (le cas échéant) sont accessibles via hello internet sur les ports 22 et 23.

* Lors de la connexion toohello __head nœuds__, utiliser le port __22__ toohello tooconnect principal head de nœud et le port __23__ tooconnect toohello du nœud principal secondaire. Bonjour toouse de nom de domaine complet est `clustername-ssh.azurehdinsight.net`, où `clustername` est le nom hello de votre cluster.

    ```bash
    # Connect tooprimary head node
    # port not specified since 22 is hello default
    ssh sshuser@clustername-ssh.azurehdinsight.net

    # Connect toosecondary head node
    ssh -p 23 sshuser@clustername-ssh.azurehdinsight.net
    ```
    
* Lorsque connectiung toohello __nœud__, utilisez le port 22. Bonjour nom de domaine complet est `edgenodename.clustername-ssh.azurehdinsight.net`, où `edgenodename` est un nom que vous avez fourni lorsque création de nœud de périmètre hello. `clustername`est le nom hello du cluster de hello.

    ```bash
    # Connect tooedge node
    ssh sshuser@edgnodename.clustername-ssh.azurehdinsight.net
    ```

> [!IMPORTANT]
> les exemples précédents Hello supposent que vous utilisez l’authentification de mot de passe, ou que l’authentification de certificat se produit automatiquement. Si vous utilisez une paire de clés SSH pour l’authentification, et les certificats hello ne sert pas automatiquement, utilisez hello `-i` clé privé du paramètre toospecify hello. Par exemple, `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`.

Une fois connecté, invite de hello change tooindicate hello SSH utilisateur nom hello nœud et que vous êtes connecté. Par exemple, lors d’une connexion toohello un nœud principal principal en tant que `sshuser`, hello invite est `sshuser@hn0-clustername:~$`.

### <a name="connect-tooworker-and-zookeeper-nodes"></a>Se connecter tooworker et les nœuds de soigneur

Hello de nœuds de travail et soigneur nœuds ne sont pas directement accessibles depuis hello internet. Est accessible à partir des nœuds principal du cluster hello ou edge. Hello Voici les nœuds de tooother tooconnect hello étapes générales :

1. Utiliser SSH tooconnect tooa head ou bord nœud :

        ssh sshuser@myedge.mycluster-ssh.azurehdinsight.net

2. À partir de hello tête de toohello de connexion SSH ou nœud de périmètre, utilisez hello `ssh` nœud de travail commande tooconnect tooa dans un cluster de hello :

        ssh sshuser@wn0-myhdi

    tooretrieve une liste de noms de domaine hello de nœuds hello dans un cluster de hello, consultez hello [HDInsight de gérer à l’aide de hello API REST de Ambari](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) document.

Si hello SSH compte est sécurisé à l’aide un __mot de passe__, entrez le mot de passe hello lors de la connexion.

Si hello SSH compte est sécurisée à l’aide de __clés SSH__, assurez-vous que la redirection de SSH est activée sur le client de hello.

> [!NOTE]
> Une autre façon toodirectly accéder à tous les nœuds de cluster de hello est tooinstall HDInsight dans un réseau virtuel Azure. Ensuite, vous pouvez joindre votre toohello de l’ordinateur distant même virtuel réseau et accéder directement à tous les nœuds de cluster de hello.
>
> Pour plus d’informations, consultez [Extension des capacités de HDInsight à l’aide d’Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).

### <a name="configure-ssh-agent-forwarding"></a>Configurer le transfert de l’agent SSH

> [!IMPORTANT]
> Hello étapes suivantes supposent une Linux ou un système UNIX et travailler avec un interpréteur de commandes sur Windows 10. Si ces étapes ne fonctionnent pas pour votre système, vous devrez peut-être la documentation de hello tooconsult pour votre client SSH.

1. Avec un éditeur de texte, ouvrez `~/.ssh/config`. Si ce fichier n’existe pas, créez-le en entrant `touch ~/.ssh/config` dans la ligne de commande.

2. Ajouter hello suivant texte toohello `config` fichier.

        Host <edgenodename>.<clustername>-ssh.azurehdinsight.net
          ForwardAgent yes

    Remplacez hello __hôte__ informations avec l’adresse hello du nœud de hello, vous vous connectez toousing SSH. Hello l’exemple précédent utilise un nœud de périmètre hello. Cette entrée configure l’agent SSH de transfert pour le nœud spécifié hello.

3. Test agent SSH de transfert à l’aide de hello de commande suivante à partir de hello Terminal Server :

        echo "$SSH_AUTH_SOCK"

    Cette commande retourne toohello similaire à informations suivant le texte :

        /tmp/ssh-rfSUL1ldCldQ/agent.1792

    Si aucun élément n’est renvoyé, alors `ssh-agent` n’est pas en cours d’exécution. Pour plus d’informations, consultez les informations de scripts de démarrage de l’agent hello à [à l’aide de ssh-agent avec ssh (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) ou de la documentation de votre client SSH.

4. Une fois que vous avez vérifié que **-l’agent ssh** est en cours d’exécution, hello utilisation suivant tooadd votre agent de toohello de clé privée SSH :

        ssh-add ~/.ssh/id_rsa

    Si votre clé privée est stockée dans un fichier différent, remplacez `~/.ssh/id_rsa` avec hello chemin d’accès toohello fichier.

5. Se connecter toohello cluster edge têtes nœuds appropriés à l’aide de SSH. Puis utilisez hello SSH commande tooconnect tooa travailleur ou un nœud de soigneur. Hello est établie à l’aide de la clé de hello transféré.

## <a name="copy-files"></a>Copie des fichiers

Hello `scp` utilitaire peut être tooand de fichiers toocopy utilisé à partir de différents nœuds hello cluster. Par exemple, hello suivant commande copies hello `test.txt` répertoire à partir du nœud principal principal toohello hello système local :

```bash
scp test.txt sshuser@clustername-ssh.azurehdinsight.net:
```

Étant donné qu’aucun chemin d’accès n’est spécifiée après hello `:`, fichier de hello est placé dans hello `sshuser` répertoire de base.

Hello suivants exemple copies hello `test.txt` fichier hello `sshuser` répertoire de base sur le système local du toohello hello principal nœud principal :

```bash
scp sshuser@clustername-ssh.azurehdinsight.net:test.txt .
```

> [!IMPORTANT]
> `scp`peut uniquement accéder de système de fichiers hello des nœuds de cluster de hello. Il ne peut pas être données tooaccess utilisé dans le stockage de cluster de hello hello HDFS compatibles.
>
> Utilisez `scp` lorsque vous devez tooupload une ressource à utiliser à partir d’une session SSH. Par exemple, télécharger un script Python et puis exécutez le script de hello à partir d’une session SSH.
>
> Pour plus d’informations sur le charger directement les données dans hello stockage de HDFS compatibles, consultez hello suivant des documents :
>
> * [HDInsight avec Stockage Azure](hdinsight-hadoop-use-blob-storage.md)
>
> * [HDInsight avec Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md)

## <a name="next-steps"></a>Étapes suivantes

* [Utilisation de SSH Tunneling pour accéder à l’interface Web Ambari, JobHistory, NameNode, Oozie et d’autres interfaces Web](hdinsight-linux-ambari-ssh-tunnel.md)
* [Extension des capacités de HDInsight à l’aide d’Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md)
* [Utiliser des nœuds de périmètre vides dans HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node)