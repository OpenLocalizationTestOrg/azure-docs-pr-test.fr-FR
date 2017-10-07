---
title: aaaUse SSH tooaccess tunneling Azure HDInsight | Documents Microsoft
description: "Découvrez comment toouse un toosecurely de tunnel SSH parcourir les ressources web hébergées sur vos nœuds HDInsight de basés sur Linux."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 879834a4-52d0-499c-a3ae-8d28863abf65
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a315c53751bbe6950a182674f4108c67c2f2f8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ssh-tunneling-tooaccess-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a>Utiliser le Tunneling SSH tooaccess Ambari web UI, JobHistory, NameNode, Oozie et autres interfaces utilisateur web

Les clusters HDInsight basés sur Linux fournissent l’interface utilisateur de web de tooAmbari accès via Internet de hello, mais certaines fonctionnalités de l’interface utilisateur de hello ne sont pas. Par exemple, hello interface utilisateur web pour d’autres services qui sont exposés via Ambari. Pour toutes les fonctionnalités de l’interface utilisateur web de Ambari hello, vous devez utiliser une tête de cluster de toohello tunnel SSH.

## <a name="why-use-an-ssh-tunnel"></a>Raisons pour lesquelles utiliser un tunnel SSH

Plusieurs menus hello dans Ambari fonctionnent uniquement via un tunnel SSH. Ces menus s’appuient sur des sites web et des services qui s’exécutent sur d’autres types de nœuds, tels que les nœuds Worker. Souvent, ces sites web ne sont pas sécurisés, donc il n’est pas sécurisé toodirectly exposent les sur hello internet.

Hello suivant des interfaces utilisateur Web nécessite un tunnel SSH :

* JobHistory
* NameNode
* Thread Stacks
* Interface utilisateur Web Oozie
* Interface HBase Master et interface de journaux

Si vous utilisez des Actions de Script toocustomize votre cluster, tous les services ou les utilitaires que vous installez qui exposent une interface utilisateur web nécessitent un tunnel SSH. Par exemple, si vous installez la teinte à l’aide d’une Action de Script, vous devez utiliser un SSH tunnel tooaccess hello teinte interface utilisateur web.

> [!IMPORTANT]
> Si vous avez tooHDInsight un accès direct via un réseau virtuel, il est inutile des tunnels toouse SSH. Pour obtenir un exemple d’accéder directement à HDInsight via un réseau virtuel, consultez hello [réseau de se connecter de HDInsight tooyour local](connect-on-premises-network.md) document.

## <a name="what-is-an-ssh-tunnel"></a>Définition d’un tunnel SSH

[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) achemine le trafic envoyé tooa port sur votre station de travail locale. le trafic de Hello est acheminé via un SSH connexion tooyour HDInsight nœud principal du cluster. demande de Hello est résolu comme si elle a été créée sur le nœud principal de hello. réponse de Hello est alors acheminé par le biais de station de travail tooyour hello tunnel.

## <a name="prerequisites"></a>Composants requis

* Un client SSH. Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

* Un navigateur web qui peut être configuré toouse un proxy SOCKS5.

    > [!WARNING]
    > prise en charge du proxy Hello SOCKS intégrée de Windows ne prend pas en charge SOCKS5 et ne fonctionne pas avec les étapes hello dans ce document. Hello navigateurs suivants s’appuient sur les paramètres de proxy de Windows et ne le faites pas actuellement utiliser des étapes hello dans ce document :
    >
    > * Microsoft Edge
    > * Microsoft Internet Explorer
    >
    > Google Chrome s’appuie également sur les paramètres du proxy Windows hello. Toutefois, vous pouvez installer des extensions qui prennent en charge SOCKS5. Nous vous recommandons [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).

## <a name="usessh"></a>Créer un tunnel à l’aide de la commande SSH de hello

Suivant de hello utilisez commande toocreate un tunnel SSH à l’aide de hello `ssh` commande. Remplacez **nom d’utilisateur** à un utilisateur SSH pour votre cluster HDInsight, puis remplacez **CLUSTERNAME** avec nom hello de votre cluster HDInsight :

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

Cette commande crée une connexion qui achemine le cluster toohello 9876 trafic toolocal port via SSH. options de Hello sont :

* **D 9876** -hello port local qui achemine le trafic via un tunnel de hello.
* **C** : compresse toutes les données car le trafic web est principalement du texte
* **2** -force SSH tootry protocol version 2 uniquement.
* **q** : mode silencieux
* **T** : désactive l’allocation pseudo-tty puisque nous transférons simplement un port
* **n** : empêche la lecture STDIN puisque nous transférons simplement un port
* **N** : n’exécute pas une commande à distance puisque nous transférons simplement un port
* **f** -s’exécutent en arrière-plan de hello.

Une fois la commande hello se termine, le trafic envoyé tooport 9876 sur l’ordinateur local de hello est routé toohello nœud principal du cluster.

## <a name="useputty"></a>Création d’un tunnel à l'aide de PuTTY

[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) est un client SSH graphique pour Windows. Utilisez hello suivant les étapes toocreate un tunnel SSH à l’aide de PuTTY :

