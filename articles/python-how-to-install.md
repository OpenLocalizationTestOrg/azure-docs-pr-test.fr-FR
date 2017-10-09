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
# <a name="installing-python-and-hello-sdk"></a><span data-ttu-id="9b2c8-103">Installation de Python et hello SDK</span><span class="sxs-lookup"><span data-stu-id="9b2c8-103">Installing Python and hello SDK</span></span>
<span data-ttu-id="9b2c8-104">Python est tooset facile sur Windows et est préinstallé sur le Mac, Linux, et [Bash pour Windows](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="9b2c8-104">Python is easy tooset up on Windows and comes pre-installed on Mac, Linux, and [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span> <span data-ttu-id="9b2c8-105">Ce guide décrit les étapes d'installation et de préparation de votre système à l'utilisation d'Azure.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-105">This guide walks you through installation and getting your machine ready for use with Azure.</span></span>

## <a name="whats-in-hello-python-azure-sdk"></a><span data-ttu-id="9b2c8-106">Ce qui est dans hello Python Azure SDK ?</span><span class="sxs-lookup"><span data-stu-id="9b2c8-106">What's in hello Python Azure SDK?</span></span>
<span data-ttu-id="9b2c8-107">Hello Azure SDK pour Python inclut des composants qui vous permettent de toodevelop, déployer et gérer des applications Python pour Azure.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-107">hello Azure SDK for Python includes components that allow you toodevelop, deploy, and manage Python applications for Azure.</span></span> <span data-ttu-id="9b2c8-108">Hello Azure SDK pour Python comprend des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="9b2c8-108">Specifically, hello Azure SDK for Python includes hello following:</span></span>

* <span data-ttu-id="9b2c8-109">**Bibliothèques de gestion**.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-109">**Management libraries**.</span></span> <span data-ttu-id="9b2c8-110">Ces bibliothèques de classes fournissent une interface de gestion des ressources Azure, comme les comptes de stockage ou les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-110">These class libraries provide an interface managing Azure resources, such as storage accounts, virtual machines.</span></span>
* <span data-ttu-id="9b2c8-111">**Bibliothèques Runtime**.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-111">**Runtime libraries**.</span></span> <span data-ttu-id="9b2c8-112">Ces bibliothèques de classes fournissent une interface permettant d’accéder aux fonctionnalités Azure, notamment le stockage et Service Bus.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-112">These class libraries provide an interface for accessing Azure features, such as storage and service bus.</span></span>

## <a name="which-python-and-which-version-toouse"></a><span data-ttu-id="9b2c8-113">Les Python et le toouse de version</span><span class="sxs-lookup"><span data-stu-id="9b2c8-113">Which Python and which version toouse</span></span>
<span data-ttu-id="9b2c8-114">Il existe différentes versions des interpréteurs Python, par exemple :</span><span class="sxs-lookup"><span data-stu-id="9b2c8-114">There are several flavors of Python interpreters available - examples include:</span></span>

* <span data-ttu-id="9b2c8-115">CPython - hello standard et les plus couramment utilisée interpréteur Python sous %</span><span class="sxs-lookup"><span data-stu-id="9b2c8-115">CPython - hello standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="9b2c8-116">PyPy - rapide et compatible autre implémentation tooCPython</span><span class="sxs-lookup"><span data-stu-id="9b2c8-116">PyPy - fast, compliant alternative implementation tooCPython</span></span>
* <span data-ttu-id="9b2c8-117">IronPython : interpréteur Python qui s'exécute sur .Net/CLR</span><span class="sxs-lookup"><span data-stu-id="9b2c8-117">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="9b2c8-118">Jython - interpréteur Python qui s’exécute sur la Machine virtuelle Java de hello</span><span class="sxs-lookup"><span data-stu-id="9b2c8-118">Jython - Python interpreter that runs on hello Java Virtual Machine</span></span>

<span data-ttu-id="9b2c8-119">**CPython** version2.7 ou v3.3 + et PyPy 5.4.0 sont testés et pris en charge pour hello Python Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-119">**CPython** v2.7 or v3.3+ and PyPy 5.4.0 are tested and supported for hello Python Azure SDK.</span></span>

## <a name="where-tooget-python"></a><span data-ttu-id="9b2c8-120">Où tooget Python ?</span><span class="sxs-lookup"><span data-stu-id="9b2c8-120">Where tooget Python?</span></span>
<span data-ttu-id="9b2c8-121">Il existe plusieurs façons tooget CPython :</span><span class="sxs-lookup"><span data-stu-id="9b2c8-121">There are several ways tooget CPython:</span></span>

* <span data-ttu-id="9b2c8-122">Directement depuis [www.python.org][www.python.org]</span><span class="sxs-lookup"><span data-stu-id="9b2c8-122">Directly from [www.python.org][www.python.org]</span></span>
* <span data-ttu-id="9b2c8-123">Auprès d’un distributeur fiable comme [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] ou [www.activestate.com][www.activestate.com]</span><span class="sxs-lookup"><span data-stu-id="9b2c8-123">From a reputable distro such as [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] or [www.activestate.com][www.activestate.com]</span></span>
* <span data-ttu-id="9b2c8-124">Génération à partir de la source !</span><span class="sxs-lookup"><span data-stu-id="9b2c8-124">Build from source!</span></span>

<span data-ttu-id="9b2c8-125">Sauf si vous avez un besoin spécifique, nous vous recommandons de hello deux premières options.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-125">Unless you have a specific need, we recommend hello first two options.</span></span>

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a><span data-ttu-id="9b2c8-126">Installation du SDK sous Windows, Linux et macOS (bibliothèques client uniquement)</span><span class="sxs-lookup"><span data-stu-id="9b2c8-126">SDK Installation on Windows, Linux, and MacOS (client libraries only)</span></span>
<span data-ttu-id="9b2c8-127">Si vous avez déjà installé de Python, vous pouvez utiliser pip tooinstall un ensemble de toutes les bibliothèques de client hello dans votre environnement de Python 3.3 + ou un existant Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-127">If you already have Python installed, you can use pip tooinstall a bundle of all hello client libraries in your existing Python 2.7 or Python 3.3+ environment.</span></span> <span data-ttu-id="9b2c8-128">Il télécharge les packages de hello de hello [Python Package Index] [ Python Package Index] (PyPI).</span><span class="sxs-lookup"><span data-stu-id="9b2c8-128">This downloads hello packages from hello [Python Package Index][Python Package Index] (PyPI).</span></span>

<span data-ttu-id="9b2c8-129">Vous aurez peut-être besoin de droits d’administrateur :</span><span class="sxs-lookup"><span data-stu-id="9b2c8-129">You may need administrator rights:</span></span>

* <span data-ttu-id="9b2c8-130">Linux et MacOS, utilisez hello `sudo` commande : `sudo pip install azure-mgmt-compute`.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-130">Linux and MacOS, use hello `sudo` command: `sudo pip install azure-mgmt-compute`.</span></span>
* <span data-ttu-id="9b2c8-131">Windows : ouvrez votre invite de commandes/PowerShell en tant qu’administrateur</span><span class="sxs-lookup"><span data-stu-id="9b2c8-131">Windows: open your PowerShell/Command prompt as an administrator</span></span>

<span data-ttu-id="9b2c8-132">Vous pouvez installer chaque bibliothèque individuellement pour chaque service Azure :</span><span class="sxs-lookup"><span data-stu-id="9b2c8-132">You can install individually each library for each Azure service:</span></span>

```console
   $ pip install azure-batch          # Install hello latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install hello latest Storage management library
```

<span data-ttu-id="9b2c8-133">Packages de la version préliminaire peuvent être installés à l’aide de hello `--pre` indicateur :</span><span class="sxs-lookup"><span data-stu-id="9b2c8-133">Preview packages can be installed using hello `--pre` flag:</span></span>

```console
   $ pip install --pre azure-mgmt-compute # installs only hello latest Compute Management library
```

<span data-ttu-id="9b2c8-134">Vous pouvez également installer un ensemble de bibliothèques Azure dans une seule ligne à l’aide de hello `azure` méta-package.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-134">You can also install a set of Azure libraries in a single line using hello `azure` meta-package.</span></span> <span data-ttu-id="9b2c8-135">Puisque pas tous les packages de ce package de métadonnées sont publiées stable, hello `azure` méta-package est toujours en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-135">Since not all packages in this meta-package are published as stable yet, hello `azure` meta-package is still in preview.</span></span>
<span data-ttu-id="9b2c8-136">Toutefois, des packages de base hello, selon les perspectives code qualité/exhaustivité peuvent être considéré comme « stables » pour l’instant</span><span class="sxs-lookup"><span data-stu-id="9b2c8-136">However, hello core packages, from code quality/completeness perspectives can be considered "stable" at this time</span></span>

* <span data-ttu-id="9b2c8-137">ils sont officiellement étiquetés comme tels dans la synchronisation avec d’autres langues, dès que possible.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-137">it is officially labeled as such in sync with other languages as soon as possible.</span></span>
  <span data-ttu-id="9b2c8-138">Nous ne prévoyons pas d’autres changements majeurs d’ici-là.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-138">We are not planning on any further major changes until then.</span></span>

<span data-ttu-id="9b2c8-139">S’agissant d’une version préliminaire, vous devez toouse hello `--pre` indicateur :</span><span class="sxs-lookup"><span data-stu-id="9b2c8-139">Since it's a preview release, you need toouse hello `--pre` flag:</span></span>

```console
   $ pip install --pre azure
```

<span data-ttu-id="9b2c8-140">ou directement</span><span class="sxs-lookup"><span data-stu-id="9b2c8-140">or directly</span></span>

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a><span data-ttu-id="9b2c8-141">Téléchargement d'autres packages</span><span class="sxs-lookup"><span data-stu-id="9b2c8-141">Getting More Packages</span></span>
<span data-ttu-id="9b2c8-142">Hello [Python Package Index] [ Python Package Index] (PyPI) a une sélection enrichie des bibliothèques de Python.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-142">hello [Python Package Index][Python Package Index] (PyPI) has a rich selection of Python libraries.</span></span>  <span data-ttu-id="9b2c8-143">Si vous avez choisi tooinstall un distributeur, vous aurez déjà la plupart des hello intéressants bits pour différents scénarios de web development tooTechnical Computing.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-143">If you chose tooinstall a Distro, you'll already have most of hello interesting bits for various scenarios from web development tooTechnical Computing.</span></span>

## <a name="python-tools-for-visual-studio"></a><span data-ttu-id="9b2c8-144">Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9b2c8-144">Python Tools for Visual Studio</span></span>
<span data-ttu-id="9b2c8-145">[Python Tools for Visual Studio][Python Tools pour Visual Studio] (PTVS) est un plug-in gratuit/OSS de Microsoft, qui transforme Visual Studio en un environnement de développement intégré (IDE) Python à part entière :</span><span class="sxs-lookup"><span data-stu-id="9b2c8-145">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) is a free/OSS plugin from Microsoft, which turns VS into a full-fledged Python IDE:</span></span>

![how-to-install-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

<span data-ttu-id="9b2c8-147">Nous vous recommandons d’utiliser PTVS même s’il est facultatif, car il vous apporte pour les projets/solutions Python et web les fonctionnalités suivantes : support technique, débogage, profilage, fenêtre interactive, modification des modèles et Intellisense.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-147">Using PTVS is optional, but is recommended as it gives you Python and Web Project/Solution support, debugging, profiling, interactive window, Template editing, and Intellisense.</span></span>

<span data-ttu-id="9b2c8-148">PTVS rend également facile toodeploy tooMicrosoft Azure, avec prise en charge pour le déploiement trop[Services de cloud computing](cloud-services/cloud-services-python-ptvs.md) et [sites Web](app-service-web/web-sites-python-ptvs-django-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="9b2c8-148">PTVS also makes it easy toodeploy tooMicrosoft Azure, with support for deployment too[Cloud Services](cloud-services/cloud-services-python-ptvs.md) and [Websites](app-service-web/web-sites-python-ptvs-django-mysql.md).</span></span>

<span data-ttu-id="9b2c8-149">PTVS fonctionne avec votre installation existante de Visual Studio 2013, 2015 ou 2017.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-149">PTVS works with your existing Visual Studio 2013, 2015, or 2017 installation.</span></span>  <span data-ttu-id="9b2c8-150">Pour accéder à la documentation, aux téléchargements et aux discussions, consultez le site [Python Tools pour Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="9b2c8-150">For documentation, downloads and discussions, see [Python Tools for Visual Studio].</span></span>  

## <a name="python-azure-scenarios-for-linux-and-macos"></a><span data-ttu-id="9b2c8-151">Scénarios Python Azure pour Linux et MacOS</span><span class="sxs-lookup"><span data-stu-id="9b2c8-151">Python Azure Scenarios for Linux and MacOS</span></span>
<span data-ttu-id="9b2c8-152">Pour Linux et macOS, les principaux scénarios Azure pris en charge sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="9b2c8-152">For Linux or MacOS, main Azure scenarios that are supported:</span></span>

1. <span data-ttu-id="9b2c8-153">Consommation de Services Azure à l’aide des bibliothèques clientes de hello pour Python</span><span class="sxs-lookup"><span data-stu-id="9b2c8-153">Consuming Azure Services by using hello client libraries for Python</span></span>
2. <span data-ttu-id="9b2c8-154">Exécution de votre application sur une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="9b2c8-154">Running your app in a Linux VM</span></span>
3. <span data-ttu-id="9b2c8-155">Développement et tooAzure sites Web de publication à l’aide de Git</span><span class="sxs-lookup"><span data-stu-id="9b2c8-155">Developing and publishing tooAzure Websites using Git</span></span>

<span data-ttu-id="9b2c8-156">premier scénario de Hello vous permet de tooauthor web riches applications qui tirent parti des hello PaaS Azure fonctionnalités telles que [stockage d’objets blob](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [file d’attente de stockage](storage/queues/storage-python-how-to-use-queue-storage.md), [stockage de table](cosmos-db/table-storage-how-to-use-python.md) etc. via des wrappers Pythonic pour hello API REST Azure.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-156">hello first scenario enables you tooauthor rich web apps that take advantage of hello Azure PaaS capabilities such as [blob storage](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [queue storage](storage/queues/storage-python-how-to-use-queue-storage.md), [table storage](cosmos-db/table-storage-how-to-use-python.md) etc. via Pythonic wrappers for hello Azure REST APIs.</span></span> <span data-ttu-id="9b2c8-157">Le fonctionnement de ces derniers est identique sous Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-157">These work identically on Windows, Mac, and Linux.</span></span>  <span data-ttu-id="9b2c8-158">Vous pouvez également utiliser ces bibliothèques clientes à partir de votre ordinateur de développement local ou une machine virtuelle Linux s'exécutant sur Azure.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-158">You can also use these client libraries from your local development machine or a Linux VM running on Azure.</span></span>

<span data-ttu-id="9b2c8-159">Pour le scénario de machine virtuelle hello, vous simplement démarrez un VM Linux de votre choix (Ubuntu, CentOS, Suse) et vous souhaitez exécuter et gérez.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-159">For hello VM scenario, you simply start a Linux VM of your choice (Ubuntu, CentOS, Suse) and run/manage what you like.</span></span>  <span data-ttu-id="9b2c8-160">Par exemple, vous pouvez exécuter [IPython] [ IPython] REPL/ordinateur portable sur votre ordinateur Mac/Windows/Linux et d’un point de votre navigateur tooa Linux ou l’exécution des machines virtuelles Windows multi-processeurs hello moteur notebooks sur Azure.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-160">As an example, you can run [IPython][IPython] REPL/notebook on your Windows/Mac/Linux machine and point your browser tooa Linux or Windows multi-proc VM running hello IPython Engine on Azure.</span></span>

<span data-ttu-id="9b2c8-161">Pour plus d’informations sur la façon de tooset d’un VM Linux, consultez hello [créer une Machine virtuelle exécutant Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-161">For information on how tooset up a Linux VM, see hello [Create a Virtual Machine Running Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.</span></span>

<span data-ttu-id="9b2c8-162">À l’aide du déploiement Git, vous pouvez développer une application web de Python et publiez-le tooan site Web Azure à partir de n’importe quel système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-162">Using Git deployment, you can develop a Python web application and publish it tooan Azure Website from any operating system.</span></span>  <span data-ttu-id="9b2c8-163">Lorsque vous appuyez sur votre tooAzure référentiel, il crée automatiquement un environnement virtuel et pip installe les packages requis.</span><span class="sxs-lookup"><span data-stu-id="9b2c8-163">When you push your repository tooAzure, it automatically creates a virtual environment and pip installs your required packages.</span></span>

<span data-ttu-id="9b2c8-164">Pour plus d’informations sur le développement et la publication de sites Web Azure, consultez les didacticiels hello pour [création de sites Web avec Django](app-service-web/web-sites-python-create-deploy-django-app.md), [création de sites Web avec Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), et [création de sites Web avec Ballon](app-service-web/web-sites-python-create-deploy-flask-app.md).</span><span class="sxs-lookup"><span data-stu-id="9b2c8-164">For more information on developing and publishing Azure Websites, see hello tutorials for [Creating Websites with Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Creating Websites with Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), and [Creating Websites with Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span></span> <span data-ttu-id="9b2c8-165">Pour des informations plus générales sur l’utilisation de n’importe quelle infrastructure compatible WSGI, consultez [Configuration de Python avec des Sites Web Azure](app-service-web/web-sites-python-configure.md).</span><span class="sxs-lookup"><span data-stu-id="9b2c8-165">For more general information on using any WSGI-compliant framework, see [Configuring Python with Azure Websites](app-service-web/web-sites-python-configure.md).</span></span>

## <a name="additional-software-and-resources"></a><span data-ttu-id="9b2c8-166">Logiciels et ressources supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="9b2c8-166">Additional Software and Resources:</span></span>
* [<span data-ttu-id="9b2c8-167">Kit de développement logiciel (SDK) Azure pour Python Read The Docs</span><span class="sxs-lookup"><span data-stu-id="9b2c8-167">Azure SDK for Python ReadTheDocs</span></span>](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [<span data-ttu-id="9b2c8-168">Kit de développement logiciel (SDK) Azure pour Python GitHub</span><span class="sxs-lookup"><span data-stu-id="9b2c8-168">Azure SDK for Python GitHub</span></span>](https://github.com/Azure/azure-sdk-for-python)
* [<span data-ttu-id="9b2c8-169">Exemples Azure officiels pour Python</span><span class="sxs-lookup"><span data-stu-id="9b2c8-169">Official Azure samples for Python</span></span>](https://azure.microsoft.com/documentation/samples/?platform=python)
* <span data-ttu-id="9b2c8-170">[Distribution de Python par Continuum Analytics (en anglais)][Continuum Analytics Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="9b2c8-170">[Continuum Analytics Python Distribution][Continuum Analytics Python Distribution]</span></span>
* <span data-ttu-id="9b2c8-171">[Distribution de Python par Enthought (en anglais)][Enthought Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="9b2c8-171">[Enthought Python Distribution][Enthought Python Distribution]</span></span>
* <span data-ttu-id="9b2c8-172">[Distribution de Python par ActiveState (en anglais)][ActiveState Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="9b2c8-172">[ActiveState Python Distribution][ActiveState Python Distribution]</span></span>
* <span data-ttu-id="9b2c8-173">[SciPy : un vaste panel de bibliothèques Scientific Python (en anglais)][SciPy - A suite of Scientific Python libraries]</span><span class="sxs-lookup"><span data-stu-id="9b2c8-173">[SciPy - A suite of Scientific Python libraries][SciPy - A suite of Scientific Python libraries]</span></span>
* <span data-ttu-id="9b2c8-174">[NumPy : une bibliothèque de valeurs numériques pour Python (en anglais)][NumPy - A numerics library for Python]</span><span class="sxs-lookup"><span data-stu-id="9b2c8-174">[NumPy - A numerics library for Python][NumPy - A numerics library for Python]</span></span>
* <span data-ttu-id="9b2c8-175">[Projet Django : une infrastructure web/un système de gestion du contenu arrivés à maturité (en anglais)][Django Project - A mature web framework/CMS]</span><span class="sxs-lookup"><span data-stu-id="9b2c8-175">[Django Project - A mature web framework/CMS][Django Project - A mature web framework/CMS]</span></span>
* <span data-ttu-id="9b2c8-176">[IPython : une solution REPL/Notebook avancée pour Python (en anglais)][IPython - an advanced REPL/Notebook for Python]</span><span class="sxs-lookup"><span data-stu-id="9b2c8-176">[IPython - an advanced REPL/Notebook for Python][IPython - an advanced REPL/Notebook for Python]</span></span>
* <span data-ttu-id="9b2c8-177">[Python Tools pour Visual Studio sur GitHub][Python Tools for Visual Studio on GitHub]</span><span class="sxs-lookup"><span data-stu-id="9b2c8-177">[Python Tools for Visual Studio on GitHub][Python Tools for Visual Studio on GitHub]</span></span>
* [<span data-ttu-id="9b2c8-178">Centre de développement Python</span><span class="sxs-lookup"><span data-stu-id="9b2c8-178">Python Developer Center</span></span>](/develop/python/)

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
