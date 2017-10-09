---
title: aaaInstall Python et hello SDK - Azure
description: "Découvrez comment tooinstall Python et hello toouse de kit de développement logiciel Azure."
services: 
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: f36294be-daeb-4caf-9129-fce18130f552
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 09/06/2016
ms.author: lmazuel
ms.openlocfilehash: c1b394770f9abd3e654a23d79ae179a9af89e2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="installing-python-and-hello-sdk"></a>Installation de Python et hello SDK
Python est tooset facile sur Windows et est préinstallé sur le Mac, Linux, et [Bash pour Windows](https://msdn.microsoft.com/commandline/wsl/about). Ce guide décrit les étapes d'installation et de préparation de votre système à l'utilisation d'Azure.

## <a name="whats-in-hello-python-azure-sdk"></a>Ce qui est dans hello Python Azure SDK ?
Hello Azure SDK pour Python inclut des composants qui vous permettent de toodevelop, déployer et gérer des applications Python pour Azure. Hello Azure SDK pour Python comprend des éléments suivants de hello :

* **Bibliothèques de gestion**. Ces bibliothèques de classes fournissent une interface de gestion des ressources Azure, comme les comptes de stockage ou les machines virtuelles.
* **Bibliothèques Runtime**. Ces bibliothèques de classes fournissent une interface permettant d’accéder aux fonctionnalités Azure, notamment le stockage et Service Bus.

## <a name="which-python-and-which-version-toouse"></a>Les Python et le toouse de version
Il existe différentes versions des interpréteurs Python, par exemple :

* CPython - hello standard et les plus couramment utilisée interpréteur Python sous %
* PyPy - rapide et compatible autre implémentation tooCPython
* IronPython : interpréteur Python qui s'exécute sur .Net/CLR
* Jython - interpréteur Python qui s’exécute sur la Machine virtuelle Java de hello

**CPython** version2.7 ou v3.3 + et PyPy 5.4.0 sont testés et pris en charge pour hello Python Azure SDK.

## <a name="where-tooget-python"></a>Où tooget Python ?
Il existe plusieurs façons tooget CPython :

* Directement depuis [www.python.org][www.python.org]
* Auprès d’un distributeur fiable comme [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] ou [www.activestate.com][www.activestate.com]
* Génération à partir de la source !

Sauf si vous avez un besoin spécifique, nous vous recommandons de hello deux premières options.

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a>Installation du SDK sous Windows, Linux et macOS (bibliothèques client uniquement)
Si vous avez déjà installé de Python, vous pouvez utiliser pip tooinstall un ensemble de toutes les bibliothèques de client hello dans votre environnement de Python 3.3 + ou un existant Python 2.7. Il télécharge les packages de hello de hello [Python Package Index] [ Python Package Index] (PyPI).

Vous aurez peut-être besoin de droits d’administrateur :

* Linux et MacOS, utilisez hello `sudo` commande : `sudo pip install azure-mgmt-compute`.
* Windows : ouvrez votre invite de commandes/PowerShell en tant qu’administrateur

Vous pouvez installer chaque bibliothèque individuellement pour chaque service Azure :

```console
   $ pip install azure-batch          # Install hello latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install hello latest Storage management library
```

Packages de la version préliminaire peuvent être installés à l’aide de hello `--pre` indicateur :

```console
   $ pip install --pre azure-mgmt-compute # installs only hello latest Compute Management library
```

Vous pouvez également installer un ensemble de bibliothèques Azure dans une seule ligne à l’aide de hello `azure` méta-package. Puisque pas tous les packages de ce package de métadonnées sont publiées stable, hello `azure` méta-package est toujours en version préliminaire.
Toutefois, des packages de base hello, selon les perspectives code qualité/exhaustivité peuvent être considéré comme « stables » pour l’instant

* ils sont officiellement étiquetés comme tels dans la synchronisation avec d’autres langues, dès que possible.
  Nous ne prévoyons pas d’autres changements majeurs d’ici-là.

S’agissant d’une version préliminaire, vous devez toouse hello `--pre` indicateur :

```console
   $ pip install --pre azure
```

ou directement

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a>Téléchargement d'autres packages
Hello [Python Package Index] [ Python Package Index] (PyPI) a une sélection enrichie des bibliothèques de Python.  Si vous avez choisi tooinstall un distributeur, vous aurez déjà la plupart des hello intéressants bits pour différents scénarios de web development tooTechnical Computing.

## <a name="python-tools-for-visual-studio"></a>Python Tools for Visual Studio
[Python Tools for Visual Studio][Python Tools pour Visual Studio] (PTVS) est un plug-in gratuit/OSS de Microsoft, qui transforme Visual Studio en un environnement de développement intégré (IDE) Python à part entière :

![how-to-install-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

Nous vous recommandons d’utiliser PTVS même s’il est facultatif, car il vous apporte pour les projets/solutions Python et web les fonctionnalités suivantes : support technique, débogage, profilage, fenêtre interactive, modification des modèles et Intellisense.

PTVS rend également facile toodeploy tooMicrosoft Azure, avec prise en charge pour le déploiement trop[Services de cloud computing](cloud-services/cloud-services-python-ptvs.md) et [sites Web](app-service-web/web-sites-python-ptvs-django-mysql.md).

PTVS fonctionne avec votre installation existante de Visual Studio 2013, 2015 ou 2017.  Pour accéder à la documentation, aux téléchargements et aux discussions, consultez le site [Python Tools pour Visual Studio].  

## <a name="python-azure-scenarios-for-linux-and-macos"></a>Scénarios Python Azure pour Linux et MacOS
Pour Linux et macOS, les principaux scénarios Azure pris en charge sont les suivants :

1. Consommation de Services Azure à l’aide des bibliothèques clientes de hello pour Python
2. Exécution de votre application sur une machine virtuelle Linux
3. Développement et tooAzure sites Web de publication à l’aide de Git

premier scénario de Hello vous permet de tooauthor web riches applications qui tirent parti des hello PaaS Azure fonctionnalités telles que [stockage d’objets blob](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [file d’attente de stockage](storage/queues/storage-python-how-to-use-queue-storage.md), [stockage de table](cosmos-db/table-storage-how-to-use-python.md) etc. via des wrappers Pythonic pour hello API REST Azure. Le fonctionnement de ces derniers est identique sous Windows, Mac et Linux.  Vous pouvez également utiliser ces bibliothèques clientes à partir de votre ordinateur de développement local ou une machine virtuelle Linux s'exécutant sur Azure.

Pour le scénario de machine virtuelle hello, vous simplement démarrez un VM Linux de votre choix (Ubuntu, CentOS, Suse) et vous souhaitez exécuter et gérez.  Par exemple, vous pouvez exécuter [IPython] [ IPython] REPL/ordinateur portable sur votre ordinateur Mac/Windows/Linux et d’un point de votre navigateur tooa Linux ou l’exécution des machines virtuelles Windows multi-processeurs hello moteur notebooks sur Azure.

Pour plus d’informations sur la façon de tooset d’un VM Linux, consultez hello [créer une Machine virtuelle exécutant Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) didacticiel.

À l’aide du déploiement Git, vous pouvez développer une application web de Python et publiez-le tooan site Web Azure à partir de n’importe quel système d’exploitation.  Lorsque vous appuyez sur votre tooAzure référentiel, il crée automatiquement un environnement virtuel et pip installe les packages requis.

Pour plus d’informations sur le développement et la publication de sites Web Azure, consultez les didacticiels hello pour [création de sites Web avec Django](app-service-web/web-sites-python-create-deploy-django-app.md), [création de sites Web avec Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), et [création de sites Web avec Ballon](app-service-web/web-sites-python-create-deploy-flask-app.md). Pour des informations plus générales sur l’utilisation de n’importe quelle infrastructure compatible WSGI, consultez [Configuration de Python avec des Sites Web Azure](app-service-web/web-sites-python-configure.md).

## <a name="additional-software-and-resources"></a>Logiciels et ressources supplémentaires :
* [Kit de développement logiciel (SDK) Azure pour Python Read The Docs](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [Kit de développement logiciel (SDK) Azure pour Python GitHub](https://github.com/Azure/azure-sdk-for-python)
* [Exemples Azure officiels pour Python](https://azure.microsoft.com/documentation/samples/?platform=python)
* [Distribution de Python par Continuum Analytics (en anglais)][Continuum Analytics Python Distribution]
* [Distribution de Python par Enthought (en anglais)][Enthought Python Distribution]
* [Distribution de Python par ActiveState (en anglais)][ActiveState Python Distribution]
* [SciPy : un vaste panel de bibliothèques Scientific Python (en anglais)][SciPy - A suite of Scientific Python libraries]
* [NumPy : une bibliothèque de valeurs numériques pour Python (en anglais)][NumPy - A numerics library for Python]
* [Projet Django : une infrastructure web/un système de gestion du contenu arrivés à maturité (en anglais)][Django Project - A mature web framework/CMS]
* [IPython : une solution REPL/Notebook avancée pour Python (en anglais)][IPython - an advanced REPL/Notebook for Python]
* [Python Tools pour Visual Studio sur GitHub][Python Tools for Visual Studio on GitHub]
* [Centre de développement Python](/develop/python/)

[Continuum Analytics Python Distribution]: http://continuum.io
[Enthought Python Distribution]: http://www.enthought.com
[ActiveState Python Distribution]: http://www.activestate.com
[www.python.org]: http://www.python.org
[www.continuum.io]: http://continuum.io
[www.enthought.com]: http://www.enthought.com
[www.activestate.com]: http://www.activestate.com
[SciPy - A suite of Scientific Python libraries]: http://www.scipy.org
[NumPy - A numerics library for Python]: http://www.numpy.org
[Django Project - A mature web framework/CMS]: http://www.djangoproject.com
[IPython - an advanced REPL/Notebook for Python]: http://ipython.org
[IPython]: http://ipython.org
[IPython Notebook on Azure]: virtual-machines-linux-jupyter-notebook.md
[Cloud Services]: cloud-services-python-ptvs.md
[Websites]: web-sites-python-ptvs-django-mysql.md
[Python Tools pour Visual Studio]: http://aka.ms/ptvs
[Python Tools for Visual Studio on GitHub]: https://github.com/microsoft/ptvs
[Python Package Index]: http://pypi.python.org/pypi
[Microsoft Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?LinkId=254281
[Microsoft Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?LinkID=516990
[Setting up a Linux VM via hello Azure portal]: create-and-configure-opensuse-vm-in-portal.md
[How toouse hello Azure Command-Line Interface]: crossplat-cmd-tools.md
[Create a Virtual Machine Running Linux]: virtual-machines-linux-quick-create-cli.md
[Creating Websites with Django]: web-sites-python-create-deploy-django-app.md
[Creating Websites with Bottle]: web-sites-python-create-deploy-bottle-app.md
[Creating Websites with Flask]: web-sites-python-create-deploy-flask-app.md
[Configuring Python with Azure Websites]: web-sites-python-configure.md
[table storage]: storage-python-how-to-use-table-storage.md
[queue storage]: storage-python-how-to-use-queue-storage.md
[blob storage]:storage/blobs/storage-python-how-to-use-blob-storage.md
