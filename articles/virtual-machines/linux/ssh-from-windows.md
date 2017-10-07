---
title: "aaaUse SSH clés avec Windows pour les machines virtuelles Linux | Documents Microsoft"
description: "Découvrez comment toogenerate et utiliser SSH clés sur une machine virtuelle Windows ordinateur tooconnect tooa Linux sur Azure."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 2cacda3b-7949-4036-bd5d-837e8b09a9c8
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: danlep
ms.openlocfilehash: 6c44217332538857cc2ca2e85de4b476aa71251c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ssh-keys-with-windows-on-azure"></a>Comment tooUse SSH clés avec Windows sur Azure
> [!div class="op_single_selector"]
> * [Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> * [Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
>
>

Lorsque vous vous connectez tooLinux virtual machines virtuelles dans Azure, vous devez utiliser [cryptographie à clé publique](https://wikipedia.org/wiki/Public-key_cryptography) tooprovide un toolog de façon plus sécurisée dans tooyour Linux VM. Ce processus implique un échange de clé publique et privé à l’aide de tooauthenticate de commande SSH (secure shell) hello vous-même au lieu d’un nom d’utilisateur et un mot de passe. Les mots de passe sont des attaques en force toobrute vulnérable, en particulier sur des machines virtuelles de côté Internet telles que des serveurs web. Cet article fournit une vue d’ensemble des clés SSH et comment toogenerate hello clés appropriées sur un ordinateur Windows.

## <a name="overview-of-ssh-and-keys"></a>Vue d’ensemble de SSH et des clés
Vous pouvez en toute sécurité vous connecter tooyour Linux VM à l’aide de clés publiques et privées :

* Hello **clé publique** est placé sur votre VM Linux, ou tout autre service que vous souhaitez toouse avec le chiffrement à clé publique.
* Hello **clé privée** êtes ce que vous tooyour présent Linux VM lors de la connexion, tooverify votre identité. Protégez cette clé privée. Ne la partagez pas.

Ces clés publiques et privées peuvent être utilisées sur plusieurs machines virtuelles et services. Il est inutile une paire de clés pour chaque ordinateur virtuel ou le service que vous souhaitez tooaccess. Pour une présentation plus détaillée, consultez [Chiffrement à clé publique](https://wikipedia.org/wiki/Public-key_cryptography).

SSH est un protocole de connexion chiffré qui permet d'ouvrir des sessions en toute sécurité à travers des connexions non sécurisées. Il est le protocole de connexion par défaut hello pour les machines virtuelles Linux hébergés dans Azure. Bien que SSH lui-même fournit une connexion chiffrée, à l’aide de mots de passe avec des connexions SSH laisse toujours les attaques en force toobrute vulnérable hello machine virtuelle ou le déchiffrement des mots de passe. Une méthode plus sécurisée et recommandée de connexion tooa machine virtuelle à l’aide de SSH est à l’aide de ces clés publiques et privées, également connu sous les clés SSH.

Si vous ne souhaitez pas les clés SSH toouse, vous pouvez toujours connecter tooyour les machines virtuelles Linux à l’aide d’un mot de passe. Si votre machine virtuelle n’est pas exposé toohello Internet, à l’aide de mots de passe peut suffire. Toutefois, vous devez toomanage vos mots de passe pour chaque VM Linux et mettre à jour les stratégies de mot de passe correct et pratiques, telles que la longueur minimale de mot de passe et les mettre à jour régulièrement. utilisation de Hello de clés SSH réduit la complexité hello de la gestion des informations d’identification individuelles entre plusieurs machines virtuelles.

## <a name="windows-packages-and-ssh-clients"></a>Packages Windows et clients SSH
Vous vous connectez tooand gérer les machines virtuelles Linux dans Azure en utilisant un **client SSH**. Aucun client SSH n’est généralement installé sur les ordinateurs Windows. Hello mise à jour de Windows 10 anniversaire ajouté Bash pour Windows et hello dernière mise à jour Windows 10 créateurs fournit des mises à jour supplémentaires. Ce sous-système Windows pour Linux permet des utilitaires toorun et d’accès tel qu’un client SSH en mode natif dans un interpréteur de commandes Bash. Puis suivez l’une des documents de Linux hello, tel que [comment la clé SSH toogenerate paires pour Linux](mac-create-ssh-keys.md). Bash pour Windows est toujours en cours de développement et est considéré comme une version bêta. Pour plus d’informations sur Bash pour Windows, consultez la page [Bash sur Ubuntu sur Windows](https://msdn.microsoft.com/commandline/wsl/about).

Si vous souhaitez toouse quelque chose que Bash pour Windows, commun Windows SSH clients que vous pouvez installer sont inclus dans hello suivant des packages :

* [Git pour Windows](https://git-for-windows.github.io/)
* [puTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/)
* [MobaXterm](http://mobaxterm.mobatek.net/)
* [Cygwin](https://cygwin.com/)


## <a name="which-key-files-do-you-need-toocreate"></a>Fichiers de clé qui toocreate avez-vous besoin ?
Azure requiert des clés publiques et privées d’au moins 2048 bits au format **ssh-rsa**. Si vous gérez des ressources Azure à l’aide du modèle de déploiement hello classique, vous devez également toogenerate un PEM (`.pem` fichier).

Voici les scénarios de déploiement hello et les types de fichiers que vous utilisez dans chaque hello :

1. **SSH-rsa** clés sont requises pour un déploiement à l’aide de hello [portail Azure](https://portal.azure.com)et les déploiements de gestionnaire de ressources à l’aide de hello [CLI d’Azure](../../cli-install-nodejs.md).
   * Il s’agit généralement des clés dont la plupart des utilisateurs ont besoin.
2. A `.pem` fichier est VMs toocreate requis à l’aide de déploiement classique de hello. Ces clés sont pris en charge dans les déploiements standard lorsque vous utilisez hello [portail Azure](https://portal.azure.com) ou [CLI d’Azure](../../cli-install-nodejs.md).
   * Vous ne devez toocreate ces clés supplémentaires et des certificats si vous gérez les ressources créées à l’aide du modèle de déploiement classique hello.

## <a name="install-git-for-windows"></a>Installation de Git pour Windows
plusieurs packages qui incluent hello répertoriés Hello section précédente `openssl` outil pour Windows. Cet outil est nécessaire toocreate des clés publiques et privées. Hello suivant le détail des exemples comment tooinstall et utiliser **Git pour Windows**, que vous pouvez choisir le package que vous préférez. **GIT pour Windows** vous donne accès toosome des logiciels open source supplémentaires ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) outils et utilitaires qui peuvent être utiles lorsque vous travaillez avec les machines virtuelles Linux.

1. Téléchargez et installez **Git pour Windows** de hello l’emplacement suivant : [https://git-for-windows.github.io/](https://git-for-windows.github.io/).
2. Acceptez les options par défaut de hello pendant hello processus d’installation, sauf si vous avez besoin de toochange les.
3. Exécutez **interpréteur de commandes Git** de hello **Menu Démarrer** > **Git** > **interpréteur de commandes Git**. console de Hello semble similaire toohello l’exemple suivant :

    ![Interpréteur de commandes Git pour Windows Bash](./media/ssh-from-windows/git-bash-window.png)

## <a name="create-a-private-key"></a>Création d’une clé privée
1. Dans votre **interpréteur de commandes Git** fenêtre, utilisez `openssl.exe` toocreate une clé privée. Hello exemple suivant crée une clé nommée `myPrivateKey` et certificat nommé `myCert.pem`:

    ```bash
    openssl.exe req -x509 -nodes -days 365 -newkey rsa:2048 \
        -keyout myPrivateKey.key -out myCert.pem
    ```

    sortie de Hello semble similaire toohello l’exemple suivant :

    ```bash
    Generating a 2048 bit RSA private key
    .......................................+++
    .......................+++
    writing new private key too'myPrivateKey.key'
    -----
    You are about toobe asked tooenter information that will be incorporated
    into your certificate request.
    What you are about tooenter is what is called a Distinguished Name or a DN.
    There are quite a few fields but you can leave some blank
    For some fields there will be a default value,
    If you enter '.', hello field will be left blank.
    -----
    Country Name (2 letter code) [AU]:
    ```

   Si bash signale une erreur, essayez d’ouvrir une nouvelle fenêtre **Git Bash** avec des privilèges élevés. Ensuite, réexécutez hello `openssl` commande.

2. Nom du pays, l’emplacement, nom de l’organisation, etc. demande hello de réponse.
3. Votre nouvelle clé privée et votre nouveau certificat sont créés dans votre répertoire de travail actuel. Par mesure de sécurité, vous devez définir des autorisations de hello sur votre clé privée, afin que les seulement vous pouvez y accéder :

    ```bash
    chmod 0600 myPrivateKey.key
    ```

4. Hello [section suivante](#create-a-private-key-for-putty) détails à l’aide de PuTTYgen tooboth afficher et utiliser la clé publique de hello et créer une clé privée spécifique pour l’utilisation de PuTTY tooSSH tooLinux machines virtuelles. Hello commande suivante génère un fichier de clé publique nommé `myPublicKey.key` que vous pouvez utiliser immédiatement :

    ```bash
    openssl.exe rsa -pubout -in myPrivateKey.key -out myPublicKey.key
    ```

5. Si vous devez également les ressources standard de toomanage, convertir hello `myCert.pem` trop`myCert.cer` (X509 binaire codé DER certificat). Effectuez cette étape facultative que si vous devez toospecifically gérer les ressources standard plus anciens.

    Convertir un certificat hello à l’aide de hello de commande suivante :

    ```bash
    openssl.exe  x509 -outform der -in myCert.pem -out myCert.cer
    ```

## <a name="create-a-private-key-for-putty"></a>Créer une clé privée pour PuTTY
PuTTY est un client SSH courant pour Windows. Vous est toouse libre n’importe quel client SSH que vous souhaitez. toouse PuTTY, vous devez toocreate un type de clé : une clé privée PuTTY (PPK) supplémentaire. Si vous ne souhaitez pas toouse PuTTY, ignorez cette section.

Hello exemple suivant crée cette clé privée supplémentaire spécifiquement pour PuTTY toouse :

1. Utilisez **interpréteur de commandes Git** tooconvert votre privé de clé dans une clé privée RSA que PuTTYgen peut comprendre. Hello exemple suivant crée une clé nommée `myPrivateKey_rsa` à partir de la clé existante de hello nommé `myPrivateKey`:

    ```bash
    openssl rsa -in ./myPrivateKey.key -out myPrivateKey_rsa
    ```

    Par mesure de sécurité, vous devez définir des autorisations de hello sur votre clé privée, afin que les seulement vous pouvez y accéder :

    ```bash
    chmod 0600 myPrivateKey_rsa
    ```
2. Téléchargez et exécutez PuTTYgen à partir de hello l’emplacement suivant : [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
3. Cliquez sur le menu de hello : **fichier** > **clé privée de charge**
4. Recherchez votre clé privée (`myPrivateKey_rsa` dans l’exemple précédent de hello). répertoire de par défaut Hello lorsque vous démarrez **interpréteur de commandes Git** est `C:\Users\%username%`. Modifier hello fichier filtre tooshow **tous les fichiers (\*.\*)** :

    ![Charger la clé privée hello dans PuTTYgen](./media/ssh-from-windows/load-private-key.png)
5. Cliquez sur **Ouvrir**. Un message indique que cette clé hello a été importée :

    ![Clé tooPuTTYgen été importées avec succès](./media/ssh-from-windows/successfully-imported-key.png)
6. Cliquez sur **OK** invite de commandes tooclose hello.
7. clé publique de Hello est affiché en haut de hello de hello **PuTTYgen** fenêtre. Vous copiez et collez cette clé publique hello portail Azure ou le modèle Azure Resource Manager lorsque vous créez un VM Linux. Vous pouvez également cliquer sur **clé publique d’enregistrement** toosave un ordinateur tooyour de copie :

    ![Enregistrer le fichier de clé publique PuTTY](./media/ssh-from-windows/save-public-key.png)

    Hello suivant montre comment vous serez copiez et collez cette clé publique hello portail Azure lorsque vous créez un VM Linux. clé publique de Hello est généralement puis stocké dans `~/.ssh/authorized_keys` sur votre nouvel ordinateur virtuel.

    ![Utiliser la clé publique lorsque vous créez une machine virtuelle dans hello portail Azure](./media/ssh-from-windows/use-public-key-azure-portal.png)
8. Dans **PuTTYgen**, cliquez sur **Enregistrer la clé privée** :

    ![Enregistrer le fichier de clé privée PuTTY](./media/ssh-from-windows/save-ppk-file.png)

   > [!WARNING]
   > Une invite vous demande si vous souhaitez toocontinue sans entrer un mot de passe pour votre clé. Une phrase secrète ressemble à une clé privée attachée tooyour de mot de passe. Même si quelqu'un tooobtain votre clé privée, ils toujours ne serait pas en mesure de tooauthenticate à l’aide de la clé de hello uniquement. Ils ont également besoin hello le mot de passe. Sans une phrase secrète, si quelqu'un obtient votre clé privée, vous pouvez connecter tooany machine virtuelle ou service qui utilise cette clé. Nous vous recommandons de créer une phrase secrète. Toutefois, si vous oubliez le mot de passe hello, il est sans toorecover de façon il.
   >
   >

    Si vous le souhaitez tooenter une phrase secrète, cliquez sur **non**, entrez une phrase secrète dans la fenêtre principale de PuTTYgen hello, puis cliquez sur **clé privée d’enregistrement** à nouveau. Sinon, cliquez sur **Oui** toocontinue sans fournir de mot de passe facultatif hello.
9. Entrez un toosave nom et l’emplacement de votre fichier PPK.

## <a name="use-putty-toossh-tooa-linux-machine"></a>Utiliser Putty tooSSH tooa Linux Machine
Là encore, PuTTY est un client SSH courant pour Windows. Vous est toouse libre n’importe quel client SSH que vous souhaitez. Hello suivant le détail des étapes comment toouse votre tooauthenticate de clé privée avec votre machine virtuelle de Azure à l’aide de SSH. étapes de Hello sont similaires dans d’autres clients de clé SSH en termes d’avoir tooload votre hello tooauthenticate clé privée connexion SSH.

1. Téléchargement et exécution putty de hello suivants emplacement : [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
2. Renseignez le nom d’hôte hello ou adresse IP de votre machine virtuelle à partir de hello portail Azure :

    ![Ouvrir une nouvelle connexion PuTTY](./media/ssh-from-windows/putty-new-connection.png)
3. Avant de sélectionner **Ouvrir**, cliquez sur l’onglet **Connexion** > **SSH** > **Auth**. Parcourir tooand sélectionner votre clé privée :

    ![Sélectionner votre clé privée PuTTY à des fins d’authentification](./media/ssh-from-windows/putty-auth-dialog.png)
4. Cliquez sur **ouvrir** tooconnect tooyour virtuels

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez également générer les clés publiques et privées hello [à l’aide du système d’exploitation X et Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Pour plus d’informations sur Bash pour Windows et les avantages de hello d’outils de systèmes d’exploitation disponibles sur votre ordinateur Windows, consultez [Bash sur Ubuntu sur Windows](https://msdn.microsoft.com/commandline/wsl/about).

Si vous avez des difficultés à l’aide de SSH tooconnect tooyour les machines virtuelles Linux, consultez [tooan dépanner SSH connexions Azure Linux VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
