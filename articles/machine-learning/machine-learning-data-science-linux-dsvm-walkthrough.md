---
title: "science aaaData sur hello une Machine virtuelle pour la science des données Linux | Documents Microsoft"
description: "Comment tooperform scientifiques de données commun plusieurs tâches avec hello VM de science des données Linux."
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
ms.openlocfilehash: 78764825f2e834fa4ddb7fdc2f59418dbe736e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-on-hello-linux-data-science-virtual-machine"></a><span data-ttu-id="fcf58-103">Recherche de données sur hello une Machine virtuelle pour la science des données Linux</span><span class="sxs-lookup"><span data-stu-id="fcf58-103">Data science on hello Linux Data Science Virtual Machine</span></span>
<span data-ttu-id="fcf58-104">Cette procédure pas à pas vous montre comment tooperform scientifiques de données commun plusieurs tâches avec hello VM de science des données Linux.</span><span class="sxs-lookup"><span data-stu-id="fcf58-104">This walkthrough shows you how tooperform several common data science tasks with hello Linux Data Science VM.</span></span> <span data-ttu-id="fcf58-105">Hello Machine virtuelle de science des données Linux (DSVM) est une image de machine virtuelle disponible sur Azure est préinstallé avec un ensemble d’outils utilisés pour l’analytique des données et l’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="fcf58-105">hello Linux Data Science Virtual Machine (DSVM) is a virtual machine image available on Azure that is pre-installed with a collection of tools commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="fcf58-106">les composants logiciels de clé Hello sont répertoriés dans hello [hello de configurer une Machine virtuelle pour la science des données Linux](machine-learning-data-science-linux-dsvm-intro.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="fcf58-106">hello key software components are itemized in hello [Provision hello Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md) topic.</span></span> <span data-ttu-id="fcf58-107">Hello image de machine virtuelle rend facile tooget commencé à faire la science des données en quelques minutes, sans avoir tooinstall et configurer chacun des outils de hello individuellement.</span><span class="sxs-lookup"><span data-stu-id="fcf58-107">hello VM image makes it easy tooget started doing data science in minutes, without having tooinstall and configure each of hello tools individually.</span></span> <span data-ttu-id="fcf58-108">Vous pouvez facilement évoluer hello machine virtuelle, si nécessaire et l’arrêter inutilisés.</span><span class="sxs-lookup"><span data-stu-id="fcf58-108">You can easily scale up hello VM, if needed, and stop it when not in use.</span></span> <span data-ttu-id="fcf58-109">Cette ressource est donc flexible et économique.</span><span class="sxs-lookup"><span data-stu-id="fcf58-109">So this resource is both elastic and cost-efficient.</span></span>

<span data-ttu-id="fcf58-110">tâches courantes relatives aux données présentées dans cette procédure pas à pas Hello suivent étapes hello hello [processus de science des données équipe](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span><span class="sxs-lookup"><span data-stu-id="fcf58-110">hello data science tasks demonstrated in this walkthrough follow hello steps outlined in hello [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span></span> <span data-ttu-id="fcf58-111">Ce processus fournit une science toodata approche systématique permettant aux équipes de chercheurs de données tooeffectively collaborer hello du cycle de vie de la création d’applications intelligentes.</span><span class="sxs-lookup"><span data-stu-id="fcf58-111">This process provides a systematic approach toodata science that enables teams of data scientists tooeffectively collaborate over hello lifecycle of building intelligent applications.</span></span> <span data-ttu-id="fcf58-112">processus de science des données Hello fournit également une infrastructure itérative pour la science des données qui peuvent être suivie par une personne.</span><span class="sxs-lookup"><span data-stu-id="fcf58-112">hello data science process also provides an iterative framework for data science that can be followed by an individual.</span></span>

<span data-ttu-id="fcf58-113">Nous analysons hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) jeu de données dans cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="fcf58-113">We analyze hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset in this walkthrough.</span></span> <span data-ttu-id="fcf58-114">Il s’agit d’un ensemble d’adresses de messagerie qui sont marqués comme étant du courrier indésirable ou ham (ce qui signifie qu’ils ne sont pas courrier indésirable), et contient également des statistiques sur le contenu des e-mails de hello hello.</span><span class="sxs-lookup"><span data-stu-id="fcf58-114">This is a set of emails that are marked as either spam or ham (meaning they are not spam), and also contains some statistics on hello content of hello emails.</span></span> <span data-ttu-id="fcf58-115">statistiques Hello inclus sont abordés plus loin dans hello mais une seule section.</span><span class="sxs-lookup"><span data-stu-id="fcf58-115">hello statistics included are discussed in hello next but one section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcf58-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fcf58-116">Prerequisites</span></span>
<span data-ttu-id="fcf58-117">Avant de pouvoir utiliser un ordinateur de virtuel de science des données Linux, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="fcf58-117">Before you can use a Linux Data Science Virtual Machine, you must have hello following:</span></span>

* <span data-ttu-id="fcf58-118">Un **abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-118">An **Azure subscription**.</span></span> <span data-ttu-id="fcf58-119">Si vous n’en avez pas déjà un, voir [Créez votre compte Azure gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="fcf58-119">If you do not already have one, see [Create your free Azure account today](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="fcf58-120">Une [**machine virtuelle de science des données Linux**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="fcf58-120">A [**Linux data science VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span></span> <span data-ttu-id="fcf58-121">Pour plus d’informations sur la configuration de cet ordinateur virtuel, consultez [hello de configurer une Machine virtuelle pour la science des données Linux](machine-learning-data-science-linux-dsvm-intro.md).</span><span class="sxs-lookup"><span data-stu-id="fcf58-121">For information on provisioning this VM, see [Provision hello Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).</span></span>
* <span data-ttu-id="fcf58-122">[X2Go](http://wiki.x2go.org/doku.php) installé sur votre ordinateur et une session XFCE ouverte.</span><span class="sxs-lookup"><span data-stu-id="fcf58-122">[X2Go](http://wiki.x2go.org/doku.php) installed on your computer and opened an XFCE session.</span></span> <span data-ttu-id="fcf58-123">Pour plus d’informations sur l’installation et la configuration d’un **client X2Go**, consultez [Installation et configuration du client X2Go](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span><span class="sxs-lookup"><span data-stu-id="fcf58-123">For information on installing and configuring an **X2Go client**, see [Installing and configuring X2Go client](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span></span> 
* <span data-ttu-id="fcf58-124">Un **compte AzureML**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-124">An **AzureML account**.</span></span> <span data-ttu-id="fcf58-125">Si vous n’avez pas encore, inscrivez-vous pour un nouveau à hello [page d’accueil AzureML](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="fcf58-125">If you don't already have one, sign up for new one at hello [AzureML homepage](https://studio.azureml.net/).</span></span> <span data-ttu-id="fcf58-126">Il existe un toohelp de niveau d’utilisation libre commencer.</span><span class="sxs-lookup"><span data-stu-id="fcf58-126">There is a free usage tier toohelp you get started.</span></span>

## <a name="download-hello-spambase-dataset"></a><span data-ttu-id="fcf58-127">Télécharger le jeu de données hello spambase</span><span class="sxs-lookup"><span data-stu-id="fcf58-127">Download hello spambase dataset</span></span>
<span data-ttu-id="fcf58-128">Hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) jeu de données est un ensemble relativement réduit de données qui contient des 4601 uniquement exemples.</span><span class="sxs-lookup"><span data-stu-id="fcf58-128">hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset is a relatively small set of data that contains only 4601 examples.</span></span> <span data-ttu-id="fcf58-129">Il s’agit d’un toouse taille pratique lors de la démonstration que certaines des fonctionnalités clés de hello Hello VM de science des données tel qu’il conserve les besoins en ressources hello modeste.</span><span class="sxs-lookup"><span data-stu-id="fcf58-129">This is a convenient size toouse when demonstrating that some of hello key features of hello Data Science VM as it keeps hello resource requirements modest.</span></span>

> [!NOTE]
> <span data-ttu-id="fcf58-130">Cette procédure pas à pas a été créée sur une machine virtuelle de science des données Linux de taille D2 v2.</span><span class="sxs-lookup"><span data-stu-id="fcf58-130">This walkthrough was created on a D2 v2-sized Linux Data Science Virtual Machine.</span></span> <span data-ttu-id="fcf58-131">Cette taille DSVM est capable de gérer des procédures hello dans cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="fcf58-131">This size DSVM is capable of handling hello procedures in this walkthrough.</span></span>
>
>

<span data-ttu-id="fcf58-132">Si vous avez besoin de davantage d’espace de stockage, vous pouvez créer des disques supplémentaires et les attacher tooyour machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fcf58-132">If you need more storage space, you can create additional disks and attach them tooyour VM.</span></span> <span data-ttu-id="fcf58-133">Ces disques utilisent le stockage Azure persistant, afin de leurs données sont conservées même lorsque le serveur de hello est remise en service dues tooresizing ou est arrêté.</span><span class="sxs-lookup"><span data-stu-id="fcf58-133">These disks use persistent Azure storage, so their data is preserved even when hello server is reprovisioned due tooresizing or is shut down.</span></span> <span data-ttu-id="fcf58-134">tooadd un disque et attacher tooyour VM, suivez les instructions de hello dans [ajouter un tooa de disque Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fcf58-134">tooadd a disk and attach it tooyour VM, follow hello instructions in [Add a disk tooa Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="fcf58-135">Ces étapes utilisent hello Azure Interface de ligne (Azure), qui est déjà installé sur hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="fcf58-135">These steps use hello Azure Command-Line Interface (Azure CLI), which is already installed on hello DSVM.</span></span> <span data-ttu-id="fcf58-136">Par conséquent, ces procédures possible entièrement à partir hello machine virtuelle proprement dite.</span><span class="sxs-lookup"><span data-stu-id="fcf58-136">So these procedures can be done entirely from hello VM itself.</span></span> <span data-ttu-id="fcf58-137">Une autre option de stockage tooincrease est toouse [fichiers Azure](../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="fcf58-137">Another option tooincrease storage is toouse [Azure files](../storage/files/storage-how-to-use-files-linux.md).</span></span>

<span data-ttu-id="fcf58-138">les données de salutation toodownload, ouvrez une fenêtre de terminal et exécuter cette commande :</span><span class="sxs-lookup"><span data-stu-id="fcf58-138">toodownload hello data, open a terminal window and run this command:</span></span>

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

<span data-ttu-id="fcf58-139">fichier téléchargé de Hello ne pas avoir une ligne d’en-tête, nous allons donc créer un autre fichier qui n’a pas un en-tête.</span><span class="sxs-lookup"><span data-stu-id="fcf58-139">hello downloaded file does not have a header row, so let's create another file that does have a header.</span></span> <span data-ttu-id="fcf58-140">Exécuter cette commande toocreate un fichier avec les en-têtes appropriés hello :</span><span class="sxs-lookup"><span data-stu-id="fcf58-140">Run this command toocreate a file with hello appropriate headers:</span></span>

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

<span data-ttu-id="fcf58-141">Puis concaténer les deux fichiers de hello avec la commande hello :</span><span class="sxs-lookup"><span data-stu-id="fcf58-141">Then concatenate hello two files together with hello command:</span></span>

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

<span data-ttu-id="fcf58-142">Hello dataset possède plusieurs types de statistiques sur chaque e-mail :</span><span class="sxs-lookup"><span data-stu-id="fcf58-142">hello dataset has several types of statistics on each email:</span></span>

* <span data-ttu-id="fcf58-143">Comme les colonnes ***word\_fréquence\_WORD*** indiquent le pourcentage hello de mots par courrier électronique hello qui correspondent aux *WORD*.</span><span class="sxs-lookup"><span data-stu-id="fcf58-143">Columns like ***word\_freq\_WORD*** indicate hello percentage of words in hello email that match *WORD*.</span></span> <span data-ttu-id="fcf58-144">Par exemple, si *word\_fréquence\_rendre* est 1, 1 % de tous les mots par courrier électronique hello ont été *rendre*.</span><span class="sxs-lookup"><span data-stu-id="fcf58-144">For example, if *word\_freq\_make* is 1, then 1% of all words in hello email were *make*.</span></span>
* <span data-ttu-id="fcf58-145">Comme les colonnes ***char\_fréquence\_CHAR*** indiquent le pourcentage hello de tous les caractères qui ont été par courrier électronique hello *CHAR*.</span><span class="sxs-lookup"><span data-stu-id="fcf58-145">Columns like ***char\_freq\_CHAR*** indicate hello percentage of all characters in hello email that were *CHAR*.</span></span>
* <span data-ttu-id="fcf58-146">***majuscule\_exécuter\_longueur\_plus longue*** est la longueur la plus importante d’une séquence de lettres majuscules hello.</span><span class="sxs-lookup"><span data-stu-id="fcf58-146">***capital\_run\_length\_longest*** is hello longest length of a sequence of capital letters.</span></span>
* <span data-ttu-id="fcf58-147">***majuscule\_exécuter\_longueur\_moyenne*** est hello la durée moyenne de toutes les séquences de lettres en majuscules.</span><span class="sxs-lookup"><span data-stu-id="fcf58-147">***capital\_run\_length\_average*** is hello average length of all sequences of capital letters.</span></span>
* <span data-ttu-id="fcf58-148">***majuscule\_exécuter\_longueur\_total*** est hello la longueur totale de toutes les séquences de lettres en majuscules.</span><span class="sxs-lookup"><span data-stu-id="fcf58-148">***capital\_run\_length\_total*** is hello total length of all sequences of capital letters.</span></span>
* <span data-ttu-id="fcf58-149">***anti-spam*** indique si les e-mails hello a été considéré comme du courrier indésirable ou non (1 = le courrier indésirable, 0 ne = pas de courrier indésirable).</span><span class="sxs-lookup"><span data-stu-id="fcf58-149">***spam*** indicates whether hello email was considered spam or not (1 = spam, 0 = not spam).</span></span>

## <a name="explore-hello-dataset-with-microsoft-r-open"></a><span data-ttu-id="fcf58-150">Explorer hello le jeu de données avec Microsoft R Open</span><span class="sxs-lookup"><span data-stu-id="fcf58-150">Explore hello dataset with Microsoft R Open</span></span>
<span data-ttu-id="fcf58-151">Nous allons examiner les données de hello et effectuer un apprentissage base avec r. hello VM de science des données est fourni avec [Microsoft R Open](https://mran.revolutionanalytics.com/open/) préinstallé.</span><span class="sxs-lookup"><span data-stu-id="fcf58-151">Let's examine hello data and do some basic machine learning with R. hello Data Science VM comes with [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installed.</span></span> <span data-ttu-id="fcf58-152">Hello des bibliothèques de mathématiques multithread dans cette version de R offrent de meilleures performances que les différentes versions monothread.</span><span class="sxs-lookup"><span data-stu-id="fcf58-152">hello multithreaded math libraries in this version of R offer better performance than various single-threaded versions.</span></span> <span data-ttu-id="fcf58-153">Microsoft R Open fournit également reproductibilité à l’aide d’un instantané d’un référentiel de packages CRAN hello.</span><span class="sxs-lookup"><span data-stu-id="fcf58-153">Microsoft R Open also provides reproducibility by using a snapshot of hello CRAN package repository.</span></span>

<span data-ttu-id="fcf58-154">exemples utilisés dans cette procédure pas à pas, hello du clone de code de copies tooget Hello **Azure-Machine-Learning--science des données** référentiel à l’aide de git, qui est préinstallé sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fcf58-154">tooget copies of hello code samples used in this walkthrough, clone hello **Azure-Machine-Learning-Data-Science** repository using git, which is pre-installed on hello VM.</span></span> <span data-ttu-id="fcf58-155">À partir de la ligne de commande git hello, exécutez :</span><span class="sxs-lookup"><span data-stu-id="fcf58-155">From hello git command line, run:</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="fcf58-156">Ouvrez une fenêtre de terminal et démarrez une nouvelle session de R à la console interactive hello R.</span><span class="sxs-lookup"><span data-stu-id="fcf58-156">Open a terminal window and start a new R session with hello R interactive console.</span></span>

> [!NOTE]
> <span data-ttu-id="fcf58-157">Vous pouvez également utiliser RStudio pour hello procédures suivantes.</span><span class="sxs-lookup"><span data-stu-id="fcf58-157">You can also use RStudio for hello following procedures.</span></span> <span data-ttu-id="fcf58-158">tooinstall RStudio, exécutez cette commande dans un terminal :`./Desktop/DSVM\ tools/installRStudio.sh`</span><span class="sxs-lookup"><span data-stu-id="fcf58-158">tooinstall RStudio, execute this command at a terminal: `./Desktop/DSVM\ tools/installRStudio.sh`</span></span>
>
>

<span data-ttu-id="fcf58-159">les données de salutation tooimport et configurer l’environnement de hello, exécutez :</span><span class="sxs-lookup"><span data-stu-id="fcf58-159">tooimport hello data and set up hello environment, run:</span></span>

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

<span data-ttu-id="fcf58-160">toosee résumé des statistiques sur chaque colonne :</span><span class="sxs-lookup"><span data-stu-id="fcf58-160">toosee summary statistics about each column:</span></span>

    summary(data)

<span data-ttu-id="fcf58-161">Pour obtenir une vue différente des données de salutation :</span><span class="sxs-lookup"><span data-stu-id="fcf58-161">For a different view of hello data:</span></span>

    str(data)

<span data-ttu-id="fcf58-162">Elle indique hello du type de chaque variable et de hello tout d’abord peu de valeurs dans le jeu de données hello.</span><span class="sxs-lookup"><span data-stu-id="fcf58-162">This shows you hello type of each variable and hello first few values in hello dataset.</span></span>

<span data-ttu-id="fcf58-163">Hello *anti-spam* colonne a été lu en tant qu’entier, mais il est réellement catégorielles variable (ou facteur).</span><span class="sxs-lookup"><span data-stu-id="fcf58-163">hello *spam* column was read as an integer, but it's actually a categorical variable (or factor).</span></span> <span data-ttu-id="fcf58-164">tooset son type :</span><span class="sxs-lookup"><span data-stu-id="fcf58-164">tooset its type:</span></span>

    data$spam <- as.factor(data$spam)

<span data-ttu-id="fcf58-165">toodo certains analyse exploratoire, l’utilisation hello [ggplot2](http://ggplot2.org/) du package, une bibliothèque de graphique courants pour R est déjà installé sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fcf58-165">toodo some exploratory analysis, use hello [ggplot2](http://ggplot2.org/) package, a popular graphing library for R that is already installed on hello VM.</span></span> <span data-ttu-id="fcf58-166">Notez, à partir des données de synthèse hello affichées précédemment, que nous avons résumé des statistiques sur la fréquence hello du caractère de point d’exclamation hello.</span><span class="sxs-lookup"><span data-stu-id="fcf58-166">Note, from hello summary data displayed earlier, that we have summary statistics on hello frequency of hello exclamation mark character.</span></span> <span data-ttu-id="fcf58-167">Nous allons tracer les fréquences ici avec hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="fcf58-167">Let's plot those frequencies here with hello following commands:</span></span>

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="fcf58-168">Étant donné que la barre de hello zéro est inclinaison de traçage hello, nous allons la supprimer :</span><span class="sxs-lookup"><span data-stu-id="fcf58-168">Since hello zero bar is skewing hello plot, let's get rid of it:</span></span>

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="fcf58-169">Il existe une densité non triviale au-dessus de 1 qui semble intéressante.</span><span class="sxs-lookup"><span data-stu-id="fcf58-169">There is a non-trivial density above 1 that looks interesting.</span></span> <span data-ttu-id="fcf58-170">Examinons simplement ces données :</span><span class="sxs-lookup"><span data-stu-id="fcf58-170">Let's look at just that data:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="fcf58-171">Ensuite, répartissez-les en courrier indésirable et courrier légitime :</span><span class="sxs-lookup"><span data-stu-id="fcf58-171">Then split it by spam vs ham:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

<span data-ttu-id="fcf58-172">Ces exemples doivent vous permettre de toomake des graphiques similaires de hello autres tooexplore colonnes hello les données qu’ils contiennent.</span><span class="sxs-lookup"><span data-stu-id="fcf58-172">These examples should enable you toomake similar plots of hello other columns tooexplore hello data contained in them.</span></span>

## <a name="train-and-test-an-ml-model"></a><span data-ttu-id="fcf58-173">Effectuer l’apprentissage et tester un modèle ML</span><span class="sxs-lookup"><span data-stu-id="fcf58-173">Train and test an ML model</span></span>
<span data-ttu-id="fcf58-174">Maintenant nous allons train quelques de l’apprentissage des modèles des messages électroniques de hello tooclassify hello DataSet comme contenant soit span ou ham.</span><span class="sxs-lookup"><span data-stu-id="fcf58-174">Now let's train a couple of machine learning models tooclassify hello emails in hello dataset as containing either span or ham.</span></span> <span data-ttu-id="fcf58-175">Dans cette section, nous effectuons l’apprentissage d’un modèle d’arbre de décision et d’un modèle de forêts aléatoires, puis nous testons la précision de leurs prédictions.</span><span class="sxs-lookup"><span data-stu-id="fcf58-175">We train a decision tree model and a random forest model in this section and then test their accuracy of their predictions.</span></span>

> [!NOTE]
> <span data-ttu-id="fcf58-176">Hello rpart (partitionnement récursif et les arbres de régression) package utilisé Bonjour suivant de code est déjà installé sur hello VM de science des données.</span><span class="sxs-lookup"><span data-stu-id="fcf58-176">hello rpart (Recursive Partitioning and Regression Trees) package used in hello following code is already installed on hello Data Science VM.</span></span>
>
>

<span data-ttu-id="fcf58-177">Tout d’abord, nous allons fractionner hello le jeu de données en jeux d’apprentissage et de test :</span><span class="sxs-lookup"><span data-stu-id="fcf58-177">First, let's split hello dataset into training and test sets:</span></span>

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

<span data-ttu-id="fcf58-178">Puis créez un Bonjour de tooclassify décision arborescence des messages électroniques.</span><span class="sxs-lookup"><span data-stu-id="fcf58-178">And then create a decision tree tooclassify hello emails.</span></span>

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

<span data-ttu-id="fcf58-179">Voici le résultat de hello :</span><span class="sxs-lookup"><span data-stu-id="fcf58-179">Here is hello result:</span></span>

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

<span data-ttu-id="fcf58-181">toodetermine si elle fonctionne bien pour la formation de hello définir, utilisez les hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="fcf58-181">toodetermine how well it performs on hello training set, use hello following code:</span></span>

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="fcf58-182">degré de toodetermine qu’il exécute sur le jeu de test hello :</span><span class="sxs-lookup"><span data-stu-id="fcf58-182">toodetermine how well it performs on hello test set:</span></span>

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="fcf58-183">Essayons également un modèle de forêts aléatoires.</span><span class="sxs-lookup"><span data-stu-id="fcf58-183">Let's also try a random forest model.</span></span> <span data-ttu-id="fcf58-184">Forêts aléatoires former une multitude d’arbres de décision et de sortie d’une classe qui est le mode de classifications hello de tous les arbres de décision individuelle hello hello.</span><span class="sxs-lookup"><span data-stu-id="fcf58-184">Random forests train a multitude of decision trees and output a class that is hello mode of hello classifications from all of hello individual decision trees.</span></span> <span data-ttu-id="fcf58-185">Ils fournissent une plus puissante d’apprentissage approche comme étant ils correcte pour la tendance d’un toooverfit de modèle de l’arborescence de la décision un jeu de données d’apprentissage hello.</span><span class="sxs-lookup"><span data-stu-id="fcf58-185">They provide a more powerful machine learning approach as they correct for hello tendency of a decision tree model toooverfit a training dataset.</span></span>

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-tooazure-ml"></a><span data-ttu-id="fcf58-186">Déployer un modèle de tooAzure ML</span><span class="sxs-lookup"><span data-stu-id="fcf58-186">Deploy a model tooAzure ML</span></span>
<span data-ttu-id="fcf58-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) est un service cloud qui la rend facile toobuild et déployer des modèles de prévision analytique.</span><span class="sxs-lookup"><span data-stu-id="fcf58-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is a cloud service that makes it easy toobuild and deploy predictive analytics models.</span></span> <span data-ttu-id="fcf58-188">Une des fonctionnalités intéressantes de hello de AzureML est son toopublish capacité tout R fonctionne comme un service web.</span><span class="sxs-lookup"><span data-stu-id="fcf58-188">One of hello nice features of AzureML is its ability toopublish any R function as a web service.</span></span> <span data-ttu-id="fcf58-189">Hello lot AzureML R rend toodo facile de déploiement à partir de notre session R sur hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="fcf58-189">hello AzureML R package makes deployment easy toodo right from our R session on hello DSVM.</span></span>

<span data-ttu-id="fcf58-190">toodeploy hello décision code de l’organigramme à partir de la section précédente de hello, vous devez toosign dans tooAzure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="fcf58-190">toodeploy hello decision tree code from hello previous section, you need toosign in tooAzure Machine Learning Studio.</span></span> <span data-ttu-id="fcf58-191">Vous avez besoin de votre ID d’espace de travail et une toosign de jeton d’autorisation dans.</span><span class="sxs-lookup"><span data-stu-id="fcf58-191">You need your workspace ID and an authorization token toosign in.</span></span> <span data-ttu-id="fcf58-192">toofind ces valeurs et des variables de AzureML hello initialize avec eux :</span><span class="sxs-lookup"><span data-stu-id="fcf58-192">toofind these values and initialize hello AzureML variables with them:</span></span>

<span data-ttu-id="fcf58-193">Sélectionnez **paramètres** sur le menu de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="fcf58-193">Select **Settings** on hello left-hand menu.</span></span> <span data-ttu-id="fcf58-194">Notez votre **ID D’ESPACE DE TRAVAIL**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-194">Note your **WORKSPACE ID**.</span></span> <span data-ttu-id="fcf58-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span><span class="sxs-lookup"><span data-stu-id="fcf58-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span></span>

<span data-ttu-id="fcf58-196">Sélectionnez **jetons d’autorisation** de menu de surcharge hello et notez votre **le jeton d’autorisation principal**.![ 3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span><span class="sxs-lookup"><span data-stu-id="fcf58-196">Select **Authorization Tokens** from hello overhead menu and note your **Primary Authorization Token**.![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span></span>

<span data-ttu-id="fcf58-197">Hello de charge **AzureML** du package et définissez les valeurs des variables hello avec votre ID de jeton et l’espace de travail dans votre session R sur hello DSVM :</span><span class="sxs-lookup"><span data-stu-id="fcf58-197">Load hello **AzureML** package and then set values of hello variables with your token and workspace ID in your R session on hello DSVM:</span></span>

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


<span data-ttu-id="fcf58-198">Nous allons simplifier hello modèle toomake cette tooimplement plus facile de démonstration.</span><span class="sxs-lookup"><span data-stu-id="fcf58-198">Let's simplify hello model toomake this demonstration easier tooimplement.</span></span> <span data-ttu-id="fcf58-199">Choisir des trois variables hello dans hello décision arborescence le plus proche toohello racine et générer une nouvelle arborescence à l’aide des ces trois variables :</span><span class="sxs-lookup"><span data-stu-id="fcf58-199">Pick hello three variables in hello decision tree closest toohello root and build a new tree using just those three variables:</span></span>

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

<span data-ttu-id="fcf58-200">Nous avons besoin d’une fonction de prédiction qui accepte les fonctions hello comme entrée et retourne hello valeurs prédites :</span><span class="sxs-lookup"><span data-stu-id="fcf58-200">We need a prediction function that takes hello features as an input and returns hello predicted values:</span></span>

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

<span data-ttu-id="fcf58-201">Publier hello predictSpam fonction tooAzureML à l’aide de hello **publishWebService** (fonction) :</span><span class="sxs-lookup"><span data-stu-id="fcf58-201">Publish hello predictSpam function tooAzureML using hello **publishWebService** function:</span></span>

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

<span data-ttu-id="fcf58-202">Cette fonction accepte hello **predictSpam** de fonction, crée un service web appelé **spamWebService** avec défini les entrées et sorties et retourne des informations sur le nouveau point de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="fcf58-202">This function takes hello **predictSpam** function, creates a web service named **spamWebService** with defined inputs and outputs, and returns information about hello new endpoint.</span></span>

<span data-ttu-id="fcf58-203">Afficher les détails de hello publié le service web, y compris ses clés de point de terminaison et l’accès aux API avec la commande hello :</span><span class="sxs-lookup"><span data-stu-id="fcf58-203">View details of hello published web service, including its API endpoint and access keys with hello command:</span></span>

    spamWebService[[2]]

<span data-ttu-id="fcf58-204">tootry son évolution horizontale sur hello 10 premières lignes du jeu de test hello :</span><span class="sxs-lookup"><span data-stu-id="fcf58-204">tootry it out on hello first 10 rows of hello test set:</span></span>

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a><span data-ttu-id="fcf58-205">Utiliser les autres outils disponibles</span><span class="sxs-lookup"><span data-stu-id="fcf58-205">Use other tools available</span></span>
<span data-ttu-id="fcf58-206">les sections restantes Hello montrent comment toouse certains des outils de hello installé sur hello VM de science des données Linux. Voici la liste hello des outils décrits :</span><span class="sxs-lookup"><span data-stu-id="fcf58-206">hello remaining sections show how toouse some of hello tools installed on hello Linux Data Science VM.Here is hello list of tools discussed:</span></span>

* <span data-ttu-id="fcf58-207">XGBoost</span><span class="sxs-lookup"><span data-stu-id="fcf58-207">XGBoost</span></span>
* <span data-ttu-id="fcf58-208">Python</span><span class="sxs-lookup"><span data-stu-id="fcf58-208">Python</span></span>
* <span data-ttu-id="fcf58-209">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="fcf58-209">Jupyterhub</span></span>
* <span data-ttu-id="fcf58-210">Rattle</span><span class="sxs-lookup"><span data-stu-id="fcf58-210">Rattle</span></span>
* <span data-ttu-id="fcf58-211">PostgreSQL et Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="fcf58-211">PostgreSQL & Squirrel SQL</span></span>
* <span data-ttu-id="fcf58-212">SQL Server Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="fcf58-212">SQL Server Data Warehouse</span></span>

## <a name="xgboost"></a><span data-ttu-id="fcf58-213">XGBoost</span><span class="sxs-lookup"><span data-stu-id="fcf58-213">XGBoost</span></span>
<span data-ttu-id="fcf58-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) est un outil qui offre une implémentation rapide et précise des arborescences optimisées.</span><span class="sxs-lookup"><span data-stu-id="fcf58-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) is a tool that provides a fast and accurate boosted tree implementation.</span></span>

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

<span data-ttu-id="fcf58-215">XGBoost peut également appeler à partir de Python ou d’une ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="fcf58-215">XGBoost can also call from python or a command line.</span></span>

## <a name="python"></a><span data-ttu-id="fcf58-216">Python</span><span class="sxs-lookup"><span data-stu-id="fcf58-216">Python</span></span>
<span data-ttu-id="fcf58-217">Pour le développement à l’aide de Python, les distributions hello Anaconda Python 2.7 et 3.5 ont été installées dans hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="fcf58-217">For development using Python, hello Anaconda Python distributions 2.7 and 3.5 have been installed in hello DSVM.</span></span>

> [!NOTE]
> <span data-ttu-id="fcf58-218">Hello distribution Anaconda inclut [Condas](http://conda.pydata.org/docs/index.html), qui peut être utilisé toocreate environnements personnalisés pour Python qui ont des versions différentes et/ou des packages installés dans les.</span><span class="sxs-lookup"><span data-stu-id="fcf58-218">hello Anaconda distribution includes [Condas](http://conda.pydata.org/docs/index.html), which can be used toocreate custom environments for Python that have different versions and/or packages installed in them.</span></span>
>
>

<span data-ttu-id="fcf58-219">Nous allons lire dans certains du jeu de données spambase hello et classer des messages électroniques hello avec des machines à vecteurs de support dans scikit-en savoir plus :</span><span class="sxs-lookup"><span data-stu-id="fcf58-219">Let's read in some of hello spambase dataset and classify hello emails with support vector machines in scikit-learn:</span></span>

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="fcf58-220">toomake prédictions :</span><span class="sxs-lookup"><span data-stu-id="fcf58-220">toomake predictions:</span></span>

    clf.predict(X.ix[0:20, :])

<span data-ttu-id="fcf58-221">tooshow comment toopublish AzureML d’un point de terminaison, nous allons créer un modèle plus simple hello trois variables comme nous l’avons fait lorsque nous avons publié le modèle de hello R précédemment.</span><span class="sxs-lookup"><span data-stu-id="fcf58-221">tooshow how toopublish an AzureML endpoint, let's make a simpler model hello three variables as we did when we published hello R model previously.</span></span>

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="fcf58-222">toopublish hello modèle tooAzureML :</span><span class="sxs-lookup"><span data-stu-id="fcf58-222">toopublish hello model tooAzureML:</span></span>

    # Publish hello model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about hello resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call hello model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> <span data-ttu-id="fcf58-223">Cette option est uniquement disponible pour Python 2.7 et n’est pas encore prise en charge sur 3.5.</span><span class="sxs-lookup"><span data-stu-id="fcf58-223">This is only available for python 2.7 and is not yet supported on 3.5.</span></span> <span data-ttu-id="fcf58-224">Exécutez avec **/anaconda/bin/python2.7**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-224">Run with **/anaconda/bin/python2.7**.</span></span>
>
>

## <a name="jupyterhub"></a><span data-ttu-id="fcf58-225">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="fcf58-225">Jupyterhub</span></span>
<span data-ttu-id="fcf58-226">distribution de Anaconda Hello Bonjour DSVM est fourni avec un bloc-notes jupyter, un environnement multiplateforme tooshare Python, R, Julia code ou et l’analyse.</span><span class="sxs-lookup"><span data-stu-id="fcf58-226">hello Anaconda distribution in hello DSVM comes with a Jupyter notebook, a cross-platform environment tooshare Python, R, or Julia code and analysis.</span></span> <span data-ttu-id="fcf58-227">Bloc-notes jupyter de Hello est accessible via JupyterHub.</span><span class="sxs-lookup"><span data-stu-id="fcf58-227">hello Jupyter notebook is accessed through JupyterHub.</span></span> <span data-ttu-id="fcf58-228">Vous vous connectez en utilisant votre nom d’utilisateur Linux local et votre mot de passe à ***https://\<nom DNS de machine virtuelle ou adresse IP\>:8000/***.</span><span class="sxs-lookup"><span data-stu-id="fcf58-228">You sign in using your local Linux user name and password at ***https://\<VM DNS name or IP Address\>:8000/***.</span></span> <span data-ttu-id="fcf58-229">Tous les fichiers de configuration pour JupyterHub se trouvent dans le répertoire **/etc/jupyterhub**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-229">All configuration files for JupyterHub are found in directory **/etc/jupyterhub**.</span></span>

<span data-ttu-id="fcf58-230">Plusieurs exemples d’agendas sont déjà installés sur hello machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="fcf58-230">Several sample notebooks are already installed on hello VM:</span></span>

* <span data-ttu-id="fcf58-231">Consultez hello [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) d’un ordinateur portable Python d’exemple.</span><span class="sxs-lookup"><span data-stu-id="fcf58-231">See hello [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) for a sample Python notebook.</span></span>
* <span data-ttu-id="fcf58-232">Consultez [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) pour un exemple de notebook **R** .</span><span class="sxs-lookup"><span data-stu-id="fcf58-232">See [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) for a sample **R** notebook.</span></span>
* <span data-ttu-id="fcf58-233">Consultez hello [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) pour un autre exemple **Python** bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="fcf58-233">See hello [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) for another sample **Python** notebook.</span></span>

> [!NOTE]
> <span data-ttu-id="fcf58-234">Hello language de Julia est également disponible à partir de la ligne de commande hello hello VM de science des données Linux.</span><span class="sxs-lookup"><span data-stu-id="fcf58-234">hello Julia language is also available from hello command line on hello Linux Data Science VM.</span></span>
>
>

## <a name="rattle"></a><span data-ttu-id="fcf58-235">Rattle</span><span class="sxs-lookup"><span data-stu-id="fcf58-235">Rattle</span></span>
<span data-ttu-id="fcf58-236">[Vibrer](https://cran.r-project.org/web/packages/rattle/index.html) (hello facilement l’outil d’analyse R tooLearn) est un outil graphique de R pour l’exploration de données.</span><span class="sxs-lookup"><span data-stu-id="fcf58-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (hello R Analytical Tool tooLearn Easily) is a graphical R tool for data mining.</span></span> <span data-ttu-id="fcf58-237">Elle a une interface intuitive qui le rend facile tooload, Explorer et transformer des données et générer et évaluer des modèles.</span><span class="sxs-lookup"><span data-stu-id="fcf58-237">It has an intuitive interface that makes it easy tooload, explore, and transform data and build and evaluate models.</span></span>  <span data-ttu-id="fcf58-238">article de Hello [vibrer : GUI d’exploration de données A pour R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) fournit une procédure pas à pas qui montre comment ses fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="fcf58-238">hello article [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) provides a walkthrough that demonstrates its features.</span></span>

<span data-ttu-id="fcf58-239">Installer et démarrer vibrer avec hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="fcf58-239">Install and start Rattle with hello following commands:</span></span>

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> <span data-ttu-id="fcf58-240">L’installation n’est pas obligatoire sur hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="fcf58-240">Installation is not required on hello DSVM.</span></span> <span data-ttu-id="fcf58-241">Mais Hochet peut vous demander de packages supplémentaires de tooinstall lors du chargement.</span><span class="sxs-lookup"><span data-stu-id="fcf58-241">But Rattle may prompt you tooinstall additional packages when it loads.</span></span>
>
>

<span data-ttu-id="fcf58-242">Rattle utilise une interface basée sur des onglets.</span><span class="sxs-lookup"><span data-stu-id="fcf58-242">Rattle uses a tab-based interface.</span></span> <span data-ttu-id="fcf58-243">La plupart des onglets de hello correspondent toosteps Bonjour [processus de science des données](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), telles que le chargement de données ou l’exploration.</span><span class="sxs-lookup"><span data-stu-id="fcf58-243">Most of hello tabs correspond toosteps in hello [Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), like loading data or exploring it.</span></span> <span data-ttu-id="fcf58-244">processus de science des données Hello circulent à partir de la gauche tooright via les onglets hello.</span><span class="sxs-lookup"><span data-stu-id="fcf58-244">hello data science process flows from left tooright through hello tabs.</span></span> <span data-ttu-id="fcf58-245">Mais le dernier onglet de hello contient un journal des commandes hello R exécuté par Hochet.</span><span class="sxs-lookup"><span data-stu-id="fcf58-245">But hello last tab contains a log of hello R commands run by Rattle.</span></span>

<span data-ttu-id="fcf58-246">tooload et configurer le jeu de données hello :</span><span class="sxs-lookup"><span data-stu-id="fcf58-246">tooload and configure hello dataset:</span></span>

* <span data-ttu-id="fcf58-247">fichier de hello tooload, sélectionnez hello **données** sous l’onglet puis</span><span class="sxs-lookup"><span data-stu-id="fcf58-247">tooload hello file, select hello **Data** tab, then</span></span>
* <span data-ttu-id="fcf58-248">Cliquez sur le sélecteur de hello suivant trop**nom de fichier** et choisissez **spambaseHeaders.data**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-248">Choose hello selector next too**Filename** and choose **spambaseHeaders.data**.</span></span>
* <span data-ttu-id="fcf58-249">fichier de hello tooload.</span><span class="sxs-lookup"><span data-stu-id="fcf58-249">tooload hello file.</span></span> <span data-ttu-id="fcf58-250">Sélectionnez **Execute** dans la ligne du haut hello de boutons.</span><span class="sxs-lookup"><span data-stu-id="fcf58-250">select **Execute** in hello top row of buttons.</span></span> <span data-ttu-id="fcf58-251">Vous devez voir un résumé de chaque colonne, y compris son type de données identifié, s’il s’agit d’une entrée, une cible ou autre type de variable et le nombre de hello de valeurs uniques.</span><span class="sxs-lookup"><span data-stu-id="fcf58-251">You should see a summary of each column, including its identified data type, whether it's an input, a target, or other type of variable, and hello number of unique values.</span></span>
* <span data-ttu-id="fcf58-252">Hochet a correctement identifié hello **anti-spam** colonne en tant que cible de hello.</span><span class="sxs-lookup"><span data-stu-id="fcf58-252">Rattle has correctly identified hello **spam** column as hello target.</span></span> <span data-ttu-id="fcf58-253">Colonne de spam hello sélectionnez, puis ensemble hello **Type de données cible** trop**Categoric**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-253">Select hello spam column, then set hello **Target Data Type** too**Categoric**.</span></span>

<span data-ttu-id="fcf58-254">données de salutation tooexplore :</span><span class="sxs-lookup"><span data-stu-id="fcf58-254">tooexplore hello data:</span></span>

* <span data-ttu-id="fcf58-255">Sélectionnez hello **Explorer** onglet.</span><span class="sxs-lookup"><span data-stu-id="fcf58-255">Select hello **Explore** tab.</span></span>
* <span data-ttu-id="fcf58-256">Cliquez sur **Résumé**, puis **Execute**, toosee certaines informations sur les types de variables hello et des statistiques de résumé.</span><span class="sxs-lookup"><span data-stu-id="fcf58-256">Click **Summary**, then **Execute**, toosee some information about hello variable types and some summary statistics.</span></span>
* <span data-ttu-id="fcf58-257">tooview autres types de statistiques à propos de chaque variable, sélectionnez d’autres options, comme **Describe** ou **notions de base**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-257">tooview other types of statistics about each variable, select other options like **Describe** or **Basics**.</span></span>

<span data-ttu-id="fcf58-258">Hello **Explorer** onglet vous permet également de toogenerate nombreux instructif trace.</span><span class="sxs-lookup"><span data-stu-id="fcf58-258">hello **Explore** tab also allows you toogenerate many insightful plots.</span></span> <span data-ttu-id="fcf58-259">tooplot un histogramme de données de salutation :</span><span class="sxs-lookup"><span data-stu-id="fcf58-259">tooplot a histogram of hello data:</span></span>

* <span data-ttu-id="fcf58-260">Sélectionnez **Distributions**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-260">Select **Distributions**.</span></span>
* <span data-ttu-id="fcf58-261">Cochez **Histogramme** pour **word_freq_remove** et **word_freq_you**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-261">Check **Histogram** for **word_freq_remove** and **word_freq_you**.</span></span>
* <span data-ttu-id="fcf58-262">Sélectionnez **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-262">Select **Execute**.</span></span> <span data-ttu-id="fcf58-263">Vous devez voir que deux densité de la trace dans une fenêtre de graphique unique, où il est clair que word hello « vous » s’affiche plus fréquemment dans les messages électroniques que « supprimer ».</span><span class="sxs-lookup"><span data-stu-id="fcf58-263">You should see both density plots in a single graph window, where it is clear that hello word "you" appears much more frequently in emails than "remove".</span></span>

<span data-ttu-id="fcf58-264">graphiques de corrélation Hello peuvent également vous intéresser.</span><span class="sxs-lookup"><span data-stu-id="fcf58-264">hello Correlation plots are also interesting.</span></span> <span data-ttu-id="fcf58-265">toocreate une :</span><span class="sxs-lookup"><span data-stu-id="fcf58-265">toocreate one:</span></span>

* <span data-ttu-id="fcf58-266">Choisissez **corrélation** comme hello **Type**, puis</span><span class="sxs-lookup"><span data-stu-id="fcf58-266">Choose **Correlation** as hello **Type**, then</span></span>
* <span data-ttu-id="fcf58-267">Sélectionnez **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-267">Select **Execute**.</span></span>
* <span data-ttu-id="fcf58-268">Rattle vous avertit qu’il recommande un maximum de 40 variables.</span><span class="sxs-lookup"><span data-stu-id="fcf58-268">Rattle warns you that it recommends a maximum of 40 variables.</span></span> <span data-ttu-id="fcf58-269">Sélectionnez **Oui** traçage de hello tooview.</span><span class="sxs-lookup"><span data-stu-id="fcf58-269">Select **Yes** tooview hello plot.</span></span>

<span data-ttu-id="fcf58-270">Il existe des corrélations intéressantes qui apparaissent : « technologie » est en corrélation trop « HP » et « labs », par exemple.</span><span class="sxs-lookup"><span data-stu-id="fcf58-270">There are some interesting correlations that come up: "technology" is strongly correlated too"HP" and "labs", for example.</span></span> <span data-ttu-id="fcf58-271">Il est également étroitement lié trop « 650 », code de région de hello de donneurs de dataset hello étant 650.</span><span class="sxs-lookup"><span data-stu-id="fcf58-271">It is also strongly correlated too"650", because hello area code of hello dataset donors is 650.</span></span>

<span data-ttu-id="fcf58-272">valeurs numériques de Hello pour les corrélations hello entre les mots sont disponibles dans la fenêtre d’Explorer hello.</span><span class="sxs-lookup"><span data-stu-id="fcf58-272">hello numeric values for hello correlations between words are available in hello Explore window.</span></span> <span data-ttu-id="fcf58-273">Il est intéressant toonote, par exemple, que « technologie » est négative corrélée avec « votre » et « money ».</span><span class="sxs-lookup"><span data-stu-id="fcf58-273">It is interesting toonote, for example, that "technology" is negatively correlated with "your" and "money".</span></span>

<span data-ttu-id="fcf58-274">Hochet peut transformer hello dataset toohandle certains problèmes courants.</span><span class="sxs-lookup"><span data-stu-id="fcf58-274">Rattle can transform hello dataset toohandle some common issues.</span></span> <span data-ttu-id="fcf58-275">Par exemple, il vous permet de toorescale fonctionnalités imputer les valeurs manquantes, gérer les observations aberrantes et supprimer des variables ou des observations avec les données manquantes.</span><span class="sxs-lookup"><span data-stu-id="fcf58-275">For example, it allows you toorescale features, impute missing values, handle outliers, and remove variables or observations with missing data.</span></span> <span data-ttu-id="fcf58-276">Rattle peut également identifier des règles d’association entre des observations et/ou des variables.</span><span class="sxs-lookup"><span data-stu-id="fcf58-276">Rattle can also identify association rules between observations and/or variables.</span></span> <span data-ttu-id="fcf58-277">Ces onglets sont hors de portée pour cette introduction pas à pas.</span><span class="sxs-lookup"><span data-stu-id="fcf58-277">These tabs are out of scope for this introductory walkthrough.</span></span>

<span data-ttu-id="fcf58-278">Rattle peut également effectuer une analyse de cluster.</span><span class="sxs-lookup"><span data-stu-id="fcf58-278">Rattle can also perform cluster analysis.</span></span> <span data-ttu-id="fcf58-279">Nous allons exclure certains tooread fonctionnalités toomake hello sortie plus facile.</span><span class="sxs-lookup"><span data-stu-id="fcf58-279">Let's exclude some features toomake hello output easier tooread.</span></span> <span data-ttu-id="fcf58-280">Sur hello **données** , onglet choisir **ignorer** tooeach suivant des variables hello, à l’exception de ces dix éléments :</span><span class="sxs-lookup"><span data-stu-id="fcf58-280">On hello **Data** tab, choose **Ignore** next tooeach of hello variables except these ten items:</span></span>

* <span data-ttu-id="fcf58-281">word_freq_hp</span><span class="sxs-lookup"><span data-stu-id="fcf58-281">word_freq_hp</span></span>
* <span data-ttu-id="fcf58-282">word_freq_technology</span><span class="sxs-lookup"><span data-stu-id="fcf58-282">word_freq_technology</span></span>
* <span data-ttu-id="fcf58-283">word_freq_george</span><span class="sxs-lookup"><span data-stu-id="fcf58-283">word_freq_george</span></span>
* <span data-ttu-id="fcf58-284">word_freq_remove</span><span class="sxs-lookup"><span data-stu-id="fcf58-284">word_freq_remove</span></span>
* <span data-ttu-id="fcf58-285">word_freq_your</span><span class="sxs-lookup"><span data-stu-id="fcf58-285">word_freq_your</span></span>
* <span data-ttu-id="fcf58-286">word_freq_dollar</span><span class="sxs-lookup"><span data-stu-id="fcf58-286">word_freq_dollar</span></span>
* <span data-ttu-id="fcf58-287">word_freq_money</span><span class="sxs-lookup"><span data-stu-id="fcf58-287">word_freq_money</span></span>
* <span data-ttu-id="fcf58-288">capital_run_length_longest</span><span class="sxs-lookup"><span data-stu-id="fcf58-288">capital_run_length_longest</span></span>
* <span data-ttu-id="fcf58-289">word_freq_business</span><span class="sxs-lookup"><span data-stu-id="fcf58-289">word_freq_business</span></span>
* <span data-ttu-id="fcf58-290">spam</span><span class="sxs-lookup"><span data-stu-id="fcf58-290">spam</span></span>

<span data-ttu-id="fcf58-291">Puis revenir en arrière toohello **Cluster** , onglet choisir **KMeans**et ensemble hello *nombre de clusters* too4.</span><span class="sxs-lookup"><span data-stu-id="fcf58-291">Then go back toohello **Cluster** tab, choose **KMeans**, and set hello *Number of clusters* too4.</span></span> <span data-ttu-id="fcf58-292">Ensuite, sélectionnez **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-292">Then **Execute**.</span></span> <span data-ttu-id="fcf58-293">résultats de Hello sont affichés dans la fenêtre de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="fcf58-293">hello results are displayed in hello output window.</span></span> <span data-ttu-id="fcf58-294">Un cluster possède une fréquence élevée de « george » et de « hp » et est probablement un e-mail professionnel légitime.</span><span class="sxs-lookup"><span data-stu-id="fcf58-294">One cluster has high frequency of "george" and "hp" and is probably a legitimate business email.</span></span>

<span data-ttu-id="fcf58-295">toobuild un modèle d’apprentissage arbre de décision simple :</span><span class="sxs-lookup"><span data-stu-id="fcf58-295">toobuild a simple decision tree machine learning model:</span></span>

* <span data-ttu-id="fcf58-296">Sélectionnez hello **modèle** onglet,</span><span class="sxs-lookup"><span data-stu-id="fcf58-296">Select hello **Model** tab,</span></span>
* <span data-ttu-id="fcf58-297">Choisissez **arborescence** comme hello **Type**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-297">Choose **Tree** as hello **Type**.</span></span>
* <span data-ttu-id="fcf58-298">Sélectionnez **Execute** arborescence de hello toodisplay sous forme de texte Bonjour fenêtre de sortie.</span><span class="sxs-lookup"><span data-stu-id="fcf58-298">Select **Execute** toodisplay hello tree in text form in hello output window.</span></span>
* <span data-ttu-id="fcf58-299">Sélectionnez hello **dessiner** bouton tooview une version graphique.</span><span class="sxs-lookup"><span data-stu-id="fcf58-299">Select hello **Draw** button tooview a graphical version.</span></span> <span data-ttu-id="fcf58-300">Cela ressemble assez similaire toohello arborescence, nous avons obtenu précédemment à l’aide de *rpart*.</span><span class="sxs-lookup"><span data-stu-id="fcf58-300">This looks quite similar toohello tree we obtained earlier using *rpart*.</span></span>

<span data-ttu-id="fcf58-301">Une des fonctionnalités intéressantes de hello de Hochet est sa capacité toorun apprentissage plusieurs méthodes et les évaluer rapidement.</span><span class="sxs-lookup"><span data-stu-id="fcf58-301">One of hello nice features of Rattle is its ability toorun several machine learning methods and quickly evaluate them.</span></span> <span data-ttu-id="fcf58-302">Voici la procédure de hello :</span><span class="sxs-lookup"><span data-stu-id="fcf58-302">Here is hello procedure:</span></span>

* <span data-ttu-id="fcf58-303">Choisissez **tous les** pour hello **Type**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-303">Choose **All** for hello **Type**.</span></span>
* <span data-ttu-id="fcf58-304">Sélectionnez **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-304">Select **Execute**.</span></span>
* <span data-ttu-id="fcf58-305">Une fois celle-ci terminée, vous pouvez cliquer sur une même **Type**, comme **SVM**et afficher les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="fcf58-305">After it finishes you can click any single **Type**, like **SVM**, and view hello results.</span></span>
* <span data-ttu-id="fcf58-306">Vous pouvez également comparer les performances de hello des modèles de hello sur validation hello définies à l’aide de hello **évaluer** onglet. Par exemple, hello **erreur matrice** sélection vous montre matrice de confusion hello, erreur global et d’erreur de classe moyenne pour chaque modèle sur l’ensemble de validation hello.</span><span class="sxs-lookup"><span data-stu-id="fcf58-306">You can also compare hello performance of hello models on hello validation set using hello **Evaluate** tab. For example, hello **Error Matrix** selection shows you hello confusion matrix, overall error, and averaged class error for each model on hello validation set.</span></span>
* <span data-ttu-id="fcf58-307">Vous pouvez également tracer des courbes ROC, effectuer des analyses de sensibilité et d’autres types d’évaluations de modèle.</span><span class="sxs-lookup"><span data-stu-id="fcf58-307">You can also plot ROC curves, perform sensitivity analysis, and do other types of model evaluations.</span></span>

<span data-ttu-id="fcf58-308">Une fois que vous avez terminé la création de modèles, sélectionnez hello **journal** onglet code de hello R tooview exécuté par Hochet pendant votre session.</span><span class="sxs-lookup"><span data-stu-id="fcf58-308">Once you're finished building models, select hello **Log** tab tooview hello R code run by Rattle during your session.</span></span> <span data-ttu-id="fcf58-309">Vous pouvez sélectionner hello **exporter** bouton toosave il.</span><span class="sxs-lookup"><span data-stu-id="fcf58-309">You can select hello **Export** button toosave it.</span></span>

> [!NOTE]
> <span data-ttu-id="fcf58-310">Il existe un bogue dans la version actuelle de Rattle.</span><span class="sxs-lookup"><span data-stu-id="fcf58-310">There is a bug in current release of Rattle.</span></span> <span data-ttu-id="fcf58-311">toomodify hello script ou utilisez-le toorepeat vos étapes plus tard, vous devez insérer un caractère # devant * exporter ce journal... * dans le texte hello du journal de hello.</span><span class="sxs-lookup"><span data-stu-id="fcf58-311">toomodify hello script or use it toorepeat your steps later, you must insert a # character in front of *Export this log ... * in hello text of hello log.</span></span>
>
>

## <a name="postgresql--squirrel-sql"></a><span data-ttu-id="fcf58-312">PostgreSQL et Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="fcf58-312">PostgreSQL & Squirrel SQL</span></span>
<span data-ttu-id="fcf58-313">Hello DSVM est fourni avec PostgreSQL installé.</span><span class="sxs-lookup"><span data-stu-id="fcf58-313">hello DSVM comes with PostgreSQL installed.</span></span> <span data-ttu-id="fcf58-314">PostgreSQL est une base de données relationnelle, open source et sophistiquée.</span><span class="sxs-lookup"><span data-stu-id="fcf58-314">PostgreSQL is a sophisticated, open-source relational database.</span></span> <span data-ttu-id="fcf58-315">Cette section montre comment tooload notre jeu de données de spam dans PostgreSQL et puis de la requête.</span><span class="sxs-lookup"><span data-stu-id="fcf58-315">This section shows how tooload our spam dataset into PostgreSQL and then query it.</span></span>

<span data-ttu-id="fcf58-316">Avant de pouvoir charger les données de salutation, vous devez tooallow d’authentification de mot de passe à partir de localhost de hello.</span><span class="sxs-lookup"><span data-stu-id="fcf58-316">Before you can load hello data, you need tooallow password authentication from hello localhost.</span></span> <span data-ttu-id="fcf58-317">À l’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="fcf58-317">At a command prompt:</span></span>

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

<span data-ttu-id="fcf58-318">Bas hello hello du fichier de configuration sont plusieurs lignes de détaillent hello de connexions autorisée :</span><span class="sxs-lookup"><span data-stu-id="fcf58-318">Near hello bottom of hello config file are several lines that detail hello allowed connections:</span></span>

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

<span data-ttu-id="fcf58-319">Modifier hello « IPv4 des connexions locales » ligne toouse md5 au lieu d’ident, afin de nous pouvons connecter à l’aide d’un nom d’utilisateur et un mot de passe :</span><span class="sxs-lookup"><span data-stu-id="fcf58-319">Change hello "IPv4 local connections" line toouse md5 instead of ident, so we can log in using a username and password:</span></span>

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

<span data-ttu-id="fcf58-320">Et redémarrez le service postgres hello :</span><span class="sxs-lookup"><span data-stu-id="fcf58-320">And restart hello postgres service:</span></span>

    sudo systemctl restart postgresql

<span data-ttu-id="fcf58-321">toolaunch psql, un terminal interactive pour PostgreSQL, en tant qu’utilisateur de postgres intégrés hello, exécutez hello de commande suivante à partir d’une invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="fcf58-321">toolaunch psql, an interactive terminal for PostgreSQL, as hello built-in postgres user, run hello following command from a prompt:</span></span>

    sudo -u postgres psql

<span data-ttu-id="fcf58-322">Créer un nouveau compte d’utilisateur, à l’aide de hello le même nom d’utilisateur comme hello compte Linux que vous êtes actuellement connecté, attribuez-lui un mot de passe :</span><span class="sxs-lookup"><span data-stu-id="fcf58-322">Create a new user account, using hello same username as hello Linux account you're currently logged in as, and give it a password:</span></span>

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

<span data-ttu-id="fcf58-323">Connectez-vous ensuite toopsql en tant que votre utilisateur :</span><span class="sxs-lookup"><span data-stu-id="fcf58-323">Then log in toopsql as your user:</span></span>

    psql

<span data-ttu-id="fcf58-324">Et importer des données de hello dans une base de données :</span><span class="sxs-lookup"><span data-stu-id="fcf58-324">And import hello data into a new database:</span></span>

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

<span data-ttu-id="fcf58-325">Maintenant, nous allons explorer les données hello et exécuter des requêtes à l’aide de **non SQL**, un outil graphique qui vous permet d’interagir avec les bases de données via un pilote JDBC.</span><span class="sxs-lookup"><span data-stu-id="fcf58-325">Now, let's explore hello data and run some queries using **Squirrel SQL**, a graphical tool that lets you interact with databases via a JDBC driver.</span></span>

<span data-ttu-id="fcf58-326">tooget de démarrer, lancez non SQL à partir du menu d’Applications hello.</span><span class="sxs-lookup"><span data-stu-id="fcf58-326">tooget started, launch Squirrel SQL from hello Applications menu.</span></span> <span data-ttu-id="fcf58-327">tooset pilote de hello :</span><span class="sxs-lookup"><span data-stu-id="fcf58-327">tooset up hello driver:</span></span>

* <span data-ttu-id="fcf58-328">Sélectionnez **Windows**, puis **Afficher les pilotes**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-328">Select **Windows**, then **View Drivers**.</span></span>
* <span data-ttu-id="fcf58-329">Cliquez avec le bouton droit sur **PostgreSQL** et sélectionnez **Modifier le pilote**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-329">Right-click on **PostgreSQL** and select **Modify Driver**.</span></span>
* <span data-ttu-id="fcf58-330">Sélectionnez **Chemin d’accès de la classe supplémentaire**, puis **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-330">Select **Extra Class Path**, then **Add**.</span></span>
* <span data-ttu-id="fcf58-331">Entrez ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** pour hello **nom de fichier** et</span><span class="sxs-lookup"><span data-stu-id="fcf58-331">Enter ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** for hello **File Name** and</span></span>
* <span data-ttu-id="fcf58-332">Sélectionnez **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-332">Select **Open**.</span></span>
* <span data-ttu-id="fcf58-333">Choisissez Pilotes de la liste, puis sélectionnez **org.postgresql.Driver** dans **Nom de la classe**, et sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-333">Choose List Drivers, then select **org.postgresql.Driver** in **Class Name**, and select **OK**.</span></span>

<span data-ttu-id="fcf58-334">tooset des hello de connexion toohello local du serveur :</span><span class="sxs-lookup"><span data-stu-id="fcf58-334">tooset up hello connection toohello local server:</span></span>

* <span data-ttu-id="fcf58-335">Sélectionnez **Windows**, puis **Afficher les alias**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-335">Select **Windows**, then **View Aliases.**</span></span>
* <span data-ttu-id="fcf58-336">Choisissez hello  **+**  bouton toomake un nouvel alias.</span><span class="sxs-lookup"><span data-stu-id="fcf58-336">Choose hello **+** button toomake a new alias.</span></span>
* <span data-ttu-id="fcf58-337">Nommez-le *base de données de courrier indésirable*, choisissez **PostgreSQL** Bonjour **pilote** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="fcf58-337">Name it *Spam database*, choose **PostgreSQL** in hello **Driver** drop-down.</span></span>
* <span data-ttu-id="fcf58-338">Définir les URL de hello trop*jdbc:postgresql://localhost/spam*.</span><span class="sxs-lookup"><span data-stu-id="fcf58-338">Set hello URL too*jdbc:postgresql://localhost/spam*.</span></span>
* <span data-ttu-id="fcf58-339">Entrez votre *nom d’utilisateur* et votre *mot de passe*.</span><span class="sxs-lookup"><span data-stu-id="fcf58-339">Enter your *username* and *password*.</span></span>
* <span data-ttu-id="fcf58-340">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-340">Click **OK**.</span></span>
* <span data-ttu-id="fcf58-341">tooopen hello **connexion** fenêtre, double-cliquez sur hello ***base de données de courrier indésirable*** alias.</span><span class="sxs-lookup"><span data-stu-id="fcf58-341">tooopen hello **Connection** window, double-click hello ***Spam database*** alias.</span></span>
* <span data-ttu-id="fcf58-342">Sélectionnez **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="fcf58-342">Select **Connect**.</span></span>

<span data-ttu-id="fcf58-343">toorun certaines requêtes :</span><span class="sxs-lookup"><span data-stu-id="fcf58-343">toorun some queries:</span></span>

* <span data-ttu-id="fcf58-344">Sélectionnez hello **SQL** onglet.</span><span class="sxs-lookup"><span data-stu-id="fcf58-344">Select hello **SQL** tab.</span></span>
* <span data-ttu-id="fcf58-345">Entrez une requête simple tel `SELECT * from data;` dans zone de texte hello requête haut hello d’onglet de hello SQL.</span><span class="sxs-lookup"><span data-stu-id="fcf58-345">Enter a simple query such as `SELECT * from data;` in hello query textbox at hello top of hello SQL tab.</span></span>
* <span data-ttu-id="fcf58-346">Appuyez sur **Ctrl + entrée** toorun il.</span><span class="sxs-lookup"><span data-stu-id="fcf58-346">Press **Ctrl-Enter** toorun it.</span></span> <span data-ttu-id="fcf58-347">Par défaut non SQL renvoie hello 100 premières lignes de votre requête.</span><span class="sxs-lookup"><span data-stu-id="fcf58-347">By default Squirrel SQL returns hello first 100 rows from your query.</span></span>

<span data-ttu-id="fcf58-348">Il existe de nombreuses requêtes plus que tooexplore pourrait utiliser ces données.</span><span class="sxs-lookup"><span data-stu-id="fcf58-348">There are many more queries you could run tooexplore this data.</span></span> <span data-ttu-id="fcf58-349">Par exemple, comment le fait hello fréquence du mot de hello *rendre* diffèrent entre anti-spam et ham ?</span><span class="sxs-lookup"><span data-stu-id="fcf58-349">For example, how does hello frequency of hello word *make* differ between spam and ham?</span></span>

    SELECT avg(word_freq_make), spam from data group by spam;

<span data-ttu-id="fcf58-350">Ou quelles sont les caractéristiques de hello des messages électroniques qui contiennent souvent *3d*?</span><span class="sxs-lookup"><span data-stu-id="fcf58-350">Or what are hello characteristics of email that frequently contain *3d*?</span></span>

    SELECT * from data order by word_freq_3d desc;

<span data-ttu-id="fcf58-351">La plupart des e-mails qui ont une occurrence élevée de *3d* sont apparemment envoyer du courrier indésirable, il peut donc être une fonction très utile pour la création d’un Bonjour tooclassify de modèle de prévision des messages électroniques.</span><span class="sxs-lookup"><span data-stu-id="fcf58-351">Most emails that have a high occurrence of *3d* are apparently spam, so it could be a useful feature for building a predictive model tooclassify hello emails.</span></span>

<span data-ttu-id="fcf58-352">Si vous souhaitiez tooperform apprentissage des données stockées dans une base de données PostgreSQL, envisagez d’utiliser [MADlib](http://madlib.incubator.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="fcf58-352">If you wanted tooperform machine learning with data stored in a PostgreSQL database, consider using [MADlib](http://madlib.incubator.apache.org/).</span></span>

## <a name="sql-server-data-warehouse"></a><span data-ttu-id="fcf58-353">SQL Server Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="fcf58-353">SQL Server Data Warehouse</span></span>
<span data-ttu-id="fcf58-354">Azure SQL Data Warehouse est une base de données de mise à l’échelle basée sur le cloud qui prend en charge le traitement de grands volumes de données relationnelles et non relationnelles.</span><span class="sxs-lookup"><span data-stu-id="fcf58-354">Azure SQL Data Warehouse is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span> <span data-ttu-id="fcf58-355">Pour plus d’informations, consultez [En quoi consiste Azure SQL Data Warehouse ?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="fcf58-355">For more information, see [What is Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span></span>

<span data-ttu-id="fcf58-356">tooconnect toohello données de l’entrepôt et créer table hello suivant de hello exécution de commandes à partir d’une invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="fcf58-356">tooconnect toohello data warehouse and create hello table, run hello following command from a command prompt:</span></span>

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

<span data-ttu-id="fcf58-357">Puis, à l’invite sqlcmd hello :</span><span class="sxs-lookup"><span data-stu-id="fcf58-357">Then at hello sqlcmd prompt:</span></span>

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

<span data-ttu-id="fcf58-358">Copier des données avec bcp :</span><span class="sxs-lookup"><span data-stu-id="fcf58-358">Copy data with bcp:</span></span>

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> <span data-ttu-id="fcf58-359">les fins de ligne Hello dans le fichier téléchargé de hello sont de type Windows, mais bcp attend de style UNIX, donc nous devez bcp tootell qu’avec hello indicateur de - r.</span><span class="sxs-lookup"><span data-stu-id="fcf58-359">hello line endings in hello downloaded file are Windows-style, but bcp expects UNIX-style, so we need tootell bcp that with hello -r flag.</span></span>
>
>

<span data-ttu-id="fcf58-360">Et exécuter des requêtes avec sqlcmd :</span><span class="sxs-lookup"><span data-stu-id="fcf58-360">And query with sqlcmd:</span></span>

    select top 10 spam, char_freq_dollar from spam;
    GO

<span data-ttu-id="fcf58-361">Vous pouvez également exécuter des requêtes avec Squirrel SQL.</span><span class="sxs-lookup"><span data-stu-id="fcf58-361">You could also query with Squirrel SQL.</span></span> <span data-ttu-id="fcf58-362">Suivez les étapes similaires pour PostgreSQL, à l’aide de hello Microsoft MSSQL Server JDBC Driver, qui se trouve dans ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span><span class="sxs-lookup"><span data-stu-id="fcf58-362">Follow similar steps for PostgreSQL, using hello Microsoft MSSQL Server JDBC Driver, which can be found in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fcf58-363">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fcf58-363">Next steps</span></span>
<span data-ttu-id="fcf58-364">Pour une vue d’ensemble des rubriques qui vous guident tout au long des tâches de hello qui impliquent des processus de science des données hello dans Azure, consultez [processus de science des données équipe](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="fcf58-364">For an overview of topics that walk you through hello tasks that comprise hello Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="fcf58-365">Pour obtenir une description de l’autre bout en bout procédures pas à pas qui illustrent les étapes hello Bonjour processus de science des données équipe pour des scénarios spécifiques, consultez [procédures pas à pas du processus de science des données équipe](data-science-process-walkthroughs.md).</span><span class="sxs-lookup"><span data-stu-id="fcf58-365">For a description of other end-to-end walkthroughs that demonstrate hello steps in hello Team Data Science Process for specific scenarios, see [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md).</span></span> <span data-ttu-id="fcf58-366">procédures pas à pas Hello également illustrent comment toocombine cloud et locaux outils et services dans un toocreate de flux de travail ou d’un pipeline, une application intelligente.</span><span class="sxs-lookup"><span data-stu-id="fcf58-366">hello walkthroughs also illustrate how toocombine cloud and on-premises tools and services into a workflow or pipeline toocreate an intelligent application.</span></span>
