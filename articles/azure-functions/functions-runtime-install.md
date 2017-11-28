---
title: "Installation du runtime d’Azure Functions | Microsoft Docs"
description: "Comment installer le runtime d’Azure Functions"
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
ms.openlocfilehash: 1e4188313a87d07f396e5f8edc8969dd5da2c436
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="install-the-azure-functions-runtime-preview"></a><span data-ttu-id="38c8d-103">Installer la version préliminaire du runtime d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="38c8d-103">Install the Azure Functions Runtime Preview</span></span>

<span data-ttu-id="38c8d-104">Suivez ces étapes pour installer la version préliminaire du runtime d’Azure Functions :</span><span class="sxs-lookup"><span data-stu-id="38c8d-104">If you would like to install the Azure Functions Runtime preview, you must follow these steps:</span></span>

1. <span data-ttu-id="38c8d-105">Vérifiez que votre ordinateur respecte la configuration minimale requise</span><span class="sxs-lookup"><span data-stu-id="38c8d-105">Ensure your machine passes the minimum requirements</span></span>
1. <span data-ttu-id="38c8d-106">Téléchargez le [programme d’installation de la version préliminaire du runtime d’Azure Functions](https://aka.ms/azafr).</span><span class="sxs-lookup"><span data-stu-id="38c8d-106">Download the [Azure Functions Runtime Preview Installer](https://aka.ms/azafr).</span></span> 
1. <span data-ttu-id="38c8d-107">Installer la version préliminaire du runtime d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="38c8d-107">Install the Azure Functions Runtime preview</span></span>
1. <span data-ttu-id="38c8d-108">Terminer la configuration de la version préliminaire du runtime d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="38c8d-108">Complete the configuration of the Azure Functions Runtime preview</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38c8d-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="38c8d-109">Prerequisites</span></span>

<span data-ttu-id="38c8d-110">Avant d’installer la version préliminaire du runtime d’Azure Functions, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="38c8d-110">Before you install the Azure Functions Runtime preview, you must have the following:</span></span>

1. <span data-ttu-id="38c8d-111">Un ordinateur exécutant Microsoft Windows Server 2016 ou Windows 10 Creators Update (édition Professionnelle ou Entreprise).</span><span class="sxs-lookup"><span data-stu-id="38c8d-111">A machine running Microsoft Windows Server 2016 or Microsoft Windows 10 Creators Update (Professional or Enterprise Edition).</span></span>
1. <span data-ttu-id="38c8d-112">Une instance SQL Server en cours d’exécution au sein de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="38c8d-112">A SQL Server instance running within your network.</span></span>  <span data-ttu-id="38c8d-113">La version minimale requise est SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="38c8d-113">Minimum edition requirement is SQL Server Express.</span></span>

## <a name="install-the-azure-functions-runtime-preview"></a><span data-ttu-id="38c8d-114">Installer la version préliminaire du runtime d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="38c8d-114">Install the Azure Functions Runtime Preview</span></span>

<span data-ttu-id="38c8d-115">Le programme d’installation en version préliminaire du runtime d’Azure Functions vous guide lors de l’installation des rôles de gestion et de travail de la version préliminaire du runtime d’Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="38c8d-115">The Azure Functions Runtime preview installer guides you through the installation of the Azure Functions Runtime preview Management and Worker Roles.</span></span>  <span data-ttu-id="38c8d-116">Il est possible d’installer le rôle de gestion et de travail sur le même ordinateur.</span><span class="sxs-lookup"><span data-stu-id="38c8d-116">It is possible to install the Management and Worker role on the same machine.</span></span>  <span data-ttu-id="38c8d-117">Toutefois, si vous ajoutez des fonctions, vous devez déployer davantage de rôles de travail sur des ordinateurs supplémentaires pour faire évoluer vos fonctions sur plusieurs rôles de travail.</span><span class="sxs-lookup"><span data-stu-id="38c8d-117">However, as you add more Functions, you must deploy more worker roles on additional machines to be able to scale your functions onto multiple workers.</span></span>

## <a name="install-the-management-and-worker-role-on-the-same-machine"></a><span data-ttu-id="38c8d-118">Installer le rôle de gestion et de travail sur le même ordinateur</span><span class="sxs-lookup"><span data-stu-id="38c8d-118">Install the Management and Worker Role on the same machine</span></span>

1. <span data-ttu-id="38c8d-119">Exécutez le programme d’installation de la version préliminaire du runtime d’Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="38c8d-119">Run the Azure Functions Runtime Preview Installer.</span></span>

    ![Programme d’installation de la version préliminaire du runtime d’Azure Functions][1]

1. <span data-ttu-id="38c8d-121">**Cliquez sur Suivant** pour progresser au-delà de la première étape du programme d’installation</span><span class="sxs-lookup"><span data-stu-id="38c8d-121">**Click Next** advance past the first stage of the installer</span></span>
1. <span data-ttu-id="38c8d-122">Une fois que vous avez lu les conditions d’utilisation du **CLUF**, **cochez la case** pour accepter les conditions d’utilisation et **cliquez sur Suivant** pour passer à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="38c8d-122">Once you have read the terms of the **EULA**, **check the box** to accept the terms and **click Next** to advance.</span></span>
1. <span data-ttu-id="38c8d-123">À présent, sélectionnez les rôles que vous souhaitez installer sur cet ordinateur **Rôle de gestion Functions** et/ou **Rôle de travail Functions** et **cliquez sur Suivant**</span><span class="sxs-lookup"><span data-stu-id="38c8d-123">Now select the roles you want to install on this machine **Functions Management Role** and/or **Functions Worker Role** and **Click Next**</span></span>

    ![Programme d’installation de la version préliminaire du runtime d’Azure Functions - Sélection du rôle][3]

    > [!NOTE]
    > <span data-ttu-id="38c8d-125">Vous pouvez installer le **rôle de travail Functions** sur plusieurs autres ordinateurs. Pour ce faire, suivez ces instructions et sélectionnez uniquement **Rôle de travail Functions** dans le programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="38c8d-125">You can install the **Functions Worker Role** on many other machines to do so, follow these instructions, and only select **Functions Worker Role** in the installer.</span></span>

1. <span data-ttu-id="38c8d-126">**Cliquez sur Suivant** pour que le **programme d’installation du runtime d’Azure Functions** s’installe sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="38c8d-126">**Click Next** to have the **Azure Functions Runtime Installer** install on your machine.</span></span>
1. <span data-ttu-id="38c8d-127">Une fois terminé, le programme d’installation lance **l’outil de configuration du runtime d’Azure Functions**.</span><span class="sxs-lookup"><span data-stu-id="38c8d-127">Once complete the installer will launch the **Azure Functions Runtime Configuration tool**.</span></span>

    ![Programme d’installation de la version préliminaire du runtime d’Azure Functions terminé][5]

    > [!NOTE]
    > <span data-ttu-id="38c8d-129">Si vous installez sous **Windows 10** et si la fonctionnalité **Conteneur** n’a pas été précédemment activée, le programme d’installation du **runtime d’Azure Functions** vous invite à redémarrer votre ordinateur pour terminer l’installation.</span><span class="sxs-lookup"><span data-stu-id="38c8d-129">If you are installing on **Windows 10** and the **Container** feature has not been previously enabled, the **Azure Functions Runtime** Installer prompts you to reboot your machine to complete the install.</span></span>

## <a name="configure-the-azure-functions-runtime"></a><span data-ttu-id="38c8d-130">Configurer le runtime d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="38c8d-130">Configure the Azure Functions Runtime</span></span>

<span data-ttu-id="38c8d-131">Pour terminer l’installation du runtime d’Azure Functions, vous devez terminer la configuration.</span><span class="sxs-lookup"><span data-stu-id="38c8d-131">To complete the Azure Functions Runtime installation you must complete the configuration.</span></span>

1. <span data-ttu-id="38c8d-132">**L’outil de configuration du runtime d’Azure Functions** vous indique les rôles installés sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="38c8d-132">The **Azure Functions Runtime Configuration Tool** shows which roles are installed on your machine.</span></span>

    ![Outil de configuration de la version préliminaire du runtime d’Azure Functions terminé][6]

1. <span data-ttu-id="38c8d-134">Cliquez sur l’onglet **Base de données**, entrez les **informations de connexion pour votre Instance SQL Server** et **cliquez sur Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="38c8d-134">Click the **Database** tab, enter the **connection details for your SQL Server Instance** and **click Apply**.</span></span>  <span data-ttu-id="38c8d-135">Cela est nécessaire pour que le runtime d’Azure Functions crée une base de données pour prendre en charge le runtime.</span><span class="sxs-lookup"><span data-stu-id="38c8d-135">This is required in order to the Azure Functions Runtime to create a database to support the Runtime.</span></span>
    
    ![Configuration de la base de données de la version préliminaire du runtime d’Azure Functions][7]

1. <span data-ttu-id="38c8d-137">Cliquez sur l’onglet **Informations d’identification**.</span><span class="sxs-lookup"><span data-stu-id="38c8d-137">Click the **Credentials** tab.</span></span>  <span data-ttu-id="38c8d-138">Dans cet écran, vous devez créer deux nouveaux jeux d’informations d’identification à utiliser avec un partage de fichiers pour l’hébergement de toutes vos Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="38c8d-138">On this screen you must create two new credentials for use with a FileShare for hosting all your Azure Functions.</span></span>  <span data-ttu-id="38c8d-139">**Spécifiez les combinaisons de nom d’utilisateur et de mot de passe** pour le **propriétaire du partage de fichiers** et **l’utilisateur du partage de fichiers** et cliquez sur **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="38c8d-139">**Specify Username and Password** combinations for the **File Share Owner** and for the **File Share User** and click **Apply**.</span></span>

    ![Informations d’identification de la version préliminaire du runtime d’Azure Functions][8]

1. <span data-ttu-id="38c8d-141">Cliquez sur l’onglet **Partage de fichiers**.</span><span class="sxs-lookup"><span data-stu-id="38c8d-141">Click the **File Share** tab.</span></span>  <span data-ttu-id="38c8d-142">Dans cet écran, vous devez spécifier les détails de **l’emplacement du partage de fichiers**.</span><span class="sxs-lookup"><span data-stu-id="38c8d-142">In this screen you must specify the details of the **File Share location**.</span></span>  <span data-ttu-id="38c8d-143">Celui-ci peut être créé pour vous ou vous pouvez utiliser un partage de fichier existant, puis cliquez sur **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="38c8d-143">This can be created for you or you can use an existing File Share and click **Apply**.</span></span>  <span data-ttu-id="38c8d-144">Si vous sélectionnez un nouvel emplacement de partage de fichiers, vous devez spécifier un répertoire que le runtime d’Azure Functions doit utiliser.</span><span class="sxs-lookup"><span data-stu-id="38c8d-144">If you select a new File Share location, you must specify a directory for use by the Azure Functions Runtime.</span></span>
    
    ![Partage de fichiers de la version préliminaire du runtime d’Azure Functions][9]

1. <span data-ttu-id="38c8d-146">Cliquez sur l’onglet **IIS**.</span><span class="sxs-lookup"><span data-stu-id="38c8d-146">Click the **IIS** tab.</span></span>  <span data-ttu-id="38c8d-147">Cet onglet affiche les détails des sites web dans IIS, que l’installation du runtime d’Azure Functions va créer.</span><span class="sxs-lookup"><span data-stu-id="38c8d-147">This tab shows the details of the websites in IIS that the Azure Functions Runtime Installation will create.</span></span>  <span data-ttu-id="38c8d-148">**Cliquez sur Appliquer** pour terminer.</span><span class="sxs-lookup"><span data-stu-id="38c8d-148">**Click Apply** to complete.</span></span>

    ![IIS de la version préliminaire du runtime d’Azure Functions][10]

1. <span data-ttu-id="38c8d-150">Cliquez sur l’onglet **Services**.</span><span class="sxs-lookup"><span data-stu-id="38c8d-150">Click the **Services** tab.</span></span>  <span data-ttu-id="38c8d-151">Cet onglet affiche l’état des services dans l’installation du runtime d’Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="38c8d-151">This tab shows the status of the services in your Azure Functions Runtime installation.</span></span>  <span data-ttu-id="38c8d-152">Si après la configuration initiale le **service d’activation hôte Azure Functions** ne fonctionne pas, cliquez sur **Démarrer le service**</span><span class="sxs-lookup"><span data-stu-id="38c8d-152">If after initial configuration the **Azure Functions Host Activation Service** is not running click **Start Service**</span></span>

    ![Configuration de la version préliminaire du runtime d’Azure Functions terminée][11]

1. <span data-ttu-id="38c8d-154">Enfin, accédez au **portail du runtime d’Azure Functions** en tant que `https://<machinename>/`</span><span class="sxs-lookup"><span data-stu-id="38c8d-154">Finally browse to the **Azure Functions Runtime Portal** as `https://<machinename>/`</span></span>

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