1. Ouvrez PuTTY et saisissez vos informations de connexion. Si vous n’êtes pas familiarisé avec PuTTY, consultez hello [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).

2. Bonjour **catégorie** toohello de la section gauche de la boîte de dialogue hello, développez **connexion**, développez **SSH**, puis sélectionnez **Tunnels**.

3. Fournir hello suivant les informations de hello **réacheminement de port Options contrôlant SSH** formulaire :
   
   * **Port source** -hello port client hello que vous souhaitez tooforward. Par exemple : **9876**.

   * **Destination** -hello adresse SSH pour le cluster HDInsight de basés sur Linux de hello. Par exemple : **moncluster-ssh.azurehdinsight.net**.

   * **Dynamique** : active le routage dynamique du proxy SOCKS.
     
     ![image des options de tunneling](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. Cliquez sur **ajouter** tooadd hello paramètres, puis cliquez sur **ouvrir** tooopen une connexion SSH.

5. Lorsque vous y êtes invité, connectez-vous toohello server.

## <a name="use-hello-tunnel-from-your-browser"></a>Utiliser le tunnel hello depuis votre navigateur

> [!IMPORTANT]
> Hello étapes cette hello d’utilisation de section navigateur Mozilla FireFox, car elle fournit hello mêmes paramètres de proxy sur toutes les plateformes. Autres navigateurs modernes, tels que Google Chrome, peuvent nécessiter une extension du type toowork FoxyProxy avec le tunnel hello.

1. Configurer hello navigateur toouse **localhost** et la création de port hello vous avez utilisé lorsque tunnel hello comme un **SOCKS v5** proxy. Voici ce que les paramètres de Firefox hello similaire. Si vous avez utilisé un port autre que 9876, modifiez hello port toohello est que celle que vous avez utilisé :
   
    ![image des paramètres de Firefox](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > En sélectionnant **DNS distant** résout les demandes de système DNS (Domain Name) à l’aide du cluster HDInsight de hello. Ce paramètre est résolu DNS à l’aide du nœud principal de hello du cluster de hello.

2. Vérifiez ce tunnel hello fonctionne en visitant un site tel que [http://www.whatismyip.com/](http://www.whatismyip.com/). Hello IP retourné doit être une utilisée par le centre de données de Microsoft Azure hello.

## <a name="verify-with-ambari-web-ui"></a>Vérification avec l'interface utilisateur Web Ambari

Une fois que le cluster de hello a été établie, utilisez hello suivant tooverify étapes que vous pouvez accéder à des interfaces utilisateur web du service à partir de hello Ambari Web :

1. Dans votre navigateur, accédez à toohttp://headnodehost:8080. Hello `headnodehost` adresse est envoyé sur le cluster de toohello tunnel hello et résoudre le nœud principal toohello qui Ambari est en cours d’exécution. Lorsque vous y êtes invité, entrez le nom d’utilisateur admin hello (admin) et le mot de passe pour votre cluster. Vous pouvez être invité à une seconde fois par l’interface utilisateur web de Ambari hello. Dans ce cas, entrez à nouveau les informations de hello.

   > [!NOTE]
   > Lorsque vous utilisez le cluster toohello tooconnect hello http://headnodehost:8080 adresse, vous vous connectez via un tunnel de hello. Communication est sécurisée à l’aide de tunnel SSH de hello au lieu de HTTPS. tooconnect plus hello internet à l’aide de HTTPS, utilisez https://CLUSTERNAME.azurehdinsight.net, où **CLUSTERNAME** est le nom hello du cluster de hello.

2. À partir de l’interface utilisateur de Ambari Web de hello, sélectionnez HDFS dans liste hello gauche hello de page de hello.

    ![Image avec HDFS sélectionné](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. Lorsque hello informations du service HDFS s’affiche, sélectionnez **liens rapides**. Une liste de nœuds principaux d’un cluster hello s’affiche. Sélectionnez un des nœuds de tête hello, puis **NameNode UI**.

    ![Image avec un menu de liens rapides hello développé](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > Lorsque vous sélectionnez __Liens rapides__, un indicateur d’attente peut apparaître. Cela peut se produire si votre connexion internet est lente. Patienter une minute ou deux pour hello toobe de données provenant du serveur de hello, puis réessayez la liste de hello.
   >
   > Certaines entrées de hello **liens rapides** menu peut être tronqué à droite hello d’écran hello. Dans ce cas, développez le menu hello à l’aide de la souris et utilisez hello flèche droite tooscroll clé hello écran toohello toosee droite hello reste du menu de hello.

4. Un toohello similaire de page suivant l’image s’affiche :

    ![Image de hello NameNode UI](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > Notez l’URL de hello pour cette page ; Il doit être similaire trop**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**. Cet URI utilise le nom de domaine complet interne hello (FQDN) du nœud de hello et est accessible uniquement lors de l’utilisation d’un tunnel SSH.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez appris comment toocreate et utilisez un tunnel SSH, consultez hello suivant du document pour les autres façons de toouse Ambari :

* [Gestion des clusters HDInsight à l'aide d’Ambari](hdinsight-hadoop-manage-ambari.md)

Pour plus d’informations sur l’utilisation de SSH avec HDInsight, voir [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

