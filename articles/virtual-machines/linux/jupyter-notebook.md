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
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a><span data-ttu-id="68114-103">Création d’une machine virtuelle Azure, installation de Jupyter et exécution d’un Notebook Jupyter sur Azure</span><span class="sxs-lookup"><span data-stu-id="68114-103">Creating an Azure VM, installing Jupyter, and running a Jupyter Notebook on Azure</span></span>
<span data-ttu-id="68114-104">Hello [Notebook projet](http://jupyter.org), anciennement hello [notebooks projet](http://ipython.org), fournit un ensemble d’outils pour le calcul scientifique à l’aide du puissants interpréteurs de commandes interactives qui combinent l’exécution du code de création de hello du calcul de document dynamique.</span><span class="sxs-lookup"><span data-stu-id="68114-104">hello [Jupyter project](http://jupyter.org), formerly hello [IPython project](http://ipython.org), provides a collection of tools for scientific computing using powerful interactive shells that combine code execution with hello creation of a live computational document.</span></span> <span data-ttu-id="68114-105">Ces fichiers de l'interpréteur contiennent du texte arbitraire, des formules mathématiques, un code d'entrée, des résultats, des graphiques, des vidéos et d'autres sortes de support qu'un navigateur Web moderne peut afficher.</span><span class="sxs-lookup"><span data-stu-id="68114-105">These notebook files can contain arbitrary text, mathematical formulas, input code, results, graphics, videos and any other kind of media that a modern web browser is capable of displaying.</span></span> <span data-ttu-id="68114-106">Si vous êtes absolument nouveau tooPython et que vous souhaitez toolearn dans un fun, un environnement interactif ou effectuez quelques grave parallèle/technique informatique, hello bloc-notes Jupyter est un bon choix.</span><span class="sxs-lookup"><span data-stu-id="68114-106">Whether you're absolutely new tooPython and want toolearn it in a fun, interactive environment or do some serious parallel/technical computing, hello Jupyter Notebook is a great choice.</span></span>

<span data-ttu-id="68114-107">![Capture d’écran de](./media/jupyter-notebook/ipy-notebook-spectral.png) à l’aide de SciPy Matplotlib packages tooanalyze hello structure et d’un enregistrement audio.</span><span class="sxs-lookup"><span data-stu-id="68114-107">![Screenshot](./media/jupyter-notebook/ipy-notebook-spectral.png) Using SciPy and Matplotlib packages tooanalyze hello structure of a sound recording.</span></span>

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a><span data-ttu-id="68114-108">Jupyter en deux modes : Azure Notebooks ou déploiement personnalisé</span><span class="sxs-lookup"><span data-stu-id="68114-108">Jupyter Two Ways: Azure Notebooks or Custom Deployment</span></span>
<span data-ttu-id="68114-109">Azure fournit un service que vous pouvez utiliser trop[commencer rapidement à l’aide du bloc-notes ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span><span class="sxs-lookup"><span data-stu-id="68114-109">Azure provides a service that you can use too[quickly start using Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span></span>  <span data-ttu-id="68114-110">À l’aide de hello Azure bloc-notes Service, vous pouvez facilement accéder interface accessibles par le web de tooJupyter d’accès aux ressources de calculs évolutives avec tous les power hello de Python et ses nombreuses bibliothèques.</span><span class="sxs-lookup"><span data-stu-id="68114-110">By using hello Azure Notebook Service, you can easily gain access tooJupyter's web-accessible interface to scalable computational resources with all hello power of Python and its many libraries.</span></span>  <span data-ttu-id="68114-111">Étant donné que l’installation de hello est gérée par le service de hello, les utilisateurs peuvent accéder à ces ressources sans avoir besoin de hello pour l’administration et de configuration par l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="68114-111">Since hello installation is handled by hello service, users can access these resources without hello need for administration and configuration by hello user.</span></span>

<span data-ttu-id="68114-112">Si le service de bloc-notes hello ne fonctionne pas pour votre scénario continuer tooread cet article qui seront vous montrera comment toodeploy hello bloc-notes Jupyter sur Microsoft Azure, à l’aide de Linux virtual machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="68114-112">If hello notebook service does not work for your scenario please continue tooread this article which will will show you how toodeploy hello Jupyter Notebook on Microsoft Azure, using Linux virtual machines (VMs).</span></span>

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a><span data-ttu-id="68114-113">Créer et configurer une machine virtuelle sur Azure</span><span class="sxs-lookup"><span data-stu-id="68114-113">Create and configure a VM on Azure</span></span>
<span data-ttu-id="68114-114">première étape de Hello est toocreate un ordinateur virtuel (VM) s’exécutant sur Azure.</span><span class="sxs-lookup"><span data-stu-id="68114-114">hello first step is toocreate a virtual machine (VM)  running on Azure.</span></span>
<span data-ttu-id="68114-115">Cet ordinateur virtuel est un système d’exploitation complet dans le cloud de hello et servira à exécuter hello bloc-notes Jupyter.</span><span class="sxs-lookup"><span data-stu-id="68114-115">This VM is a complete operating system in hello cloud and will be used to run hello Jupyter Notebook.</span></span> <span data-ttu-id="68114-116">Azure est capable d’exécuter des machines virtuelles Linux et Windows, et nous allons aborder, le programme d’installation de hello de Notebook sur les deux types d’ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="68114-116">Azure is capable of running both Linux and Windows virtual machines, and we will cover hello setup of Jupyter on both types of virtual machines.</span></span>

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a><span data-ttu-id="68114-117">Créer une machine virtuelle Linux et ouvrir un port pour Jupyter</span><span class="sxs-lookup"><span data-stu-id="68114-117">Create a Linux VM and open a port for Jupyter</span></span>
<span data-ttu-id="68114-118">Suivez les instructions de hello données [ici] [ portal-vm-linux] toocreate une machine virtuelle de hello *Ubuntu* distribution.</span><span class="sxs-lookup"><span data-stu-id="68114-118">Follow hello instructions given [here][portal-vm-linux] toocreate a virtual machine of hello *Ubuntu* distribution.</span></span> <span data-ttu-id="68114-119">Ce didacticiel utilise Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="68114-119">This tutorial uses Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="68114-120">Nous supposons que nom d’utilisateur hello *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="68114-120">We'll assume hello user name *azureuser*.</span></span>

<span data-ttu-id="68114-121">Une fois que la machine virtuelle de hello déploie, nous devons tooopen une règle de sécurité de groupe de sécurité réseau hello.</span><span class="sxs-lookup"><span data-stu-id="68114-121">After hello virtual machine deploys we need tooopen up a security rule on hello network security group.</span></span>  <span data-ttu-id="68114-122">À partir de hello portail Azure, accédez trop**groupes de sécurité réseau** et ouvrez hello pour tooyour correspondante du groupe de sécurité hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="68114-122">From hello Azure portal, go too**Network Security Groups** and open hello tab for hello Security Group corresponding tooyour VM.</span></span> <span data-ttu-id="68114-123">Vous devez tooadd une règle de sécurité de trafic entrant avec hello suivant paramètres : **TCP** pour le protocole de hello,  **\***  pour le port de la source (public) hello et **9999** pour port de destination (privé) Hello.</span><span class="sxs-lookup"><span data-stu-id="68114-123">You need tooadd an Inbound Security rule with hello following settings: **TCP** for hello protocol, **\*** for hello source (public) port and **9999** for hello destination (private) port.</span></span>

![Capture d'écran](./media/jupyter-notebook/azure-add-endpoint.png)

<span data-ttu-id="68114-125">Dans votre groupe de sécurité réseau, cliquez sur **Interfaces réseau** et Remarque Bonjour **adresse IP publique** car elle sera nécessaire tooconnect tooyour machine virtuelle à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="68114-125">While in your Network Security Group, click on **Network Interfaces** and note hello **Public IP Address** as it will be needed tooconnect tooyour VM in hello next step.</span></span>

## <a name="install-required-software-on-hello-vm"></a><span data-ttu-id="68114-126">Installer les logiciels requis sur la machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="68114-126">Install required software on hello VM</span></span>
<span data-ttu-id="68114-127">toorun hello bloc-notes Jupyter sur notre machine virtuelle, nous devons d’abord installer Notebook et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="68114-127">toorun hello Jupyter Notebook on our VM, we must first install Jupyter and its dependencies.</span></span> <span data-ttu-id="68114-128">Connecter la machine virtuelle linux de tooyour à l’aide de ssh et paire nom d’utilisateur/mot de passe de hello choisis lors de la création hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="68114-128">Connect tooyour linux vm using ssh and hello username/password pair you chose when you created hello vm.</span></span> <span data-ttu-id="68114-129">Dans ce didacticiel, nous utiliserons PuTTY pour nous connecter à partir de Windows.</span><span class="sxs-lookup"><span data-stu-id="68114-129">In this tutorial we will use PuTTY and connect from Windows.</span></span>

### <a name="installing-jupyter-on-ubuntu"></a><span data-ttu-id="68114-130">Installation de Jupyter sur Ubuntu</span><span class="sxs-lookup"><span data-stu-id="68114-130">Installing Jupyter on Ubuntu</span></span>
<span data-ttu-id="68114-131">Installer Anaconda, une distribution de python de science des données courants, à l’aide d’un des liens hello fournis par [Continuum Analytique](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="68114-131">Install Anaconda, a popular data science python distribution, using one of hello links provided from [Continuum Analytics](https://www.continuum.io/downloads).</span></span>  <span data-ttu-id="68114-132">Au moment de rédaction hello de ce document, hello liens ci-dessous sont hello plus de versions de toodate.</span><span class="sxs-lookup"><span data-stu-id="68114-132">As of hello writing of this document, hello below links are hello most up toodate versions.</span></span>

#### <a name="anaconda-installs-for-linux"></a><span data-ttu-id="68114-133">Installations Anaconda pour Linux</span><span class="sxs-lookup"><span data-stu-id="68114-133">Anaconda Installs for Linux</span></span>
<table>
  <th><span data-ttu-id="68114-134">Python 3.4</span><span class="sxs-lookup"><span data-stu-id="68114-134">Python 3.4</span></span></th>
  <th><span data-ttu-id="68114-135">Python 2.7</span><span class="sxs-lookup"><span data-stu-id="68114-135">Python 2.7</span></span></th>
  <tr>
    <td><span data-ttu-id="68114-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="68114-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
    <td><span data-ttu-id="68114-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="68114-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="68114-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="68114-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>
    <td><span data-ttu-id="68114-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="68114-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a><span data-ttu-id="68114-140">Installation d’Anaconda3 2.3.0 64 bits sur Ubuntu</span><span class="sxs-lookup"><span data-stu-id="68114-140">Installing Anaconda3 2.3.0 64-bit on Ubuntu</span></span>
<span data-ttu-id="68114-141">Voici un exemple d’installation d’Anaconda sur Ubuntu</span><span class="sxs-lookup"><span data-stu-id="68114-141">As an example, this is how you can install Anaconda on Ubuntu</span></span>

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

### <a name="configuring-jupyter-and-using-ssl"></a><span data-ttu-id="68114-143">Configuration de Jupyter et utilisation de SSL</span><span class="sxs-lookup"><span data-stu-id="68114-143">Configuring Jupyter and using SSL</span></span>
<span data-ttu-id="68114-144">Après l’installation de nous devons tootake un fichier de configuration actuellement toosetup hello pour notebook.</span><span class="sxs-lookup"><span data-stu-id="68114-144">After installing we need tootake a moment toosetup hello configuration files for Jupyter.</span></span> <span data-ttu-id="68114-145">Si vous rencontrez des problèmes de configuration disponible, il peut être utile toolook à hello [Documentation disponible pour l’exécution d’un serveur de l’ordinateur portable](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span><span class="sxs-lookup"><span data-stu-id="68114-145">If you experience troubles with configuring Jupyter it may be helpful toolook at hello [Jupyter Documentation for Running a Notebook Server](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span></span>

<span data-ttu-id="68114-146">Suivant nous `cd` toohello profil Active toocreate notre certificat SSL et modifier le fichier de configuration de profils hello.</span><span class="sxs-lookup"><span data-stu-id="68114-146">Next we `cd` toohello profile directory toocreate our SSL certificate and edit hello profiles configuration file.</span></span>

<span data-ttu-id="68114-147">Sur Linux, utilisez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="68114-147">On Linux use hello following command.</span></span>

    cd ~/.jupyter

<span data-ttu-id="68114-148">Utilisez hello suivant le certificat SSL hello commande de toocreate (Linux et Windows).</span><span class="sxs-lookup"><span data-stu-id="68114-148">Use hello following command toocreate hello SSL certificate(Linux and Windows).</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="68114-149">Notez qu’étant donné que nous allons créer un certificat SSL auto-signé, lors de la connexion toohello bloc-notes votre navigateur vous donne un avertissement de sécurité.</span><span class="sxs-lookup"><span data-stu-id="68114-149">Note that since we are creating a self-signed SSL certificate, when connecting toohello notebook your browser will give you a security warning.</span></span>  <span data-ttu-id="68114-150">Pour la production à long terme, vous pouvez toouse un certificat signé correctement associé à votre organisation.</span><span class="sxs-lookup"><span data-stu-id="68114-150">For long-term production use, you will want toouse a properly signed certificate associated with your organization.</span></span>  <span data-ttu-id="68114-151">Étant donné que la gestion des certificats n’est pas abordée de hello de cette démonstration, nous tiendrons tooa un certificat auto-signé pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="68114-151">Since certificate management is beyond hello scope of this demo, we will stick tooa self-signed certificate for now.</span></span>

<span data-ttu-id="68114-152">En outre toousing un certificat, vous devez également fournir un mot de passe tooprotect votre ordinateur portable à partir de toute utilisation non autorisée.</span><span class="sxs-lookup"><span data-stu-id="68114-152">In addition toousing a certificate, you must also provide a password tooprotect your notebook from unauthorized use.</span></span>  <span data-ttu-id="68114-153">Pour des raisons de sécurité Notebook utilise des mots de passe chiffrés dans son fichier de configuration, vous devez tooencrypt votre mot de passe tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="68114-153">For security reasons Jupyter uses encrypted passwords in its configuration file, so you'll need tooencrypt your password first.</span></span>  <span data-ttu-id="68114-154">IPython fournit un utilitaire toodo à l’invite de commandes, exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="68114-154">IPython provides a utility toodo so; at a command prompt run hello following command.</span></span>

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

<span data-ttu-id="68114-155">Cela vous demandera un mot de passe et la confirmation et imprime ensuite le mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="68114-155">This will prompt you for a password and confirmation, and will then print hello password.</span></span> <span data-ttu-id="68114-156">Notez ce pourquoi suivant l’étape.</span><span class="sxs-lookup"><span data-stu-id="68114-156">Note this for hello following step.</span></span>

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided hello rest for security)

<span data-ttu-id="68114-157">Ensuite, nous allons modifier le fichier de configuration du profil hello, qui est le `jupyter_notebook_config.py` fichier répertoire hello dans.</span><span class="sxs-lookup"><span data-stu-id="68114-157">Next, we will edit hello profile's configuration file, which is the `jupyter_notebook_config.py` file in hello directory you are in.</span></span>  <span data-ttu-id="68114-158">Notez que ce fichier n’existe pas, créez simplement les cas de hello.</span><span class="sxs-lookup"><span data-stu-id="68114-158">Note that this file may not exist -- just create it if that is hello case.</span></span>  <span data-ttu-id="68114-159">Ce fichier comporte de nombreux champs, tous commentés par défaut.  Vous pouvez ouvrir ce fichier avec un éditeur de texte de vos besoins, et vous devez vous assurer qu’il a au moins hello après le contenu.</span><span class="sxs-lookup"><span data-stu-id="68114-159">This file has a number of fields and by default all are commented out.  You can open this file with any text editor of your liking, and you should ensure that it has at least hello following content.</span></span> <span data-ttu-id="68114-160">**Être c.NotebookApp.password de hello tooreplace que dans la configuration de hello avec sha1 hello à partir de l’étape précédente de hello**.</span><span class="sxs-lookup"><span data-stu-id="68114-160">**Be sure tooreplace hello c.NotebookApp.password in hello config with hello sha1 from hello previous step**.</span></span>

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

### <a name="run-hello-jupyter-notebook"></a><span data-ttu-id="68114-161">Exécutez hello bloc-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="68114-161">Run hello Jupyter Notebook</span></span>
<span data-ttu-id="68114-162">À ce stade, nous sommes prêts toostart hello bloc-notes Jupyter.</span><span class="sxs-lookup"><span data-stu-id="68114-162">At this point we are ready toostart hello Jupyter Notebook.</span></span> <span data-ttu-id="68114-163">toodo, accédez répertoire toohello vous souhaitez toostore portables dans et commencer hello server de bloc-notes Jupyter hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="68114-163">toodo this, navigate toohello directory you want toostore notebooks in and start hello Jupyter Notebook server with hello following command.</span></span>

    /anaconda3/bin/jupyter-notebook

<span data-ttu-id="68114-164">Vous devez maintenant être en mesure de tooaccess votre bloc-notes Jupyter adresse hello `https://[PUBLIC-IP-ADDRESS]:9999`.</span><span class="sxs-lookup"><span data-stu-id="68114-164">You should now be able tooaccess your Jupyter Notebook at hello address `https://[PUBLIC-IP-ADDRESS]:9999`.</span></span>

<span data-ttu-id="68114-165">Lorsque vous accédez à votre ordinateur portable tout d’abord, page de connexion hello vous demande votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="68114-165">When you first access your notebook, hello login page asks for your password.</span></span> <span data-ttu-id="68114-166">Et une fois que vous vous connectez, vous verrez hello « Tableau de bord Notebook portables », qui est le centre de contrôle pour toutes les opérations de l’ordinateur portable.</span><span class="sxs-lookup"><span data-stu-id="68114-166">And once you log in, you will see hello "Jupyter Notebook Dashboard", which is the ontrol center for all notebook operations.</span></span>  <span data-ttu-id="68114-167">Dans cette page, vous pouvez créer des interpréteurs et ouvrir des interpréteurs existants.</span><span class="sxs-lookup"><span data-stu-id="68114-167">From this page you can create new notebooks and open existing ones.</span></span>

![Capture d'écran](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-hello-jupyter-notebook"></a><span data-ttu-id="68114-169">À l’aide de hello bloc-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="68114-169">Using hello Jupyter Notebook</span></span>
<span data-ttu-id="68114-170">Si vous cliquez sur hello **nouveau** bouton, vous verrez hello après l’ouverture de la page.</span><span class="sxs-lookup"><span data-stu-id="68114-170">If you click hello **New** button, you will see hello following opening page.</span></span>

![Capture d'écran](./media/jupyter-notebook/jupyter-untitled-notebook.png)

<span data-ttu-id="68114-172">zone de Hello marqués avec un `In []:` invite est la zone d’entrée de hello et ici, vous pouvez taper n’importe quel code Python valide et il ne s’exécute lorsque vous atteignez `Shift-Enter` ou sur l’icône de « Lire » hello (hello pointant vers la droite triangle dans la barre d’outils hello).</span><span class="sxs-lookup"><span data-stu-id="68114-172">hello area marked with an `In []:` prompt is hello input area, and here you can type any valid Python code and it will execute when you hit `Shift-Enter` or click on hello "Play" icon (hello right-pointing triangle in hello toolbar).</span></span>

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a><span data-ttu-id="68114-173">Un puissant paradigme : documents de calcul dynamique avec des supports puissants</span><span class="sxs-lookup"><span data-stu-id="68114-173">A powerful paradigm: live computational documents with rich media</span></span>
<span data-ttu-id="68114-174">bloc-notes Hello lui-même devriez vous sentir tooanyone très naturelle ayant utilisé Python et un traitement de texte, car il est une combinaison des deux à certains égards : vous pouvez exécuter des blocs de code Python, mais vous pouvez également conserver des notes et tout autre texte en modifiant le style de hello d’une cellule à partir de « Code » trop « Ma rkdown » à l’aide du menu déroulant de hello dans la barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="68114-174">hello notebook itself should feel very natural tooanyone who has used Python and a word processor, because it is in some ways a mix of both: you can execute blocks of Python code, but you can also keep notes and other text by changing hello style of a cell from "Code" too"Markdown" using hello drop-down menu in the toolbar.</span></span>

<span data-ttu-id="68114-175">Jupyter est bien plus qu’un traitement de texte, car il permet l’association de calculs et de supports puissants (texte, graphiques, vidéos et, virtuellement, tout ce qu’un navigateur web actuel peut afficher).</span><span class="sxs-lookup"><span data-stu-id="68114-175">Jupyter is much more than a word processor as it allows the mixing of computation and rich media (text, graphics, video and virtually anything a modern web browser can display).</span></span> <span data-ttu-id="68114-176">Vous pouvez associer du texte, du code, des vidéos et bien plus encore !</span><span class="sxs-lookup"><span data-stu-id="68114-176">You can mix, text, code, videos and more!</span></span>

![Capture d'écran](./media/jupyter-notebook/jupyter-editing-experience.png)

<span data-ttu-id="68114-178">Et avec la puissance de hello de nombreuses bibliothèques excellents Python informatique scientifiques et techniques, Bonjour suivant capture d’écran, un calcul simple peut être effectué avec hello même faciliter en tant qu’une analyse de réseau complexes, dans un environnement.</span><span class="sxs-lookup"><span data-stu-id="68114-178">And with hello power of Python's many excellent libraries for scientific and technical computing, in hello following screenshot, a simple calculation can be performed with hello same ease as a complex network analysis, all in one environment.</span></span>

<span data-ttu-id="68114-179">Ce paradigme de mélange power hello du site web moderne hello avec calcul dynamique offre de nombreuses possibilités et convient parfaitement pour le cloud de hello ; Hello bloc-notes peut être utilisée :</span><span class="sxs-lookup"><span data-stu-id="68114-179">This paradigm of mixing hello power of hello modern web with live computation offers many possibilities, and is ideally suited for hello cloud; hello Notebook can be used:</span></span>

* <span data-ttu-id="68114-180">Un toorecord bloc-notes calcul exploratoire de travailler sur un problème.</span><span class="sxs-lookup"><span data-stu-id="68114-180">As a computational scratchpad toorecord exploratory work on a problem.</span></span>
* <span data-ttu-id="68114-181">tooshare résultats avec vos collègues, dans le formulaire de calcul « live » ou dans des formats de papier (HTML, PDF).</span><span class="sxs-lookup"><span data-stu-id="68114-181">tooshare results with colleagues, either in 'live' computational form or in hardcopy formats (HTML, PDF).</span></span>
* <span data-ttu-id="68114-182">toodistribute présent matériaux apprentissage dynamique qui impliquent le calcul, les étudiants peuvent immédiatement procéder à des essais avec le code réel de hello, modifier et exécuter de nouveau interactivement.</span><span class="sxs-lookup"><span data-stu-id="68114-182">toodistribute and present live teaching materials that involve computation, so students can immediately experiment with hello real code, modify it and re-execute it interactively.</span></span>
* <span data-ttu-id="68114-183">tooprovide « livres exécutables » qui présentent des résultats hello de la recherche d’une façon qui peut être reproduite immédiatement, validé et étendu par d’autres.</span><span class="sxs-lookup"><span data-stu-id="68114-183">tooprovide "executable papers" that present hello results of research in a way that can be immediately reproduced, validated and extended by others.</span></span>
* <span data-ttu-id="68114-184">En tant que plateforme de collaboration de calcul : plusieurs utilisateurs peuvent se connecter toothe même serveur jupyter tooshare une session de calcul en temps réel.</span><span class="sxs-lookup"><span data-stu-id="68114-184">As a platform for collaborative computing: multiple users can log in toothe same notebook server tooshare a live computational session.</span></span>

<span data-ttu-id="68114-185">Si vous passez le code source de IPython toohello [référentiel][repository], vous trouverez un répertoire entier avec des exemples d’ordinateur portable que vous pouvez télécharger et expérimenter sur votre propre machine virtuelle de Azure disponible.</span><span class="sxs-lookup"><span data-stu-id="68114-185">If you go toohello IPython source code [repository][repository], you will find an entire directory with notebook examples which you can download and then experiment with on your own Azure Jupyter VM.</span></span>  <span data-ttu-id="68114-186">Il suffit de télécharger hello `.ipynb` fichiers hello de site et les télécharger sur le tableau de bord hello de votre machine virtuelle Azure bloc-notes (ou les télécharger directement sur hello machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="68114-186">Simply download hello `.ipynb` files from hello site and upload them onto hello dashboard of your notebook Azure VM (or download them directly into hello VM).</span></span>

## <a name="conclusion"></a><span data-ttu-id="68114-187">Conclusion</span><span class="sxs-lookup"><span data-stu-id="68114-187">Conclusion</span></span>
<span data-ttu-id="68114-188">Hello bloc-notes Jupyter fournit une interface puissante pour accéder aux interactivement power hello de l’écosystème de Python hello sur Azure.</span><span class="sxs-lookup"><span data-stu-id="68114-188">hello Jupyter Notebook provides a powerful interface for accessing interactively hello power of hello Python ecosystem on Azure.</span></span>  <span data-ttu-id="68114-189">Il couvre une large gamme de cas d'utilisation, notamment les simples exploration et apprentissage de Python, l'analyse et la visualisation des données, le calcul de simulation et parallèle.</span><span class="sxs-lookup"><span data-stu-id="68114-189">It covers a wide range of usage cases including simple exploration and learning Python, data analysis and visualization, simulation and parallel computing.</span></span> <span data-ttu-id="68114-190">Hello résultant bloc-notes documents contiennent d’un enregistrement complet de calculs hello qui sont effectuées et peuvent être partagées avec d’autres utilisateurs du bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="68114-190">hello resulting Notebook documents contain a complete record of hello computations that are performed and can be shared with other Jupyter users.</span></span>  <span data-ttu-id="68114-191">Hello bloc-notes Jupyter peut être utilisé en tant qu’une application locale, mais il convient parfaitement aux déploiements de cloud sur Azure</span><span class="sxs-lookup"><span data-stu-id="68114-191">hello Jupyter Notebook can be used as a local application, but it is ideally suited for cloud deployments on Azure</span></span>

<span data-ttu-id="68114-192">Hello principales fonctionnalités des Notebook sont également disponibles à l’intérieur de Visual Studio via la [outils Python pour Visual Studio] [ Python Tools for Visual Studio] (PTVS).</span><span class="sxs-lookup"><span data-stu-id="68114-192">hello core features of Jupyter are also available inside Visual Studio via the [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS).</span></span> <span data-ttu-id="68114-193">PTVS est un plug-in open source gratuit de Microsoft qui transforme Visual Studio en environnement de développement Python avancé qui inclut un éditeur avancé avec IntelliSense, ainsi qu'une intégration de débogage, de profilage et de calcul parallèle.</span><span class="sxs-lookup"><span data-stu-id="68114-193">PTVS is a free and open-source plug-in from Microsoft that turns Visual Studio into an advanced Python development environment that includes an advanced editor with IntelliSense, debugging, profiling and parallel computing integration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68114-194">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="68114-194">Next steps</span></span>
<span data-ttu-id="68114-195">Pour plus d’informations, consultez hello [centre de développement Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="68114-195">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
