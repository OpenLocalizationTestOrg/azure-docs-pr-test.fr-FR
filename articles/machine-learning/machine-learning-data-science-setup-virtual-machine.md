---
title: aaaSet une machine virtuelle comme serveur notebooks bloc-notes | Documents Microsoft
description: "Configurez une machine virtuelle Azure pour l’utiliser dans un environnement de science des données avec un serveur IPython à des fins d’analyse avancée."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 818617c1-048e-49c2-b941-f9a983f93998
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: 58386140ec7742ade1f7e183ec842a2b09b9dfca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>Configurer une machine virtuelle Azure comme serveur IPython Notebook pour des analyses avancées
Cette rubrique montre comment tooprovision et configurer une machine virtuelle Azure pour analytique avancée qui peut être utilisé en tant que partie d’un environnement de science des données. l’ordinateur virtuel Windows Hello est configuré avec la prise en charge des outils tels que des notebooks portable, l’Explorateur de stockage Azure, AzCopy, ainsi que d’autres utilitaires qui sont utiles pour les projets d’analytique avancée. Azure Storage Explorer et AzCopy, par exemple, fournissent des moyens pratiques stockage d’objets blob tooAzure tooupload données à partir de votre ordinateur local ou un toodownload il tooyour la machine locale à partir du stockage d’objets blob.

