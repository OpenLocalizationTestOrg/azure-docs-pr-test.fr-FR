---
title: "Azure Data Lake Tools : Utiliser Azure Data Lake Tools pour Visual Studio Code | Microsoft Docs"
description: "Découvrez comment utiliser Azure Data Lake Tools pour Visual Studio Code pour créer, tester et exécuter des scripts U-SQL. "
Keywords: "VScode,Azure Data Lake Tools,exécution locale,débogage local,Débogage local,aperçu du fichier de stockage,charger vers le chemin de stockage"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: 833d14af47454a01fa3c97ffa854d688dd35871f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a><span data-ttu-id="3537a-104">Utiliser Azure Data Lake Tools pour Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="3537a-104">Use Azure Data Lake Tools for Visual Studio Code</span></span>

<span data-ttu-id="3537a-105">Découvrez comment utiliser Azure Data Lake Tools pour Visual Studio Code (VS Code) pour créer, tester et exécuter des scripts U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3537a-105">Learn how to use Azure Data Lake Tools for Visual Studio Code (VS Code) to create, test, and run U-SQL scripts.</span></span> <span data-ttu-id="3537a-106">Ces informations sont également décrites dans la vidéo suivante :</span><span class="sxs-lookup"><span data-stu-id="3537a-106">The information is also covered in the following video:</span></span>

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a><span data-ttu-id="3537a-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3537a-107">Prerequisites</span></span>

<span data-ttu-id="3537a-108">Vous pouvez installer Data Lake Tools sur les plateformes prises en charge par VS Code.</span><span class="sxs-lookup"><span data-stu-id="3537a-108">Data Lake Tools can be installed on the platforms supported by VS Code.</span></span> <span data-ttu-id="3537a-109">Les plateformes prises en charge incluent Windows, Linux et MacOS.</span><span class="sxs-lookup"><span data-stu-id="3537a-109">The supported platforms include Windows, Linux, and MacOS.</span></span> <span data-ttu-id="3537a-110">Les différentes plateformes ont les prérequis suivants :</span><span class="sxs-lookup"><span data-stu-id="3537a-110">The different platforms have the following prerequisites:</span></span>

