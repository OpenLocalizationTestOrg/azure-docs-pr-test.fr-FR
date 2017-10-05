---
title: "Création d’un bloc-notes Jupyter/IPython Notebook | Microsoft Docs"
description: "Découvrez comment déployer un bloc-notes Jupyter/IPython Notebook sur une machine virtuelle Linux créée avec le modèle de déploiement du Gestionnaire de ressources Azure."
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
ms.openlocfilehash: b5940190822cd5c5b78ea0e8f5c8695608d351d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a><span data-ttu-id="66290-103">Création d’une machine virtuelle Azure, installation de Jupyter et exécution d’un Notebook Jupyter sur Azure</span><span class="sxs-lookup"><span data-stu-id="66290-103">Creating an Azure VM, installing Jupyter, and running a Jupyter Notebook on Azure</span></span>
<span data-ttu-id="66290-104">Le [projet Jupyter](http://jupyter.org), anciennement appelé [projet IPython](http://ipython.org), fournit un ensemble d’outils destiné au calcul scientifique. Ces outils utilisent des interpréteurs de commandes interactifs et puissants qui associent l’exécution de code à la création d’un document de calcul dynamique.</span><span class="sxs-lookup"><span data-stu-id="66290-104">The [Jupyter project](http://jupyter.org), formerly the [IPython project](http://ipython.org), provides a collection of tools for scientific computing using powerful interactive shells that combine code execution with the creation of a live computational document.</span></span> <span data-ttu-id="66290-105">Ces fichiers de l'interpréteur contiennent du texte arbitraire, des formules mathématiques, un code d'entrée, des résultats, des graphiques, des vidéos et d'autres sortes de support qu'un navigateur Web moderne peut afficher.</span><span class="sxs-lookup"><span data-stu-id="66290-105">These notebook files can contain arbitrary text, mathematical formulas, input code, results, graphics, videos and any other kind of media that a modern web browser is capable of displaying.</span></span> <span data-ttu-id="66290-106">Que vous soyez complètement novice sur Python et que vous souhaitiez apprendre à vous en servir dans un environnement divertissant et interactif ou que vous souhaitiez effectuer d’importants calculs parallèles/techniques, l'interpréteur Jupyter Notebook est un choix optimal.</span><span class="sxs-lookup"><span data-stu-id="66290-106">Whether you're absolutely new to Python and want to learn it in a fun, interactive environment or do some serious parallel/technical computing, the Jupyter Notebook is a great choice.</span></span>

<span data-ttu-id="66290-107">![Capture d’écran](./media/jupyter-notebook/ipy-notebook-spectral.png) Utilisation des packages SciPy et Matplotlib pour analyser la structure d’un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="66290-107">![Screenshot](./media/jupyter-notebook/ipy-notebook-spectral.png) Using SciPy and Matplotlib packages to analyze the structure of a sound recording.</span></span>

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a><span data-ttu-id="66290-108">Jupyter en deux modes : Azure Notebooks ou déploiement personnalisé</span><span class="sxs-lookup"><span data-stu-id="66290-108">Jupyter Two Ways: Azure Notebooks or Custom Deployment</span></span>
<span data-ttu-id="66290-109">Azure fournit un service qui vous aidera à [prendre rapidement en main Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span><span class="sxs-lookup"><span data-stu-id="66290-109">Azure provides a service that you can use to [quickly start using Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span></span>  <span data-ttu-id="66290-110">En utilisant Azure Notebook Service, vous avez facilement accès à l’interface web de Jupyter et à des ressources de calcul évolutives avec toute la puissance de Python et de ses nombreuses bibliothèques.</span><span class="sxs-lookup"><span data-stu-id="66290-110">By using the Azure Notebook Service, you can easily gain access to Jupyter's web-accessible interface to scalable computational resources with all the power of Python and its many libraries.</span></span>  <span data-ttu-id="66290-111">Étant donné que l’installation est gérée par le service, les utilisateurs peuvent accéder à ces ressources sans avoir à effectuer aucun travail d’administration et de configuration.</span><span class="sxs-lookup"><span data-stu-id="66290-111">Since the installation is handled by the service, users can access these resources without the need for administration and configuration by the user.</span></span>

<span data-ttu-id="66290-112">Si le service Notebook n’est pas approprié pour votre scénario, poursuivez la lecture de cet article qui vous indiquera comment déployer Jupyter Notebook sur Microsoft Azure, à l'aide de machines virtuelles Linux (VM).</span><span class="sxs-lookup"><span data-stu-id="66290-112">If the notebook service does not work for your scenario please continue to read this article which will will show you how to deploy the Jupyter Notebook on Microsoft Azure, using Linux virtual machines (VMs).</span></span>

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a><span data-ttu-id="66290-113">Créer et configurer une machine virtuelle sur Azure</span><span class="sxs-lookup"><span data-stu-id="66290-113">Create and configure a VM on Azure</span></span>
<span data-ttu-id="66290-114">La première étape consiste à créer une machine virtuelle s’exécutant sur Azure.</span><span class="sxs-lookup"><span data-stu-id="66290-114">The first step is to create a virtual machine (VM)  running on Azure.</span></span>
<span data-ttu-id="66290-115">Cette machine virtuelle est un système d’exploitation complet dans le cloud et sera utilisée pour exécuter l’interpréteur Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="66290-115">This VM is a complete operating system in the cloud and will be used to run the Jupyter Notebook.</span></span> <span data-ttu-id="66290-116">Azure peut exécuter des machines virtuelles Linux et Windows. C’est pourquoi nous allons étudier la configuration de Jupyter sur les deux types de machines.</span><span class="sxs-lookup"><span data-stu-id="66290-116">Azure is capable of running both Linux and Windows virtual machines, and we will cover the setup of Jupyter on both types of virtual machines.</span></span>

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a><span data-ttu-id="66290-117">Créer une machine virtuelle Linux et ouvrir un port pour Jupyter</span><span class="sxs-lookup"><span data-stu-id="66290-117">Create a Linux VM and open a port for Jupyter</span></span>
<span data-ttu-id="66290-118">Suivez les instructions fournies [ici][portal-vm-linux] pour créer une machine virtuelle de la distribution *Ubuntu*.</span><span class="sxs-lookup"><span data-stu-id="66290-118">Follow the instructions given [here][portal-vm-linux] to create a virtual machine of the *Ubuntu* distribution.</span></span> <span data-ttu-id="66290-119">Ce didacticiel utilise Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="66290-119">This tutorial uses Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="66290-120">Nous présumerons que le nom d’utilisateur est *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="66290-120">We'll assume the user name *azureuser*.</span></span>

<span data-ttu-id="66290-121">Après le déploiement de la machine virtuelle, nous devons activer une règle de sécurité sur le groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="66290-121">After the virtual machine deploys we need to open up a security rule on the network security group.</span></span>  <span data-ttu-id="66290-122">À partir du portail Azure, accédez à **Groupes de sécurité réseau** et ouvrez l’onglet du groupe de sécurité correspondant à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="66290-122">From the Azure portal, go to **Network Security Groups** and open the tab for the Security Group corresponding to your VM.</span></span> <span data-ttu-id="66290-123">Vous devez ajouter une règle de sécurité de trafic entrant avec les paramètres suivants : **TCP** pour le protocole, **\*** pour le port source (public) et **9999** pour le port de destination (privé).</span><span class="sxs-lookup"><span data-stu-id="66290-123">You need to add an Inbound Security rule with the following settings: **TCP** for the protocol, **\*** for the source (public) port and **9999** for the destination (private) port.</span></span>

![Capture d'écran](./media/jupyter-notebook/azure-add-endpoint.png)

<span data-ttu-id="66290-125">Dans votre groupe de sécurité réseau, cliquez sur **Interfaces réseau** et notez **l’adresse IP publique**, car vous en aurez besoin pour vous connecter à votre machine virtuelle à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="66290-125">While in your Network Security Group, click on **Network Interfaces** and note the **Public IP Address** as it will be needed to connect to your VM in the next step.</span></span>

## <a name="install-required-software-on-the-vm"></a><span data-ttu-id="66290-126">Installer les logiciels requis sur la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="66290-126">Install required software on the VM</span></span>
<span data-ttu-id="66290-127">Pour exécuter Jupyter Notebook sur votre machine virtuelle, vous devez tout d’abord installer Jupyter et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="66290-127">To run the Jupyter Notebook on our VM, we must first install Jupyter and its dependencies.</span></span> <span data-ttu-id="66290-128">Connectez-vous à votre machine virtuelle Linux à l’aide de SSH et de la combinaison nom d’utilisateur/mot de passe que vous avez choisie au moment de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="66290-128">Connect to your linux vm using ssh and the username/password pair you chose when you created the vm.</span></span> <span data-ttu-id="66290-129">Dans ce didacticiel, nous utiliserons PuTTY pour nous connecter à partir de Windows.</span><span class="sxs-lookup"><span data-stu-id="66290-129">In this tutorial we will use PuTTY and connect from Windows.</span></span>

### <a name="installing-jupyter-on-ubuntu"></a><span data-ttu-id="66290-130">Installation de Jupyter sur Ubuntu</span><span class="sxs-lookup"><span data-stu-id="66290-130">Installing Jupyter on Ubuntu</span></span>
<span data-ttu-id="66290-131">Installez Anaconda, une distribution de Python courante dans le domaine de la science des données, à partir d’un des liens fournis dans [Continuum Analytics](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="66290-131">Install Anaconda, a popular data science python distribution, using one of the links provided from [Continuum Analytics](https://www.continuum.io/downloads).</span></span>  <span data-ttu-id="66290-132">Les liens ci-dessous correspondent aux versions les plus récentes (au moment de la rédaction de ce document).</span><span class="sxs-lookup"><span data-stu-id="66290-132">As of the writing of this document, the below links are the most up to date versions.</span></span>

#### <a name="anaconda-installs-for-linux"></a><span data-ttu-id="66290-133">Installations Anaconda pour Linux</span><span class="sxs-lookup"><span data-stu-id="66290-133">Anaconda Installs for Linux</span></span>
<table>
  <th><span data-ttu-id="66290-134">Python 3.4</span><span class="sxs-lookup"><span data-stu-id="66290-134">Python 3.4</span></span></th>
  <th><span data-ttu-id="66290-135">Python 2.7</span><span class="sxs-lookup"><span data-stu-id="66290-135">Python 2.7</span></span></th>
  <tr>
    <td><span data-ttu-id="66290-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="66290-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
    <td><span data-ttu-id="66290-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="66290-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="66290-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="66290-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>
    <td><span data-ttu-id="66290-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="66290-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a><span data-ttu-id="66290-140">Installation d’Anaconda3 2.3.0 64 bits sur Ubuntu</span><span class="sxs-lookup"><span data-stu-id="66290-140">Installing Anaconda3 2.3.0 64-bit on Ubuntu</span></span>
<span data-ttu-id="66290-141">Voici un exemple d’installation d’Anaconda sur Ubuntu</span><span class="sxs-lookup"><span data-stu-id="66290-141">As an example, this is how you can install Anaconda on Ubuntu</span></span>

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter to the latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![Capture d'écran](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a><span data-ttu-id="66290-143">Configuration de Jupyter et utilisation de SSL</span><span class="sxs-lookup"><span data-stu-id="66290-143">Configuring Jupyter and using SSL</span></span>
<span data-ttu-id="66290-144">Après l’installation, nous devons prendre un moment pour configurer les fichiers de configuration pour Jupyter.</span><span class="sxs-lookup"><span data-stu-id="66290-144">After installing we need to take a moment to setup the configuration files for Jupyter.</span></span> <span data-ttu-id="66290-145">Si vous rencontrez des problèmes pour configurer Jupyter, nous vous conseillons de consulter la [documentation Jupyter relative à l’exécution d’un serveur Notebook](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span><span class="sxs-lookup"><span data-stu-id="66290-145">If you experience troubles with configuring Jupyter it may be helpful to look at the [Jupyter Documentation for Running a Notebook Server](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span></span>

<span data-ttu-id="66290-146">Ensuite, nous utilisons la commande `cd` pour accéder au répertoire de profil afin de créer notre certificat SSL et de modifier le fichier de configuration des profils.</span><span class="sxs-lookup"><span data-stu-id="66290-146">Next we `cd` to the profile directory to create our SSL certificate and edit the profiles configuration file.</span></span>

<span data-ttu-id="66290-147">Sur Linux, utilisez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="66290-147">On Linux use the following command.</span></span>

    cd ~/.jupyter

<span data-ttu-id="66290-148">Utilisez la commande suivante pour créer le certificat SSL (Linux et Windows).</span><span class="sxs-lookup"><span data-stu-id="66290-148">Use the following command to create the SSL certificate(Linux and Windows).</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="66290-149">Notez que puisque nous créons un certificat SSL auto-signé, lors de la connexion à l'interpréteur, votre navigateur affiche un message d'avertissement.</span><span class="sxs-lookup"><span data-stu-id="66290-149">Note that since we are creating a self-signed SSL certificate, when connecting to the notebook your browser will give you a security warning.</span></span>  <span data-ttu-id="66290-150">Pour une utilisation à long terme, vous souhaiterez utiliser un certificat correctement signé associé à votre organisation.</span><span class="sxs-lookup"><span data-stu-id="66290-150">For long-term production use, you will want to use a properly signed certificate associated with your organization.</span></span>  <span data-ttu-id="66290-151">Comme la gestion des certificats ne figure pas dans cette démonstration, nous nous en tiendrons à un certificat auto-signé pour l'instant.</span><span class="sxs-lookup"><span data-stu-id="66290-151">Since certificate management is beyond the scope of this demo, we will stick to a self-signed certificate for now.</span></span>

<span data-ttu-id="66290-152">En plus de l'utilisation d'un certificat, vous devez également fournir un mot de passe pour protéger votre interpréteur contre toute utilisation non autorisée.</span><span class="sxs-lookup"><span data-stu-id="66290-152">In addition to using a certificate, you must also provide a password to protect your notebook from unauthorized use.</span></span>  <span data-ttu-id="66290-153">Pour des raisons de sécurité, Jupyter utilise des mots de passe chiffrés dans son fichier de configuration. De ce fait, vous devez tout d’abord chiffrer votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="66290-153">For security reasons Jupyter uses encrypted passwords in its configuration file, so you'll need to encrypt your password first.</span></span>  <span data-ttu-id="66290-154">Pour ce faire, iPython fournit un utilitaire. À une invite de commandes, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="66290-154">IPython provides a utility to do so; at a command prompt run the following command.</span></span>

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

<span data-ttu-id="66290-155">Vous serez invité à fournir un mot de passe et une confirmation, puis le mot de passe s'affichera.</span><span class="sxs-lookup"><span data-stu-id="66290-155">This will prompt you for a password and confirmation, and will then print the password.</span></span> <span data-ttu-id="66290-156">Notez cette information, car vous en aurez besoin à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="66290-156">Note this for the following step.</span></span>

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided the rest for security)

<span data-ttu-id="66290-157">Nous allons ensuite modifier le fichier de configuration du profil (fichier `jupyter_notebook_config.py` du répertoire dans lequel vous vous trouvez).</span><span class="sxs-lookup"><span data-stu-id="66290-157">Next, we will edit the profile's configuration file, which is the `jupyter_notebook_config.py` file in the directory you are in.</span></span>  <span data-ttu-id="66290-158">Si ce fichier n’existe pas encore, vous devez le créer.</span><span class="sxs-lookup"><span data-stu-id="66290-158">Note that this file may not exist -- just create it if that is the case.</span></span>  <span data-ttu-id="66290-159">Ce fichier comporte de nombreux champs, tous commentés par défaut.</span><span class="sxs-lookup"><span data-stu-id="66290-159">This file has a number of fields and by default all are commented out.</span></span>  <span data-ttu-id="66290-160">Vous pouvez ouvrir ce fichier avec un éditeur de texte de votre choix et vous devez vous assurer qu’il a au moins le contenu suivant.</span><span class="sxs-lookup"><span data-stu-id="66290-160">You can open this file with any text editor of your liking, and you should ensure that it has at least the following content.</span></span> <span data-ttu-id="66290-161">**Remplacez c.NotebookApp.password dans la configuration par sha1 fourni à l’étape précédente**.</span><span class="sxs-lookup"><span data-stu-id="66290-161">**Be sure to replace the c.NotebookApp.password in the config with the sha1 from the previous step**.</span></span>

    c = get_config()

    # You must give the path to the certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-the-jupyter-notebook"></a><span data-ttu-id="66290-162">Exécutez Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="66290-162">Run the Jupyter Notebook</span></span>
<span data-ttu-id="66290-163">À présent, nous sommes prêts à démarrer Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="66290-163">At this point we are ready to start the Jupyter Notebook.</span></span> <span data-ttu-id="66290-164">Pour ce faire, accédez au répertoire où vous voulez stocker les blocs-notes, puis démarrez le serveur Jupyter Notebook avec la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="66290-164">To do this, navigate to the directory you want to store notebooks in and start the Jupyter Notebook server with the following command.</span></span>

    /anaconda3/bin/jupyter-notebook

<span data-ttu-id="66290-165">Vous devez à présent être en mesure d’accéder à Jupyter Notebook à l’adresse `https://[PUBLIC-IP-ADDRESS]:9999`.</span><span class="sxs-lookup"><span data-stu-id="66290-165">You should now be able to access your Jupyter Notebook at the address `https://[PUBLIC-IP-ADDRESS]:9999`.</span></span>

<span data-ttu-id="66290-166">Quand vous accédez pour la première fois à votre interpréteur, la page de connexion demande votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="66290-166">When you first access your notebook, the login page asks for your password.</span></span> <span data-ttu-id="66290-167">Une fois que vous êtes connecté, « Jupyter Notebook Dashboard » s'affiche. Il s'agit du centre de commande de toutes les opérations de bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="66290-167">And once you log in, you will see the "Jupyter Notebook Dashboard", which is the ontrol center for all notebook operations.</span></span>  <span data-ttu-id="66290-168">Dans cette page, vous pouvez créer des interpréteurs et ouvrir des interpréteurs existants.</span><span class="sxs-lookup"><span data-stu-id="66290-168">From this page you can create new notebooks and open existing ones.</span></span>

![Capture d'écran](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-the-jupyter-notebook"></a><span data-ttu-id="66290-170">Utilisation de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="66290-170">Using the Jupyter Notebook</span></span>
<span data-ttu-id="66290-171">Si vous cliquez sur le bouton **Nouveau** , la page d’ouverture suivante s’affiche.</span><span class="sxs-lookup"><span data-stu-id="66290-171">If you click the **New** button, you will see the following opening page.</span></span>

![Capture d'écran](./media/jupyter-notebook/jupyter-untitled-notebook.png)

<span data-ttu-id="66290-173">La zone marquée par une invite `In []:` est la zone d’entrée. Vous pouvez y taper tout code Python valide qui s’exécutera quand vous appuierez sur les touches `Shift-Enter` ou que vous cliquerez sur l’icône « Lire » (triangle pointant vers la droite dans la barre d’outils).</span><span class="sxs-lookup"><span data-stu-id="66290-173">The area marked with an `In []:` prompt is the input area, and here you can type any valid Python code and it will execute when you hit `Shift-Enter` or click on the "Play" icon (the right-pointing triangle in the toolbar).</span></span>

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a><span data-ttu-id="66290-174">Un puissant paradigme : documents de calcul dynamique avec des supports puissants</span><span class="sxs-lookup"><span data-stu-id="66290-174">A powerful paradigm: live computational documents with rich media</span></span>
<span data-ttu-id="66290-175">L’interpréteur lui-même semble très naturel à toute personne ayant utilisé Python et un traitement de texte, car c’est une combinaison des deux à certains égards : vous pouvez exécuter des blocs de code Python, mais vous pouvez également conserver des notes et d’autres types de texte en changeant le style d’une cellule de « Code » en  « Texte » à l’aide du menu déroulant dans la barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="66290-175">The notebook itself should feel very natural to anyone who has used Python and a word processor, because it is in some ways a mix of both: you can execute blocks of Python code, but you can also keep notes and other text by changing the style of a cell from "Code" to "Markdown" using the drop-down menu in the toolbar.</span></span>

<span data-ttu-id="66290-176">Jupyter est bien plus qu’un traitement de texte, car il permet l’association de calculs et de supports puissants (texte, graphiques, vidéos et, virtuellement, tout ce qu’un navigateur web actuel peut afficher).</span><span class="sxs-lookup"><span data-stu-id="66290-176">Jupyter is much more than a word processor as it allows the mixing of computation and rich media (text, graphics, video and virtually anything a modern web browser can display).</span></span> <span data-ttu-id="66290-177">Vous pouvez associer du texte, du code, des vidéos et bien plus encore !</span><span class="sxs-lookup"><span data-stu-id="66290-177">You can mix, text, code, videos and more!</span></span>

![Capture d'écran](./media/jupyter-notebook/jupyter-editing-experience.png)

<span data-ttu-id="66290-179">De même, avec la puissance des nombreuses et très performantes bibliothèques de Python pour le calcul scientifique et technique, un simple calcul peut être effectué avec la même facilité qu’une analyse complexe d’un réseau, le tout dans un même environnement.</span><span class="sxs-lookup"><span data-stu-id="66290-179">And with the power of Python's many excellent libraries for scientific and technical computing, in the following screenshot, a simple calculation can be performed with the same ease as a complex network analysis, all in one environment.</span></span>

<span data-ttu-id="66290-180">Ce paradigme d'association de la puissance du Web avec le calcul dynamique offre de nombreuses possibilités et est idéalement approprié au cloud. L'interpréteur peut être utilisé :</span><span class="sxs-lookup"><span data-stu-id="66290-180">This paradigm of mixing the power of the modern web with live computation offers many possibilities, and is ideally suited for the cloud; the Notebook can be used:</span></span>

* <span data-ttu-id="66290-181">en tant que bloc-notes de calcul pour enregistrer le travail exploratoire relatif à un problème ;</span><span class="sxs-lookup"><span data-stu-id="66290-181">As a computational scratchpad to record exploratory work on a problem.</span></span>
* <span data-ttu-id="66290-182">pour partager des résultats avec des collègues, sous la forme d’un calcul « dynamique » ou de formats de sortie papier (HTML, PDF) ;</span><span class="sxs-lookup"><span data-stu-id="66290-182">To share results with colleagues, either in 'live' computational form or in hardcopy formats (HTML, PDF).</span></span>
* <span data-ttu-id="66290-183">pour distribuer et présenter des supports de formation en direct impliquant du calcul, afin que les participants puissent immédiatement utiliser le code réel, le modifier et le réexécuter interactivement ;</span><span class="sxs-lookup"><span data-stu-id="66290-183">To distribute and present live teaching materials that involve computation, so students can immediately experiment with the real code, modify it and re-execute it interactively.</span></span>
* <span data-ttu-id="66290-184">pour fournir d’autres « papiers exécutables » qui présentent les résultats de recherches d’une manière qui peut être immédiatement reproduite, validée et étendue par d’autres ;</span><span class="sxs-lookup"><span data-stu-id="66290-184">To provide "executable papers" that present the results of research in a way that can be immediately reproduced, validated and extended by others.</span></span>
* <span data-ttu-id="66290-185">comme plateforme pour le calcul collaboratif : plusieurs utilisateurs peuvent se connecter au même serveur d’interpréteur afin de partager une session de calcul en direct.</span><span class="sxs-lookup"><span data-stu-id="66290-185">As a platform for collaborative computing: multiple users can log in to the same notebook server to share a live computational session.</span></span>

<span data-ttu-id="66290-186">Si vous accédez au [référentiel][repository] de code source IPython, vous y trouverez un répertoire complet avec des exemples de bloc-notes, que vous pourrez télécharger et expérimenter sur votre propre machine virtuelle Azure Jupyter.</span><span class="sxs-lookup"><span data-stu-id="66290-186">If you go to the IPython source code [repository][repository], you will find an entire directory with notebook examples which you can download and then experiment with on your own Azure Jupyter VM.</span></span>  <span data-ttu-id="66290-187">Téléchargez simplement les fichiers `.ipynb` à partir du site et chargez-les sur le tableau de bord de la machine virtuelle Azure de l’interpréteur (ou téléchargez-les directement dans la machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="66290-187">Simply download the `.ipynb` files from the site and upload them onto the dashboard of your notebook Azure VM (or download them directly into the VM).</span></span>

## <a name="conclusion"></a><span data-ttu-id="66290-188">Conclusion</span><span class="sxs-lookup"><span data-stu-id="66290-188">Conclusion</span></span>
<span data-ttu-id="66290-189">Grâce à son interface performante, Jupyter Notebook offre un accès interactif aux puissantes fonctionnalités de l’écosystème Python sur Azure.</span><span class="sxs-lookup"><span data-stu-id="66290-189">The Jupyter Notebook provides a powerful interface for accessing interactively the power of the Python ecosystem on Azure.</span></span>  <span data-ttu-id="66290-190">Il couvre une large gamme de cas d'utilisation, notamment les simples exploration et apprentissage de Python, l'analyse et la visualisation des données, le calcul de simulation et parallèle.</span><span class="sxs-lookup"><span data-stu-id="66290-190">It covers a wide range of usage cases including simple exploration and learning Python, data analysis and visualization, simulation and parallel computing.</span></span> <span data-ttu-id="66290-191">Les documents Notebook obtenus contiennent un enregistrement complet des calculs qui sont effectués et peuvent être partagés avec d’autres utilisateurs de Jupyter.</span><span class="sxs-lookup"><span data-stu-id="66290-191">The resulting Notebook documents contain a complete record of the computations that are performed and can be shared with other Jupyter users.</span></span>  <span data-ttu-id="66290-192">Jupyter Notebook peut être utilisé comme application locale, mais il est plus particulièrement conçu pour des déploiements cloud sur Azure.</span><span class="sxs-lookup"><span data-stu-id="66290-192">The Jupyter Notebook can be used as a local application, but it is ideally suited for cloud deployments on Azure</span></span>

<span data-ttu-id="66290-193">Les fonctionnalités principales de Jupyter sont également disponibles dans Visual Studio par le biais des [outils Python pour Visual Studio][Python Tools for Visual Studio] (PTVS).</span><span class="sxs-lookup"><span data-stu-id="66290-193">The core features of Jupyter are also available inside Visual Studio via the [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS).</span></span> <span data-ttu-id="66290-194">PTVS est un plug-in open source gratuit de Microsoft qui transforme Visual Studio en environnement de développement Python avancé qui inclut un éditeur avancé avec IntelliSense, ainsi qu'une intégration de débogage, de profilage et de calcul parallèle.</span><span class="sxs-lookup"><span data-stu-id="66290-194">PTVS is a free and open-source plug-in from Microsoft that turns Visual Studio into an advanced Python development environment that includes an advanced editor with IntelliSense, debugging, profiling and parallel computing integration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66290-195">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="66290-195">Next steps</span></span>
<span data-ttu-id="66290-196">Pour plus d’informations, consultez le [Centre pour développeurs Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="66290-196">For more information, see the [Python Developer Center](/develop/python/).</span></span>

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
