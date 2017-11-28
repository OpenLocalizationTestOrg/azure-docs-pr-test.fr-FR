---
title: Installation de Python et du kit SDK - Azure
description: "Découvrez comment installer Python et le kit SDK à utiliser avec Azure."
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
ms.openlocfilehash: c9df4e1f7677b2ed10684f6f3c981f2abf64f171
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="installing-python-and-the-sdk"></a><span data-ttu-id="3d4ec-103">Installation de Python et du kit SDK</span><span class="sxs-lookup"><span data-stu-id="3d4ec-103">Installing Python and the SDK</span></span>
<span data-ttu-id="3d4ec-104">La configuration de Python sous Windows s’effectue en toute simplicité. La solution est préinstallée sous Mac, Linux et [Bash pour Windows](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="3d4ec-104">Python is easy to set up on Windows and comes pre-installed on Mac, Linux, and [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span> <span data-ttu-id="3d4ec-105">Ce guide décrit les étapes d'installation et de préparation de votre système à l'utilisation d'Azure.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-105">This guide walks you through installation and getting your machine ready for use with Azure.</span></span>

## <a name="whats-in-the-python-azure-sdk"></a><span data-ttu-id="3d4ec-106">Que contient le kit SDK Python Azure ?</span><span class="sxs-lookup"><span data-stu-id="3d4ec-106">What's in the Python Azure SDK?</span></span>
<span data-ttu-id="3d4ec-107">Le kit SDK Azure pour Python contient les composants qui vous permettent de développer, déployer et gérer des applications Python pour Azure.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-107">The Azure SDK for Python includes components that allow you to develop, deploy, and manage Python applications for Azure.</span></span> <span data-ttu-id="3d4ec-108">Il inclut plus précisément les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3d4ec-108">Specifically, the Azure SDK for Python includes the following:</span></span>

* <span data-ttu-id="3d4ec-109">**Bibliothèques de gestion**.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-109">**Management libraries**.</span></span> <span data-ttu-id="3d4ec-110">Ces bibliothèques de classes fournissent une interface de gestion des ressources Azure, comme les comptes de stockage ou les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-110">These class libraries provide an interface managing Azure resources, such as storage accounts, virtual machines.</span></span>
* <span data-ttu-id="3d4ec-111">**Bibliothèques Runtime**.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-111">**Runtime libraries**.</span></span> <span data-ttu-id="3d4ec-112">Ces bibliothèques de classes fournissent une interface permettant d’accéder aux fonctionnalités Azure, notamment le stockage et Service Bus.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-112">These class libraries provide an interface for accessing Azure features, such as storage and service bus.</span></span>

## <a name="which-python-and-which-version-to-use"></a><span data-ttu-id="3d4ec-113">Quelle solution Python et quelle version utiliser ?</span><span class="sxs-lookup"><span data-stu-id="3d4ec-113">Which Python and which version to use</span></span>
<span data-ttu-id="3d4ec-114">Il existe différentes versions des interpréteurs Python, par exemple :</span><span class="sxs-lookup"><span data-stu-id="3d4ec-114">There are several flavors of Python interpreters available - examples include:</span></span>

* <span data-ttu-id="3d4ec-115">CPython : interpréteur Python standard le plus couramment utilisé</span><span class="sxs-lookup"><span data-stu-id="3d4ec-115">CPython - the standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="3d4ec-116">PyPy : implémentation rapide et conforme autre que CPython</span><span class="sxs-lookup"><span data-stu-id="3d4ec-116">PyPy - fast, compliant alternative implementation to CPython</span></span>
* <span data-ttu-id="3d4ec-117">IronPython : interpréteur Python qui s'exécute sur .Net/CLR</span><span class="sxs-lookup"><span data-stu-id="3d4ec-117">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="3d4ec-118">Jython : interpréteur Python qui s’exécute sur la Machine Virtuelle Java</span><span class="sxs-lookup"><span data-stu-id="3d4ec-118">Jython - Python interpreter that runs on the Java Virtual Machine</span></span>

<span data-ttu-id="3d4ec-119">**CPython** v2.7 ou v3.3+ et PyPy 5.4.0 sont testés et pris en charge par le kit SDK Python Azure.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-119">**CPython** v2.7 or v3.3+ and PyPy 5.4.0 are tested and supported for the Python Azure SDK.</span></span>

## <a name="where-to-get-python"></a><span data-ttu-id="3d4ec-120">Où télécharger Python ?</span><span class="sxs-lookup"><span data-stu-id="3d4ec-120">Where to get Python?</span></span>
<span data-ttu-id="3d4ec-121">Il existe plusieurs façons de télécharger CPython :</span><span class="sxs-lookup"><span data-stu-id="3d4ec-121">There are several ways to get CPython:</span></span>

* <span data-ttu-id="3d4ec-122">Directement depuis [www.python.org][www.python.org]</span><span class="sxs-lookup"><span data-stu-id="3d4ec-122">Directly from [www.python.org][www.python.org]</span></span>
* <span data-ttu-id="3d4ec-123">Auprès d’un distributeur fiable comme [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] ou [www.activestate.com][www.activestate.com]</span><span class="sxs-lookup"><span data-stu-id="3d4ec-123">From a reputable distro such as [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] or [www.activestate.com][www.activestate.com]</span></span>
* <span data-ttu-id="3d4ec-124">Génération à partir de la source !</span><span class="sxs-lookup"><span data-stu-id="3d4ec-124">Build from source!</span></span>

<span data-ttu-id="3d4ec-125">Sauf en cas de nécessité particulière, nous vous recommandons d’opter pour l’une des deux premières options.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-125">Unless you have a specific need, we recommend the first two options.</span></span>

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a><span data-ttu-id="3d4ec-126">Installation du SDK sous Windows, Linux et macOS (bibliothèques client uniquement)</span><span class="sxs-lookup"><span data-stu-id="3d4ec-126">SDK Installation on Windows, Linux, and MacOS (client libraries only)</span></span>
<span data-ttu-id="3d4ec-127">Si vous avez déjà installé Python, vous pouvez utiliser pip pour installer un lot de toutes les bibliothèques client dans votre environnement Python 2.7 ou Python 3.3+ existant.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-127">If you already have Python installed, you can use pip to install a bundle of all the client libraries in your existing Python 2.7 or Python 3.3+ environment.</span></span> <span data-ttu-id="3d4ec-128">Cela télécharge les packages depuis [l’index Python Package][Python Package Index] (PyPI).</span><span class="sxs-lookup"><span data-stu-id="3d4ec-128">This downloads the packages from the [Python Package Index][Python Package Index] (PyPI).</span></span>

<span data-ttu-id="3d4ec-129">Vous aurez peut-être besoin de droits d’administrateur :</span><span class="sxs-lookup"><span data-stu-id="3d4ec-129">You may need administrator rights:</span></span>

* <span data-ttu-id="3d4ec-130">Linux et macOS, utilisez la commande `sudo` : `sudo pip install azure-mgmt-compute`.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-130">Linux and MacOS, use the `sudo` command: `sudo pip install azure-mgmt-compute`.</span></span>
* <span data-ttu-id="3d4ec-131">Windows : ouvrez votre invite de commandes/PowerShell en tant qu’administrateur</span><span class="sxs-lookup"><span data-stu-id="3d4ec-131">Windows: open your PowerShell/Command prompt as an administrator</span></span>

<span data-ttu-id="3d4ec-132">Vous pouvez installer chaque bibliothèque individuellement pour chaque service Azure :</span><span class="sxs-lookup"><span data-stu-id="3d4ec-132">You can install individually each library for each Azure service:</span></span>

```console
   $ pip install azure-batch          # Install the latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="3d4ec-133">L’aperçu des packages peut être installé à l’aide de l’indicateur `--pre` :</span><span class="sxs-lookup"><span data-stu-id="3d4ec-133">Preview packages can be installed using the `--pre` flag:</span></span>

```console
   $ pip install --pre azure-mgmt-compute # installs only the latest Compute Management library
```

<span data-ttu-id="3d4ec-134">Vous pouvez également installer un ensemble de bibliothèques Azure d’une seule ligne à l’aide du méta-package `azure` .</span><span class="sxs-lookup"><span data-stu-id="3d4ec-134">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span> <span data-ttu-id="3d4ec-135">Étant donné que tous les packages de ce méta-package ne sont pas encore publiés de façon stable, le méta-package `azure` est encore en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-135">Since not all packages in this meta-package are published as stable yet, the `azure` meta-package is still in preview.</span></span>
<span data-ttu-id="3d4ec-136">Toutefois, les packages de base peuvent pour l’instant être considérés comme « stables » du point de vue de la qualité / l’exhaustivité du code</span><span class="sxs-lookup"><span data-stu-id="3d4ec-136">However, the core packages, from code quality/completeness perspectives can be considered "stable" at this time</span></span>

* <span data-ttu-id="3d4ec-137">ils sont officiellement étiquetés comme tels dans la synchronisation avec d’autres langues, dès que possible.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-137">it is officially labeled as such in sync with other languages as soon as possible.</span></span>
  <span data-ttu-id="3d4ec-138">Nous ne prévoyons pas d’autres changements majeurs d’ici-là.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-138">We are not planning on any further major changes until then.</span></span>

<span data-ttu-id="3d4ec-139">Puisqu’il s’agit d’une version préliminaire, vous devez utiliser l’indicateur `--pre` :</span><span class="sxs-lookup"><span data-stu-id="3d4ec-139">Since it's a preview release, you need to use the `--pre` flag:</span></span>

```console
   $ pip install --pre azure
```

<span data-ttu-id="3d4ec-140">ou directement</span><span class="sxs-lookup"><span data-stu-id="3d4ec-140">or directly</span></span>

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a><span data-ttu-id="3d4ec-141">Téléchargement d'autres packages</span><span class="sxs-lookup"><span data-stu-id="3d4ec-141">Getting More Packages</span></span>
<span data-ttu-id="3d4ec-142">[Python Package Index][Python Package Index] (PyPI) comporte une sélection étoffée de bibliothèques Python.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-142">The [Python Package Index][Python Package Index] (PyPI) has a rich selection of Python libraries.</span></span>  <span data-ttu-id="3d4ec-143">Si vous avez installé une version fournie par un distributeur, vous disposez déjà de la plupart des éléments nécessaires pour différents scénarios, du développement web au calcul technique.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-143">If you chose to install a Distro, you'll already have most of the interesting bits for various scenarios from web development to Technical Computing.</span></span>

## <a name="python-tools-for-visual-studio"></a><span data-ttu-id="3d4ec-144">Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3d4ec-144">Python Tools for Visual Studio</span></span>
<span data-ttu-id="3d4ec-145">[Python Tools for Visual Studio][Python Tools pour Visual Studio] (PTVS) est un plug-in gratuit/OSS de Microsoft, qui transforme Visual Studio en un environnement de développement intégré (IDE) Python à part entière :</span><span class="sxs-lookup"><span data-stu-id="3d4ec-145">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) is a free/OSS plugin from Microsoft, which turns VS into a full-fledged Python IDE:</span></span>

![how-to-install-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

<span data-ttu-id="3d4ec-147">Nous vous recommandons d’utiliser PTVS même s’il est facultatif, car il vous apporte pour les projets/solutions Python et web les fonctionnalités suivantes : support technique, débogage, profilage, fenêtre interactive, modification des modèles et Intellisense.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-147">Using PTVS is optional, but is recommended as it gives you Python and Web Project/Solution support, debugging, profiling, interactive window, Template editing, and Intellisense.</span></span>

<span data-ttu-id="3d4ec-148">PTVS simplifie également le déploiement sur Microsoft Azure, avec une prise en charge du déploiement sur [Cloud Services](cloud-services/cloud-services-python-ptvs.md) et [Sites Web](app-service-web/web-sites-python-ptvs-django-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="3d4ec-148">PTVS also makes it easy to deploy to Microsoft Azure, with support for deployment to [Cloud Services](cloud-services/cloud-services-python-ptvs.md) and [Websites](app-service-web/web-sites-python-ptvs-django-mysql.md).</span></span>

<span data-ttu-id="3d4ec-149">PTVS fonctionne avec votre installation existante de Visual Studio 2013, 2015 ou 2017.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-149">PTVS works with your existing Visual Studio 2013, 2015, or 2017 installation.</span></span>  <span data-ttu-id="3d4ec-150">Pour accéder à la documentation, aux téléchargements et aux discussions, consultez le site [Python Tools pour Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="3d4ec-150">For documentation, downloads and discussions, see [Python Tools for Visual Studio].</span></span>  

## <a name="python-azure-scenarios-for-linux-and-macos"></a><span data-ttu-id="3d4ec-151">Scénarios Python Azure pour Linux et MacOS</span><span class="sxs-lookup"><span data-stu-id="3d4ec-151">Python Azure Scenarios for Linux and MacOS</span></span>
<span data-ttu-id="3d4ec-152">Pour Linux et macOS, les principaux scénarios Azure pris en charge sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="3d4ec-152">For Linux or MacOS, main Azure scenarios that are supported:</span></span>

1. <span data-ttu-id="3d4ec-153">Consommation des services Azure par le biais des bibliothèques clientes pour Python</span><span class="sxs-lookup"><span data-stu-id="3d4ec-153">Consuming Azure Services by using the client libraries for Python</span></span>
2. <span data-ttu-id="3d4ec-154">Exécution de votre application sur une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="3d4ec-154">Running your app in a Linux VM</span></span>
3. <span data-ttu-id="3d4ec-155">Développement et publication de sites web Azure à l'aide de Git</span><span class="sxs-lookup"><span data-stu-id="3d4ec-155">Developing and publishing to Azure Websites using Git</span></span>

<span data-ttu-id="3d4ec-156">Le premier scénario vous permet de créer des applications web enrichies qui tirent parti des fonctionnalités PaaS d’Azure, comme le [Stockage Blob](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), le [Stockage File d’attente](storage/queues/storage-python-how-to-use-queue-storage.md) ou le [Stockage Table](cosmos-db/table-storage-how-to-use-python.md), par le biais de wrappers Python pour les API REST Azure.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-156">The first scenario enables you to author rich web apps that take advantage of the Azure PaaS capabilities such as [blob storage](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [queue storage](storage/queues/storage-python-how-to-use-queue-storage.md), [table storage](cosmos-db/table-storage-how-to-use-python.md) etc. via Pythonic wrappers for the Azure REST APIs.</span></span> <span data-ttu-id="3d4ec-157">Le fonctionnement de ces derniers est identique sous Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-157">These work identically on Windows, Mac, and Linux.</span></span>  <span data-ttu-id="3d4ec-158">Vous pouvez également utiliser ces bibliothèques clientes à partir de votre ordinateur de développement local ou une machine virtuelle Linux s'exécutant sur Azure.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-158">You can also use these client libraries from your local development machine or a Linux VM running on Azure.</span></span>

<span data-ttu-id="3d4ec-159">Pour le scénario nécessitant une machine virtuelle, vous pouvez tout simplement démarrer une machine virtuelle Linux de votre choix (Ubuntu, CentOS, Suse) et exécuter/gérer les logiciels souhaités.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-159">For the VM scenario, you simply start a Linux VM of your choice (Ubuntu, CentOS, Suse) and run/manage what you like.</span></span>  <span data-ttu-id="3d4ec-160">Par exemple, vous pouvez exécuter [IPython][IPython] REPL/Notebook sur votre machine Windows/Mac/Linux et pointer votre navigateur vers une machine virtuelle multiprocesseur Linux ou Windows exécutant le moteur IPython Engine sur Azure.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-160">As an example, you can run [IPython][IPython] REPL/notebook on your Windows/Mac/Linux machine and point your browser to a Linux or Windows multi-proc VM running the IPython Engine on Azure.</span></span>

<span data-ttu-id="3d4ec-161">Pour plus d’informations sur la configuration d’une machine virtuelle Linux, consultez le didacticiel [Créer une machine virtuelle exécutant Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="3d4ec-161">For information on how to set up a Linux VM, see the [Create a Virtual Machine Running Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.</span></span>

<span data-ttu-id="3d4ec-162">À l'aide du déploiement Git, vous pouvez développer une application web Python et la publier sur un site web Azure à partir de n'importe quel système d'exploitation.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-162">Using Git deployment, you can develop a Python web application and publish it to an Azure Website from any operating system.</span></span>  <span data-ttu-id="3d4ec-163">Quand vous placez votre référentiel sur Azure, il crée automatiquement un environnement virtuel et utilise pip pour installer vos packages requis.</span><span class="sxs-lookup"><span data-stu-id="3d4ec-163">When you push your repository to Azure, it automatically creates a virtual environment and pip installs your required packages.</span></span>

<span data-ttu-id="3d4ec-164">Pour plus d’informations sur le développement et la publication de sites web Azure, consultez les didacticiels [Création de sites web avec Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Création de sites web avec Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md) et [Création de sites web avec Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span><span class="sxs-lookup"><span data-stu-id="3d4ec-164">For more information on developing and publishing Azure Websites, see the tutorials for [Creating Websites with Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Creating Websites with Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), and [Creating Websites with Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span></span> <span data-ttu-id="3d4ec-165">Pour des informations plus générales sur l’utilisation de n’importe quelle infrastructure compatible WSGI, consultez [Configuration de Python avec des Sites Web Azure](app-service-web/web-sites-python-configure.md).</span><span class="sxs-lookup"><span data-stu-id="3d4ec-165">For more general information on using any WSGI-compliant framework, see [Configuring Python with Azure Websites](app-service-web/web-sites-python-configure.md).</span></span>

## <a name="additional-software-and-resources"></a><span data-ttu-id="3d4ec-166">Logiciels et ressources supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="3d4ec-166">Additional Software and Resources:</span></span>
* [<span data-ttu-id="3d4ec-167">Kit de développement logiciel (SDK) Azure pour Python Read The Docs</span><span class="sxs-lookup"><span data-stu-id="3d4ec-167">Azure SDK for Python ReadTheDocs</span></span>](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [<span data-ttu-id="3d4ec-168">Kit de développement logiciel (SDK) Azure pour Python GitHub</span><span class="sxs-lookup"><span data-stu-id="3d4ec-168">Azure SDK for Python GitHub</span></span>](https://github.com/Azure/azure-sdk-for-python)
* [<span data-ttu-id="3d4ec-169">Exemples Azure officiels pour Python</span><span class="sxs-lookup"><span data-stu-id="3d4ec-169">Official Azure samples for Python</span></span>](https://azure.microsoft.com/documentation/samples/?platform=python)
* <span data-ttu-id="3d4ec-170">[Distribution de Python par Continuum Analytics (en anglais)][Continuum Analytics Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="3d4ec-170">[Continuum Analytics Python Distribution][Continuum Analytics Python Distribution]</span></span>
* <span data-ttu-id="3d4ec-171">[Distribution de Python par Enthought (en anglais)][Enthought Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="3d4ec-171">[Enthought Python Distribution][Enthought Python Distribution]</span></span>
* <span data-ttu-id="3d4ec-172">[Distribution de Python par ActiveState (en anglais)][ActiveState Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="3d4ec-172">[ActiveState Python Distribution][ActiveState Python Distribution]</span></span>
* <span data-ttu-id="3d4ec-173">[SciPy : un vaste panel de bibliothèques Scientific Python (en anglais)][SciPy - A suite of Scientific Python libraries]</span><span class="sxs-lookup"><span data-stu-id="3d4ec-173">[SciPy - A suite of Scientific Python libraries][SciPy - A suite of Scientific Python libraries]</span></span>
* <span data-ttu-id="3d4ec-174">[NumPy : une bibliothèque de valeurs numériques pour Python (en anglais)][NumPy - A numerics library for Python]</span><span class="sxs-lookup"><span data-stu-id="3d4ec-174">[NumPy - A numerics library for Python][NumPy - A numerics library for Python]</span></span>
* <span data-ttu-id="3d4ec-175">[Projet Django : une infrastructure web/un système de gestion du contenu arrivés à maturité (en anglais)][Django Project - A mature web framework/CMS]</span><span class="sxs-lookup"><span data-stu-id="3d4ec-175">[Django Project - A mature web framework/CMS][Django Project - A mature web framework/CMS]</span></span>
* <span data-ttu-id="3d4ec-176">[IPython : une solution REPL/Notebook avancée pour Python (en anglais)][IPython - an advanced REPL/Notebook for Python]</span><span class="sxs-lookup"><span data-stu-id="3d4ec-176">[IPython - an advanced REPL/Notebook for Python][IPython - an advanced REPL/Notebook for Python]</span></span>
* <span data-ttu-id="3d4ec-177">[Python Tools pour Visual Studio sur GitHub][Python Tools for Visual Studio on GitHub]</span><span class="sxs-lookup"><span data-stu-id="3d4ec-177">[Python Tools for Visual Studio on GitHub][Python Tools for Visual Studio on GitHub]</span></span>
* [<span data-ttu-id="3d4ec-178">Centre de développement Python</span><span class="sxs-lookup"><span data-stu-id="3d4ec-178">Python Developer Center</span></span>](/develop/python/)

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
[Setting up a Linux VM via the Azure portal]: create-and-configure-opensuse-vm-in-portal.md
[How to use the Azure Command-Line Interface]: crossplat-cmd-tools.md
[Create a Virtual Machine Running Linux]: virtual-machines-linux-quick-create-cli.md
[Creating Websites with Django]: web-sites-python-create-deploy-django-app.md
[Creating Websites with Bottle]: web-sites-python-create-deploy-bottle-app.md
[Creating Websites with Flask]: web-sites-python-create-deploy-flask-app.md
[Configuring Python with Azure Websites]: web-sites-python-configure.md
[table storage]: storage-python-how-to-use-table-storage.md
[queue storage]: storage-python-how-to-use-queue-storage.md
[blob storage]:storage/blobs/storage-python-how-to-use-blob-storage.md
