---
title: aaaAzure fonctions Runtime Installation | Documents Microsoft
description: Comment tooInstall hello Azure fonctions Runtime
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 67c6d10b5c0ac43e880d29cff0ae7b099f82bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-functions-runtime-preview"></a><span data-ttu-id="dab42-103">Installer hello Azure en version préliminaire fonctions Runtime</span><span class="sxs-lookup"><span data-stu-id="dab42-103">Install hello Azure Functions Runtime Preview</span></span>

<span data-ttu-id="dab42-104">Si vous souhaitez que la version préliminaire de Azure fonctions Runtime tooinstall hello, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="dab42-104">If you would like tooinstall hello Azure Functions Runtime preview, you must follow these steps:</span></span>

1. <span data-ttu-id="dab42-105">Vérifiez que votre ordinateur passe requise hello</span><span class="sxs-lookup"><span data-stu-id="dab42-105">Ensure your machine passes hello minimum requirements</span></span>
1. <span data-ttu-id="dab42-106">Télécharger hello [le programme d’installation de Azure fonctions Runtime Preview](https://aka.ms/azafr).</span><span class="sxs-lookup"><span data-stu-id="dab42-106">Download hello [Azure Functions Runtime Preview Installer](https://aka.ms/azafr).</span></span> 
1. <span data-ttu-id="dab42-107">Installez hello Azure fonctions Runtime preview</span><span class="sxs-lookup"><span data-stu-id="dab42-107">Install hello Azure Functions Runtime preview</span></span>
1. <span data-ttu-id="dab42-108">Configuration de hello complète de l’aperçu du Runtime de fonctions Azure hello</span><span class="sxs-lookup"><span data-stu-id="dab42-108">Complete hello configuration of hello Azure Functions Runtime preview</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dab42-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dab42-109">Prerequisites</span></span>

<span data-ttu-id="dab42-110">Avant d’installer de version préliminaire du Runtime de fonctions Azure hello, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="dab42-110">Before you install hello Azure Functions Runtime preview, you must have hello following:</span></span>

1. <span data-ttu-id="dab42-111">Un ordinateur exécutant Microsoft Windows Server 2016 ou Windows 10 Creators Update (édition Professionnelle ou Entreprise).</span><span class="sxs-lookup"><span data-stu-id="dab42-111">A machine running Microsoft Windows Server 2016 or Microsoft Windows 10 Creators Update (Professional or Enterprise Edition).</span></span>
1. <span data-ttu-id="dab42-112">Une instance SQL Server en cours d’exécution au sein de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="dab42-112">A SQL Server instance running within your network.</span></span>  <span data-ttu-id="dab42-113">La version minimale requise est SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="dab42-113">Minimum edition requirement is SQL Server Express.</span></span>

## <a name="install-hello-azure-functions-runtime-preview"></a><span data-ttu-id="dab42-114">Installer hello Azure en version préliminaire fonctions Runtime</span><span class="sxs-lookup"><span data-stu-id="dab42-114">Install hello Azure Functions Runtime Preview</span></span>

<span data-ttu-id="dab42-115">le programme d’installation de Hello Azure fonctions Runtime preview vous guide tout au long des installation hello d’aperçu du Runtime de fonctions Azure hello Management et les rôles de travail.</span><span class="sxs-lookup"><span data-stu-id="dab42-115">hello Azure Functions Runtime preview installer guides you through hello installation of hello Azure Functions Runtime preview Management and Worker Roles.</span></span>  <span data-ttu-id="dab42-116">Il est possible tooinstall hello gestion et le rôle de travail sur hello même ordinateur.</span><span class="sxs-lookup"><span data-stu-id="dab42-116">It is possible tooinstall hello Management and Worker role on hello same machine.</span></span>  <span data-ttu-id="dab42-117">Toutefois, lorsque vous ajoutez des fonctions, vous devez déployer plusieurs rôles de travail sur tooscale en mesure de machines supplémentaires toobe vos fonctions sur plusieurs threads de travail.</span><span class="sxs-lookup"><span data-stu-id="dab42-117">However, as you add more Functions, you must deploy more worker roles on additional machines toobe able tooscale your functions onto multiple workers.</span></span>

## <a name="install-hello-management-and-worker-role-on-hello-same-machine"></a><span data-ttu-id="dab42-118">Installer hello gestion et le rôle de travail sur hello même ordinateur</span><span class="sxs-lookup"><span data-stu-id="dab42-118">Install hello Management and Worker Role on hello same machine</span></span>

1. <span data-ttu-id="dab42-119">Exécutez hello le programme d’installation de Azure fonctions Runtime Preview.</span><span class="sxs-lookup"><span data-stu-id="dab42-119">Run hello Azure Functions Runtime Preview Installer.</span></span>

    ![Programme d’installation de la version préliminaire du runtime d’Azure Functions][1]

1. <span data-ttu-id="dab42-121">**Cliquez sur Suivant** avance au-delà de hello première étape du programme d’installation Bonjour</span><span class="sxs-lookup"><span data-stu-id="dab42-121">**Click Next** advance past hello first stage of hello installer</span></span>
1. <span data-ttu-id="dab42-122">Une fois que vous avez lu les termes du contrat de hello Hello **CLUF**, **hello case à cocher** termes de hello tooaccept et **cliquez sur Suivant** tooadvance.</span><span class="sxs-lookup"><span data-stu-id="dab42-122">Once you have read hello terms of hello **EULA**, **check hello box** tooaccept hello terms and **click Next** tooadvance.</span></span>
1. <span data-ttu-id="dab42-123">À présent, sélectionnez hello rôles lequel tooinstall sur cet ordinateur **rôle de fonctions de gestion** et/ou **rôle de travail des fonctions** et **cliquez sur Suivant**</span><span class="sxs-lookup"><span data-stu-id="dab42-123">Now select hello roles you want tooinstall on this machine **Functions Management Role** and/or **Functions Worker Role** and **Click Next**</span></span>

    ![Programme d’installation de la version préliminaire du runtime d’Azure Functions - Sélection du rôle][3]

    > [!NOTE]
    > <span data-ttu-id="dab42-125">Vous pouvez installer hello **rôle de travail des fonctions** sur nombreux autres toodo machines, suivez ces instructions, puis sélectionnez uniquement **rôle de travail des fonctions** dans le programme d’installation hello.</span><span class="sxs-lookup"><span data-stu-id="dab42-125">You can install hello **Functions Worker Role** on many other machines toodo so, follow these instructions, and only select **Functions Worker Role** in hello installer.</span></span>

1. <span data-ttu-id="dab42-126">**Cliquez sur Suivant** toohave hello **le programme d’installation de Azure fonctions Runtime** installer sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="dab42-126">**Click Next** toohave hello **Azure Functions Runtime Installer** install on your machine.</span></span>
1. <span data-ttu-id="dab42-127">Une fois que le programme d’installation complète hello lancera hello **outil de Configuration d’exécution Azure fonctions**.</span><span class="sxs-lookup"><span data-stu-id="dab42-127">Once complete hello installer will launch hello **Azure Functions Runtime Configuration tool**.</span></span>

    ![Programme d’installation de la version préliminaire du runtime d’Azure Functions terminé][5]

    > [!NOTE]
    > <span data-ttu-id="dab42-129">Si vous installez sur **Windows 10** et hello **conteneur** fonctionnalité a été précédemment désactivée, hello **Azure fonctions Runtime** programme d’installation vous invite tooreboot installation de votre hello toocomplete de machine.</span><span class="sxs-lookup"><span data-stu-id="dab42-129">If you are installing on **Windows 10** and hello **Container** feature has not been previously enabled, hello **Azure Functions Runtime** Installer prompts you tooreboot your machine toocomplete hello install.</span></span>

## <a name="configure-hello-azure-functions-runtime"></a><span data-ttu-id="dab42-130">Configurer hello Azure fonctions Runtime</span><span class="sxs-lookup"><span data-stu-id="dab42-130">Configure hello Azure Functions Runtime</span></span>

<span data-ttu-id="dab42-131">hello toocomplete installation Azure fonctions Runtime vous devez effectuer la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="dab42-131">toocomplete hello Azure Functions Runtime installation you must complete hello configuration.</span></span>

1. <span data-ttu-id="dab42-132">Hello **outil de Configuration du Runtime Azure fonctions** montre les rôles installés sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="dab42-132">hello **Azure Functions Runtime Configuration Tool** shows which roles are installed on your machine.</span></span>

    ![Outil de configuration de la version préliminaire du runtime d’Azure Functions terminé][6]

1. <span data-ttu-id="dab42-134">Cliquez sur hello **base de données** , entrez hello **détails de connexion pour votre Instance de SQL Server** et **cliquez sur Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="dab42-134">Click hello **Database** tab, enter hello **connection details for your SQL Server Instance** and **click Apply**.</span></span>  <span data-ttu-id="dab42-135">Cela est nécessaire dans l’ordre toohello Azure fonctions Runtime toocreate un Bonjour de toosupport Runtime de base de données.</span><span class="sxs-lookup"><span data-stu-id="dab42-135">This is required in order toohello Azure Functions Runtime toocreate a database toosupport hello Runtime.</span></span>
    
    ![Configuration de la base de données de la version préliminaire du runtime d’Azure Functions][7]

1. <span data-ttu-id="dab42-137">Cliquez sur hello **informations d’identification** onglet.  Dans cet écran, vous devez créer deux nouveaux jeux d’informations d’identification à utiliser avec un partage de fichiers pour l’hébergement de toutes vos Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="dab42-137">Click hello **Credentials** tab.  On this screen you must create two new credentials for use with a FileShare for hosting all your Azure Functions.</span></span>  <span data-ttu-id="dab42-138">**Spécifiez le nom d’utilisateur et mot de passe** combinaisons pour hello **propriétaire du partage de fichiers** et pourquoi **utilisateur du partage de fichiers** et cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="dab42-138">**Specify Username and Password** combinations for hello **File Share Owner** and for hello **File Share User** and click **Apply**.</span></span>

    ![Informations d’identification de la version préliminaire du runtime d’Azure Functions][8]

1. <span data-ttu-id="dab42-140">Cliquez sur hello **partage de fichiers** onglet.  Dans cet écran, vous devez spécifier les détails de hello Hello **emplacement du partage de fichiers**.</span><span class="sxs-lookup"><span data-stu-id="dab42-140">Click hello **File Share** tab.  In this screen you must specify hello details of hello **File Share location**.</span></span>  <span data-ttu-id="dab42-141">Celui-ci peut être créé pour vous ou vous pouvez utiliser un partage de fichier existant, puis cliquez sur **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="dab42-141">This can be created for you or you can use an existing File Share and click **Apply**.</span></span>  <span data-ttu-id="dab42-142">Si vous sélectionnez un nouvel emplacement de partage de fichiers, vous devez spécifier un répertoire pour une utilisation par hello Azure fonctions Runtime.</span><span class="sxs-lookup"><span data-stu-id="dab42-142">If you select a new File Share location, you must specify a directory for use by hello Azure Functions Runtime.</span></span>
    
    ![Partage de fichiers de la version préliminaire du runtime d’Azure Functions][9]

1. <span data-ttu-id="dab42-144">Cliquez sur hello **IIS** onglet.  Cet onglet affiche les détails de hello de hello des sites Web dans IIS qui hello Azure fonctions Runtime Installation va créer.</span><span class="sxs-lookup"><span data-stu-id="dab42-144">Click hello **IIS** tab.  This tab shows hello details of hello websites in IIS that hello Azure Functions Runtime Installation will create.</span></span>  <span data-ttu-id="dab42-145">**Cliquez sur Appliquer** toocomplete.</span><span class="sxs-lookup"><span data-stu-id="dab42-145">**Click Apply** toocomplete.</span></span>

    ![IIS de la version préliminaire du runtime d’Azure Functions][10]

1. <span data-ttu-id="dab42-147">Cliquez sur hello **Services** onglet.  Cet onglet affiche l’état hello de services de hello dans votre installation de l’exécution de fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="dab42-147">Click hello **Services** tab.  This tab shows hello status of hello services in your Azure Functions Runtime installation.</span></span>  <span data-ttu-id="dab42-148">Si, après avoir hello de la configuration initiale **Service d’Activation de Azure fonctions hôte** ne fonctionne pas cliquez **démarrer le Service**</span><span class="sxs-lookup"><span data-stu-id="dab42-148">If after initial configuration hello **Azure Functions Host Activation Service** is not running click **Start Service**</span></span>

    ![Configuration de la version préliminaire du runtime d’Azure Functions terminée][11]

1. <span data-ttu-id="dab42-150">Enfin Parcourir toohello **Azure fonctions Runtime portail** en tant que`https://<machinename>/`</span><span class="sxs-lookup"><span data-stu-id="dab42-150">Finally browse toohello **Azure Functions Runtime Portal** as `https://<machinename>/`</span></span>

    ![Portail du runtime d’Azure Functions en version préliminaire][12]


<!--Image references-->
[1]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer1.png
[2]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer2-EULA.png
[3]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer3-ChooseRoles.png
[4]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer4-Install.png
[5]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer5-InstallComplete.png
[6]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration1.png
[7]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration2_SQL.png
[8]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration3_Credentials.png
[9]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration4_Fileshare.png
[10]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration5_IIS.png
[11]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration6_Services.png
[12]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal.png