## <a name="create-vm"></a>Étape 1 : créer une machine virtuelle Azure à usage général
Si vous disposez déjà d’une machine virtuelle Azure et que vous souhaitiez tooset d’un serveur notebooks bloc-notes sur celui-ci, vous pouvez ignorer cette étape et passez trop[étape 2 : ajouter un point de terminaison pour l’ordinateur virtuel existant de notebooks Ipython tooan](#add-endpoint).

Avant de commencer le processus hello de création d’un ordinateur virtuel sur Azure, vous devez taille de hello toodetermine d’ordinateur hello qui sont des données hello tooprocess nécessaire pour son projet. Les machines de taille réduite comportent moins de mémoire et de cœurs de processeur que les machines de grande taille, mais se révèlent également moins coûteuses. Pour obtenir la liste de prix et les types d’ordinateurs, consultez hello <a href="http://azure.microsoft.com/pricing/details/virtual-machines/" target="_blank">tarification des Machines virtuelles </a> page

1. Connectez-vous trop<a href="https://manage.windowsazure.com" target="_blank">portail Azure classic</a>, puis cliquez sur **nouveau** dans hello bas à gauche. Une fenêtre s’affiche. Sélectionnez **CALCUL** -> **MACHINE VIRTUELLE** -> **DE LA GALERIE**.
   
    ![Create workspace][24]
2. Choisissez une des hello suivant des images :
   
   * Windows Server 2012 R2 Datacenter
   * Expérience Windows Server Essentials (Windows Server 2012 R2)
     
     Ensuite, cliquez sur flèche hello pointant vers droite hello inférieure droite toogo hello page de configuration suivante.
     
     ![Create workspace][25]
3. Entrez un nom pour la machine virtuelle de hello souhaité toocreate, taille hello select de la machine de hello (par défaut : A3) en fonction de taille hello de l’ordinateur de hello données hello est continu tooprocess et la puissance hello machine toobe (mémoire taille et hello nombre de cœurs de calcul) , entrez un nom d’utilisateur et un mot de passe pour l’ordinateur de hello. Ensuite, cliquez sur flèche hello pointant vers la page de configuration suivante toogo droit toohello.
   
    ![Create workspace][26]
4. Sélectionnez hello **régions ou d’affinités groupe/réseau virtuel** contenant hello **compte de stockage** que vous envisagez de toouse pour cet ordinateur virtuel et sélectionnez ce compte de stockage. Ajouter un point de terminaison en bas hello Bonjour **points de terminaison** champ en entrant le nom hello du point de terminaison hello (« IPython » ici). Vous pouvez choisir n’importe quelle chaîne comme hello **nom** de point de terminaison hello et n’importe quel entier compris entre 0 et 65536 **disponible** comme hello **PORT PUBLIC**. Hello **PORT privé** a toobe **9999**. Vous devez **éviter** d’utiliser des ports publics déjà attribués pour des services Internet. L’article concernant les <a href="http://www.chebucto.ns.ca/~rakerman/port-table.html" target="_blank">ports associés aux services Internet</a> répertorie les ports qui sont attribués et qui doivent donc être évités.
   
    ![Create workspace][27]
5. Cliquez sur le processus de configuration de machine virtuelle de hello coche toostart hello.
   
    ![Create workspace][28]

Il peut prendre 15 à 25 minutes toocomplete hello virtual machine, processus de configuration. Une fois l’ordinateur virtuel de hello a été créé, état hello de cet ordinateur doit être **en cours d’exécution**.

![Create workspace][29]

## <a name="add-endpoint"></a>Étape 2 : Ajouter un point de terminaison pour l’ordinateur virtuel existant de notebooks Ipython tooan
Si vous avez créé l’ordinateur virtuel de hello en suivant les instructions de hello à l’étape 1, puis hello point de terminaison pour IPython Notebook a déjà été ajouté et cette étape peut être ignorée.

Si la machine virtuelle de hello existe déjà et vous devez tooadd un point de terminaison pour IPython Notebook que vous allez installer à l’étape 3 ci-dessous, première connexion tooAzure portail classique, sélectionnez la machine virtuelle hello et ajouter hello de point de terminaison pour le serveur de notebooks bloc-notes. Hello figure suivante contient une capture d’écran du portail de hello après que le point de terminaison hello pour IPython Notebook a été ajouté à l’ordinateur virtuel tooa Windows.

![Create workspace][17]

## <a name="run-commands"></a>Étape 3 : installer Notebook IPython et les autres outils connexes
Après la création de la machine virtuelle de hello, utilisez toolog du protocole RDP (Remote Desktop) sur l’ordinateur virtuel toohello Windows. Pour obtenir des instructions, consultez [comment tooLog sur tooa Machine virtuelle exécutant Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Ouvrez hello **invite de commandes** (**pas les fenêtre de commande Powershell hello**) en tant qu’un **administrateur** et hello exécution de commande suivante.

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

Lorsque hello installation terminée, hello server de l’ordinateur portable de notebooks est automatiquement lancé Bonjour *C:\\utilisateurs\\\<nom d’utilisateur\>\\Documents\\IPython Ordinateurs portables* active.

Lorsque vous y êtes invité, entrez un mot de passe pour hello notebooks bloc-notes et hello d’administrateur d’ordinateur hello. Cela permet de hello notebooks bloc-notes toorun en tant que service sur l’ordinateur de hello.

## <a name="access"></a>Étape 4 : accéder à Notebook IPython à partir d’un navigateur web
tooaccess hello server des notebooks bloc-notes, ouvrez un site web navigateur et entrée *nom DNS de l’ordinateur https://&#60;virtual > : &#60; numéro de port public >* dans la zone de texte URL hello. Ici, hello *&#60; numéro de port public >* doit être de numéro de port hello vous avez spécifié lorsque hello notebooks bloc-notes point de terminaison a été ajouté.

Hello *&#60; le nom DNS de machine virtuelle >* trouverez hello portail Azure classic. Après l’ouverture dans le portail classique de toohello, cliquez sur **virtuels**, sélectionnez ordinateur hello vous créé, puis sélectionnez **tableau de bord**, nom DNS hello s’affichera comme suit :

![Create workspace][19]

Vous rencontrerez un avertissement indiquant que *il existe un problème avec le certificat de sécurité de ce site Web* (Internet Explorer) ou *votre connexion n’est pas privée* (Chrome), comme indiqué dans les éléments suivants de hello chiffres. Cliquez sur **site Web de toothis continuer (non recommandé)** (Internet Explorer) ou **avancé** , puis  **continuer trop &#60;* Nom DNS*> (non sécurisé) ** (Chrome) toocontinue. Entrez un mot de passe hello vous spécifié tooaccess antérieures hello notebooks Ipython.

**Internet Explorer :**
![Créer un espace de travail][20]

**Chrome :**
![Créer un espace de travail][21]

Une fois la session toohello notebooks portable, un répertoire *DataScienceSamples* s’affiche dans le navigateur de hello. Ce répertoire contient un exemple notebooks Ipython qui sont partagées par Microsoft toohelp utilisateurs conduite des tâches de science des données. Ces exemples notebooks Ipython sont extraits à partir de [ **référentiel GitHub** ](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) virtuels toohello pendant hello processus d’installation de serveur notebooks bloc-notes. Microsoft gère ce dépôt et le met régulièrement à jour. Les utilisateurs peuvent visiter GitHub référentiel tooget hello plus récemment mises à jour exemple hello notebooks Ipython.
![Create workspace][18]

## <a name="upload"></a>Étape 5 : Téléchargez un bloc-notes notebooks existant à partir d’un toohello de l’ordinateur local server de notebooks bloc-notes
IPython Notebook fournissent un moyen simple pour tooupload d’utilisateurs un bloc-notes notebooks sur leur toohello ordinateurs locaux serveur notebooks bloc-notes sur des machines virtuelles de hello. Une fois la session toohello notebooks bloc-notes dans un navigateur web, cliquez sur la hello **répertoire** que hello notebooks bloc-notes sera téléchargé vers. Ensuite, sélectionnez un tooupload de fichier .ipynb notebooks bloc-notes à partir de l’ordinateur local de hello Bonjour **l’Explorateur de fichiers**et faites glisser toohello active des notebooks bloc-notes de navigateur hello. Cliquez sur hello **télécharger** bouton tooupload hello .ipynb fichier toohello server des notebooks bloc-notes. D’autres utilisateurs peuvent alors commencer à utiliser ce fichier dans leur navigateur web.

![Create workspace][22]

![Create workspace][23]

## <a name="shutdown"></a>Arrêter et libérer une machine virtuelle inutilisée
Le service Azure Virtual Machines est facturé au tarif du **paiement à l’utilisation**. tooensure qui vous ne sont pas facturées lorsque vous n’utilisez ne pas votre machine virtuelle, il a toobe Bonjour **arrêté (désalloué)** état inutilisés.

> [!NOTE]
> Si vous arrêtez l’ordinateur virtuel de hello d’à l’intérieur de hello machine virtuelle (à l’aide des options d’alimentation de Windows), hello machine virtuelle est arrêté, mais il reste allouée. tooensure vous ne continuez pas toobe facturé, toujours s’arrêter les machines virtuelles à partir de hello [portail Azure classic](http://manage.windowsazure.com/). Vous pouvez également arrêter hello machine virtuelle via Powershell en appelant **ShutdownRoleOperation** « PostShutdownAction » égal trop « StoppedDeallocated ».
> 
> 

tooshut vers le bas et désallouer une machine virtuelle hello :

1. Connectez-vous à toohello [portail Azure classic](http://manage.windowsazure.com/) à l’aide de votre compte.  
2. Sélectionnez **virtuels** à partir de la barre de navigation gauche hello.
3. Dans la liste hello des machines virtuelles, cliquez sur nom hello de votre machine virtuelle, puis accédez toohello **tableau de bord** page.
4. Au bas de hello de page de hello, cliquez sur **arrêt**.

![Arrêt de la machine virtuelle][15]

machine virtuelle de Hello sera libérée mais pas supprimé. Vous pouvez redémarrer votre machine virtuelle à tout moment à partir de hello portail Azure classic.

## <a name="your-azure-vm-is-ready-toouse-whats-next"></a>Votre machine virtuelle Azure est prêt toouse : quelle est la suite ?
Votre ordinateur virtuel est maintenant prêt toouse dans vos exercices de science des données. machine virtuelle de Hello est également prêt à être utilisé comme un serveur notebooks bloc-notes de hello et le traitement des données et d’autres tâches conjointement avec Azure Machine Learning et hello processus de science des données équipe.

étapes Hello Bonjour processus de science des données équipe sont mappées dans hello [d’apprentissage de chemin d’accès](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) et peuvent inclure des étapes de déplacement des données dans HDInsight, processus et les exemples de celui-ci en préparation pour l’apprentissage à partir des données de hello avec Azure Machine L’apprentissage.

[15]: ./media/machine-learning-data-science-setup-virtual-machine/vmshutdown.png
[17]: ./media/machine-learning-data-science-setup-virtual-machine/add-endpoints-after-creation.png
[18]: ./media/machine-learning-data-science-setup-virtual-machine/sample-ipnbs.png
[19]: ./media/machine-learning-data-science-setup-virtual-machine/dns-name-and-host-name.png
[20]: ./media/machine-learning-data-science-setup-virtual-machine/browser-warning-ie.png
[21]: ./media/machine-learning-data-science-setup-virtual-machine/browser-warning.png
[22]: ./media/machine-learning-data-science-setup-virtual-machine/upload-ipnb-1.png
[23]: ./media/machine-learning-data-science-setup-virtual-machine/upload-ipnb-2.png
[24]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-1.png
[25]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-2.png
[26]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-3.png
[27]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-4.png
[28]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-5.png
[29]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-6.png