- <span data-ttu-id="3537a-111">Windows</span><span class="sxs-lookup"><span data-stu-id="3537a-111">Windows</span></span>

    - <span data-ttu-id="3537a-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="3537a-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="3537a-113">[Java SE Runtime Environment version 8 mise à jour 77 ou ultérieure](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="3537a-113">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="3537a-114">Ajoutez le chemin java.exe à la variable d’environnement système Path.</span><span class="sxs-lookup"><span data-stu-id="3537a-114">Add the java.exe path to the system environment variable path.</span></span> <span data-ttu-id="3537a-115">Pour obtenir des instructions sur la configuration, consultez [Comment définir ou modifier la variable système Path ?]( https://www.java.com/download/help/path.xml).</span><span class="sxs-lookup"><span data-stu-id="3537a-115">For configuration instructions, see [How do I set or change the Path system variable?]( https://www.java.com/download/help/path.xml).</span></span> <span data-ttu-id="3537a-116">Le chemin est semblable à C:\Program Files\Java\jdk1.8.0_77\jre\bin.</span><span class="sxs-lookup"><span data-stu-id="3537a-116">The path is similar to C:\Program Files\Java\jdk1.8.0_77\jre\bin.</span></span>
    - <span data-ttu-id="3537a-117">[Kit SDK .NET Core 1.0.3 ou runtime .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="3537a-117">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
    
- <span data-ttu-id="3537a-118">Linux (nous recommandons Ubuntu 14.04 LTS)</span><span class="sxs-lookup"><span data-stu-id="3537a-118">Linux (We recommend Ubuntu 14.04 LTS)</span></span>

    - <span data-ttu-id="3537a-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="3537a-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span> <span data-ttu-id="3537a-120">Pour installer le code, entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3537a-120">To install the code, enter the following command:</span></span>

              sudo dpkg -i code_<version_number>_amd64.deb

    - <span data-ttu-id="3537a-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span><span class="sxs-lookup"><span data-stu-id="3537a-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span></span> 

        - <span data-ttu-id="3537a-122">Pour mettre à jour la source du package deb, entrez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="3537a-122">To update the deb package source, enter the following commands:</span></span>

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - <span data-ttu-id="3537a-123">Pour installer Mono, entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3537a-123">To install Mono, enter the following command:</span></span>

                sudo apt-get install mono-complete

            > [!NOTE] 
            > <span data-ttu-id="3537a-124">Mono 4.6 n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3537a-124">Mono 4.6 is not supported.</span></span> <span data-ttu-id="3537a-125">Désinstallez entièrement la version 4.6 avant d’installer la version 4.2.x.</span><span class="sxs-lookup"><span data-stu-id="3537a-125">Uninstall version 4.6 entirely before you install 4.2.x.</span></span>  

        - <span data-ttu-id="3537a-126">[Java SE Runtime Environment version 8 mise à jour 77 ou ultérieure](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="3537a-126">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="3537a-127">Pour obtenir des instructions sur l’installation, consultez la page [Instructions d’installation de Java pour Linux 64 bits ]( https://java.com/en/download/help/linux_x64_install.xml).</span><span class="sxs-lookup"><span data-stu-id="3537a-127">For instructions on installation, see the [Linux 64-bit installation instructions for Java]( https://java.com/en/download/help/linux_x64_install.xml) page.</span></span>
        - <span data-ttu-id="3537a-128">[Kit SDK .NET Core 1.0.3 ou runtime .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="3537a-128">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
- <span data-ttu-id="3537a-129">MacOS</span><span class="sxs-lookup"><span data-stu-id="3537a-129">MacOS</span></span>

    - <span data-ttu-id="3537a-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="3537a-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="3537a-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span><span class="sxs-lookup"><span data-stu-id="3537a-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span></span> 
    - <span data-ttu-id="3537a-132">[Java SE Runtime Environment version 8 mise à jour 77 ou ultérieure](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="3537a-132">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="3537a-133">Pour obtenir des instructions sur l’installation, consultez la page [Instructions d’installation de Java pour Linux 64 bits ](https://java.com/en/download/help/mac_install.xml).</span><span class="sxs-lookup"><span data-stu-id="3537a-133">For instructions on installation, see the [Linux 64-bit installation instructions for Java](https://java.com/en/download/help/mac_install.xml) page.</span></span>
    - <span data-ttu-id="3537a-134">[Kit SDK .NET Core 1.0.3 ou runtime .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="3537a-134">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>

## <a name="install-data-lake-tools"></a><span data-ttu-id="3537a-135">Installer Data Lake Tools</span><span class="sxs-lookup"><span data-stu-id="3537a-135">Install Data Lake Tools</span></span>

<span data-ttu-id="3537a-136">Après avoir installé les prérequis, vous pouvez installer Data Lake Tools pour VS Code.</span><span class="sxs-lookup"><span data-stu-id="3537a-136">After you install the prerequisites, you can install Data Lake Tools for VS Code.</span></span>

<span data-ttu-id="3537a-137">**Pour installer Data Lake Tools**</span><span class="sxs-lookup"><span data-stu-id="3537a-137">**To install Data Lake Tools**</span></span>

1. <span data-ttu-id="3537a-138">Ouvrez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="3537a-138">Open Visual Studio Code.</span></span>
2. <span data-ttu-id="3537a-139">Sélectionnez Ctrl+P, puis entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3537a-139">Select Ctrl+P, and then enter the following command:</span></span>
```
ext install usql-vscode-ext
```
<span data-ttu-id="3537a-140">Une liste des extensions de code Visual Studio s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3537a-140">You can see a list of Visual Studio code extensions.</span></span> <span data-ttu-id="3537a-141">L’une d’elles est **Azure Data Lake Tools**.</span><span class="sxs-lookup"><span data-stu-id="3537a-141">One of them is **Azure Data Lake Tools**.</span></span>

3. <span data-ttu-id="3537a-142">Sélectionnez **Installer** en regard de **Azure Data Lake Tools**.</span><span class="sxs-lookup"><span data-stu-id="3537a-142">Select **Install** next to **Azure Data Lake Tools**.</span></span> <span data-ttu-id="3537a-143">Après quelques secondes, le bouton **Installer** est remplacé par le bouton **Recharger**.</span><span class="sxs-lookup"><span data-stu-id="3537a-143">After a few seconds, the **Install** button changes to **Reload**.</span></span>
4. <span data-ttu-id="3537a-144">Sélectionnez **Recharger** pour activer l’extension.</span><span class="sxs-lookup"><span data-stu-id="3537a-144">Select **Reload** to activate the extension.</span></span>
5. <span data-ttu-id="3537a-145">Sélectionnez **OK** pour confirmer.</span><span class="sxs-lookup"><span data-stu-id="3537a-145">Select **OK** to confirm.</span></span> <span data-ttu-id="3537a-146">Azure Data Lake Tools s’affiche dans le volet **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="3537a-146">You can see Azure Data Lake Tools in the **Extensions** pane.</span></span>
    <span data-ttu-id="3537a-147">![Volet Extensions de Data Lake Tools pour Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span><span class="sxs-lookup"><span data-stu-id="3537a-147">![Data Lake Tools for Visual Studio Code Extensions pane](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span></span>

## <a name="activate-azure-data-lake-tools"></a><span data-ttu-id="3537a-148">Activer Azure Data Lake Tools</span><span class="sxs-lookup"><span data-stu-id="3537a-148">Activate Azure Data Lake Tools</span></span>
<span data-ttu-id="3537a-149">Créez un fichier .usql ou ouvrez un fichier .usql existant pour activer l’extension.</span><span class="sxs-lookup"><span data-stu-id="3537a-149">Create a new .usql file or open an existing .usql file to activate the extension.</span></span> 

## <a name="connect-to-azure"></a><span data-ttu-id="3537a-150">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="3537a-150">Connect to Azure</span></span>

<span data-ttu-id="3537a-151">Avant de pouvoir compiler et exécuter des scripts U-SQL dans Data Lake Analytics, vous devez vous connecter à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="3537a-151">Before you can compile and run U-SQL scripts in Data Lake Analytics, you must connect to your Azure account.</span></span>

<span data-ttu-id="3537a-152">**Pour vous connecter à Azure**</span><span class="sxs-lookup"><span data-stu-id="3537a-152">**To connect to Azure**</span></span>

1.  <span data-ttu-id="3537a-153">Sélectionnez Ctrl+Maj+P pour ouvrir la palette de commandes.</span><span class="sxs-lookup"><span data-stu-id="3537a-153">Select Ctrl+Shift+P to open the command palette.</span></span> 
2.  <span data-ttu-id="3537a-154">Entrez **ADL: Login**.</span><span class="sxs-lookup"><span data-stu-id="3537a-154">Enter **ADL: Login**.</span></span> <span data-ttu-id="3537a-155">Les informations de connexion s’affichent dans le volet **Output**.</span><span class="sxs-lookup"><span data-stu-id="3537a-155">The login information appears in the **Output** pane.</span></span>

    <span data-ttu-id="3537a-156">![Palette de commandes de Data Lake Tools pour Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Informations de connexion d’appareil Data Lake Tools pour Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span><span class="sxs-lookup"><span data-stu-id="3537a-156">![Data Lake Tools for Visual Studio Code command palette](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
![Data Lake Tools for Visual Studio Code device login information](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span></span>
3. <span data-ttu-id="3537a-157">Sélectionnez Ctrl+clic sur l’URL de connexion : https://aka.ms/devicelogin pour ouvrir la page web de connexion.</span><span class="sxs-lookup"><span data-stu-id="3537a-157">Select Ctrl+click on the login URL: https://aka.ms/devicelogin to open the login webpage.</span></span> <span data-ttu-id="3537a-158">Entrez le code **G567LX42V** dans la zone de texte, puis sélectionnez **Continuer**.</span><span class="sxs-lookup"><span data-stu-id="3537a-158">Enter the code **G567LX42V** into the text box, and then select **Continue**.</span></span>

   ![Data Lake Tools pour Visual Studio Code - Coller le code de connexion](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  <span data-ttu-id="3537a-160">Suivez les instructions pour vous connecter à partir de la page web.</span><span class="sxs-lookup"><span data-stu-id="3537a-160">Follow the instructions to sign in from the webpage.</span></span> <span data-ttu-id="3537a-161">Une fois connecté, le nom de votre compte Azure s’affiche dans la barre d’état dans le coin inférieur gauche de la fenêtre **VS Code**.</span><span class="sxs-lookup"><span data-stu-id="3537a-161">When you're connected, your Azure account name appears on the status bar in the lower-left corner of the **VS Code** window.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="3537a-162">Si votre compte a deux facteurs activés, nous vous recommandons d’utiliser l’authentification par téléphone plutôt qu’un code PIN.</span><span class="sxs-lookup"><span data-stu-id="3537a-162">If your account has two factors enabled, we recommend that you use phone authentication rather than using a PIN.</span></span>

<span data-ttu-id="3537a-163">Pour vous déconnecter, entrez la commande **ADL: Logout**.</span><span class="sxs-lookup"><span data-stu-id="3537a-163">To sign out, enter the command **ADL: Logout**.</span></span>

## <a name="list-your-data-lake-analytics-accounts"></a><span data-ttu-id="3537a-164">Répertorier vos comptes Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3537a-164">List your Data Lake Analytics accounts</span></span>

<span data-ttu-id="3537a-165">Pour tester la connexion, obtenez une liste de vos comptes Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3537a-165">To test the connection, get a list of your Data Lake Analytics accounts.</span></span>

<span data-ttu-id="3537a-166">**Pour répertorier les comptes Data Lake Analytics dans votre abonnement Azure**</span><span class="sxs-lookup"><span data-stu-id="3537a-166">**To list the Data Lake Analytics accounts under your Azure subscription**</span></span>

1. <span data-ttu-id="3537a-167">Sélectionnez Ctrl+Maj+P pour ouvrir la palette de commandes.</span><span class="sxs-lookup"><span data-stu-id="3537a-167">Select Ctrl+Shift+P to open the command palette.</span></span>
2. <span data-ttu-id="3537a-168">Entrez **ADL: List Accounts**.</span><span class="sxs-lookup"><span data-stu-id="3537a-168">Enter **ADL: List Accounts**.</span></span> <span data-ttu-id="3537a-169">Les comptes s’affichent dans le panneau **Sortie**.</span><span class="sxs-lookup"><span data-stu-id="3537a-169">The accounts appear in the **Output** pane.</span></span>

## <a name="open-the-sample-script"></a><span data-ttu-id="3537a-170">Ouvrir l’exemple de script</span><span class="sxs-lookup"><span data-stu-id="3537a-170">Open the sample script</span></span>
<span data-ttu-id="3537a-171">Ouvrez la palette de commandes (Ctrl+Maj+P) et entrez **ADL: Open Sample Script**.</span><span class="sxs-lookup"><span data-stu-id="3537a-171">Open the command palette (Ctrl+Shift+P) and enter **ADL: Open Sample Script**.</span></span> <span data-ttu-id="3537a-172">Une autre instance de cet exemple s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="3537a-172">This opens another instance of this sample.</span></span> <span data-ttu-id="3537a-173">Vous pouvez également modifier, configurer et envoyer un script sur cette instance.</span><span class="sxs-lookup"><span data-stu-id="3537a-173">You can also edit, configure, and submit script on this instance.</span></span>

## <a name="work-with-u-sql"></a><span data-ttu-id="3537a-174">Utilisation de U-SQL</span><span class="sxs-lookup"><span data-stu-id="3537a-174">Work with U-SQL</span></span>

<span data-ttu-id="3537a-175">Vous devez ouvrir un dossier ou un fichier U-SQL pour utiliser U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3537a-175">You need open either a U-SQL file or a folder to work with U-SQL.</span></span>

<span data-ttu-id="3537a-176">**Pour ouvrir un dossier pour votre projet U-SQL**</span><span class="sxs-lookup"><span data-stu-id="3537a-176">**To open a folder for your U-SQL project**</span></span>

1. <span data-ttu-id="3537a-177">À partir de Visual Studio Code, sélectionnez le menu **Fichier**, puis **Ouvrir un dossier**.</span><span class="sxs-lookup"><span data-stu-id="3537a-177">From Visual Studio Code, select the **File** menu, and then select **Open Folder**.</span></span>
2. <span data-ttu-id="3537a-178">Spécifiez un dossier, puis sélectionnez **Sélectionner le dossier**.</span><span class="sxs-lookup"><span data-stu-id="3537a-178">Specify a folder, and then select **Select Folder**.</span></span>
3. <span data-ttu-id="3537a-179">Sélectionnez le menu **Fichier**, puis **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="3537a-179">Select the **File** menu, and then select **New**.</span></span> <span data-ttu-id="3537a-180">Un fichier Untitled-1 est ajouté au projet.</span><span class="sxs-lookup"><span data-stu-id="3537a-180">An Untitled-1 file is added to the project.</span></span>
4. <span data-ttu-id="3537a-181">Entrez le code suivant dans le fichier Untitled-1 :</span><span class="sxs-lookup"><span data-stu-id="3537a-181">Enter the following code into the Untitled-1 file:</span></span>

        @departments  = 
            SELECT * FROM 
                (VALUES
                    (31,    "Sales"),
                    (33,    "Engineering"), 
                    (34,    "Clerical"),
                    (35,    "Marketing")
                ) AS 
                      D( DepID, DepName );
         
        OUTPUT @departments
            TO “/Output/departments.csv”

    <span data-ttu-id="3537a-182">Le script crée un fichier departments.csv avec des données dans le dossier /output.</span><span class="sxs-lookup"><span data-stu-id="3537a-182">The script creates a departments.csv file with some data included in the /output folder.</span></span>

5. <span data-ttu-id="3537a-183">Enregistrez le fichier sous **myUSQL.usql** dans le dossier ouvert.</span><span class="sxs-lookup"><span data-stu-id="3537a-183">Save the file as **myUSQL.usql** in the opened folder.</span></span> <span data-ttu-id="3537a-184">Un fichier de configuration adltools_settings.json est également ajouté au projet.</span><span class="sxs-lookup"><span data-stu-id="3537a-184">A adltools_settings.json configuration file is also added to the project.</span></span>
4. <span data-ttu-id="3537a-185">Ouvrez et configurez le fichier adltools_settings.json avec les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="3537a-185">Open and configure adltools_settings.json with the following properties:</span></span>

    - <span data-ttu-id="3537a-186">Compte : un compte Data Lake Analytics dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="3537a-186">Account:  A Data Lake Analytics account under your Azure subscription.</span></span>
    - <span data-ttu-id="3537a-187">Base de données : une base de données sous votre compte.</span><span class="sxs-lookup"><span data-stu-id="3537a-187">Database: A database under your account.</span></span> <span data-ttu-id="3537a-188">La valeur par défaut est **master**.</span><span class="sxs-lookup"><span data-stu-id="3537a-188">The default is **master**.</span></span>
    - <span data-ttu-id="3537a-189">Schéma : un schéma sous votre base de données.</span><span class="sxs-lookup"><span data-stu-id="3537a-189">Schema: A schema under your database.</span></span> <span data-ttu-id="3537a-190">La valeur par défaut est **dbo**.</span><span class="sxs-lookup"><span data-stu-id="3537a-190">The default is **dbo**.</span></span>
    - <span data-ttu-id="3537a-191">Paramètres facultatifs :</span><span class="sxs-lookup"><span data-stu-id="3537a-191">Optional settings:</span></span>
        - <span data-ttu-id="3537a-192">Priorité : la plage de priorité est comprise entre 1 et 1000. 1 correspond à la priorité la plus élevée.</span><span class="sxs-lookup"><span data-stu-id="3537a-192">Priority: The priority range is from 1 to 1000 with 1 as the highest priority.</span></span> <span data-ttu-id="3537a-193">La valeur par défaut est **1000**.</span><span class="sxs-lookup"><span data-stu-id="3537a-193">The default value is **1000**.</span></span>
        - <span data-ttu-id="3537a-194">Parallélisme : la plage de parallélisme est comprise entre 1 et 150.</span><span class="sxs-lookup"><span data-stu-id="3537a-194">Parallelism: The parallelism range is from 1 to 150.</span></span> <span data-ttu-id="3537a-195">La valeur par défaut est le parallélisme maximal autorisé dans votre compte Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3537a-195">The default value is the maximum parallelism allowed in your Azure Data Lake Analytics account.</span></span> 
        
        > [!NOTE] 
        > <span data-ttu-id="3537a-196">Si les paramètres ne sont pas valides, les valeurs par défaut sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="3537a-196">If the settings are invalid, the default values are used.</span></span>

    ![Fichier de configuration de Data Lake Tools pour Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    <span data-ttu-id="3537a-198">Un compte Data Lake Analytics de calcul est nécessaire pour compiler et exécuter des travaux U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3537a-198">A compute Data Lake Analytics account is needed to compile and run U-SQL jobs.</span></span> <span data-ttu-id="3537a-199">Vous devez configurer le compte d’ordinateur avant de compiler et d’exécuter des travaux U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3537a-199">You must configure the computer account before you can compile and run U-SQL jobs.</span></span>
    
<span data-ttu-id="3537a-200">Une fois la configuration enregistrée, les informations de compte, de base de données et de schéma s’affichent dans la barre d’état dans l’angle inférieur gauche du fichier .usql correspondant.</span><span class="sxs-lookup"><span data-stu-id="3537a-200">After the configuration is saved, the account, database, and schema information appears on the status bar at the bottom-left corner of the corresponding .usql file.</span></span> 
 
 
<span data-ttu-id="3537a-201">Par rapport à l’ouverture d’un fichier, quand vous ouvrez un dossier, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="3537a-201">Compared to opening a file, when you open a folder you can:</span></span>

- <span data-ttu-id="3537a-202">Utiliser un fichier code-behind.</span><span class="sxs-lookup"><span data-stu-id="3537a-202">Use a code-behind file.</span></span> <span data-ttu-id="3537a-203">En mode de fichier unique, code-behind n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3537a-203">In the single-file mode, code-behind is not supported.</span></span>
- <span data-ttu-id="3537a-204">Utiliser un fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="3537a-204">Use a configuration file.</span></span> <span data-ttu-id="3537a-205">Quand vous ouvrez un dossier, les scripts dans le dossier de travail partagent un même fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="3537a-205">When you open a folder, the scripts in the working folder share a single configuration file.</span></span>


<span data-ttu-id="3537a-206">Le script U-SQL est compilé à distance par le biais du service Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3537a-206">The U-SQL script compiles remotely through the Data Lake Analytics service.</span></span> <span data-ttu-id="3537a-207">Quand vous émettez la commande **compile**, le script U-SQL est envoyé à votre compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3537a-207">When you issue the **compile** command, the U-SQL script is sent to your Data Lake Analytics account.</span></span> <span data-ttu-id="3537a-208">Plus tard, Visual Studio Code reçoit le résultat de la compilation.</span><span class="sxs-lookup"><span data-stu-id="3537a-208">Later, Visual Studio Code receives the compilation result.</span></span> <span data-ttu-id="3537a-209">En raison de la compilation à distance, Visual Studio Code impose que vous mentionniez les informations nécessaires à la connexion à votre compte Data Lake Analytics dans le fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="3537a-209">Due to the remote compilation, Visual Studio Code requires that you list the information to connect to your Data Lake Analytics account in the configuration file.</span></span>

<span data-ttu-id="3537a-210">**Pour compiler un script U-SQL**</span><span class="sxs-lookup"><span data-stu-id="3537a-210">**To compile a U-SQL script**</span></span>

1. <span data-ttu-id="3537a-211">Sélectionnez Ctrl+Maj+P pour ouvrir la palette de commandes.</span><span class="sxs-lookup"><span data-stu-id="3537a-211">Select Ctrl+Shift+P to open the command palette.</span></span> 
2. <span data-ttu-id="3537a-212">Entrez **ADL: Compile Script**.</span><span class="sxs-lookup"><span data-stu-id="3537a-212">Enter **ADL: Compile Script**.</span></span> <span data-ttu-id="3537a-213">Les résultats de la compilation s’affichent dans la fenêtre **Output**.</span><span class="sxs-lookup"><span data-stu-id="3537a-213">The compile results appear in the **Output** window.</span></span> <span data-ttu-id="3537a-214">Vous pouvez également cliquer avec le bouton droit sur un fichier de script, puis sélectionnez **ADL: Compile Script** pour compiler un travail U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3537a-214">You can also right-click a script file, and then select **ADL: Compile Script** to compile a U-SQL job.</span></span> <span data-ttu-id="3537a-215">Le résultat de la compilation s’affiche dans le volet **Output**.</span><span class="sxs-lookup"><span data-stu-id="3537a-215">The compilation result appears in the **Output** pane.</span></span>
 

<span data-ttu-id="3537a-216">**Pour envoyer un script U-SQL**</span><span class="sxs-lookup"><span data-stu-id="3537a-216">**To submit a U-SQL script**</span></span>

1. <span data-ttu-id="3537a-217">Sélectionnez Ctrl+Maj+P pour ouvrir la palette de commandes.</span><span class="sxs-lookup"><span data-stu-id="3537a-217">Select Ctrl+Shift+P to open the command palette.</span></span> 
2. <span data-ttu-id="3537a-218">Entrez **ADL: Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="3537a-218">Enter **ADL: Submit Job**.</span></span>  <span data-ttu-id="3537a-219">Vous pouvez également cliquer avec le bouton droit sur un fichier de script, puis sélectionner **ADL: Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="3537a-219">You can also right-click a script file, and then select **ADL: Submit Job**.</span></span> 

<span data-ttu-id="3537a-220">Une fois que vous avez envoyé un travail U-SQL, les journaux d’envoi apparaissent dans la fenêtre **Output** dans VS Code.</span><span class="sxs-lookup"><span data-stu-id="3537a-220">After you submit a U-SQL job, the submission logs appear in the **Output** window in VS Code.</span></span> <span data-ttu-id="3537a-221">Si l’envoi a réussi, l’URL du travail est également affichée.</span><span class="sxs-lookup"><span data-stu-id="3537a-221">If the submission is successful, the job URL appears as well.</span></span> <span data-ttu-id="3537a-222">Vous pouvez ouvrir l’URL du travail dans un navigateur web pour suivre l’état du travail en temps réel.</span><span class="sxs-lookup"><span data-stu-id="3537a-222">You can open the job URL in a web browser to track the real-time job status.</span></span>

<span data-ttu-id="3537a-223">Pour activer la sortie des informations sur le travail, définissez **jobInformationOutputPath** dans le fichier **vs code for the u-sql_settings.json**.</span><span class="sxs-lookup"><span data-stu-id="3537a-223">To enable the output of the job details, set **jobInformationOutputPath** in the **vs code for the u-sql_settings.json** file.</span></span>
 
## <a name="use-a-code-behind-file"></a><span data-ttu-id="3537a-224">Utiliser un fichier code-behind</span><span class="sxs-lookup"><span data-stu-id="3537a-224">Use a code-behind file</span></span>

<span data-ttu-id="3537a-225">Un fichier code-behind est un fichier C# associé à un script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3537a-225">A code-behind file is a C# file associated with a single U-SQL script.</span></span> <span data-ttu-id="3537a-226">Vous pouvez définir un script dédié à UDO, UDA, UDT et UDF dans le fichier code-behind.</span><span class="sxs-lookup"><span data-stu-id="3537a-226">You can define a script dedicated to UDO, UDA, UDT, and UDF in the code-behind file.</span></span> <span data-ttu-id="3537a-227">UDO, UDA, UDT et UDF peuvent être utilisés directement dans le script sans inscription préalable de l’assembly.</span><span class="sxs-lookup"><span data-stu-id="3537a-227">The UDO, UDA, UDT, and UDF can be used directly in the script without registering the assembly first.</span></span> <span data-ttu-id="3537a-228">Le fichier code-behind est placé dans le même dossier que le fichier de script U-SQL correspondant.</span><span class="sxs-lookup"><span data-stu-id="3537a-228">The code-behind file is put in the same folder as its peering U-SQL script file.</span></span> <span data-ttu-id="3537a-229">Si le script est nommé xxx.usql, le fichier code-behind est nommé xxx.usql.cs.</span><span class="sxs-lookup"><span data-stu-id="3537a-229">If the script is named xxx.usql, the code-behind is named as xxx.usql.cs.</span></span> <span data-ttu-id="3537a-230">Si vous supprimez manuellement le fichier code-behind, la fonctionnalité code-behind est désactivée pour le script U-SQL associé.</span><span class="sxs-lookup"><span data-stu-id="3537a-230">If you manually delete the code-behind file, the code-behind feature is disabled for its associated U-SQL script.</span></span> <span data-ttu-id="3537a-231">Pour plus d’informations sur l’écriture de code client pour le script U-SQL, consultez [Écriture et utilisation de code personnalisé dans U-SQL - Fonctions définies par l’utilisateur]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span><span class="sxs-lookup"><span data-stu-id="3537a-231">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL: User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span></span>

<span data-ttu-id="3537a-232">Pour la prise en charge du code-behind, vous devez ouvrir un dossier de travail.</span><span class="sxs-lookup"><span data-stu-id="3537a-232">To support code-behind, you must open a working folder.</span></span> 

<span data-ttu-id="3537a-233">**Pour générer un fichier code-behind**</span><span class="sxs-lookup"><span data-stu-id="3537a-233">**To generate a code-behind file**</span></span>

1. <span data-ttu-id="3537a-234">Ouvrez un fichier source.</span><span class="sxs-lookup"><span data-stu-id="3537a-234">Open a source file.</span></span> 
2. <span data-ttu-id="3537a-235">Sélectionnez Ctrl+Maj+P pour ouvrir la palette de commandes.</span><span class="sxs-lookup"><span data-stu-id="3537a-235">Select Ctrl+Shift+P to open the command palette.</span></span>
3. <span data-ttu-id="3537a-236">Entrez **ADL: Generate Code Behind**.</span><span class="sxs-lookup"><span data-stu-id="3537a-236">Enter **ADL: Generate Code Behind**.</span></span> <span data-ttu-id="3537a-237">Un fichier code-behind est créé dans le même dossier.</span><span class="sxs-lookup"><span data-stu-id="3537a-237">A code-behind file is created in the same folder.</span></span> 

<span data-ttu-id="3537a-238">Vous pouvez également cliquer avec le bouton droit sur un fichier de script, puis sélectionner **ADL: Generate Code Behind**.</span><span class="sxs-lookup"><span data-stu-id="3537a-238">You can also right-click a script file, and then select **ADL: Generate Code Behind**.</span></span> 

<span data-ttu-id="3537a-239">La compilation et l’envoi d’un script U-SQL avec un fichier code-behind s’effectuent exactement comme avec la version autonome du fichier de script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3537a-239">To compile and submit a U-SQL script with a code-behind file is the same as with the standalone U-SQL script file.</span></span>

<span data-ttu-id="3537a-240">Les deux captures d’écran suivantes illustrent un fichier code-behind et le fichier de script U-SQL associé :</span><span class="sxs-lookup"><span data-stu-id="3537a-240">The following two screenshots show a code-behind file and its associated U-SQL script file:</span></span>
 
![Data Lake Tools pour Visual Studio Code - code behind](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Data Lake Tools pour Visual Studio Code - fichier de script code behind](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a><span data-ttu-id="3537a-243">Utiliser les assemblys</span><span class="sxs-lookup"><span data-stu-id="3537a-243">Use assemblies</span></span>

<span data-ttu-id="3537a-244">Pour plus d’informations sur le développement d’assemblys, consultez [Développement d’assemblys U-SQL pour les tâches d’Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="3537a-244">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>

<span data-ttu-id="3537a-245">Vous pouvez utiliser Data Lake Tools pour inscrire des assemblys de code personnalisé dans le catalogue Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3537a-245">You can use Data Lake Tools to register custom code assemblies in the Data Lake Analytics catalog.</span></span>

<span data-ttu-id="3537a-246">**Pour inscrire un assembly**</span><span class="sxs-lookup"><span data-stu-id="3537a-246">**To register an assembly**</span></span>

<span data-ttu-id="3537a-247">Vous pouvez inscrire l’assembly par le biais de la commande **ADL: Register Assembly** ou **ADL: Register Assembly through Configuration**.</span><span class="sxs-lookup"><span data-stu-id="3537a-247">You can register the assembly through the **ADL: Register Assembly** or **ADL: Register Assembly through Configuration** commands.</span></span>

<span data-ttu-id="3537a-248">**Pour inscrire par le biais de la commande ADL: Register Assembly command**</span><span class="sxs-lookup"><span data-stu-id="3537a-248">**To register through the ADL: Register Assembly command**</span></span>
1.  <span data-ttu-id="3537a-249">Sélectionnez Ctrl+Maj+P pour ouvrir la palette de commandes.</span><span class="sxs-lookup"><span data-stu-id="3537a-249">Select Ctrl+Shift+P to open the command palette.</span></span>
2.  <span data-ttu-id="3537a-250">Entrez **ADL: Register Assembly**.</span><span class="sxs-lookup"><span data-stu-id="3537a-250">Enter **ADL: Register Assembly**.</span></span> 
3.  <span data-ttu-id="3537a-251">Spécifiez le chemin d’accès de l’assembly local.</span><span class="sxs-lookup"><span data-stu-id="3537a-251">Specify the local assembly path.</span></span> 
4.  <span data-ttu-id="3537a-252">Sélectionnez un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3537a-252">Select a Data Lake Analytics account.</span></span>
5.  <span data-ttu-id="3537a-253">Sélectionnez une base de données.</span><span class="sxs-lookup"><span data-stu-id="3537a-253">Select a database.</span></span>

<span data-ttu-id="3537a-254">Résultats : le portail s’ouvre dans le navigateur et affiche le processus d’inscription de l’assembly.</span><span class="sxs-lookup"><span data-stu-id="3537a-254">Results: The portal is opened in a browser and displays the assembly registration process.</span></span>  

<span data-ttu-id="3537a-255">Une autre méthode pratique pour déclencher la commande **ADL: Register Assembly** consiste à cliquer avec le bouton droit sur le fichier .dll dans l’Explorateur de fichiers.</span><span class="sxs-lookup"><span data-stu-id="3537a-255">Another convenient way to trigger the **ADL: Register Assembly** command is to right-click the .dll file in File Explorer.</span></span> 

<span data-ttu-id="3537a-256">**Pour inscrire par le biais de la commande ADL: Register Assembly through Configuration**</span><span class="sxs-lookup"><span data-stu-id="3537a-256">**To register though the ADL: Register Assembly through Configuration command**</span></span>
1.  <span data-ttu-id="3537a-257">Sélectionnez Ctrl+Maj+P pour ouvrir la palette de commandes.</span><span class="sxs-lookup"><span data-stu-id="3537a-257">Select Ctrl+Shift+P to open the command palette.</span></span>
2.  <span data-ttu-id="3537a-258">Entrez **ADL: Register Assembly through Configuration**.</span><span class="sxs-lookup"><span data-stu-id="3537a-258">Enter **ADL: Register Assembly through Configuration**.</span></span> 
3.  <span data-ttu-id="3537a-259">Spécifiez le chemin d’accès de l’assembly local.</span><span class="sxs-lookup"><span data-stu-id="3537a-259">Specify the local assembly path.</span></span> 
4.  <span data-ttu-id="3537a-260">Le fichier JSON s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3537a-260">The JSON file is displayed.</span></span> <span data-ttu-id="3537a-261">Examinez et modifiez, si nécessaire, les paramètres des ressources et les dépendances de l’assembly.</span><span class="sxs-lookup"><span data-stu-id="3537a-261">Review and edit the assembly dependencies and resource parameters, if needed.</span></span> <span data-ttu-id="3537a-262">Les instructions s’affichent dans la fenêtre **Output**.</span><span class="sxs-lookup"><span data-stu-id="3537a-262">Instructions are displayed in the **Output** window.</span></span> <span data-ttu-id="3537a-263">Pour procéder à l’inscription de l’assembly, enregistrez (Ctrl+S) le fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="3537a-263">To proceed to the assembly registration, save (Ctrl+S) the JSON file.</span></span>

![Data Lake Tools pour Visual Studio Code - code behind](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- <span data-ttu-id="3537a-265">Dépendances de l’assembly : Azure Data Lake Tools détecte automatiquement si la DLL a des dépendances.</span><span class="sxs-lookup"><span data-stu-id="3537a-265">Assembly dependencies: Azure Data Lake Tools autodetects whether the DLL has any dependencies.</span></span> <span data-ttu-id="3537a-266">Une fois détectées, les dépendances s’affichent dans le fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="3537a-266">The dependencies are displayed in the JSON file after they are detected.</span></span> 
>- <span data-ttu-id="3537a-267">Ressources : vous pouvez charger vos ressources DLL (par exemple .txt, .png et .csv) dans le cadre de l’inscription de l’assembly.</span><span class="sxs-lookup"><span data-stu-id="3537a-267">Resources: You can upload your DLL resources (for example, .txt, .png, and .csv) as part of the assembly registration.</span></span> 

<span data-ttu-id="3537a-268">Une autre méthode pour déclencher la commande **ADL: Register Assembly through Configuration** consiste à cliquer avec le bouton droit sur le fichier .dll dans l’Explorateur de fichiers.</span><span class="sxs-lookup"><span data-stu-id="3537a-268">Another way to trigger the **ADL: Register Assembly through Configuration** command is to right-click the .dll file in File Explorer.</span></span> 

<span data-ttu-id="3537a-269">Le code U-SQL suivant montre comment appeler un assembly.</span><span class="sxs-lookup"><span data-stu-id="3537a-269">The following U-SQL code demonstrates how to call an assembly.</span></span> <span data-ttu-id="3537a-270">Dans l’exemple, le nom de l’assembly est *test*.</span><span class="sxs-lookup"><span data-stu-id="3537a-270">In the sample, the assembly name is *test*.</span></span>

```
REFERENCE ASSEMBLY [test];

@a = 
    EXTRACT 
        Iid int,
    Starts DateTime,
    Region string,
    Query string,
    DwellTime int,
    Results string,
    ClickedUrls string 
    FROM @"Sample/SearchLog.txt" 
    USING Extractors.Tsv();

@d =
    SELECT DISTINCT Region 
    FROM @a;

@d1 = 
    PROCESS @d
    PRODUCE 
        Region string,
    Mkt string
    USING new USQLApplication_codebehind.MyProcessor();

OUTPUT @d1 
    TO @"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-the-data-lake-analytics-catalog"></a><span data-ttu-id="3537a-271">Accès au catalogue Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3537a-271">Access the Data Lake Analytics catalog</span></span>

<span data-ttu-id="3537a-272">Une fois connecté à Azure, vous pouvez utiliser les étapes suivantes pour accéder au catalogue U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3537a-272">After you have connected to Azure, you can use the following steps to access the U-SQL catalog.</span></span>

<span data-ttu-id="3537a-273">**Pour accéder aux métadonnées Azure Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="3537a-273">**To access the Azure Data Lake Analytics metadata**</span></span>

1.  <span data-ttu-id="3537a-274">Sélectionnez Ctrl+Maj+P et entrez **ADL: List Tables**.</span><span class="sxs-lookup"><span data-stu-id="3537a-274">Select Ctrl+Shift+P, and then enter **ADL: List Tables**.</span></span>
2.  <span data-ttu-id="3537a-275">Sélectionnez l’un des comptes Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3537a-275">Select one of the Data Lake Analytics accounts.</span></span>
3.  <span data-ttu-id="3537a-276">Sélectionnez l’une des bases de données Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3537a-276">Select one of the Data Lake Analytics databases.</span></span>
4.  <span data-ttu-id="3537a-277">Sélectionnez l’un des schémas.</span><span class="sxs-lookup"><span data-stu-id="3537a-277">Select one of the schemas.</span></span> <span data-ttu-id="3537a-278">La liste des tables s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3537a-278">You can see the list of tables.</span></span>

## <a name="view-data-lake-analytics-jobs"></a><span data-ttu-id="3537a-279">Afficher les travaux Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3537a-279">View Data Lake Analytics jobs</span></span>

<span data-ttu-id="3537a-280">**Pour afficher les travaux Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="3537a-280">**To view Data Lake Analytics jobs**</span></span>
1.  <span data-ttu-id="3537a-281">Ouvrez la palette de commandes (Ctrl+Maj+P) et sélectionnez **ADL: Show Job**.</span><span class="sxs-lookup"><span data-stu-id="3537a-281">Open the command palette (Ctrl+Shift+P) and select **ADL: Show Job**.</span></span> 
2.  <span data-ttu-id="3537a-282">Sélectionnez un compte local ou Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3537a-282">Select a Data Lake Analytics or local account.</span></span> 
3.  <span data-ttu-id="3537a-283">Attendez que la liste des travaux pour le compte apparaisse.</span><span class="sxs-lookup"><span data-stu-id="3537a-283">Wait for the jobs list for the account to appear.</span></span>
4.  <span data-ttu-id="3537a-284">Sélectionnez un travail dans la liste, Data Lake Tools ouvre les détails du travail dans le portail et affiche le fichier JobInfo dans VS Code.</span><span class="sxs-lookup"><span data-stu-id="3537a-284">Select a job from job list, Data Lake Tools opens the job details in the Azure portal and displays the JobInfo file in VS Code.</span></span>

![Data Lake Tools pour Visual Studio Code - Types d’objets IntelliSense](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a><span data-ttu-id="3537a-286">Intégration d’Azure Data Lake Storage</span><span class="sxs-lookup"><span data-stu-id="3537a-286">Azure Data Lake Storage integration</span></span>

<span data-ttu-id="3537a-287">Vous pouvez utiliser les commandes Azure Data Lake Storage pour :</span><span class="sxs-lookup"><span data-stu-id="3537a-287">You can use Azure Data Lake Storage-related commands to:</span></span>
 - <span data-ttu-id="3537a-288">Parcourir les ressources de stockage Azure Data Lake Storage</span><span class="sxs-lookup"><span data-stu-id="3537a-288">Browse through the Azure Data Lake Storage resources.</span></span> 
 - <span data-ttu-id="3537a-289">Afficher un aperçu du fichier de stockage Azure Data Lake Storage</span><span class="sxs-lookup"><span data-stu-id="3537a-289">Preview the Azure Data Lake Storage file.</span></span>  
 - <span data-ttu-id="3537a-290">Charger le fichier directement sur Azure Data Lake Storage dans VS Code</span><span class="sxs-lookup"><span data-stu-id="3537a-290">Upload the file directly to Azure Data Lake Storage in VS Code.</span></span> 

### <a name="list-the-storage-path"></a><span data-ttu-id="3537a-291">Répertorier le chemin de stockage</span><span class="sxs-lookup"><span data-stu-id="3537a-291">List the storage path</span></span> 
<span data-ttu-id="3537a-292">Vous pouvez répertorier le chemin de stockage par le biais de la palette de commandes ou avec un clic sur le bouton droit.</span><span class="sxs-lookup"><span data-stu-id="3537a-292">You can list the storage path through the command palette or through right-click.</span></span>

<span data-ttu-id="3537a-293">**Pour répertorier le chemin de stockage par le biais de la palette de commandes**</span><span class="sxs-lookup"><span data-stu-id="3537a-293">**To list the storage path through the command palette**</span></span>

1.  <span data-ttu-id="3537a-294">Ouvrez la palette de commandes (Ctrl+Maj+P) et entrez **ADL: List Storage Path**.</span><span class="sxs-lookup"><span data-stu-id="3537a-294">Open the command palette (Ctrl+Shift+P) and enter **ADL: List Storage Path**.</span></span>

    ![Data Lake Tools pour Visual Studio Code - Répertorier le chemin de stockage](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  <span data-ttu-id="3537a-296">Sélectionnez la façon dont vous voulez répertorier le chemin de stockage.</span><span class="sxs-lookup"><span data-stu-id="3537a-296">Select your preferred way for listing the storage path.</span></span> <span data-ttu-id="3537a-297">Cette section utilise **Entrer un chemin d’accès** comme exemple.</span><span class="sxs-lookup"><span data-stu-id="3537a-297">This passage uses **Enter a path** as an example.</span></span>

    ![Data Lake Tools pour Visual Studio Code - Une façon de répertorier le chemin de stockage](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- <span data-ttu-id="3537a-299">VS Code conserve le dernier chemin visité dans chaque compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3537a-299">VS Code keeps the last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="3537a-300">Par exemple : /tt/ss.</span><span class="sxs-lookup"><span data-stu-id="3537a-300">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="3537a-301">Browser from root path : chemin racine de liste à partir de votre compte Data Lake Analytics sélectionné ou un chemin local.</span><span class="sxs-lookup"><span data-stu-id="3537a-301">Browser from root path: The list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="3537a-302">Enter a path : indiquez un chemin spécifié à partir de votre compte Data Lake Analytics sélectionné ou un chemin local.</span><span class="sxs-lookup"><span data-stu-id="3537a-302">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>
    
3. <span data-ttu-id="3537a-303">Sélectionnez un compte à partir du chemin local ou un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3537a-303">Select an account from the local path or a Data Lake Analytics account.</span></span>

    ![Data Lake Tools pour Visual Studio Code - Sélectionner Plus](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. <span data-ttu-id="3537a-305">Sélectionnez **more** pour répertorier davantage de comptes Data Lake Analytics, puis sélectionnez un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3537a-305">Select **more** to list more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

    ![Data Lake Tools pour Visual Studio Code - Sélectionner un compte](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  <span data-ttu-id="3537a-307">Entrez un chemin de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="3537a-307">Enter an Azure storage path.</span></span> <span data-ttu-id="3537a-308">Par exemple : /output.</span><span class="sxs-lookup"><span data-stu-id="3537a-308">For example, /output.</span></span>

    ![Data Lake Tools pour Visual Studio Code - Entrer le chemin de stockage](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  <span data-ttu-id="3537a-310">Résultats : la palette de commandes répertorie les informations sur le chemin en fonction des informations que vous avez entrées.</span><span class="sxs-lookup"><span data-stu-id="3537a-310">Results: The command palette lists the path information based on your entries.</span></span>

    ![Data Lake Tools pour Visual Studio Code - Répertorier le chemin de stockage, résultats](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

<span data-ttu-id="3537a-312">Il est plus pratique d’utiliser le menu contextuel accessible par un clic droit pour répertorier le chemin relatif.</span><span class="sxs-lookup"><span data-stu-id="3537a-312">A more convenient way to list the relative path is through the right-click context menu.</span></span>

<span data-ttu-id="3537a-313">**Pour répertorier le chemin de stockage par le biais d’un clic droit**</span><span class="sxs-lookup"><span data-stu-id="3537a-313">**To list the storage path through right-click**</span></span>

1.  <span data-ttu-id="3537a-314">Cliquez avec le bouton droit sur la chaîne du chemin pour sélectionner **List Storage Path**.</span><span class="sxs-lookup"><span data-stu-id="3537a-314">Right-click the path string to select **List Storage Path**.</span></span>

       ![Data Lake Tools pour Visual Studio Code - Menu contextuel accessible par un clic droit](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. <span data-ttu-id="3537a-316">Le chemin relatif sélectionné apparaît dans la palette de commandes.</span><span class="sxs-lookup"><span data-stu-id="3537a-316">The selected relative path appears in the command palette.</span></span>

   ![Data Lake Tools pour Visual Studio Code - Chemin relatif sélectionné](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  <span data-ttu-id="3537a-318">Sélectionnez un compte à partir du chemin local ou un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3537a-318">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools pour Visual Studio Code - Sélectionner un compte](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  <span data-ttu-id="3537a-320">Résultats : la palette de commandes répertorie les dossiers et les fichiers correspondant au chemin actuel.</span><span class="sxs-lookup"><span data-stu-id="3537a-320">Results: The command palette lists the folders and files for the current path.</span></span>

       ![Data Lake Tools pour Visual Studio Code - Répertorier le chemin actuel](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-the-storage-file"></a><span data-ttu-id="3537a-322">Afficher un aperçu du fichier de stockage</span><span class="sxs-lookup"><span data-stu-id="3537a-322">Preview the storage file</span></span>
<span data-ttu-id="3537a-323">Vous pouvez afficher un aperçu du fichier de stockage par le biais de la palette de commandes ou avec un clic sur le bouton droit.</span><span class="sxs-lookup"><span data-stu-id="3537a-323">You can preview the storage file through the command palette or through right-click.</span></span>

<span data-ttu-id="3537a-324">**Pour afficher un aperçu du fichier de stockage par le biais de la palette de commandes**</span><span class="sxs-lookup"><span data-stu-id="3537a-324">**To preview the storage file through the command palette**</span></span>

1.  <span data-ttu-id="3537a-325">Ouvrez la palette de commandes (Ctrl+Maj+P) et entrez **ADL: Preview Storage File**.</span><span class="sxs-lookup"><span data-stu-id="3537a-325">Open the command palette (Ctrl+Shift+P) and enter **ADL: Preview Storage File**.</span></span>

       ![Data Lake Tools pour Visual Studio Code - Aperçu du fichier de stockage](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  <span data-ttu-id="3537a-327">Sélectionnez un compte à partir du chemin local ou un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3537a-327">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools pour Visual Studio Code - Répertorier un compte](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="3537a-329">Sélectionnez **more** pour répertorier davantage de comptes Data Lake Analytics, puis sélectionnez un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3537a-329">Select **more** to list more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

       ![Data Lake Tools pour Visual Studio Code - Sélectionner un compte](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  <span data-ttu-id="3537a-331">Entrez un fichier ou chemin de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="3537a-331">Enter an Azure storage path or file.</span></span> <span data-ttu-id="3537a-332">Par exemple : /output/SearchLog.txt.</span><span class="sxs-lookup"><span data-stu-id="3537a-332">For example, /output/SearchLog.txt.</span></span>

       ![Data Lake Tools pour Visual Studio Code - Entrer le fichier et le chemin de stockage](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  <span data-ttu-id="3537a-334">Résultats : la palette de commandes répertorie les informations sur le chemin en fonction des informations que vous avez entrées.</span><span class="sxs-lookup"><span data-stu-id="3537a-334">Results: The command palette lists the path information based on your entries.</span></span>

       ![Data Lake Tools pour Visual Studio Code - Aperçu du fichier, résultats](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

<span data-ttu-id="3537a-336">**Pour répertorier le chemin de stockage par le biais d’un clic droit**</span><span class="sxs-lookup"><span data-stu-id="3537a-336">**To list the storage path through right-click**</span></span>

1.  <span data-ttu-id="3537a-337">Pour afficher un aperçu d’un fichier, cliquez avec le bouton droit sur le chemin de fichier.</span><span class="sxs-lookup"><span data-stu-id="3537a-337">To preview a file, right-click the file path.</span></span>

   ![Data Lake Tools pour Visual Studio Code - Menu contextuel accessible par un clic droit](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  <span data-ttu-id="3537a-339">Sélectionnez un compte à partir du chemin local ou un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3537a-339">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools pour Visual Studio Code - Sélectionner un compte](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="3537a-341">Résultats : VS Code affiche les résultats de l’aperçu du fichier.</span><span class="sxs-lookup"><span data-stu-id="3537a-341">Results: VS Code displays the preview results of the file.</span></span>

       ![Data Lake Tools pour Visual Studio Code - Aperçu du fichier, résultats](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a><span data-ttu-id="3537a-343">Charger un fichier</span><span class="sxs-lookup"><span data-stu-id="3537a-343">Upload a file</span></span> 

<span data-ttu-id="3537a-344">Vous pouvez charger des fichiers en entrant la commande **ADL: Upload File** ou **ADL: Upload File through Configuration**.</span><span class="sxs-lookup"><span data-stu-id="3537a-344">You can upload files by entering the commands **ADL: Upload File** or **ADL: Upload File through Configuration**.</span></span>

<span data-ttu-id="3537a-345">**Pour charger des fichiers par le biais de la commande ADL: Upload File**</span><span class="sxs-lookup"><span data-stu-id="3537a-345">**To upload files though the ADL: Upload File command**</span></span>
1. <span data-ttu-id="3537a-346">Sélectionnez sur Ctrl+Maj+P pour ouvrir la palette de commandes ou cliquez avec le bouton droit sur l’éditeur de script, puis entrez **Upload File**.</span><span class="sxs-lookup"><span data-stu-id="3537a-346">Select Ctrl+Shift+P to open the command palette or right-click the script editor, and then enter **Upload File**.</span></span>
2.  <span data-ttu-id="3537a-347">Pour charger le fichier, entrez un chemin local.</span><span class="sxs-lookup"><span data-stu-id="3537a-347">To upload the file, enter a local path.</span></span>

    ![Data Lake Tools pour Visual Studio Code - Entrer un chemin local](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. <span data-ttu-id="3537a-349">Sélectionnez l’une des manières de répertorier le chemin de stockage.</span><span class="sxs-lookup"><span data-stu-id="3537a-349">Select one of the ways of listing the storage path.</span></span> <span data-ttu-id="3537a-350">Cette section utilise **Entrer un chemin d’accès** comme exemple.</span><span class="sxs-lookup"><span data-stu-id="3537a-350">This passage uses **Enter a path** as an example.</span></span>

    ![Data Lake Tools pour Visual Studio Code - Répertorier le chemin de stockage](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- <span data-ttu-id="3537a-352">VS Code conserve le dernier chemin visité dans chaque compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3537a-352">VS Code keeps the last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="3537a-353">Par exemple : /tt/ss.</span><span class="sxs-lookup"><span data-stu-id="3537a-353">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="3537a-354">Browser from root path : chemin racine de liste à partir de votre compte Data Lake Analytics sélectionné ou un chemin local.</span><span class="sxs-lookup"><span data-stu-id="3537a-354">Browser from root path: The list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="3537a-355">Enter a path : indiquez un chemin spécifié à partir de votre compte Data Lake Analytics sélectionné ou un chemin local.</span><span class="sxs-lookup"><span data-stu-id="3537a-355">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>

4. <span data-ttu-id="3537a-356">Sélectionnez un compte à partir du chemin local ou un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3537a-356">Select an account from the local path or a Data Lake Analytics account.</span></span>

    ![Data Lake Tools pour Visual Studio Code - Stockage accessible par un clic droit](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. <span data-ttu-id="3537a-358">Entrez un chemin de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="3537a-358">Enter an Azure storage path.</span></span> <span data-ttu-id="3537a-359">Par exemple : /output.</span><span class="sxs-lookup"><span data-stu-id="3537a-359">For example: /output.</span></span>

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. <span data-ttu-id="3537a-360">Recherchez votre chemin de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="3537a-360">Find your Azure storage path.</span></span> <span data-ttu-id="3537a-361">Sélectionnez **Choisir le dossier actuel**.</span><span class="sxs-lookup"><span data-stu-id="3537a-361">Select **Choose current folder**.</span></span>

    ![Data Lake Tools pour Visual Studio Code - Sélectionner un dossier](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  <span data-ttu-id="3537a-363">Résultats : la fenêtre **Output** affiche l’état de chargement du fichier.</span><span class="sxs-lookup"><span data-stu-id="3537a-363">Results: The **Output** window displays the file upload status.</span></span>

       ![Data Lake Tools pour Visual Studio Code - État du chargement](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

<span data-ttu-id="3537a-365">**Pour charger des fichiers par le biais de la commande ADL: Upload File through Configuration**</span><span class="sxs-lookup"><span data-stu-id="3537a-365">**To upload files though the ADL: Upload File through Configuration command**</span></span>
1.  <span data-ttu-id="3537a-366">Sélectionnez Ctrl+Maj+P pour ouvrir la palette de commandes ou cliquez avec le bouton droit sur l’éditeur de script, puis entrez **Upload File through Configuration**.</span><span class="sxs-lookup"><span data-stu-id="3537a-366">Select Ctrl+Shift+P to open the command palette or right-click the script editor, and then enter **Upload File through Configuration**.</span></span>
2.  <span data-ttu-id="3537a-367">VS Code affiche un fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="3537a-367">VS Code displays a JSON file.</span></span> <span data-ttu-id="3537a-368">Vous pouvez entrer des chemins de fichiers et charger plusieurs fichiers en même temps.</span><span class="sxs-lookup"><span data-stu-id="3537a-368">You can enter file paths and upload multiple files at the same time.</span></span> <span data-ttu-id="3537a-369">Les instructions s’affichent dans la fenêtre **Output**.</span><span class="sxs-lookup"><span data-stu-id="3537a-369">Instructions are displayed in the **Output** window.</span></span> <span data-ttu-id="3537a-370">Pour continuer à charger le fichier, enregistrez (Ctrl+S) le fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="3537a-370">To proceed to upload the file, save (Ctrl+S) the JSON file.</span></span>

       ![Chemin de fichier Data Lake Tools pour Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  <span data-ttu-id="3537a-372">Résultats : la fenêtre **Output** affiche l’état de chargement du fichier.</span><span class="sxs-lookup"><span data-stu-id="3537a-372">Results: The **Output** window displays the file upload status.</span></span>

       ![Data Lake Tools pour Visual Studio Code - État du chargement](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

<span data-ttu-id="3537a-374">Vous pouvez également charger un fichier dans le stockage à l’aide du menu accessible par un clic droit sur le chemin complet du fichier ou le chemin relatif du fichier dans l’éditeur de script.</span><span class="sxs-lookup"><span data-stu-id="3537a-374">Another way to upload a file to storage is through the right-click menu on the file's full path or the file's relative path in the script editor.</span></span> <span data-ttu-id="3537a-375">Entrez le chemin de fichier local, puis sélectionnez le compte.</span><span class="sxs-lookup"><span data-stu-id="3537a-375">Enter the local file path, and then select the account.</span></span> <span data-ttu-id="3537a-376">La fenêtre **Output** affiche l’état du chargement.</span><span class="sxs-lookup"><span data-stu-id="3537a-376">The **Output** window displays the upload status.</span></span> 

### <a name="open-azure-storage-explorer"></a><span data-ttu-id="3537a-377">Ouvrir l’Explorateur de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="3537a-377">Open Azure Storage Explorer</span></span>
<span data-ttu-id="3537a-378">Vous pouvez ouvrir l’**Explorateur de stockage Azure** en entrant la commande **ADL: Open Web Azure Storage Explorer** ou en le sélectionnant dans le menu contextuel accessible par un clic droit.</span><span class="sxs-lookup"><span data-stu-id="3537a-378">You can open **Azure Storage Explorer** by entering the command **ADL: Open Web Azure Storage Explorer** or by selecting it from the right-click context menu.</span></span>

<span data-ttu-id="3537a-379">**Pour ouvrir l’Explorateur de stockage Azure**</span><span class="sxs-lookup"><span data-stu-id="3537a-379">**To open Azure Storage Explorer**</span></span>

1. <span data-ttu-id="3537a-380">Sélectionnez Ctrl+Maj+P pour ouvrir la palette de commandes.</span><span class="sxs-lookup"><span data-stu-id="3537a-380">Select Ctrl+Shift+P to open the command palette.</span></span>
2. <span data-ttu-id="3537a-381">Entrez **Open Web Azure Storage Explorer** ou cliquez avec le bouton droit sur un chemin relatif ou le chemin complet dans l’éditeur de script, puis sélectionnez **Open Web Azure Storage Explorer**.</span><span class="sxs-lookup"><span data-stu-id="3537a-381">Enter **Open Web Azure Storage Explorer** or right-click on a relative path or the full path in the script editor, and then select **Open Web Azure Storage Explorer**.</span></span>
3. <span data-ttu-id="3537a-382">Sélectionnez un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3537a-382">Select a Data Lake Analytics account.</span></span>

<span data-ttu-id="3537a-383">Data Lake Tools ouvre le chemin de stockage Azure dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3537a-383">Data Lake Tools opens the Azure storage path in the Azure portal.</span></span> <span data-ttu-id="3537a-384">Vous pouvez rechercher le chemin et afficher un aperçu du fichier à partir du web.</span><span class="sxs-lookup"><span data-stu-id="3537a-384">You can find the path and preview the file from the web.</span></span>

### <a name="local-run-and-local-debug-for-windows-users"></a><span data-ttu-id="3537a-385">Exécution locale et débogage local pour les utilisateurs de Windows</span><span class="sxs-lookup"><span data-stu-id="3537a-385">Local run and local debug for Windows users</span></span>
<span data-ttu-id="3537a-386">L’exécution locale de U-SQL teste vos données locales et valide votre script localement, avant que votre code soit publié dans Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3537a-386">U-SQL local run tests your local data and validates your script locally, before your code is published to Data Lake Analytics.</span></span> <span data-ttu-id="3537a-387">La fonctionnalité de débogage local vous permet d’effectuer les tâches suivantes avant que votre code soit soumis à Data Lake Analytics :</span><span class="sxs-lookup"><span data-stu-id="3537a-387">The local debug feature enables you to complete the following tasks before your code is submitted to Data Lake Analytics:</span></span> 
- <span data-ttu-id="3537a-388">Déboguer votre code-behind C#</span><span class="sxs-lookup"><span data-stu-id="3537a-388">Debug your C# code-behind.</span></span> 
- <span data-ttu-id="3537a-389">Examiner le code</span><span class="sxs-lookup"><span data-stu-id="3537a-389">Step through the code.</span></span> 
- <span data-ttu-id="3537a-390">Valider votre script localement</span><span class="sxs-lookup"><span data-stu-id="3537a-390">Validate your script locally.</span></span>

<span data-ttu-id="3537a-391">Pour obtenir des instructions sur l’exécution locale et le débogage local, consultez [Exécution locale et débogage local U-SQL avec Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="3537a-391">For instructions on local run and local debug, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>

## <a name="additional-features"></a><span data-ttu-id="3537a-392">Fonctionnalités supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3537a-392">Additional features</span></span>

<span data-ttu-id="3537a-393">Data Lake Tools pour VS Code prend en charge les fonctionnalités suivantes :</span><span class="sxs-lookup"><span data-stu-id="3537a-393">Data Lake Tools for VS Code supports the following features:</span></span>

-   <span data-ttu-id="3537a-394">Saisie semi-automatique IntelliSense : des suggestions s’affichent dans des fenêtres indépendantes autour des éléments tels que les mots clés, les méthodes et les variables.</span><span class="sxs-lookup"><span data-stu-id="3537a-394">IntelliSense auto-complete: Suggestions appear in pop-up windows around items, such as keywords, methods, and variables.</span></span> <span data-ttu-id="3537a-395">Des icônes différentes représentent des types d’objets différents :</span><span class="sxs-lookup"><span data-stu-id="3537a-395">Different icons represent different types of the objects:</span></span>

    - <span data-ttu-id="3537a-396">Type de données Scala</span><span class="sxs-lookup"><span data-stu-id="3537a-396">Scala data type</span></span>
    - <span data-ttu-id="3537a-397">Type de données complexe</span><span class="sxs-lookup"><span data-stu-id="3537a-397">Complex data type</span></span>
    - <span data-ttu-id="3537a-398">Types définis par l’utilisateur (UDT) intégrés</span><span class="sxs-lookup"><span data-stu-id="3537a-398">Built-in UDTs</span></span>
    - <span data-ttu-id="3537a-399">Classes et collection .NET</span><span class="sxs-lookup"><span data-stu-id="3537a-399">.NET collection and classes</span></span>
    - <span data-ttu-id="3537a-400">Expressions C#</span><span class="sxs-lookup"><span data-stu-id="3537a-400">C# expressions</span></span>
    - <span data-ttu-id="3537a-401">UDF, UDO et UDAAG C# intégrés</span><span class="sxs-lookup"><span data-stu-id="3537a-401">Built-in C# UDFs, UDOs, and UDAAGs</span></span> 
    - <span data-ttu-id="3537a-402">Fonctions U-SQL</span><span class="sxs-lookup"><span data-stu-id="3537a-402">U-SQL functions</span></span>
    - <span data-ttu-id="3537a-403">Fonction de fenêtrage U-SQL</span><span class="sxs-lookup"><span data-stu-id="3537a-403">U-SQL windowing function</span></span>
 
    ![Data Lake Tools pour Visual Studio Code - Types d’objets IntelliSense](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   <span data-ttu-id="3537a-405">Saisie semi-automatique IntelliSense sur les métadonnées Data Lake Analytics : Data Lake Tools télécharge les informations de métadonnées Data Lake Analytics localement.</span><span class="sxs-lookup"><span data-stu-id="3537a-405">IntelliSense auto-complete on Data Lake Analytics metadata: Data Lake Tools downloads the Data Lake Analytics metadata information locally.</span></span> <span data-ttu-id="3537a-406">La fonctionnalité IntelliSense remplit automatiquement les objets, notamment les bases de données, les schémas, les tables, les vues, les fonctions table, les procédures et les assemblys C# à partir des métadonnées Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3537a-406">The IntelliSense feature automatically populates objects, including the database, schema, table, view, table-valued function, procedures, and C# assemblies, from the Data Lake Analytics metadata.</span></span>
 
    ![Data Lake Tools pour Visual Studio Code - Métadonnées IntelliSense](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   <span data-ttu-id="3537a-408">Marqueur d’erreur IntelliSense : Data Lake Tools souligne les erreurs d’édition pour U-SQL et C#.</span><span class="sxs-lookup"><span data-stu-id="3537a-408">IntelliSense error marker: Data Lake Tools underlines the editing errors for U-SQL and C#.</span></span> 
-   <span data-ttu-id="3537a-409">Coloration syntaxique : Data Lake Tools utilise différentes couleurs pour différencier les éléments tels que les variables, les mots clés, les types de données et les fonctions.</span><span class="sxs-lookup"><span data-stu-id="3537a-409">Syntax highlights: Data Lake Tools uses different colors to differentiate items, such as variables, keywords, data type, and functions.</span></span> 

    ![Data Lake Tools pour Visual Studio Code - Points clés de la syntaxe](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a><span data-ttu-id="3537a-411">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3537a-411">Next steps</span></span>

- <span data-ttu-id="3537a-412">Pour l’exécution locale et le débogage local U-SQL avec Visual Studio Code, consultez [Exécution locale et débogage local U-SQL avec Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="3537a-412">For U-SQL local run and local debug with Visual Studio Code, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>
- <span data-ttu-id="3537a-413">Pour obtenir des informations sur la prise en main de Data Lake Analytics, consultez [Didacticiel : bien démarrer avec Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3537a-413">For getting-started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="3537a-414">Pour obtenir des informations sur l’utilisation de Data Lake Tools pour Visual Studio, consultez [Didacticiel : développer des scripts U-SQL avec Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3537a-414">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="3537a-415">Pour plus d’informations sur le développement d’assemblys, consultez [Développement d’assemblys U-SQL pour les tâches d’Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="3537a-415">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>



