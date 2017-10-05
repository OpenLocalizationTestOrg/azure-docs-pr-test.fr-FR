---
title: "Science des données d’une machine virtuelle de science des données Linux | Microsoft Docs"
description: "Comment effectuer plusieurs tâches courantes de science des données avec la machine virtuelle de science des données Linux."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 34ef0b10-9270-474f-8800-eecb183bbce4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev;paulsh
ms.openlocfilehash: 6da9a8e3f9f8ac851c2a8deb861ac1d0b3ec5874
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="data-science-on-the-linux-data-science-virtual-machine"></a><span data-ttu-id="89bdf-103">Science des données sur la machine virtuelle de science des données Linux</span><span class="sxs-lookup"><span data-stu-id="89bdf-103">Data science on the Linux Data Science Virtual Machine</span></span>
<span data-ttu-id="89bdf-104">Cette procédure pas à pas vous montre comment effectuer plusieurs tâches courantes de science des données avec la machine virtuelle de science des données Linux.</span><span class="sxs-lookup"><span data-stu-id="89bdf-104">This walkthrough shows you how to perform several common data science tasks with the Linux Data Science VM.</span></span> <span data-ttu-id="89bdf-105">La machine virtuelle de science des données Linux est une image de machine virtuelle disponible sur Azure qui est préinstallée avec plusieurs outils couramment utilisés dans le cadre de l’analyse de données et du Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="89bdf-105">The Linux Data Science Virtual Machine (DSVM) is a virtual machine image available on Azure that is pre-installed with a collection of tools commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="89bdf-106">Les composants logiciels clés sont détaillés dans la rubrique [Approvisionnement d’une machine virtuelle de science des données Linux](machine-learning-data-science-linux-dsvm-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="89bdf-106">The key software components are itemized in the [Provision the Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md) topic.</span></span> <span data-ttu-id="89bdf-107">L’image de la machine virtuelle facilite la prise en main de la science des données en quelques minutes, sans avoir à installer et à configurer individuellement chacun des outils individuellement.</span><span class="sxs-lookup"><span data-stu-id="89bdf-107">The VM image makes it easy to get started doing data science in minutes, without having to install and configure each of the tools individually.</span></span> <span data-ttu-id="89bdf-108">Le cas échéant, vous pouvez facilement faire monter en puissance la machine virtuelle, et l’arrêter lorsqu’elle est inutilisée.</span><span class="sxs-lookup"><span data-stu-id="89bdf-108">You can easily scale up the VM, if needed, and stop it when not in use.</span></span> <span data-ttu-id="89bdf-109">Cette ressource est donc flexible et économique.</span><span class="sxs-lookup"><span data-stu-id="89bdf-109">So this resource is both elastic and cost-efficient.</span></span>

<span data-ttu-id="89bdf-110">Les tâches de science des données décrites dans cette procédure pas à pas suivent les étapes décrites dans le [processus de science des données pour les équipes](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span><span class="sxs-lookup"><span data-stu-id="89bdf-110">The data science tasks demonstrated in this walkthrough follow the steps outlined in the [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span></span> <span data-ttu-id="89bdf-111">Ce processus fournit une approche systématique de la science des données qui permet aux équipes de scientifiques des données de collaborer efficacement tout au long du cycle de vie du développement d’applications intelligentes.</span><span class="sxs-lookup"><span data-stu-id="89bdf-111">This process provides a systematic approach to data science that enables teams of data scientists to effectively collaborate over the lifecycle of building intelligent applications.</span></span> <span data-ttu-id="89bdf-112">Le processus de science des données fournit également une infrastructure itérative pour la science des données, qui peut être suivie par une personne.</span><span class="sxs-lookup"><span data-stu-id="89bdf-112">The data science process also provides an iterative framework for data science that can be followed by an individual.</span></span>

<span data-ttu-id="89bdf-113">Au cours de cette procédure pas à pas, nous analysons le jeu de données [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) .</span><span class="sxs-lookup"><span data-stu-id="89bdf-113">We analyze the [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset in this walkthrough.</span></span> <span data-ttu-id="89bdf-114">Il s’agit d’un ensemble d’e-mails marqués comme courrier indésirable ou courrier légitime (non indésirable), qui contient également des statistiques sur le contenu des e-mails.</span><span class="sxs-lookup"><span data-stu-id="89bdf-114">This is a set of emails that are marked as either spam or ham (meaning they are not spam), and also contains some statistics on the content of the emails.</span></span> <span data-ttu-id="89bdf-115">Les statistiques incluses sont évoquées dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="89bdf-115">The statistics included are discussed in the next but one section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89bdf-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="89bdf-116">Prerequisites</span></span>
<span data-ttu-id="89bdf-117">Avant de pouvoir utiliser une machine virtuelle de science des données Linux, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="89bdf-117">Before you can use a Linux Data Science Virtual Machine, you must have the following:</span></span>

* <span data-ttu-id="89bdf-118">Un **abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-118">An **Azure subscription**.</span></span> <span data-ttu-id="89bdf-119">Si vous n’en avez pas déjà un, voir [Créez votre compte Azure gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="89bdf-119">If you do not already have one, see [Create your free Azure account today](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="89bdf-120">Une [**machine virtuelle de science des données Linux**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="89bdf-120">A [**Linux data science VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span></span> <span data-ttu-id="89bdf-121">Pour plus d’informations sur l’approvisionnement de cette machine virtuelle, consultez [Approvisionnement d’une machine virtuelle de science des données Linux](machine-learning-data-science-linux-dsvm-intro.md).</span><span class="sxs-lookup"><span data-stu-id="89bdf-121">For information on provisioning this VM, see [Provision the Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).</span></span>
* <span data-ttu-id="89bdf-122">[X2Go](http://wiki.x2go.org/doku.php) installé sur votre ordinateur et une session XFCE ouverte.</span><span class="sxs-lookup"><span data-stu-id="89bdf-122">[X2Go](http://wiki.x2go.org/doku.php) installed on your computer and opened an XFCE session.</span></span> <span data-ttu-id="89bdf-123">Pour plus d’informations sur l’installation et la configuration d’un **client X2Go**, consultez [Installation et configuration du client X2Go](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span><span class="sxs-lookup"><span data-stu-id="89bdf-123">For information on installing and configuring an **X2Go client**, see [Installing and configuring X2Go client](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span></span> 
* <span data-ttu-id="89bdf-124">Un **compte AzureML**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-124">An **AzureML account**.</span></span> <span data-ttu-id="89bdf-125">Si vous n’avez pas déjà un, inscrivez-vous pour en obtenir un nouveau sur la [page d’accueil AzureML](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="89bdf-125">If you don't already have one, sign up for new one at the [AzureML homepage](https://studio.azureml.net/).</span></span> <span data-ttu-id="89bdf-126">Il existe un niveau d’utilisation gratuit pour vous aider à commencer.</span><span class="sxs-lookup"><span data-stu-id="89bdf-126">There is a free usage tier to help you get started.</span></span>

## <a name="download-the-spambase-dataset"></a><span data-ttu-id="89bdf-127">Télécharger le jeu de données spambase</span><span class="sxs-lookup"><span data-stu-id="89bdf-127">Download the spambase dataset</span></span>
<span data-ttu-id="89bdf-128">Le jeu de données [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) est un ensemble de données relativement réduit qui ne contient que 4 601 exemples.</span><span class="sxs-lookup"><span data-stu-id="89bdf-128">The [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset is a relatively small set of data that contains only 4601 examples.</span></span> <span data-ttu-id="89bdf-129">Il s’agit d’une taille pratique à utiliser lors de la démonstration de certaines des fonctionnalités clés de la machine virtuelle de science des données, car elle limite les besoins en ressources.</span><span class="sxs-lookup"><span data-stu-id="89bdf-129">This is a convenient size to use when demonstrating that some of the key features of the Data Science VM as it keeps the resource requirements modest.</span></span>

> [!NOTE]
> <span data-ttu-id="89bdf-130">Cette procédure pas à pas a été créée sur une machine virtuelle de science des données Linux de taille D2 v2.</span><span class="sxs-lookup"><span data-stu-id="89bdf-130">This walkthrough was created on a D2 v2-sized Linux Data Science Virtual Machine.</span></span> <span data-ttu-id="89bdf-131">Cette taille de machine virtuelle de science des données est capable de gérer les procédures décrites dans cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="89bdf-131">This size DSVM is capable of handling the procedures in this walkthrough.</span></span>
>
>

<span data-ttu-id="89bdf-132">Si vous avez besoin de plus d’espace de stockage, vous pouvez créer des disques supplémentaires et les joindre à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89bdf-132">If you need more storage space, you can create additional disks and attach them to your VM.</span></span> <span data-ttu-id="89bdf-133">Ces disques utilisent le stockage Azure persistant ; ainsi, leurs données sont conservées même lorsque le serveur est réapprovisionné en raison d’un redimensionnement ou d’un arrêt.</span><span class="sxs-lookup"><span data-stu-id="89bdf-133">These disks use persistent Azure storage, so their data is preserved even when the server is reprovisioned due to resizing or is shut down.</span></span> <span data-ttu-id="89bdf-134">Pour ajouter un disque et l’attacher à votre machine virtuelle, suivez les instructions [Ajouter un disque à une machine virtuelle Linux](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="89bdf-134">To add a disk and attach it to your VM, follow the instructions in [Add a disk to a Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="89bdf-135">Cette procédure utilise l’interface de ligne de commande Azure (Azure CLI), qui est déjà installée sur la machine virtuelle de science des données.</span><span class="sxs-lookup"><span data-stu-id="89bdf-135">These steps use the Azure Command-Line Interface (Azure CLI), which is already installed on the DSVM.</span></span> <span data-ttu-id="89bdf-136">Par conséquent, ces procédures peuvent être entièrement effectuées à partir de la machine virtuelle elle-même.</span><span class="sxs-lookup"><span data-stu-id="89bdf-136">So these procedures can be done entirely from the VM itself.</span></span> <span data-ttu-id="89bdf-137">Une autre option pour augmenter le stockage consiste à utiliser les [fichiers Azure](../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="89bdf-137">Another option to increase storage is to use [Azure files](../storage/files/storage-how-to-use-files-linux.md).</span></span>

<span data-ttu-id="89bdf-138">Pour télécharger les données, ouvrez une fenêtre de terminal et exécutez cette commande :</span><span class="sxs-lookup"><span data-stu-id="89bdf-138">To download the data, open a terminal window and run this command:</span></span>

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

<span data-ttu-id="89bdf-139">Le fichier téléchargé n’a pas de ligne d’en-tête, nous allons donc créer un autre fichier doté d’un en-tête.</span><span class="sxs-lookup"><span data-stu-id="89bdf-139">The downloaded file does not have a header row, so let's create another file that does have a header.</span></span> <span data-ttu-id="89bdf-140">Exécutez cette commande pour créer un fichier avec les en-têtes appropriés :</span><span class="sxs-lookup"><span data-stu-id="89bdf-140">Run this command to create a file with the appropriate headers:</span></span>

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

<span data-ttu-id="89bdf-141">Ensuite, concaténez les deux fichiers ensemble avec la commande :</span><span class="sxs-lookup"><span data-stu-id="89bdf-141">Then concatenate the two files together with the command:</span></span>

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

<span data-ttu-id="89bdf-142">Le jeu de données possède plusieurs types de statistiques sur chaque e-mail :</span><span class="sxs-lookup"><span data-stu-id="89bdf-142">The dataset has several types of statistics on each email:</span></span>

* <span data-ttu-id="89bdf-143">Les colonnes comme ***word\_freq\_WORD*** indiquent le pourcentage de mots dans l’e-mail correspondant à *WORD*.</span><span class="sxs-lookup"><span data-stu-id="89bdf-143">Columns like ***word\_freq\_WORD*** indicate the percentage of words in the email that match *WORD*.</span></span> <span data-ttu-id="89bdf-144">Par exemple, si la valeur *word\_freq\_make* correspond à 1, 1 % de tous les mots dans l’e-mail était *make*.</span><span class="sxs-lookup"><span data-stu-id="89bdf-144">For example, if *word\_freq\_make* is 1, then 1% of all words in the email were *make*.</span></span>
* <span data-ttu-id="89bdf-145">Les colonnes comme ***char\_freq\_CHAR*** indiquent le pourcentage de tous les caractères dans l’e-mail correspondant à *CHAR*.</span><span class="sxs-lookup"><span data-stu-id="89bdf-145">Columns like ***char\_freq\_CHAR*** indicate the percentage of all characters in the email that were *CHAR*.</span></span>
* <span data-ttu-id="89bdf-146">***capital\_run\_length\_longest*** est la longueur la plus longue d’une séquence de lettres majuscules.</span><span class="sxs-lookup"><span data-stu-id="89bdf-146">***capital\_run\_length\_longest*** is the longest length of a sequence of capital letters.</span></span>
* <span data-ttu-id="89bdf-147">***capital\_run\_length\_average*** est la longueur moyenne de toutes les séquences de lettres majuscules.</span><span class="sxs-lookup"><span data-stu-id="89bdf-147">***capital\_run\_length\_average*** is the average length of all sequences of capital letters.</span></span>
* <span data-ttu-id="89bdf-148">***capital\_run\_length\_total*** est la longueur totale de toutes les séquences de lettres majuscules.</span><span class="sxs-lookup"><span data-stu-id="89bdf-148">***capital\_run\_length\_total*** is the total length of all sequences of capital letters.</span></span>
* <span data-ttu-id="89bdf-149">***spam*** indique si l’e-mail a été considéré comme du courrier indésirable ou non (1 = courrier indésirable, 0 = courrier non indésirable).</span><span class="sxs-lookup"><span data-stu-id="89bdf-149">***spam*** indicates whether the email was considered spam or not (1 = spam, 0 = not spam).</span></span>

## <a name="explore-the-dataset-with-microsoft-r-open"></a><span data-ttu-id="89bdf-150">Explorer le jeu de données avec Microsoft R Open</span><span class="sxs-lookup"><span data-stu-id="89bdf-150">Explore the dataset with Microsoft R Open</span></span>
<span data-ttu-id="89bdf-151">Nous allons examiner les données et découvrir certaines fonctionnalités de base du Machine Learning avec R. La machine virtuelle de science des données est fournie avec [Microsoft R Open](https://mran.revolutionanalytics.com/open/) préinstallé.</span><span class="sxs-lookup"><span data-stu-id="89bdf-151">Let's examine the data and do some basic machine learning with R. The Data Science VM comes with [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installed.</span></span> <span data-ttu-id="89bdf-152">Les bibliothèques mathématiques multithread dans cette version de R offrent de meilleures performances que les différentes versions monothread.</span><span class="sxs-lookup"><span data-stu-id="89bdf-152">The multithreaded math libraries in this version of R offer better performance than various single-threaded versions.</span></span> <span data-ttu-id="89bdf-153">Microsoft R Open fournit également la reproductibilité à l’aide d’une capture instantanée du référentiel du package CRAN.</span><span class="sxs-lookup"><span data-stu-id="89bdf-153">Microsoft R Open also provides reproducibility by using a snapshot of the CRAN package repository.</span></span>

<span data-ttu-id="89bdf-154">Pour obtenir des copies des exemples de code utilisés dans cette procédure pas à pas, clonez le référentiel **Azure-Machine-Learning-Data-Science** à l’aide de git, qui est déjà préinstallé sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89bdf-154">To get copies of the code samples used in this walkthrough, clone the **Azure-Machine-Learning-Data-Science** repository using git, which is pre-installed on the VM.</span></span> <span data-ttu-id="89bdf-155">Depuis la ligne de commande git, exécutez :</span><span class="sxs-lookup"><span data-stu-id="89bdf-155">From the git command line, run:</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="89bdf-156">Ouvrez une fenêtre de terminal et démarrez une nouvelle session R avec la console interactive R.</span><span class="sxs-lookup"><span data-stu-id="89bdf-156">Open a terminal window and start a new R session with the R interactive console.</span></span>

> [!NOTE]
> <span data-ttu-id="89bdf-157">Vous pouvez également utiliser RStudio pour les procédures suivantes.</span><span class="sxs-lookup"><span data-stu-id="89bdf-157">You can also use RStudio for the following procedures.</span></span> <span data-ttu-id="89bdf-158">Pour installer RStudio, exécutez cette commande à partir d’un terminal : `./Desktop/DSVM\ tools/installRStudio.sh`</span><span class="sxs-lookup"><span data-stu-id="89bdf-158">To install RStudio, execute this command at a terminal: `./Desktop/DSVM\ tools/installRStudio.sh`</span></span>
>
>

<span data-ttu-id="89bdf-159">Pour importer les données et configurer l’environnement, exécutez :</span><span class="sxs-lookup"><span data-stu-id="89bdf-159">To import the data and set up the environment, run:</span></span>

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

<span data-ttu-id="89bdf-160">Pour afficher un résumé des statistiques de chaque colonne :</span><span class="sxs-lookup"><span data-stu-id="89bdf-160">To see summary statistics about each column:</span></span>

    summary(data)

<span data-ttu-id="89bdf-161">Pour une vue différente des données :</span><span class="sxs-lookup"><span data-stu-id="89bdf-161">For a different view of the data:</span></span>

    str(data)

<span data-ttu-id="89bdf-162">Vous voyez le type de chaque variable et les premières valeurs dans le jeu de données.</span><span class="sxs-lookup"><span data-stu-id="89bdf-162">This shows you the type of each variable and the first few values in the dataset.</span></span>

<span data-ttu-id="89bdf-163">La colonne *spam* a été lue comme un entier, mais il s’agit en fait d’une variable par catégorie (ou facteur).</span><span class="sxs-lookup"><span data-stu-id="89bdf-163">The *spam* column was read as an integer, but it's actually a categorical variable (or factor).</span></span> <span data-ttu-id="89bdf-164">Pour définir son type :</span><span class="sxs-lookup"><span data-stu-id="89bdf-164">To set its type:</span></span>

    data$spam <- as.factor(data$spam)

<span data-ttu-id="89bdf-165">Pour effectuer une analyse exploratoire, utilisez le package [ggplot2](http://ggplot2.org/) , une bibliothèque de graphiques populaire pour R qui est déjà installée sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89bdf-165">To do some exploratory analysis, use the [ggplot2](http://ggplot2.org/) package, a popular graphing library for R that is already installed on the VM.</span></span> <span data-ttu-id="89bdf-166">Remarque : à partir des données récapitulatives affichées précédemment, nous disposons de statistiques résumées sur la fréquence du point d’exclamation.</span><span class="sxs-lookup"><span data-stu-id="89bdf-166">Note, from the summary data displayed earlier, that we have summary statistics on the frequency of the exclamation mark character.</span></span> <span data-ttu-id="89bdf-167">Nous allons tracer ces fréquences ici avec les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="89bdf-167">Let's plot those frequencies here with the following commands:</span></span>

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="89bdf-168">Étant donné que la barre de zéro décale le tracé, nous allons nous en débarrasser :</span><span class="sxs-lookup"><span data-stu-id="89bdf-168">Since the zero bar is skewing the plot, let's get rid of it:</span></span>

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="89bdf-169">Il existe une densité non triviale au-dessus de 1 qui semble intéressante.</span><span class="sxs-lookup"><span data-stu-id="89bdf-169">There is a non-trivial density above 1 that looks interesting.</span></span> <span data-ttu-id="89bdf-170">Examinons simplement ces données :</span><span class="sxs-lookup"><span data-stu-id="89bdf-170">Let's look at just that data:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="89bdf-171">Ensuite, répartissez-les en courrier indésirable et courrier légitime :</span><span class="sxs-lookup"><span data-stu-id="89bdf-171">Then split it by spam vs ham:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

<span data-ttu-id="89bdf-172">Ces exemples doivent vous permettre d’effectuer des tracés similaires des autres colonnes pour explorer les données qu’elles contiennent.</span><span class="sxs-lookup"><span data-stu-id="89bdf-172">These examples should enable you to make similar plots of the other columns to explore the data contained in them.</span></span>

## <a name="train-and-test-an-ml-model"></a><span data-ttu-id="89bdf-173">Effectuer l’apprentissage et tester un modèle ML</span><span class="sxs-lookup"><span data-stu-id="89bdf-173">Train and test an ML model</span></span>
<span data-ttu-id="89bdf-174">À présent, nous allons effectuer l’apprentissage de quelques modèles de Machine Learning pour classer les e-mails dans le jeu de données comme courrier indésirable ou courrier légitime.</span><span class="sxs-lookup"><span data-stu-id="89bdf-174">Now let's train a couple of machine learning models to classify the emails in the dataset as containing either span or ham.</span></span> <span data-ttu-id="89bdf-175">Dans cette section, nous effectuons l’apprentissage d’un modèle d’arbre de décision et d’un modèle de forêts aléatoires, puis nous testons la précision de leurs prédictions.</span><span class="sxs-lookup"><span data-stu-id="89bdf-175">We train a decision tree model and a random forest model in this section and then test their accuracy of their predictions.</span></span>

> [!NOTE]
> <span data-ttu-id="89bdf-176">Le package rpart (partition récursive et arbres de régression) utilisé dans le code suivant est déjà installé sur la machine virtuelle de science des données.</span><span class="sxs-lookup"><span data-stu-id="89bdf-176">The rpart (Recursive Partitioning and Regression Trees) package used in the following code is already installed on the Data Science VM.</span></span>
>
>

<span data-ttu-id="89bdf-177">Nous allons commencer par diviser le jeu de données en jeu d’apprentissage et jeu de test :</span><span class="sxs-lookup"><span data-stu-id="89bdf-177">First, let's split the dataset into training and test sets:</span></span>

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

<span data-ttu-id="89bdf-178">Ensuite, nous allons créer un arbre de décision pour classer les e-mails.</span><span class="sxs-lookup"><span data-stu-id="89bdf-178">And then create a decision tree to classify the emails.</span></span>

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

<span data-ttu-id="89bdf-179">Voici le résultat :</span><span class="sxs-lookup"><span data-stu-id="89bdf-179">Here is the result:</span></span>

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

<span data-ttu-id="89bdf-181">Pour déterminer la qualité d’exécution sur l’ensemble d’apprentissage, utilisez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="89bdf-181">To determine how well it performs on the training set, use the following code:</span></span>

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="89bdf-182">Pour déterminer la qualité d’exécution sur le jeu de test :</span><span class="sxs-lookup"><span data-stu-id="89bdf-182">To determine how well it performs on the test set:</span></span>

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="89bdf-183">Essayons également un modèle de forêts aléatoires.</span><span class="sxs-lookup"><span data-stu-id="89bdf-183">Let's also try a random forest model.</span></span> <span data-ttu-id="89bdf-184">Les forêts aléatoires effectuent l’apprentissage d’une multitude d’arbres de décision et génèrent une classe qui constitue le mode de classification de tous les arbres de décision individuels.</span><span class="sxs-lookup"><span data-stu-id="89bdf-184">Random forests train a multitude of decision trees and output a class that is the mode of the classifications from all of the individual decision trees.</span></span> <span data-ttu-id="89bdf-185">Elles fournissent une approche de Machine Learning plus puissante, car elles corrigent la tendance d’un modèle d’arbre de décision à dépasser un jeu de données d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="89bdf-185">They provide a more powerful machine learning approach as they correct for the tendency of a decision tree model to overfit a training dataset.</span></span>

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-to-azure-ml"></a><span data-ttu-id="89bdf-186">Déployer un modèle dans Azure ML</span><span class="sxs-lookup"><span data-stu-id="89bdf-186">Deploy a model to Azure ML</span></span>
<span data-ttu-id="89bdf-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) est un service cloud qui facilite la création et le déploiement des modèles d’analyse prédictive.</span><span class="sxs-lookup"><span data-stu-id="89bdf-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is a cloud service that makes it easy to build and deploy predictive analytics models.</span></span> <span data-ttu-id="89bdf-188">L’une des fonctionnalités intéressantes d’AzureML est sa capacité à publier toute fonction R comme un service web.</span><span class="sxs-lookup"><span data-stu-id="89bdf-188">One of the nice features of AzureML is its ability to publish any R function as a web service.</span></span> <span data-ttu-id="89bdf-189">Le package R AzureML rend le déploiement facile à réaliser à partir de notre session R sur la machine virtuelle de science des données.</span><span class="sxs-lookup"><span data-stu-id="89bdf-189">The AzureML R package makes deployment easy to do right from our R session on the DSVM.</span></span>

<span data-ttu-id="89bdf-190">Pour déployer le code de l’arbre de décision à partir de la section précédente, vous devez vous connecter à Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="89bdf-190">To deploy the decision tree code from the previous section, you need to sign in to Azure Machine Learning Studio.</span></span> <span data-ttu-id="89bdf-191">Vous avez besoin de votre ID d’espace de travail et d’un jeton d’autorisation pour vous connecter.</span><span class="sxs-lookup"><span data-stu-id="89bdf-191">You need your workspace ID and an authorization token to sign in.</span></span> <span data-ttu-id="89bdf-192">Pour rechercher ces valeurs et initialiser les variables AzureML avec celles-ci :</span><span class="sxs-lookup"><span data-stu-id="89bdf-192">To find these values and initialize the AzureML variables with them:</span></span>

<span data-ttu-id="89bdf-193">Sélectionnez **Paramètres** dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="89bdf-193">Select **Settings** on the left-hand menu.</span></span> <span data-ttu-id="89bdf-194">Notez votre **ID D’ESPACE DE TRAVAIL**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-194">Note your **WORKSPACE ID**.</span></span> <span data-ttu-id="89bdf-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span><span class="sxs-lookup"><span data-stu-id="89bdf-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span></span>

<span data-ttu-id="89bdf-196">Sélectionnez **Jetons d’authentification** dans le menu général et notez votre **Jeton d’autorisation principal**.![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span><span class="sxs-lookup"><span data-stu-id="89bdf-196">Select **Authorization Tokens** from the overhead menu and note your **Primary Authorization Token**.![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span></span>

<span data-ttu-id="89bdf-197">Chargez le package **AzureML** , puis définissez les valeurs des variables avec votre jeton et votre ID d’espace de travail dans votre session R sur la machine virtuelle de science des données :</span><span class="sxs-lookup"><span data-stu-id="89bdf-197">Load the **AzureML** package and then set values of the variables with your token and workspace ID in your R session on the DSVM:</span></span>

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


<span data-ttu-id="89bdf-198">Nous allons simplifier le modèle afin de rendre cette démonstration plus facile à implémenter.</span><span class="sxs-lookup"><span data-stu-id="89bdf-198">Let's simplify the model to make this demonstration easier to implement.</span></span> <span data-ttu-id="89bdf-199">Sélectionnez les trois variables dans l’arbre de décision le plus proche de la racine, et créez un arbre à l’aide de ces trois variables seulement :</span><span class="sxs-lookup"><span data-stu-id="89bdf-199">Pick the three variables in the decision tree closest to the root and build a new tree using just those three variables:</span></span>

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

<span data-ttu-id="89bdf-200">Nous avons besoin d’une fonction de prédiction qui prend les fonctionnalités comme une entrée et renvoie les valeurs prédites :</span><span class="sxs-lookup"><span data-stu-id="89bdf-200">We need a prediction function that takes the features as an input and returns the predicted values:</span></span>

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

<span data-ttu-id="89bdf-201">Publiez la fonction predictSpam sur AzureML à l’aide de la fonction **publishWebService** :</span><span class="sxs-lookup"><span data-stu-id="89bdf-201">Publish the predictSpam function to AzureML using the **publishWebService** function:</span></span>

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

<span data-ttu-id="89bdf-202">Cette fonction prend la fonction **predictSpam**, crée un service web nommé **spamWebService** avec des entrées et des sorties définies, et renvoie des informations sur le nouveau point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="89bdf-202">This function takes the **predictSpam** function, creates a web service named **spamWebService** with defined inputs and outputs, and returns information about the new endpoint.</span></span>

<span data-ttu-id="89bdf-203">Affichez les détails du service web publié, notamment son point de terminaison d’API et les touches d’accès rapide avec la commande :</span><span class="sxs-lookup"><span data-stu-id="89bdf-203">View details of the published web service, including its API endpoint and access keys with the command:</span></span>

    spamWebService[[2]]

<span data-ttu-id="89bdf-204">Pour l’essayer sur les 10 premières lignes du test défini :</span><span class="sxs-lookup"><span data-stu-id="89bdf-204">To try it out on the first 10 rows of the test set:</span></span>

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a><span data-ttu-id="89bdf-205">Utiliser les autres outils disponibles</span><span class="sxs-lookup"><span data-stu-id="89bdf-205">Use other tools available</span></span>
<span data-ttu-id="89bdf-206">Les sections suivantes montrent comment utiliser certains des outils installés sur la machine virtuelle de science des données Linux. Voici la liste des outils abordés :</span><span class="sxs-lookup"><span data-stu-id="89bdf-206">The remaining sections show how to use some of the tools installed on the Linux Data Science VM.Here is the list of tools discussed:</span></span>

* <span data-ttu-id="89bdf-207">XGBoost</span><span class="sxs-lookup"><span data-stu-id="89bdf-207">XGBoost</span></span>
* <span data-ttu-id="89bdf-208">Python</span><span class="sxs-lookup"><span data-stu-id="89bdf-208">Python</span></span>
* <span data-ttu-id="89bdf-209">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="89bdf-209">Jupyterhub</span></span>
* <span data-ttu-id="89bdf-210">Rattle</span><span class="sxs-lookup"><span data-stu-id="89bdf-210">Rattle</span></span>
* <span data-ttu-id="89bdf-211">PostgreSQL et Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="89bdf-211">PostgreSQL & Squirrel SQL</span></span>
* <span data-ttu-id="89bdf-212">SQL Server Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="89bdf-212">SQL Server Data Warehouse</span></span>

## <a name="xgboost"></a><span data-ttu-id="89bdf-213">XGBoost</span><span class="sxs-lookup"><span data-stu-id="89bdf-213">XGBoost</span></span>
<span data-ttu-id="89bdf-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) est un outil qui offre une implémentation rapide et précise des arborescences optimisées.</span><span class="sxs-lookup"><span data-stu-id="89bdf-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) is a tool that provides a fast and accurate boosted tree implementation.</span></span>

    require(xgboost)
    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

    bst <- xgboost(data = data.matrix(trainSet[,0:57]), label = trainSet$spam, nthread = 2, nrounds = 2, objective = "binary:logistic")

    pred <- predict(bst, data.matrix(testSet[, 0:57]))
    accuracy <- 1.0 - mean(as.numeric(pred > 0.5) != testSet$spam)
    print(paste("test accuracy = ", accuracy))

<span data-ttu-id="89bdf-215">XGBoost peut également appeler à partir de Python ou d’une ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="89bdf-215">XGBoost can also call from python or a command line.</span></span>

## <a name="python"></a><span data-ttu-id="89bdf-216">Python</span><span class="sxs-lookup"><span data-stu-id="89bdf-216">Python</span></span>
<span data-ttu-id="89bdf-217">Pour un développement basé sur Python, les versions 2.7 et 3.5 des distributions Anaconda Python ont été installées dans la machine virtuelle de science des données Linux.</span><span class="sxs-lookup"><span data-stu-id="89bdf-217">For development using Python, the Anaconda Python distributions 2.7 and 3.5 have been installed in the DSVM.</span></span>

> [!NOTE]
> <span data-ttu-id="89bdf-218">La distribution Anaconda inclut [Condas](http://conda.pydata.org/docs/index.html), qui peut être utilisé pour créer des environnements personnalisés pour Python avec des versions et/ou des packages différents installés.</span><span class="sxs-lookup"><span data-stu-id="89bdf-218">The Anaconda distribution includes [Condas](http://conda.pydata.org/docs/index.html), which can be used to create custom environments for Python that have different versions and/or packages installed in them.</span></span>
>
>

<span data-ttu-id="89bdf-219">Nous allons lire le jeu de données spambase et classer les e-mails avec des machines à vecteurs de support dans scikit-learn :</span><span class="sxs-lookup"><span data-stu-id="89bdf-219">Let's read in some of the spambase dataset and classify the emails with support vector machines in scikit-learn:</span></span>

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="89bdf-220">Pour effectuer des prédictions :</span><span class="sxs-lookup"><span data-stu-id="89bdf-220">To make predictions:</span></span>

    clf.predict(X.ix[0:20, :])

<span data-ttu-id="89bdf-221">Pour montrer comment publier un point de terminaison AzureML, créons un modèle plus simple des trois variables comme nous l’avons fait précédemment lorsque nous avons publié le modèle R.</span><span class="sxs-lookup"><span data-stu-id="89bdf-221">To show how to publish an AzureML endpoint, let's make a simpler model the three variables as we did when we published the R model previously.</span></span>

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="89bdf-222">Pour publier le modèle dans AzureML :</span><span class="sxs-lookup"><span data-stu-id="89bdf-222">To publish the model to AzureML:</span></span>

    # Publish the model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about the resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call the model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> <span data-ttu-id="89bdf-223">Cette option est uniquement disponible pour Python 2.7 et n’est pas encore prise en charge sur 3.5.</span><span class="sxs-lookup"><span data-stu-id="89bdf-223">This is only available for python 2.7 and is not yet supported on 3.5.</span></span> <span data-ttu-id="89bdf-224">Exécutez avec **/anaconda/bin/python2.7**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-224">Run with **/anaconda/bin/python2.7**.</span></span>
>
>

## <a name="jupyterhub"></a><span data-ttu-id="89bdf-225">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="89bdf-225">Jupyterhub</span></span>
<span data-ttu-id="89bdf-226">La distribution Anaconda dans la machine virtuelle de science des données est fournie avec un bloc-notes Jupyter, un environnement multiplateforme pour partager Python, R, ou le code et l’analyse Julia.</span><span class="sxs-lookup"><span data-stu-id="89bdf-226">The Anaconda distribution in the DSVM comes with a Jupyter notebook, a cross-platform environment to share Python, R, or Julia code and analysis.</span></span> <span data-ttu-id="89bdf-227">Le serveur Jupyter Notebook est accessible via JupyterHub.</span><span class="sxs-lookup"><span data-stu-id="89bdf-227">The Jupyter notebook is accessed through JupyterHub.</span></span> <span data-ttu-id="89bdf-228">Vous vous connectez en utilisant votre nom d’utilisateur Linux local et votre mot de passe à ***https://\<nom DNS de machine virtuelle ou adresse IP\>:8000/***.</span><span class="sxs-lookup"><span data-stu-id="89bdf-228">You sign in using your local Linux user name and password at ***https://\<VM DNS name or IP Address\>:8000/***.</span></span> <span data-ttu-id="89bdf-229">Tous les fichiers de configuration pour JupyterHub se trouvent dans le répertoire **/etc/jupyterhub**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-229">All configuration files for JupyterHub are found in directory **/etc/jupyterhub**.</span></span>

<span data-ttu-id="89bdf-230">Plusieurs exemples de notebooks sont déjà installés sur la machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="89bdf-230">Several sample notebooks are already installed on the VM:</span></span>

* <span data-ttu-id="89bdf-231">Consultez [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) pour un exemple de notebook Python.</span><span class="sxs-lookup"><span data-stu-id="89bdf-231">See the [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) for a sample Python notebook.</span></span>
* <span data-ttu-id="89bdf-232">Consultez [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) pour un exemple de notebook **R** .</span><span class="sxs-lookup"><span data-stu-id="89bdf-232">See [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) for a sample **R** notebook.</span></span>
* <span data-ttu-id="89bdf-233">Consultez [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) pour un autre exemple de notebook **Python** .</span><span class="sxs-lookup"><span data-stu-id="89bdf-233">See the [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) for another sample **Python** notebook.</span></span>

> [!NOTE]
> <span data-ttu-id="89bdf-234">Le langage Julia est également disponible à partir de la ligne de commande sur la machine virtuelle de science des données Linux.</span><span class="sxs-lookup"><span data-stu-id="89bdf-234">The Julia language is also available from the command line on the Linux Data Science VM.</span></span>
>
>

## <a name="rattle"></a><span data-ttu-id="89bdf-235">Rattle</span><span class="sxs-lookup"><span data-stu-id="89bdf-235">Rattle</span></span>
<span data-ttu-id="89bdf-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (l’outil d’analyse R pour apprendre plus facilement) est un outil R graphique pour l’exploration de données.</span><span class="sxs-lookup"><span data-stu-id="89bdf-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (the R Analytical Tool To Learn Easily) is a graphical R tool for data mining.</span></span> <span data-ttu-id="89bdf-237">Il possède une interface intuitive qui facilite la charge, l’exploration et la transformation des données, ainsi que la création et l’évaluation des modèles.</span><span class="sxs-lookup"><span data-stu-id="89bdf-237">It has an intuitive interface that makes it easy to load, explore, and transform data and build and evaluate models.</span></span>  <span data-ttu-id="89bdf-238">L’article [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) (Rattle : une interface utilisateur graphique pour l’exploration de données pour R) fournit une procédure pas à pas présentant ses fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="89bdf-238">The article [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) provides a walkthrough that demonstrates its features.</span></span>

<span data-ttu-id="89bdf-239">Installez et démarrez Rattle avec les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="89bdf-239">Install and start Rattle with the following commands:</span></span>

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> <span data-ttu-id="89bdf-240">L’installation n’est pas obligatoire sur la machine virtuelle de science des données.</span><span class="sxs-lookup"><span data-stu-id="89bdf-240">Installation is not required on the DSVM.</span></span> <span data-ttu-id="89bdf-241">Toutefois, Rattle peut vous inviter à installer des packages supplémentaires lors de son chargement.</span><span class="sxs-lookup"><span data-stu-id="89bdf-241">But Rattle may prompt you to install additional packages when it loads.</span></span>
>
>

<span data-ttu-id="89bdf-242">Rattle utilise une interface basée sur des onglets.</span><span class="sxs-lookup"><span data-stu-id="89bdf-242">Rattle uses a tab-based interface.</span></span> <span data-ttu-id="89bdf-243">La plupart des onglets correspondent aux étapes du [Processus de science des données](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), telles que le chargement de données ou l’exploration.</span><span class="sxs-lookup"><span data-stu-id="89bdf-243">Most of the tabs correspond to steps in the [Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), like loading data or exploring it.</span></span> <span data-ttu-id="89bdf-244">Le processus de science des données se déroule de gauche à droite à travers les onglets.</span><span class="sxs-lookup"><span data-stu-id="89bdf-244">The data science process flows from left to right through the tabs.</span></span> <span data-ttu-id="89bdf-245">Cependant, le dernier onglet contient un journal des commandes R exécutées par Rattle.</span><span class="sxs-lookup"><span data-stu-id="89bdf-245">But the last tab contains a log of the R commands run by Rattle.</span></span>

<span data-ttu-id="89bdf-246">Pour charger et configurer le jeu de données :</span><span class="sxs-lookup"><span data-stu-id="89bdf-246">To load and configure the dataset:</span></span>

* <span data-ttu-id="89bdf-247">Pour charger le fichier, sélectionnez l’onglet **Données** , puis</span><span class="sxs-lookup"><span data-stu-id="89bdf-247">To load the file, select the **Data** tab, then</span></span>
* <span data-ttu-id="89bdf-248">Choisissez le sélecteur en regard de **Nom de fichier**, puis **spambaseHeaders.data**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-248">Choose the selector next to **Filename** and choose **spambaseHeaders.data**.</span></span>
* <span data-ttu-id="89bdf-249">Pour charger le fichier,</span><span class="sxs-lookup"><span data-stu-id="89bdf-249">To load the file.</span></span> <span data-ttu-id="89bdf-250">sélectionnez **Exécuter** dans la première ligne de boutons.</span><span class="sxs-lookup"><span data-stu-id="89bdf-250">select **Execute** in the top row of buttons.</span></span> <span data-ttu-id="89bdf-251">Vous devez voir un résumé de chaque colonne, notamment son type de données identifié, qu’il s’agisse d’une entrée, d’une cible ou d’un autre type de variable, ainsi que le nombre de valeurs uniques.</span><span class="sxs-lookup"><span data-stu-id="89bdf-251">You should see a summary of each column, including its identified data type, whether it's an input, a target, or other type of variable, and the number of unique values.</span></span>
* <span data-ttu-id="89bdf-252">Rattle a correctement identifié la colonne **spam** comme étant la cible.</span><span class="sxs-lookup"><span data-stu-id="89bdf-252">Rattle has correctly identified the **spam** column as the target.</span></span> <span data-ttu-id="89bdf-253">Sélectionnez la colonne spam, puis définissez le **Type de données cible** sur **Par catégorie**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-253">Select the spam column, then set the **Target Data Type** to **Categoric**.</span></span>

<span data-ttu-id="89bdf-254">Pour explorer les données :</span><span class="sxs-lookup"><span data-stu-id="89bdf-254">To explore the data:</span></span>

* <span data-ttu-id="89bdf-255">Sélectionnez l’onglet **Explorer** .</span><span class="sxs-lookup"><span data-stu-id="89bdf-255">Select the **Explore** tab.</span></span>
* <span data-ttu-id="89bdf-256">Cliquez sur **Résumé**, puis sur **Exécuter**, pour afficher des informations sur les types de variable et certaines statistiques résumées.</span><span class="sxs-lookup"><span data-stu-id="89bdf-256">Click **Summary**, then **Execute**, to see some information about the variable types and some summary statistics.</span></span>
* <span data-ttu-id="89bdf-257">Pour afficher d’autres types de statistiques relatives à chaque variable, sélectionnez d’autres options, comme **Décrire** ou **Concepts de base**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-257">To view other types of statistics about each variable, select other options like **Describe** or **Basics**.</span></span>

<span data-ttu-id="89bdf-258">L’onglet **Explorer** vous permet également de générer de nombreux tracés ingénieux.</span><span class="sxs-lookup"><span data-stu-id="89bdf-258">The **Explore** tab also allows you to generate many insightful plots.</span></span> <span data-ttu-id="89bdf-259">Pour tracer un histogramme des données :</span><span class="sxs-lookup"><span data-stu-id="89bdf-259">To plot a histogram of the data:</span></span>

* <span data-ttu-id="89bdf-260">Sélectionnez **Distributions**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-260">Select **Distributions**.</span></span>
* <span data-ttu-id="89bdf-261">Cochez **Histogramme** pour **word_freq_remove** et **word_freq_you**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-261">Check **Histogram** for **word_freq_remove** and **word_freq_you**.</span></span>
* <span data-ttu-id="89bdf-262">Sélectionnez **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-262">Select **Execute**.</span></span> <span data-ttu-id="89bdf-263">Vous devez voir les deux graphiques de densité dans une seule fenêtre de graphique, où il est clair que le mot « you » (vous) apparaît beaucoup plus fréquemment dans les e-mails que le mot « remove » (supprimer).</span><span class="sxs-lookup"><span data-stu-id="89bdf-263">You should see both density plots in a single graph window, where it is clear that the word "you" appears much more frequently in emails than "remove".</span></span>

<span data-ttu-id="89bdf-264">Les tracés de corrélation sont également intéressants.</span><span class="sxs-lookup"><span data-stu-id="89bdf-264">The Correlation plots are also interesting.</span></span> <span data-ttu-id="89bdf-265">Pour en créer un :</span><span class="sxs-lookup"><span data-stu-id="89bdf-265">To create one:</span></span>

* <span data-ttu-id="89bdf-266">Choisissez **Corrélation** comme **Type**, puis</span><span class="sxs-lookup"><span data-stu-id="89bdf-266">Choose **Correlation** as the **Type**, then</span></span>
* <span data-ttu-id="89bdf-267">Sélectionnez **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-267">Select **Execute**.</span></span>
* <span data-ttu-id="89bdf-268">Rattle vous avertit qu’il recommande un maximum de 40 variables.</span><span class="sxs-lookup"><span data-stu-id="89bdf-268">Rattle warns you that it recommends a maximum of 40 variables.</span></span> <span data-ttu-id="89bdf-269">Sélectionnez **Oui** pour afficher le tracé.</span><span class="sxs-lookup"><span data-stu-id="89bdf-269">Select **Yes** to view the plot.</span></span>

<span data-ttu-id="89bdf-270">Des corrélations intéressantes existent : le terme « technologie » est étroitement corrélé avec les termes « HP » et « laboratoires », par exemple.</span><span class="sxs-lookup"><span data-stu-id="89bdf-270">There are some interesting correlations that come up: "technology" is strongly correlated to "HP" and "labs", for example.</span></span> <span data-ttu-id="89bdf-271">Il est également étroitement corrélé avec « 650 », car le code de région des donneurs du dataset est 650.</span><span class="sxs-lookup"><span data-stu-id="89bdf-271">It is also strongly correlated to "650", because the area code of the dataset donors is 650.</span></span>

<span data-ttu-id="89bdf-272">Les valeurs numériques des corrélations entre les mots sont disponibles dans la fenêtre d’exploration.</span><span class="sxs-lookup"><span data-stu-id="89bdf-272">The numeric values for the correlations between words are available in the Explore window.</span></span> <span data-ttu-id="89bdf-273">Il est intéressant de noter, par exemple, que le terme « technologie » est négativement corrélé avec les termes « votre » et « argent ».</span><span class="sxs-lookup"><span data-stu-id="89bdf-273">It is interesting to note, for example, that "technology" is negatively correlated with "your" and "money".</span></span>

<span data-ttu-id="89bdf-274">Rattle peut transformer le jeu de données pour gérer certains problèmes courants.</span><span class="sxs-lookup"><span data-stu-id="89bdf-274">Rattle can transform the dataset to handle some common issues.</span></span> <span data-ttu-id="89bdf-275">Par exemple, il vous permet de remettre à l’échelle les fonctionnalités, d’imputer les valeurs manquantes, de gérer les valeurs hors-norme et de supprimer des variables ou des observations avec des données manquantes.</span><span class="sxs-lookup"><span data-stu-id="89bdf-275">For example, it allows you to rescale features, impute missing values, handle outliers, and remove variables or observations with missing data.</span></span> <span data-ttu-id="89bdf-276">Rattle peut également identifier des règles d’association entre des observations et/ou des variables.</span><span class="sxs-lookup"><span data-stu-id="89bdf-276">Rattle can also identify association rules between observations and/or variables.</span></span> <span data-ttu-id="89bdf-277">Ces onglets sont hors de portée pour cette introduction pas à pas.</span><span class="sxs-lookup"><span data-stu-id="89bdf-277">These tabs are out of scope for this introductory walkthrough.</span></span>

<span data-ttu-id="89bdf-278">Rattle peut également effectuer une analyse de cluster.</span><span class="sxs-lookup"><span data-stu-id="89bdf-278">Rattle can also perform cluster analysis.</span></span> <span data-ttu-id="89bdf-279">Nous allons exclure certaines fonctionnalités pour simplifier la lecture de la sortie.</span><span class="sxs-lookup"><span data-stu-id="89bdf-279">Let's exclude some features to make the output easier to read.</span></span> <span data-ttu-id="89bdf-280">Sous l’onglet **Données**, choisissez **Ignorer** en regard de chacune des variables à l’exception de ces dix éléments :</span><span class="sxs-lookup"><span data-stu-id="89bdf-280">On the **Data** tab, choose **Ignore** next to each of the variables except these ten items:</span></span>

* <span data-ttu-id="89bdf-281">word_freq_hp</span><span class="sxs-lookup"><span data-stu-id="89bdf-281">word_freq_hp</span></span>
* <span data-ttu-id="89bdf-282">word_freq_technology</span><span class="sxs-lookup"><span data-stu-id="89bdf-282">word_freq_technology</span></span>
* <span data-ttu-id="89bdf-283">word_freq_george</span><span class="sxs-lookup"><span data-stu-id="89bdf-283">word_freq_george</span></span>
* <span data-ttu-id="89bdf-284">word_freq_remove</span><span class="sxs-lookup"><span data-stu-id="89bdf-284">word_freq_remove</span></span>
* <span data-ttu-id="89bdf-285">word_freq_your</span><span class="sxs-lookup"><span data-stu-id="89bdf-285">word_freq_your</span></span>
* <span data-ttu-id="89bdf-286">word_freq_dollar</span><span class="sxs-lookup"><span data-stu-id="89bdf-286">word_freq_dollar</span></span>
* <span data-ttu-id="89bdf-287">word_freq_money</span><span class="sxs-lookup"><span data-stu-id="89bdf-287">word_freq_money</span></span>
* <span data-ttu-id="89bdf-288">capital_run_length_longest</span><span class="sxs-lookup"><span data-stu-id="89bdf-288">capital_run_length_longest</span></span>
* <span data-ttu-id="89bdf-289">word_freq_business</span><span class="sxs-lookup"><span data-stu-id="89bdf-289">word_freq_business</span></span>
* <span data-ttu-id="89bdf-290">spam</span><span class="sxs-lookup"><span data-stu-id="89bdf-290">spam</span></span>

<span data-ttu-id="89bdf-291">Ensuite, revenez à l’onglet **Cluster**, choisissez **KMeans**, et définissez le *Nombre de clusters* sur 4.</span><span class="sxs-lookup"><span data-stu-id="89bdf-291">Then go back to the **Cluster** tab, choose **KMeans**, and set the *Number of clusters* to 4.</span></span> <span data-ttu-id="89bdf-292">Ensuite, sélectionnez **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-292">Then **Execute**.</span></span> <span data-ttu-id="89bdf-293">Les résultats s’affichent dans la fenêtre de sortie.</span><span class="sxs-lookup"><span data-stu-id="89bdf-293">The results are displayed in the output window.</span></span> <span data-ttu-id="89bdf-294">Un cluster possède une fréquence élevée de « george » et de « hp » et est probablement un e-mail professionnel légitime.</span><span class="sxs-lookup"><span data-stu-id="89bdf-294">One cluster has high frequency of "george" and "hp" and is probably a legitimate business email.</span></span>

<span data-ttu-id="89bdf-295">Pour créer un modèle Machine Learning d’arbre de décision simple :</span><span class="sxs-lookup"><span data-stu-id="89bdf-295">To build a simple decision tree machine learning model:</span></span>

* <span data-ttu-id="89bdf-296">Sélectionnez l’onglet **Modèle** ,</span><span class="sxs-lookup"><span data-stu-id="89bdf-296">Select the **Model** tab,</span></span>
* <span data-ttu-id="89bdf-297">Choisissez **Arbre** en tant que **Type**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-297">Choose **Tree** as the **Type**.</span></span>
* <span data-ttu-id="89bdf-298">Sélectionnez **Exécuter** pour afficher l’arbre sous forme de texte dans la fenêtre de sortie.</span><span class="sxs-lookup"><span data-stu-id="89bdf-298">Select **Execute** to display the tree in text form in the output window.</span></span>
* <span data-ttu-id="89bdf-299">Sélectionnez le bouton **Dessin** pour afficher une version graphique.</span><span class="sxs-lookup"><span data-stu-id="89bdf-299">Select the **Draw** button to view a graphical version.</span></span> <span data-ttu-id="89bdf-300">Celle-ci est très similaire à l’arbre obtenu précédemment à l’aide de *rpart*.</span><span class="sxs-lookup"><span data-stu-id="89bdf-300">This looks quite similar to the tree we obtained earlier using *rpart*.</span></span>

<span data-ttu-id="89bdf-301">L’une des fonctionnalités intéressantes de Rattle est sa capacité à exécuter plusieurs méthodes Machine Learning et à les évaluer rapidement.</span><span class="sxs-lookup"><span data-stu-id="89bdf-301">One of the nice features of Rattle is its ability to run several machine learning methods and quickly evaluate them.</span></span> <span data-ttu-id="89bdf-302">Voici la procédure :</span><span class="sxs-lookup"><span data-stu-id="89bdf-302">Here is the procedure:</span></span>

* <span data-ttu-id="89bdf-303">Choisissez **Tous** pour le **Type**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-303">Choose **All** for the **Type**.</span></span>
* <span data-ttu-id="89bdf-304">Sélectionnez **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-304">Select **Execute**.</span></span>
* <span data-ttu-id="89bdf-305">Une fois la procédure terminée, vous pouvez cliquer sur n’importe quel **Type** unique, comme **SVM**, et afficher les résultats.</span><span class="sxs-lookup"><span data-stu-id="89bdf-305">After it finishes you can click any single **Type**, like **SVM**, and view the results.</span></span>
* <span data-ttu-id="89bdf-306">Vous pouvez également comparer les performances des modèles sur le jeu de validation à l’aide de l’onglet **Évaluer** . Par exemple, la sélection de l’option **Matrice d’erreur** affiche la matrice de confusion, l’erreur globale et l’erreur de classe moyennée pour chaque modèle sur le jeu de validation.</span><span class="sxs-lookup"><span data-stu-id="89bdf-306">You can also compare the performance of the models on the validation set using the **Evaluate** tab. For example, the **Error Matrix** selection shows you the confusion matrix, overall error, and averaged class error for each model on the validation set.</span></span>
* <span data-ttu-id="89bdf-307">Vous pouvez également tracer des courbes ROC, effectuer des analyses de sensibilité et d’autres types d’évaluations de modèle.</span><span class="sxs-lookup"><span data-stu-id="89bdf-307">You can also plot ROC curves, perform sensitivity analysis, and do other types of model evaluations.</span></span>

<span data-ttu-id="89bdf-308">Une fois que vous avez terminé la création de modèles, sélectionnez l’onglet **Journal** pour afficher le code R exécuté par Rattle pendant votre session.</span><span class="sxs-lookup"><span data-stu-id="89bdf-308">Once you're finished building models, select the **Log** tab to view the R code run by Rattle during your session.</span></span> <span data-ttu-id="89bdf-309">Vous pouvez sélectionner le bouton **Exporter** pour l’enregistrer.</span><span class="sxs-lookup"><span data-stu-id="89bdf-309">You can select the **Export** button to save it.</span></span>

> [!NOTE]
> <span data-ttu-id="89bdf-310">Il existe un bogue dans la version actuelle de Rattle.</span><span class="sxs-lookup"><span data-stu-id="89bdf-310">There is a bug in current release of Rattle.</span></span> <span data-ttu-id="89bdf-311">Pour modifier le script ou l’utiliser pour répéter les étapes ultérieurement, vous devez insérer un symbole dièse (#) devant *Exporter ce journal… * dans le texte du journal.</span><span class="sxs-lookup"><span data-stu-id="89bdf-311">To modify the script or use it to repeat your steps later, you must insert a # character in front of *Export this log ... * in the text of the log.</span></span>
>
>

## <a name="postgresql--squirrel-sql"></a><span data-ttu-id="89bdf-312">PostgreSQL et Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="89bdf-312">PostgreSQL & Squirrel SQL</span></span>
<span data-ttu-id="89bdf-313">La machine virtuelle de science des données est fournie avec PostgreSQL installé.</span><span class="sxs-lookup"><span data-stu-id="89bdf-313">The DSVM comes with PostgreSQL installed.</span></span> <span data-ttu-id="89bdf-314">PostgreSQL est une base de données relationnelle, open source et sophistiquée.</span><span class="sxs-lookup"><span data-stu-id="89bdf-314">PostgreSQL is a sophisticated, open-source relational database.</span></span> <span data-ttu-id="89bdf-315">Cette section montre comment charger notre jeu de données spam dans PostgreSQL, puis l’interroger.</span><span class="sxs-lookup"><span data-stu-id="89bdf-315">This section shows how to load our spam dataset into PostgreSQL and then query it.</span></span>

<span data-ttu-id="89bdf-316">Avant de pouvoir charger les données, vous devez autoriser l’authentification par mot de passe à partir de l’hôte local.</span><span class="sxs-lookup"><span data-stu-id="89bdf-316">Before you can load the data, you need to allow password authentication from the localhost.</span></span> <span data-ttu-id="89bdf-317">À l’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="89bdf-317">At a command prompt:</span></span>

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

<span data-ttu-id="89bdf-318">Au bas du fichier de configuration, plusieurs lignes détaillent les connexions autorisées :</span><span class="sxs-lookup"><span data-stu-id="89bdf-318">Near the bottom of the config file are several lines that detail the allowed connections:</span></span>

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

<span data-ttu-id="89bdf-319">Modifiez la ligne « connexions locales IPv4 » pour utiliser md5 au lieu d’ident, afin de permettre la connexion avec un nom d’utilisateur et un mot de passe :</span><span class="sxs-lookup"><span data-stu-id="89bdf-319">Change the "IPv4 local connections" line to use md5 instead of ident, so we can log in using a username and password:</span></span>

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

<span data-ttu-id="89bdf-320">Ensuite, redémarrez le service postgres :</span><span class="sxs-lookup"><span data-stu-id="89bdf-320">And restart the postgres service:</span></span>

    sudo systemctl restart postgresql

<span data-ttu-id="89bdf-321">Pour lancer psql, un terminal interactif pour PostgreSQL, en tant qu’utilisateur postgres intégré, exécutez la commande suivante à partir d’une invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="89bdf-321">To launch psql, an interactive terminal for PostgreSQL, as the built-in postgres user, run the following command from a prompt:</span></span>

    sudo -u postgres psql

<span data-ttu-id="89bdf-322">Créez un compte d’utilisateur à l’aide du même nom d’utilisateur que celui du compte Linux avec lequel vous êtes actuellement connecté, et attribuez-lui un mot de passe :</span><span class="sxs-lookup"><span data-stu-id="89bdf-322">Create a new user account, using the same username as the Linux account you're currently logged in as, and give it a password:</span></span>

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

<span data-ttu-id="89bdf-323">Ensuite, connectez-vous à psql en tant qu’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="89bdf-323">Then log in to psql as your user:</span></span>

    psql

<span data-ttu-id="89bdf-324">Et importez les données dans une base de données :</span><span class="sxs-lookup"><span data-stu-id="89bdf-324">And import the data into a new database:</span></span>

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

<span data-ttu-id="89bdf-325">À présent, nous allons explorer les données et exécuter des requêtes à l’aide de **Squirrel SQL**, un outil graphique qui vous permet d’interagir avec les bases de données via un pilote JDBC.</span><span class="sxs-lookup"><span data-stu-id="89bdf-325">Now, let's explore the data and run some queries using **Squirrel SQL**, a graphical tool that lets you interact with databases via a JDBC driver.</span></span>

<span data-ttu-id="89bdf-326">Pour commencer, lancez Squirrel SQL à partir du menu Applications.</span><span class="sxs-lookup"><span data-stu-id="89bdf-326">To get started, launch Squirrel SQL from the Applications menu.</span></span> <span data-ttu-id="89bdf-327">Pour configurer le pilote :</span><span class="sxs-lookup"><span data-stu-id="89bdf-327">To set up the driver:</span></span>

* <span data-ttu-id="89bdf-328">Sélectionnez **Windows**, puis **Afficher les pilotes**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-328">Select **Windows**, then **View Drivers**.</span></span>
* <span data-ttu-id="89bdf-329">Cliquez avec le bouton droit sur **PostgreSQL** et sélectionnez **Modifier le pilote**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-329">Right-click on **PostgreSQL** and select **Modify Driver**.</span></span>
* <span data-ttu-id="89bdf-330">Sélectionnez **Chemin d’accès de la classe supplémentaire**, puis **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-330">Select **Extra Class Path**, then **Add**.</span></span>
* <span data-ttu-id="89bdf-331">Entrez ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** pour le **nom de fichier** et</span><span class="sxs-lookup"><span data-stu-id="89bdf-331">Enter ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** for the **File Name** and</span></span>
* <span data-ttu-id="89bdf-332">Sélectionnez **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-332">Select **Open**.</span></span>
* <span data-ttu-id="89bdf-333">Choisissez Pilotes de la liste, puis sélectionnez **org.postgresql.Driver** dans **Nom de la classe**, et sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-333">Choose List Drivers, then select **org.postgresql.Driver** in **Class Name**, and select **OK**.</span></span>

<span data-ttu-id="89bdf-334">Pour configurer la connexion au serveur local :</span><span class="sxs-lookup"><span data-stu-id="89bdf-334">To set up the connection to the local server:</span></span>

* <span data-ttu-id="89bdf-335">Sélectionnez **Windows**, puis **Afficher les alias**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-335">Select **Windows**, then **View Aliases.**</span></span>
* <span data-ttu-id="89bdf-336">Choisissez le bouton **+** pour créer un alias.</span><span class="sxs-lookup"><span data-stu-id="89bdf-336">Choose the **+** button to make a new alias.</span></span>
* <span data-ttu-id="89bdf-337">Nommez-le *Base de données de courrier indésirable*, et choisissez **PostgreSQL** dans la liste déroulante **Pilote**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-337">Name it *Spam database*, choose **PostgreSQL** in the **Driver** drop-down.</span></span>
* <span data-ttu-id="89bdf-338">Définissez l’URL sur *jdbc:postgresql://localhost/spam*.</span><span class="sxs-lookup"><span data-stu-id="89bdf-338">Set the URL to *jdbc:postgresql://localhost/spam*.</span></span>
* <span data-ttu-id="89bdf-339">Entrez votre *nom d’utilisateur* et votre *mot de passe*.</span><span class="sxs-lookup"><span data-stu-id="89bdf-339">Enter your *username* and *password*.</span></span>
* <span data-ttu-id="89bdf-340">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-340">Click **OK**.</span></span>
* <span data-ttu-id="89bdf-341">Pour ouvrir la fenêtre **Connexion**, double-cliquez sur l’alias de la ***Base de données de courrier indésirable***.</span><span class="sxs-lookup"><span data-stu-id="89bdf-341">To open the **Connection** window, double-click the ***Spam database*** alias.</span></span>
* <span data-ttu-id="89bdf-342">Sélectionnez **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="89bdf-342">Select **Connect**.</span></span>

<span data-ttu-id="89bdf-343">Pour exécuter des requêtes :</span><span class="sxs-lookup"><span data-stu-id="89bdf-343">To run some queries:</span></span>

* <span data-ttu-id="89bdf-344">Sélectionnez l’onglet **SQL** .</span><span class="sxs-lookup"><span data-stu-id="89bdf-344">Select the **SQL** tab.</span></span>
* <span data-ttu-id="89bdf-345">Entrez une requête simple telle que `SELECT * from data;` dans la zone de texte de requête en haut de l’onglet SQL.</span><span class="sxs-lookup"><span data-stu-id="89bdf-345">Enter a simple query such as `SELECT * from data;` in the query textbox at the top of the SQL tab.</span></span>
* <span data-ttu-id="89bdf-346">Appuyez sur **Ctrl+Entrée** pour l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="89bdf-346">Press **Ctrl-Enter** to run it.</span></span> <span data-ttu-id="89bdf-347">Par défaut, SQL Squirrel renvoie les 100 premières lignes de votre requête.</span><span class="sxs-lookup"><span data-stu-id="89bdf-347">By default Squirrel SQL returns the first 100 rows from your query.</span></span>

<span data-ttu-id="89bdf-348">Il existe de nombreuses requêtes supplémentaires, que vous pouvez exécuter pour explorer ces données.</span><span class="sxs-lookup"><span data-stu-id="89bdf-348">There are many more queries you could run to explore this data.</span></span> <span data-ttu-id="89bdf-349">Par exemple, en quoi la fréquence du mot *make* diffère-t-elle entre le courrier indésirable et le courrier légitime ?</span><span class="sxs-lookup"><span data-stu-id="89bdf-349">For example, how does the frequency of the word *make* differ between spam and ham?</span></span>

    SELECT avg(word_freq_make), spam from data group by spam;

<span data-ttu-id="89bdf-350">Ou quelles sont les caractéristiques des e-mails qui contiennent souvent le terme *3d*?</span><span class="sxs-lookup"><span data-stu-id="89bdf-350">Or what are the characteristics of email that frequently contain *3d*?</span></span>

    SELECT * from data order by word_freq_3d desc;

<span data-ttu-id="89bdf-351">La plupart des e-mails qui présentent de nombreuses occurrences de *3d* sont apparemment du courrier indésirable. Cela peut donc constituer une fonctionnalité utile pour la création d’un modèle prédictif de classement des e-mails.</span><span class="sxs-lookup"><span data-stu-id="89bdf-351">Most emails that have a high occurrence of *3d* are apparently spam, so it could be a useful feature for building a predictive model to classify the emails.</span></span>

<span data-ttu-id="89bdf-352">Si vous souhaitiez effectuer du Machine Learning avec des données stockées dans une base de données PostgreSQL, envisagez d’utiliser [MADlib](http://madlib.incubator.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="89bdf-352">If you wanted to perform machine learning with data stored in a PostgreSQL database, consider using [MADlib](http://madlib.incubator.apache.org/).</span></span>

## <a name="sql-server-data-warehouse"></a><span data-ttu-id="89bdf-353">SQL Server Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="89bdf-353">SQL Server Data Warehouse</span></span>
<span data-ttu-id="89bdf-354">Azure SQL Data Warehouse est une base de données de mise à l’échelle basée sur le cloud qui prend en charge le traitement de grands volumes de données relationnelles et non relationnelles.</span><span class="sxs-lookup"><span data-stu-id="89bdf-354">Azure SQL Data Warehouse is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span> <span data-ttu-id="89bdf-355">Pour plus d’informations, consultez [En quoi consiste Azure SQL Data Warehouse ?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="89bdf-355">For more information, see [What is Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span></span>

<span data-ttu-id="89bdf-356">Pour vous connecter à l’entrepôt de données et créer la table, exécutez la commande suivante depuis une invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="89bdf-356">To connect to the data warehouse and create the table, run the following command from a command prompt:</span></span>

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

<span data-ttu-id="89bdf-357">Ensuite, à l’invite sqlcmd :</span><span class="sxs-lookup"><span data-stu-id="89bdf-357">Then at the sqlcmd prompt:</span></span>

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

<span data-ttu-id="89bdf-358">Copier des données avec bcp :</span><span class="sxs-lookup"><span data-stu-id="89bdf-358">Copy data with bcp:</span></span>

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> <span data-ttu-id="89bdf-359">Les fins de ligne dans le fichier téléchargé sont de type Windows, mais bcp attend le style UNIX ; il convient donc de l’indiquer à bcp avec l’indicateur -r.</span><span class="sxs-lookup"><span data-stu-id="89bdf-359">The line endings in the downloaded file are Windows-style, but bcp expects UNIX-style, so we need to tell bcp that with the -r flag.</span></span>
>
>

<span data-ttu-id="89bdf-360">Et exécuter des requêtes avec sqlcmd :</span><span class="sxs-lookup"><span data-stu-id="89bdf-360">And query with sqlcmd:</span></span>

    select top 10 spam, char_freq_dollar from spam;
    GO

<span data-ttu-id="89bdf-361">Vous pouvez également exécuter des requêtes avec Squirrel SQL.</span><span class="sxs-lookup"><span data-stu-id="89bdf-361">You could also query with Squirrel SQL.</span></span> <span data-ttu-id="89bdf-362">Suivez des étapes similaires pour PostgreSQL, à l’aide du pilote JDBC Microsoft MSSQL Server, disponible dans ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span><span class="sxs-lookup"><span data-stu-id="89bdf-362">Follow similar steps for PostgreSQL, using the Microsoft MSSQL Server JDBC Driver, which can be found in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89bdf-363">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="89bdf-363">Next steps</span></span>
<span data-ttu-id="89bdf-364">Pour une vue d’ensemble des rubriques qui vous guident à travers les tâches qui constituent le processus de science des données dans Azure, consultez [processus de science des données pour les équipes](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="89bdf-364">For an overview of topics that walk you through the tasks that comprise the Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="89bdf-365">Pour une description des autres procédures pas à pas complètes illustrant les étapes du processus TDSP pour des scénarios spécifiques, voir [Procédures pas à pas du processus TDSP (Team Data Science Process)](data-science-process-walkthroughs.md).</span><span class="sxs-lookup"><span data-stu-id="89bdf-365">For a description of other end-to-end walkthroughs that demonstrate the steps in the Team Data Science Process for specific scenarios, see [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md).</span></span> <span data-ttu-id="89bdf-366">Les procédures pas à pas montrent également comment combiner les outils et services dans le cloud et sur site dans un flux de travail ou un pipeline pour créer une application intelligente.</span><span class="sxs-lookup"><span data-stu-id="89bdf-366">The walkthroughs also illustrate how to combine cloud and on-premises tools and services into a workflow or pipeline to create an intelligent application.</span></span>
