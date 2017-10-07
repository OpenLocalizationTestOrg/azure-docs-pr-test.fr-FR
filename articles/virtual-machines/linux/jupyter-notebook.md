---
title: aaaCreate un bloc-notes Notebook/notebooks | Documents Microsoft
description: "Découvrez comment toodeploy hello Notebook/notebooks bloc-notes sur une machine virtuelle Linux créé avec le modèle de déploiement resource manager hello dans Azure."
services: virtual-machines-linux
documentationcenter: python
author: crwilcox
manager: wpickett
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 519f36dd-865e-4c1d-abe7-b87037796aa7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 11/10/2015
ms.author: crwilcox
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d7f2e45a8ba95163ebfb0f10babc91a2b3fd9390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a>Création d’une machine virtuelle Azure, installation de Jupyter et exécution d’un Notebook Jupyter sur Azure
Hello [Notebook projet](http://jupyter.org), anciennement hello [notebooks projet](http://ipython.org), fournit un ensemble d’outils pour le calcul scientifique à l’aide du puissants interpréteurs de commandes interactives qui combinent l’exécution du code de création de hello du calcul de document dynamique. Ces fichiers de l'interpréteur contiennent du texte arbitraire, des formules mathématiques, un code d'entrée, des résultats, des graphiques, des vidéos et d'autres sortes de support qu'un navigateur Web moderne peut afficher. Si vous êtes absolument nouveau tooPython et que vous souhaitez toolearn dans un fun, un environnement interactif ou effectuez quelques grave parallèle/technique informatique, hello bloc-notes Jupyter est un bon choix.

![Capture d’écran de](./media/jupyter-notebook/ipy-notebook-spectral.png) à l’aide de SciPy Matplotlib packages tooanalyze hello structure et d’un enregistrement audio.

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a>Jupyter en deux modes : Azure Notebooks ou déploiement personnalisé
Azure fournit un service que vous pouvez utiliser trop[commencer rapidement à l’aide du bloc-notes ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).  À l’aide de hello Azure bloc-notes Service, vous pouvez facilement accéder interface accessibles par le web de tooJupyter d’accès aux ressources de calculs évolutives avec tous les power hello de Python et ses nombreuses bibliothèques.  Étant donné que l’installation de hello est gérée par le service de hello, les utilisateurs peuvent accéder à ces ressources sans avoir besoin de hello pour l’administration et de configuration par l’utilisateur de hello.

Si le service de bloc-notes hello ne fonctionne pas pour votre scénario continuer tooread cet article qui seront vous montrera comment toodeploy hello bloc-notes Jupyter sur Microsoft Azure, à l’aide de Linux virtual machines virtuelles.

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a>Créer et configurer une machine virtuelle sur Azure
première étape de Hello est toocreate un ordinateur virtuel (VM) s’exécutant sur Azure.
Cet ordinateur virtuel est un système d’exploitation complet dans le cloud de hello et servira à exécuter hello bloc-notes Jupyter. Azure est capable d’exécuter des machines virtuelles Linux et Windows, et nous allons aborder, le programme d’installation de hello de Notebook sur les deux types d’ordinateurs virtuels.

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a>Créer une machine virtuelle Linux et ouvrir un port pour Jupyter
Suivez les instructions de hello données [ici] [ portal-vm-linux] toocreate une machine virtuelle de hello *Ubuntu* distribution. Ce didacticiel utilise Ubuntu Server 14.04 LTS. Nous supposons que nom d’utilisateur hello *azureuser*.

Une fois que la machine virtuelle de hello déploie, nous devons tooopen une règle de sécurité de groupe de sécurité réseau hello.  À partir de hello portail Azure, accédez trop**groupes de sécurité réseau** et ouvrez hello pour tooyour correspondante du groupe de sécurité hello machine virtuelle. Vous devez tooadd une règle de sécurité de trafic entrant avec hello suivant paramètres : **TCP** pour le protocole de hello,  **\***  pour le port de la source (public) hello et **9999** pour port de destination (privé) Hello.

![Capture d'écran](./media/jupyter-notebook/azure-add-endpoint.png)

Dans votre groupe de sécurité réseau, cliquez sur **Interfaces réseau** et Remarque Bonjour **adresse IP publique** car elle sera nécessaire tooconnect tooyour machine virtuelle à l’étape suivante de hello.

## <a name="install-required-software-on-hello-vm"></a>Installer les logiciels requis sur la machine virtuelle de hello
toorun hello bloc-notes Jupyter sur notre machine virtuelle, nous devons d’abord installer Notebook et ses dépendances. Connecter la machine virtuelle linux de tooyour à l’aide de ssh et paire nom d’utilisateur/mot de passe de hello choisis lors de la création hello machine virtuelle. Dans ce didacticiel, nous utiliserons PuTTY pour nous connecter à partir de Windows.

### <a name="installing-jupyter-on-ubuntu"></a>Installation de Jupyter sur Ubuntu
Installer Anaconda, une distribution de python de science des données courants, à l’aide d’un des liens hello fournis par [Continuum Analytique](https://www.continuum.io/downloads).  Au moment de rédaction hello de ce document, hello liens ci-dessous sont hello plus de versions de toodate.

#### <a name="anaconda-installs-for-linux"></a>Installations Anaconda pour Linux
<table>
  <th>Python 3.4</th>
  <th>Python 2.7</th>
  <tr>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bits</href>
    </td>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bits</href>
    </td>
  </tr>
  <tr>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bits</href>
    </td>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bits</href>
    </td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a>Installation d’Anaconda3 2.3.0 64 bits sur Ubuntu
Voici un exemple d’installation d’Anaconda sur Ubuntu

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter toohello latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![Capture d'écran](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a>Configuration de Jupyter et utilisation de SSL
Après l’installation de nous devons tootake un fichier de configuration actuellement toosetup hello pour notebook. Si vous rencontrez des problèmes de configuration disponible, il peut être utile toolook à hello [Documentation disponible pour l’exécution d’un serveur de l’ordinateur portable](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).

Suivant nous `cd` toohello profil Active toocreate notre certificat SSL et modifier le fichier de configuration de profils hello.

Sur Linux, utilisez hello commande suivante.

    cd ~/.jupyter

Utilisez hello suivant le certificat SSL hello commande de toocreate (Linux et Windows).

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

Notez qu’étant donné que nous allons créer un certificat SSL auto-signé, lors de la connexion toohello bloc-notes votre navigateur vous donne un avertissement de sécurité.  Pour la production à long terme, vous pouvez toouse un certificat signé correctement associé à votre organisation.  Étant donné que la gestion des certificats n’est pas abordée de hello de cette démonstration, nous tiendrons tooa un certificat auto-signé pour l’instant.

En outre toousing un certificat, vous devez également fournir un mot de passe tooprotect votre ordinateur portable à partir de toute utilisation non autorisée.  Pour des raisons de sécurité Notebook utilise des mots de passe chiffrés dans son fichier de configuration, vous devez tooencrypt votre mot de passe tout d’abord.  IPython fournit un utilitaire toodo à l’invite de commandes, exécutez hello commande suivante.

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

Cela vous demandera un mot de passe et la confirmation et imprime ensuite le mot de passe hello. Notez ce pourquoi suivant l’étape.

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided hello rest for security)

Ensuite, nous allons modifier le fichier de configuration du profil hello, qui est le `jupyter_notebook_config.py` fichier répertoire hello dans.  Notez que ce fichier n’existe pas, créez simplement les cas de hello.  Ce fichier comporte de nombreux champs, tous commentés par défaut.  Vous pouvez ouvrir ce fichier avec un éditeur de texte de vos besoins, et vous devez vous assurer qu’il a au moins hello après le contenu. **Être c.NotebookApp.password de hello tooreplace que dans la configuration de hello avec sha1 hello à partir de l’étape précédente de hello**.

    c = get_config()

    # You must give hello path toohello certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-hello-jupyter-notebook"></a>Exécutez hello bloc-notes Jupyter
À ce stade, nous sommes prêts toostart hello bloc-notes Jupyter. toodo, accédez répertoire toohello vous souhaitez toostore portables dans et commencer hello server de bloc-notes Jupyter hello commande suivante.

    /anaconda3/bin/jupyter-notebook

Vous devez maintenant être en mesure de tooaccess votre bloc-notes Jupyter adresse hello `https://[PUBLIC-IP-ADDRESS]:9999`.

Lorsque vous accédez à votre ordinateur portable tout d’abord, page de connexion hello vous demande votre mot de passe. Et une fois que vous vous connectez, vous verrez hello « Tableau de bord Notebook portables », qui est le centre de contrôle pour toutes les opérations de l’ordinateur portable.  Dans cette page, vous pouvez créer des interpréteurs et ouvrir des interpréteurs existants.

![Capture d'écran](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-hello-jupyter-notebook"></a>À l’aide de hello bloc-notes Jupyter
Si vous cliquez sur hello **nouveau** bouton, vous verrez hello après l’ouverture de la page.

![Capture d'écran](./media/jupyter-notebook/jupyter-untitled-notebook.png)

zone de Hello marqués avec un `In []:` invite est la zone d’entrée de hello et ici, vous pouvez taper n’importe quel code Python valide et il ne s’exécute lorsque vous atteignez `Shift-Enter` ou sur l’icône de « Lire » hello (hello pointant vers la droite triangle dans la barre d’outils hello).

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a>Un puissant paradigme : documents de calcul dynamique avec des supports puissants
bloc-notes Hello lui-même devriez vous sentir tooanyone très naturelle ayant utilisé Python et un traitement de texte, car il est une combinaison des deux à certains égards : vous pouvez exécuter des blocs de code Python, mais vous pouvez également conserver des notes et tout autre texte en modifiant le style de hello d’une cellule à partir de « Code » trop « Ma rkdown » à l’aide du menu déroulant de hello dans la barre d’outils.

Jupyter est bien plus qu’un traitement de texte, car il permet l’association de calculs et de supports puissants (texte, graphiques, vidéos et, virtuellement, tout ce qu’un navigateur web actuel peut afficher). Vous pouvez associer du texte, du code, des vidéos et bien plus encore !

![Capture d'écran](./media/jupyter-notebook/jupyter-editing-experience.png)

Et avec la puissance de hello de nombreuses bibliothèques excellents Python informatique scientifiques et techniques, Bonjour suivant capture d’écran, un calcul simple peut être effectué avec hello même faciliter en tant qu’une analyse de réseau complexes, dans un environnement.

Ce paradigme de mélange power hello du site web moderne hello avec calcul dynamique offre de nombreuses possibilités et convient parfaitement pour le cloud de hello ; Hello bloc-notes peut être utilisée :

* Un toorecord bloc-notes calcul exploratoire de travailler sur un problème.
* tooshare résultats avec vos collègues, dans le formulaire de calcul « live » ou dans des formats de papier (HTML, PDF).
* toodistribute présent matériaux apprentissage dynamique qui impliquent le calcul, les étudiants peuvent immédiatement procéder à des essais avec le code réel de hello, modifier et exécuter de nouveau interactivement.
* tooprovide « livres exécutables » qui présentent des résultats hello de la recherche d’une façon qui peut être reproduite immédiatement, validé et étendu par d’autres.
* En tant que plateforme de collaboration de calcul : plusieurs utilisateurs peuvent se connecter toothe même serveur jupyter tooshare une session de calcul en temps réel.

Si vous passez le code source de IPython toohello [référentiel][repository], vous trouverez un répertoire entier avec des exemples d’ordinateur portable que vous pouvez télécharger et expérimenter sur votre propre machine virtuelle de Azure disponible.  Il suffit de télécharger hello `.ipynb` fichiers hello de site et les télécharger sur le tableau de bord hello de votre machine virtuelle Azure bloc-notes (ou les télécharger directement sur hello machine virtuelle).

## <a name="conclusion"></a>Conclusion
Hello bloc-notes Jupyter fournit une interface puissante pour accéder aux interactivement power hello de l’écosystème de Python hello sur Azure.  Il couvre une large gamme de cas d'utilisation, notamment les simples exploration et apprentissage de Python, l'analyse et la visualisation des données, le calcul de simulation et parallèle. Hello résultant bloc-notes documents contiennent d’un enregistrement complet de calculs hello qui sont effectuées et peuvent être partagées avec d’autres utilisateurs du bloc-notes.  Hello bloc-notes Jupyter peut être utilisé en tant qu’une application locale, mais il convient parfaitement aux déploiements de cloud sur Azure

Hello principales fonctionnalités des Notebook sont également disponibles à l’intérieur de Visual Studio via la [outils Python pour Visual Studio] [ Python Tools for Visual Studio] (PTVS). PTVS est un plug-in open source gratuit de Microsoft qui transforme Visual Studio en environnement de développement Python avancé qui inclut un éditeur avancé avec IntelliSense, ainsi qu'une intégration de débogage, de profilage et de calcul parallèle.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez hello [centre de développement Python](/develop/python/).

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
