---
title: "Azure Data Lake Tools : Utiliser Azure Data Lake Tools pour Visual Studio Code | Microsoft Docs"
description: "Découvrez comment toouse Azure Data Lake Tools pour Visual Studio Code toocreate, tester et exécuter des scripts U-SQL. "
Keywords: "Chemin d’accès de le toostorage de téléchargement VScode, Azure Data Lake Tools, exécution, le fichier de stockage débogage Local, le débogage Local, version d’évaluation locale"
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
ms.openlocfilehash: 77771c5d5dae3bfce4ad2df240ea6c6ef848f288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a><span data-ttu-id="28277-104">Utiliser Azure Data Lake Tools pour Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="28277-104">Use Azure Data Lake Tools for Visual Studio Code</span></span>

<span data-ttu-id="28277-105">Découvrez comment toouse Azure Data Lake Tools pour Visual Studio Code (Code de Visual Studio), toocreate, tester et exécuter des scripts U-SQL.</span><span class="sxs-lookup"><span data-stu-id="28277-105">Learn how toouse Azure Data Lake Tools for Visual Studio Code (VS Code) toocreate, test, and run U-SQL scripts.</span></span> <span data-ttu-id="28277-106">informations de Hello sont également décrite dans hello suivant vidéo :</span><span class="sxs-lookup"><span data-stu-id="28277-106">hello information is also covered in hello following video:</span></span>

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a><span data-ttu-id="28277-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="28277-107">Prerequisites</span></span>

<span data-ttu-id="28277-108">Outils de LAC de données peuvent être installés sur les plateformes hello pris en charge par le Code de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="28277-108">Data Lake Tools can be installed on hello platforms supported by VS Code.</span></span> <span data-ttu-id="28277-109">les plateformes de Hello pris en charge incluent Windows, Linux et MacOS.</span><span class="sxs-lookup"><span data-stu-id="28277-109">hello supported platforms include Windows, Linux, and MacOS.</span></span> <span data-ttu-id="28277-110">différentes plateformes de Hello ont hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="28277-110">hello different platforms have hello following prerequisites:</span></span>

- <span data-ttu-id="28277-111">Windows</span><span class="sxs-lookup"><span data-stu-id="28277-111">Windows</span></span>

    - <span data-ttu-id="28277-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="28277-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="28277-113">[Java SE Runtime Environment version 8 mise à jour 77 ou ultérieure](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="28277-113">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="28277-114">Ajoutez hello java.exe chemin d’accès toohello système variable d’environnement path.</span><span class="sxs-lookup"><span data-stu-id="28277-114">Add hello java.exe path toohello system environment variable path.</span></span> <span data-ttu-id="28277-115">Pour obtenir des instructions de configuration, consultez [comment définir ou modifier la variable système Path hello ?]( https://www.java.com/download/help/path.xml).</span><span class="sxs-lookup"><span data-stu-id="28277-115">For configuration instructions, see [How do I set or change hello Path system variable?]( https://www.java.com/download/help/path.xml).</span></span> <span data-ttu-id="28277-116">chemin d’accès Hello est tooC:\Program Files\Java\jdk1.8.0_77\jre\bin similaire.</span><span class="sxs-lookup"><span data-stu-id="28277-116">hello path is similar tooC:\Program Files\Java\jdk1.8.0_77\jre\bin.</span></span>
    - <span data-ttu-id="28277-117">[Kit SDK .NET Core 1.0.3 ou runtime .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="28277-117">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
    
- <span data-ttu-id="28277-118">Linux (nous recommandons Ubuntu 14.04 LTS)</span><span class="sxs-lookup"><span data-stu-id="28277-118">Linux (We recommend Ubuntu 14.04 LTS)</span></span>

    - <span data-ttu-id="28277-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="28277-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span> <span data-ttu-id="28277-120">tooinstall hello code, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="28277-120">tooinstall hello code, enter hello following command:</span></span>

              sudo dpkg -i code_<version_number>_amd64.deb

    - <span data-ttu-id="28277-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span><span class="sxs-lookup"><span data-stu-id="28277-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span></span> 

        - <span data-ttu-id="28277-122">package de deb hello tooupdate source, entrez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="28277-122">tooupdate hello deb package source, enter hello following commands:</span></span>

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - <span data-ttu-id="28277-123">tooinstall Mono, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="28277-123">tooinstall Mono, enter hello following command:</span></span>

                sudo apt-get install mono-complete

            > [!NOTE] 
            > <span data-ttu-id="28277-124">Mono 4.6 n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="28277-124">Mono 4.6 is not supported.</span></span> <span data-ttu-id="28277-125">Désinstallez entièrement la version 4.6 avant d’installer la version 4.2.x.</span><span class="sxs-lookup"><span data-stu-id="28277-125">Uninstall version 4.6 entirely before you install 4.2.x.</span></span>  

        - <span data-ttu-id="28277-126">[Java SE Runtime Environment version 8 mise à jour 77 ou ultérieure](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="28277-126">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="28277-127">Pour obtenir des instructions sur l’installation, consultez hello [des instructions d’installation Linux 64 bits pour Java]( https://java.com/en/download/help/linux_x64_install.xml) page.</span><span class="sxs-lookup"><span data-stu-id="28277-127">For instructions on installation, see hello [Linux 64-bit installation instructions for Java]( https://java.com/en/download/help/linux_x64_install.xml) page.</span></span>
        - <span data-ttu-id="28277-128">[Kit SDK .NET Core 1.0.3 ou runtime .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="28277-128">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
- <span data-ttu-id="28277-129">MacOS</span><span class="sxs-lookup"><span data-stu-id="28277-129">MacOS</span></span>

    - <span data-ttu-id="28277-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="28277-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="28277-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span><span class="sxs-lookup"><span data-stu-id="28277-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span></span> 
    - <span data-ttu-id="28277-132">[Java SE Runtime Environment version 8 mise à jour 77 ou ultérieure](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="28277-132">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="28277-133">Pour obtenir des instructions sur l’installation, consultez hello [des instructions d’installation Linux 64 bits pour Java](https://java.com/en/download/help/mac_install.xml) page.</span><span class="sxs-lookup"><span data-stu-id="28277-133">For instructions on installation, see hello [Linux 64-bit installation instructions for Java](https://java.com/en/download/help/mac_install.xml) page.</span></span>
    - <span data-ttu-id="28277-134">[Kit SDK .NET Core 1.0.3 ou runtime .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="28277-134">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>

## <a name="install-data-lake-tools"></a><span data-ttu-id="28277-135">Installer Data Lake Tools</span><span class="sxs-lookup"><span data-stu-id="28277-135">Install Data Lake Tools</span></span>

<span data-ttu-id="28277-136">Après avoir installé les composants requis de hello, vous pouvez installer les outils de LAC de données pour le Code de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="28277-136">After you install hello prerequisites, you can install Data Lake Tools for VS Code.</span></span>

<span data-ttu-id="28277-137">**tooinstall Data Lake Tools**</span><span class="sxs-lookup"><span data-stu-id="28277-137">**tooinstall Data Lake Tools**</span></span>

1. <span data-ttu-id="28277-138">Ouvrez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="28277-138">Open Visual Studio Code.</span></span>
2. <span data-ttu-id="28277-139">Sélectionnez Ctrl + P et entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="28277-139">Select Ctrl+P, and then enter hello following command:</span></span>
```
ext install usql-vscode-ext
```
<span data-ttu-id="28277-140">Une liste des extensions de code Visual Studio s’affiche.</span><span class="sxs-lookup"><span data-stu-id="28277-140">You can see a list of Visual Studio code extensions.</span></span> <span data-ttu-id="28277-141">L’une d’elles est **Azure Data Lake Tools**.</span><span class="sxs-lookup"><span data-stu-id="28277-141">One of them is **Azure Data Lake Tools**.</span></span>

3. <span data-ttu-id="28277-142">Sélectionnez **installer** suivant trop**Azure Data Lake Tools**.</span><span class="sxs-lookup"><span data-stu-id="28277-142">Select **Install** next too**Azure Data Lake Tools**.</span></span> <span data-ttu-id="28277-143">Après quelques secondes, hello **installer** bouton modifications trop**recharger**.</span><span class="sxs-lookup"><span data-stu-id="28277-143">After a few seconds, hello **Install** button changes too**Reload**.</span></span>
4. <span data-ttu-id="28277-144">Sélectionnez **recharger** extension de hello tooactivate.</span><span class="sxs-lookup"><span data-stu-id="28277-144">Select **Reload** tooactivate hello extension.</span></span>
5. <span data-ttu-id="28277-145">Sélectionnez **OK** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="28277-145">Select **OK** tooconfirm.</span></span> <span data-ttu-id="28277-146">Vous pouvez voir Azure Data Lake Tools Bonjour **Extensions** volet.</span><span class="sxs-lookup"><span data-stu-id="28277-146">You can see Azure Data Lake Tools in hello **Extensions** pane.</span></span>
    <span data-ttu-id="28277-147">![Volet Extensions de Data Lake Tools pour Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span><span class="sxs-lookup"><span data-stu-id="28277-147">![Data Lake Tools for Visual Studio Code Extensions pane](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span></span>

## <a name="activate-azure-data-lake-tools"></a><span data-ttu-id="28277-148">Activer Azure Data Lake Tools</span><span class="sxs-lookup"><span data-stu-id="28277-148">Activate Azure Data Lake Tools</span></span>
<span data-ttu-id="28277-149">Créer un nouveau fichier .usql ou ouvrir une extension .usql fichier tooactivate hello.</span><span class="sxs-lookup"><span data-stu-id="28277-149">Create a new .usql file or open an existing .usql file tooactivate hello extension.</span></span> 

## <a name="connect-tooazure"></a><span data-ttu-id="28277-150">Se connecter tooAzure</span><span class="sxs-lookup"><span data-stu-id="28277-150">Connect tooAzure</span></span>

<span data-ttu-id="28277-151">Avant de pouvoir compiler et exécuter des scripts U-SQL dans Analytique lac de données, vous devez vous connecter tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="28277-151">Before you can compile and run U-SQL scripts in Data Lake Analytics, you must connect tooyour Azure account.</span></span>

<span data-ttu-id="28277-152">**tooconnect tooAzure**</span><span class="sxs-lookup"><span data-stu-id="28277-152">**tooconnect tooAzure**</span></span>

1.  <span data-ttu-id="28277-153">Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="28277-153">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2.  <span data-ttu-id="28277-154">Entrez **ADL: Login**.</span><span class="sxs-lookup"><span data-stu-id="28277-154">Enter **ADL: Login**.</span></span> <span data-ttu-id="28277-155">les informations de connexion Hello s’affiche dans hello **sortie** volet.</span><span class="sxs-lookup"><span data-stu-id="28277-155">hello login information appears in hello **Output** pane.</span></span>

    <span data-ttu-id="28277-156">![Palette de commandes de Data Lake Tools pour Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Informations de connexion d’appareil Data Lake Tools pour Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span><span class="sxs-lookup"><span data-stu-id="28277-156">![Data Lake Tools for Visual Studio Code command palette](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
![Data Lake Tools for Visual Studio Code device login information](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span></span>
3. <span data-ttu-id="28277-157">Sélectionnez Ctrl + clic sur l’URL de connexion hello : page de connexion Web https://aka.ms/devicelogin tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="28277-157">Select Ctrl+click on hello login URL: https://aka.ms/devicelogin tooopen hello login webpage.</span></span> <span data-ttu-id="28277-158">Entrez le code de hello **G567LX42V** dans la zone de texte hello et sélectionnez **continuer**.</span><span class="sxs-lookup"><span data-stu-id="28277-158">Enter hello code **G567LX42V** into hello text box, and then select **Continue**.</span></span>

   ![Data Lake Tools pour Visual Studio Code - Coller le code de connexion](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  <span data-ttu-id="28277-160">Suivez toosign d’instructions hello dans à partir de la page Web de hello.</span><span class="sxs-lookup"><span data-stu-id="28277-160">Follow hello instructions toosign in from hello webpage.</span></span> <span data-ttu-id="28277-161">Lorsque vous êtes connecté, le nom de votre compte Azure s’affiche sur la barre d’état hello dans le coin inférieur gauche de hello Hello **VS Code** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="28277-161">When you're connected, your Azure account name appears on hello status bar in hello lower-left corner of hello **VS Code** window.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="28277-162">Si votre compte a deux facteurs activés, nous vous recommandons d’utiliser l’authentification par téléphone plutôt qu’un code PIN.</span><span class="sxs-lookup"><span data-stu-id="28277-162">If your account has two factors enabled, we recommend that you use phone authentication rather than using a PIN.</span></span>

<span data-ttu-id="28277-163">toosign, entrez la commande hello **ADL : déconnexion**.</span><span class="sxs-lookup"><span data-stu-id="28277-163">toosign out, enter hello command **ADL: Logout**.</span></span>

## <a name="list-your-data-lake-analytics-accounts"></a><span data-ttu-id="28277-164">Répertorier vos comptes Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="28277-164">List your Data Lake Analytics accounts</span></span>

<span data-ttu-id="28277-165">connexion de hello tootest, obtenir une liste de vos comptes Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="28277-165">tootest hello connection, get a list of your Data Lake Analytics accounts.</span></span>

<span data-ttu-id="28277-166">**comptes d’Analytique lac de données toolist hello sous votre abonnement Azure**</span><span class="sxs-lookup"><span data-stu-id="28277-166">**toolist hello Data Lake Analytics accounts under your Azure subscription**</span></span>

1. <span data-ttu-id="28277-167">Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="28277-167">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2. <span data-ttu-id="28277-168">Entrez **ADL: List Accounts**.</span><span class="sxs-lookup"><span data-stu-id="28277-168">Enter **ADL: List Accounts**.</span></span> <span data-ttu-id="28277-169">Hello apparaissent dans hello **sortie** volet.</span><span class="sxs-lookup"><span data-stu-id="28277-169">hello accounts appear in hello **Output** pane.</span></span>

## <a name="open-hello-sample-script"></a><span data-ttu-id="28277-170">Exemple de script hello ouvert</span><span class="sxs-lookup"><span data-stu-id="28277-170">Open hello sample script</span></span>
<span data-ttu-id="28277-171">Ouvrez la palette de commandes hello (Ctrl + Maj + P), puis entrez **ADL : exemple de Script Open**.</span><span class="sxs-lookup"><span data-stu-id="28277-171">Open hello command palette (Ctrl+Shift+P) and enter **ADL: Open Sample Script**.</span></span> <span data-ttu-id="28277-172">Une autre instance de cet exemple s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="28277-172">This opens another instance of this sample.</span></span> <span data-ttu-id="28277-173">Vous pouvez également modifier, configurer et envoyer un script sur cette instance.</span><span class="sxs-lookup"><span data-stu-id="28277-173">You can also edit, configure, and submit script on this instance.</span></span>

## <a name="work-with-u-sql"></a><span data-ttu-id="28277-174">Utilisation de U-SQL</span><span class="sxs-lookup"><span data-stu-id="28277-174">Work with U-SQL</span></span>

<span data-ttu-id="28277-175">Vous devez ouvrir un fichier U-SQL ou un dossier toowork avec U-SQL.</span><span class="sxs-lookup"><span data-stu-id="28277-175">You need open either a U-SQL file or a folder toowork with U-SQL.</span></span>

<span data-ttu-id="28277-176">**tooopen un dossier pour votre projet U-SQL**</span><span class="sxs-lookup"><span data-stu-id="28277-176">**tooopen a folder for your U-SQL project**</span></span>

1. <span data-ttu-id="28277-177">À partir du Code Visual Studio, sélectionnez hello **fichier** menu, puis sélectionnez **ouvrir le dossier**.</span><span class="sxs-lookup"><span data-stu-id="28277-177">From Visual Studio Code, select hello **File** menu, and then select **Open Folder**.</span></span>
2. <span data-ttu-id="28277-178">Spécifiez un dossier, puis sélectionnez **Sélectionner le dossier**.</span><span class="sxs-lookup"><span data-stu-id="28277-178">Specify a folder, and then select **Select Folder**.</span></span>
3. <span data-ttu-id="28277-179">Sélectionnez hello **fichier** menu, puis sélectionnez **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="28277-179">Select hello **File** menu, and then select **New**.</span></span> <span data-ttu-id="28277-180">Un fichier sans titre-1 est ajouté toohello projet.</span><span class="sxs-lookup"><span data-stu-id="28277-180">An Untitled-1 file is added toohello project.</span></span>
4. <span data-ttu-id="28277-181">Entrez hello après le code dans le fichier de hello sans titre-1 :</span><span class="sxs-lookup"><span data-stu-id="28277-181">Enter hello following code into hello Untitled-1 file:</span></span>

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

    <span data-ttu-id="28277-182">script de Hello crée un fichier de departments.csv avec des données incluses dans le dossier de Start hello.</span><span class="sxs-lookup"><span data-stu-id="28277-182">hello script creates a departments.csv file with some data included in hello /output folder.</span></span>

5. <span data-ttu-id="28277-183">Enregistrer le fichier hello sous **myUSQL.usql** Bonjour dossier ouvert.</span><span class="sxs-lookup"><span data-stu-id="28277-183">Save hello file as **myUSQL.usql** in hello opened folder.</span></span> <span data-ttu-id="28277-184">Un fichier de configuration adltools_settings.json est également ajouté toohello projet.</span><span class="sxs-lookup"><span data-stu-id="28277-184">A adltools_settings.json configuration file is also added toohello project.</span></span>
4. <span data-ttu-id="28277-185">Ouvrez et configurez adltools_settings.json avec hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="28277-185">Open and configure adltools_settings.json with hello following properties:</span></span>

    - <span data-ttu-id="28277-186">Compte : un compte Data Lake Analytics dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="28277-186">Account:  A Data Lake Analytics account under your Azure subscription.</span></span>
    - <span data-ttu-id="28277-187">Base de données : une base de données sous votre compte.</span><span class="sxs-lookup"><span data-stu-id="28277-187">Database: A database under your account.</span></span> <span data-ttu-id="28277-188">valeur par défaut Hello est **master**.</span><span class="sxs-lookup"><span data-stu-id="28277-188">hello default is **master**.</span></span>
    - <span data-ttu-id="28277-189">Schéma : un schéma sous votre base de données.</span><span class="sxs-lookup"><span data-stu-id="28277-189">Schema: A schema under your database.</span></span> <span data-ttu-id="28277-190">valeur par défaut Hello est **dbo**.</span><span class="sxs-lookup"><span data-stu-id="28277-190">hello default is **dbo**.</span></span>
    - <span data-ttu-id="28277-191">Paramètres facultatifs :</span><span class="sxs-lookup"><span data-stu-id="28277-191">Optional settings:</span></span>
        - <span data-ttu-id="28277-192">Priorité : plage de priorité hello est de 1 too1000 avec 1 comme priorité la plus élevée de hello.</span><span class="sxs-lookup"><span data-stu-id="28277-192">Priority: hello priority range is from 1 too1000 with 1 as hello highest priority.</span></span> <span data-ttu-id="28277-193">la valeur par défaut Hello est **1000**.</span><span class="sxs-lookup"><span data-stu-id="28277-193">hello default value is **1000**.</span></span>
        - <span data-ttu-id="28277-194">Parallélisme : plage de parallélisme hello est de 1 too150.</span><span class="sxs-lookup"><span data-stu-id="28277-194">Parallelism: hello parallelism range is from 1 too150.</span></span> <span data-ttu-id="28277-195">valeur par défaut de Hello est hello maximal parallélisme autorisé dans votre compte Analytique de LAC de données Azure.</span><span class="sxs-lookup"><span data-stu-id="28277-195">hello default value is hello maximum parallelism allowed in your Azure Data Lake Analytics account.</span></span> 
        
        > [!NOTE] 
        > <span data-ttu-id="28277-196">Si les paramètres hello ne sont pas valides, les valeurs par défaut de hello sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="28277-196">If hello settings are invalid, hello default values are used.</span></span>

    ![Fichier de configuration de Data Lake Tools pour Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    <span data-ttu-id="28277-198">Un calcul Analytique lac de données compte est nécessaire toocompile et exécuter les tâches de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="28277-198">A compute Data Lake Analytics account is needed toocompile and run U-SQL jobs.</span></span> <span data-ttu-id="28277-199">Vous devez configurer le compte d’ordinateur hello avant de pouvoir compiler et exécuter des travaux U-SQL.</span><span class="sxs-lookup"><span data-stu-id="28277-199">You must configure hello computer account before you can compile and run U-SQL jobs.</span></span>
    
<span data-ttu-id="28277-200">Après que la configuration de hello est enregistrée, les informations de compte, de base de données et de schéma hello s’affiche sur la barre d’état hello en hello en bas à gauche du fichier de .usql hello correspondant.</span><span class="sxs-lookup"><span data-stu-id="28277-200">After hello configuration is saved, hello account, database, and schema information appears on hello status bar at hello bottom-left corner of hello corresponding .usql file.</span></span> 
 
 
<span data-ttu-id="28277-201">Comparés tooopening un fichier, lorsque vous ouvrez un dossier, que vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="28277-201">Compared tooopening a file, when you open a folder you can:</span></span>

- <span data-ttu-id="28277-202">Utiliser un fichier code-behind.</span><span class="sxs-lookup"><span data-stu-id="28277-202">Use a code-behind file.</span></span> <span data-ttu-id="28277-203">En mode de fichier unique hello, code-behind n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="28277-203">In hello single-file mode, code-behind is not supported.</span></span>
- <span data-ttu-id="28277-204">Utiliser un fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="28277-204">Use a configuration file.</span></span> <span data-ttu-id="28277-205">Lorsque vous ouvrez un dossier, les scripts hello Bonjour dossier de travail partagent un seul fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="28277-205">When you open a folder, hello scripts in hello working folder share a single configuration file.</span></span>


<span data-ttu-id="28277-206">Hello script U-SQL compile à distance via le service de données Lake Analytique de hello.</span><span class="sxs-lookup"><span data-stu-id="28277-206">hello U-SQL script compiles remotely through hello Data Lake Analytics service.</span></span> <span data-ttu-id="28277-207">Lorsque vous émettez hello **compiler** hello script U-SQL est envoyé de compte de tooyour Analytique lac de données de la commande.</span><span class="sxs-lookup"><span data-stu-id="28277-207">When you issue hello **compile** command, hello U-SQL script is sent tooyour Data Lake Analytics account.</span></span> <span data-ttu-id="28277-208">Une version ultérieure, Visual Studio Code reçoit de résultat de la compilation hello.</span><span class="sxs-lookup"><span data-stu-id="28277-208">Later, Visual Studio Code receives hello compilation result.</span></span> <span data-ttu-id="28277-209">En raison de la compilation à distance de toohello, Code de Visual Studio requiert que vous répertoriez les informations de hello tooconnect tooyour Analytique lac de données de compte dans le fichier de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="28277-209">Due toohello remote compilation, Visual Studio Code requires that you list hello information tooconnect tooyour Data Lake Analytics account in hello configuration file.</span></span>

<span data-ttu-id="28277-210">**script de toocompile U-SQL**</span><span class="sxs-lookup"><span data-stu-id="28277-210">**toocompile a U-SQL script**</span></span>

1. <span data-ttu-id="28277-211">Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="28277-211">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2. <span data-ttu-id="28277-212">Entrez **ADL: Compile Script**.</span><span class="sxs-lookup"><span data-stu-id="28277-212">Enter **ADL: Compile Script**.</span></span> <span data-ttu-id="28277-213">Hello compilation résultats s’affichent dans hello **sortie** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="28277-213">hello compile results appear in hello **Output** window.</span></span> <span data-ttu-id="28277-214">Vous pouvez également cliquez sur un fichier de script, puis sélectionnez **ADL : Script de compilation** toocompile U-SQL travail.</span><span class="sxs-lookup"><span data-stu-id="28277-214">You can also right-click a script file, and then select **ADL: Compile Script** toocompile a U-SQL job.</span></span> <span data-ttu-id="28277-215">résultat de la compilation Hello s’affiche dans hello **sortie** volet.</span><span class="sxs-lookup"><span data-stu-id="28277-215">hello compilation result appears in hello **Output** pane.</span></span>
 

<span data-ttu-id="28277-216">**script de toosubmit U-SQL**</span><span class="sxs-lookup"><span data-stu-id="28277-216">**toosubmit a U-SQL script**</span></span>

1. <span data-ttu-id="28277-217">Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="28277-217">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2. <span data-ttu-id="28277-218">Entrez **ADL: Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="28277-218">Enter **ADL: Submit Job**.</span></span>  <span data-ttu-id="28277-219">Vous pouvez également cliquer avec le bouton droit sur un fichier de script, puis sélectionner **ADL: Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="28277-219">You can also right-click a script file, and then select **ADL: Submit Job**.</span></span> 

<span data-ttu-id="28277-220">Une fois que vous envoyez un travail U-SQL, les journaux de soumission de hello s’affichent dans hello **sortie** fenêtre dans VS Code.</span><span class="sxs-lookup"><span data-stu-id="28277-220">After you submit a U-SQL job, hello submission logs appear in hello **Output** window in VS Code.</span></span> <span data-ttu-id="28277-221">Si l’envoi de hello est réussie, hello travail URL s’affiche également.</span><span class="sxs-lookup"><span data-stu-id="28277-221">If hello submission is successful, hello job URL appears as well.</span></span> <span data-ttu-id="28277-222">Vous pouvez ouvrir les URL de tâche hello dans un état de travail en temps réel web navigateur tootrack hello.</span><span class="sxs-lookup"><span data-stu-id="28277-222">You can open hello job URL in a web browser tootrack hello real-time job status.</span></span>

<span data-ttu-id="28277-223">sortie de hello tooenable des détails d’une tâche hello, définissez **jobInformationOutputPath** Bonjour **vs code pour hello u-sql_settings.json** fichier.</span><span class="sxs-lookup"><span data-stu-id="28277-223">tooenable hello output of hello job details, set **jobInformationOutputPath** in hello **vs code for hello u-sql_settings.json** file.</span></span>
 
## <a name="use-a-code-behind-file"></a><span data-ttu-id="28277-224">Utiliser un fichier code-behind</span><span class="sxs-lookup"><span data-stu-id="28277-224">Use a code-behind file</span></span>

<span data-ttu-id="28277-225">Un fichier code-behind est un fichier C# associé à un script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="28277-225">A code-behind file is a C# file associated with a single U-SQL script.</span></span> <span data-ttu-id="28277-226">Vous pouvez définir un script dédié tooUDO UDA, UDT et UDF dans le fichier de code-behind hello.</span><span class="sxs-lookup"><span data-stu-id="28277-226">You can define a script dedicated tooUDO, UDA, UDT, and UDF in hello code-behind file.</span></span> <span data-ttu-id="28277-227">Hello UDO, agrégat, UDT et UDF peuvent servir directement dans le script de hello sans tout d’abord l’inscription d’assembly hello.</span><span class="sxs-lookup"><span data-stu-id="28277-227">hello UDO, UDA, UDT, and UDF can be used directly in hello script without registering hello assembly first.</span></span> <span data-ttu-id="28277-228">Hello fichier code-behind est placé dans hello même dossier que son fichier de script U-SQL d’homologation.</span><span class="sxs-lookup"><span data-stu-id="28277-228">hello code-behind file is put in hello same folder as its peering U-SQL script file.</span></span> <span data-ttu-id="28277-229">Si le script de hello est nommé xxx.usql, hello code-behind est nommé xxx.usql.cs.</span><span class="sxs-lookup"><span data-stu-id="28277-229">If hello script is named xxx.usql, hello code-behind is named as xxx.usql.cs.</span></span> <span data-ttu-id="28277-230">Si vous supprimez manuellement le fichier code-behind de hello, fonction de code-behind hello est désactivée pour son script U-SQL associé.</span><span class="sxs-lookup"><span data-stu-id="28277-230">If you manually delete hello code-behind file, hello code-behind feature is disabled for its associated U-SQL script.</span></span> <span data-ttu-id="28277-231">Pour plus d’informations sur l’écriture de code client pour le script U-SQL, consultez [Écriture et utilisation de code personnalisé dans U-SQL - Fonctions définies par l’utilisateur]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span><span class="sxs-lookup"><span data-stu-id="28277-231">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL: User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span></span>

<span data-ttu-id="28277-232">toosupport code-behind, vous devez ouvrir un dossier de travail.</span><span class="sxs-lookup"><span data-stu-id="28277-232">toosupport code-behind, you must open a working folder.</span></span> 

<span data-ttu-id="28277-233">**toogenerate un fichier code-behind**</span><span class="sxs-lookup"><span data-stu-id="28277-233">**toogenerate a code-behind file**</span></span>

1. <span data-ttu-id="28277-234">Ouvrez un fichier source.</span><span class="sxs-lookup"><span data-stu-id="28277-234">Open a source file.</span></span> 
2. <span data-ttu-id="28277-235">Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="28277-235">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
3. <span data-ttu-id="28277-236">Entrez **ADL: Generate Code Behind**.</span><span class="sxs-lookup"><span data-stu-id="28277-236">Enter **ADL: Generate Code Behind**.</span></span> <span data-ttu-id="28277-237">Un fichier code-behind est créé dans hello même dossier.</span><span class="sxs-lookup"><span data-stu-id="28277-237">A code-behind file is created in hello same folder.</span></span> 

<span data-ttu-id="28277-238">Vous pouvez également cliquer avec le bouton droit sur un fichier de script, puis sélectionner **ADL: Generate Code Behind**.</span><span class="sxs-lookup"><span data-stu-id="28277-238">You can also right-click a script file, and then select **ADL: Generate Code Behind**.</span></span> 

<span data-ttu-id="28277-239">toocompile et envoi d’un script U-SQL avec un fichier code-behind est hello identique au fichier de script avec hello autonome U-SQL.</span><span class="sxs-lookup"><span data-stu-id="28277-239">toocompile and submit a U-SQL script with a code-behind file is hello same as with hello standalone U-SQL script file.</span></span>

<span data-ttu-id="28277-240">Hello suivant deux captures d’écran affiche un fichier code-behind et son fichier de script U-SQL associé :</span><span class="sxs-lookup"><span data-stu-id="28277-240">hello following two screenshots show a code-behind file and its associated U-SQL script file:</span></span>
 
![Data Lake Tools pour Visual Studio Code - code behind](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Data Lake Tools pour Visual Studio Code - fichier de script code behind](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a><span data-ttu-id="28277-243">Utiliser les assemblys</span><span class="sxs-lookup"><span data-stu-id="28277-243">Use assemblies</span></span>

<span data-ttu-id="28277-244">Pour plus d’informations sur le développement d’assemblys, consultez [Développement d’assemblys U-SQL pour les tâches d’Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="28277-244">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>

<span data-ttu-id="28277-245">Vous pouvez utiliser Data Lake Tools tooregister assemblys personnalisés dans le catalogue de données Lake Analytique hello.</span><span class="sxs-lookup"><span data-stu-id="28277-245">You can use Data Lake Tools tooregister custom code assemblies in hello Data Lake Analytics catalog.</span></span>

<span data-ttu-id="28277-246">**tooregister un assembly**</span><span class="sxs-lookup"><span data-stu-id="28277-246">**tooregister an assembly**</span></span>

<span data-ttu-id="28277-247">Vous pouvez inscrire assembly hello via hello **ADL : enregistrer l’Assembly** ou **ADL : enregistrer l’Assembly via la Configuration** commandes.</span><span class="sxs-lookup"><span data-stu-id="28277-247">You can register hello assembly through hello **ADL: Register Assembly** or **ADL: Register Assembly through Configuration** commands.</span></span>

<span data-ttu-id="28277-248">**tooregister via hello ADL : commande d’enregistrer l’Assembly**</span><span class="sxs-lookup"><span data-stu-id="28277-248">**tooregister through hello ADL: Register Assembly command**</span></span>
1.  <span data-ttu-id="28277-249">Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="28277-249">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2.  <span data-ttu-id="28277-250">Entrez **ADL: Register Assembly**.</span><span class="sxs-lookup"><span data-stu-id="28277-250">Enter **ADL: Register Assembly**.</span></span> 
3.  <span data-ttu-id="28277-251">Spécifiez le chemin d’accès de hello assembly local.</span><span class="sxs-lookup"><span data-stu-id="28277-251">Specify hello local assembly path.</span></span> 
4.  <span data-ttu-id="28277-252">Sélectionnez un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="28277-252">Select a Data Lake Analytics account.</span></span>
5.  <span data-ttu-id="28277-253">Sélectionnez une base de données.</span><span class="sxs-lookup"><span data-stu-id="28277-253">Select a database.</span></span>

<span data-ttu-id="28277-254">Résultats : portail de hello est ouvert dans un navigateur et affiche le processus d’inscription d’assembly hello.</span><span class="sxs-lookup"><span data-stu-id="28277-254">Results: hello portal is opened in a browser and displays hello assembly registration process.</span></span>  

<span data-ttu-id="28277-255">Hello de tootrigger un autre moyen pratique **ADL : enregistrer l’Assembly** commande est le fichier clic tooright hello dans l’Explorateur de fichiers.</span><span class="sxs-lookup"><span data-stu-id="28277-255">Another convenient way tootrigger hello **ADL: Register Assembly** command is tooright-click hello .dll file in File Explorer.</span></span> 

<span data-ttu-id="28277-256">**tooregister hello cependant ADL : enregistrer l’Assembly via la commande de Configuration**</span><span class="sxs-lookup"><span data-stu-id="28277-256">**tooregister though hello ADL: Register Assembly through Configuration command**</span></span>
1.  <span data-ttu-id="28277-257">Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="28277-257">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2.  <span data-ttu-id="28277-258">Entrez **ADL: Register Assembly through Configuration**.</span><span class="sxs-lookup"><span data-stu-id="28277-258">Enter **ADL: Register Assembly through Configuration**.</span></span> 
3.  <span data-ttu-id="28277-259">Spécifiez le chemin d’accès de hello assembly local.</span><span class="sxs-lookup"><span data-stu-id="28277-259">Specify hello local assembly path.</span></span> 
4.  <span data-ttu-id="28277-260">fichier JSON de Hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="28277-260">hello JSON file is displayed.</span></span> <span data-ttu-id="28277-261">Examinez et modifiez les dépendances d’assembly hello et les paramètres de la ressource, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="28277-261">Review and edit hello assembly dependencies and resource parameters, if needed.</span></span> <span data-ttu-id="28277-262">Instructions qui s’affichent dans hello **sortie** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="28277-262">Instructions are displayed in hello **Output** window.</span></span> <span data-ttu-id="28277-263">tooproceed toohello assembly l’inscription, enregistrez le fichier JSON de hello (Ctrl + S).</span><span class="sxs-lookup"><span data-stu-id="28277-263">tooproceed toohello assembly registration, save (Ctrl+S) hello JSON file.</span></span>

![Data Lake Tools pour Visual Studio Code - code behind](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- <span data-ttu-id="28277-265">Dépendances d’assembly : détecte automatiquement les Azure Data Lake Tools si hello DLL possède des dépendances.</span><span class="sxs-lookup"><span data-stu-id="28277-265">Assembly dependencies: Azure Data Lake Tools autodetects whether hello DLL has any dependencies.</span></span> <span data-ttu-id="28277-266">dépendances de Hello sont affichent dans le fichier JSON de hello lorsqu’elles sont détectées.</span><span class="sxs-lookup"><span data-stu-id="28277-266">hello dependencies are displayed in hello JSON file after they are detected.</span></span> 
>- <span data-ttu-id="28277-267">Ressources : Vous pouvez télécharger vos ressources DLL (par exemple, .txt, .png et .csv) dans le cadre de l’inscription de l’assembly hello.</span><span class="sxs-lookup"><span data-stu-id="28277-267">Resources: You can upload your DLL resources (for example, .txt, .png, and .csv) as part of hello assembly registration.</span></span> 

<span data-ttu-id="28277-268">Un autre hello tootrigger de façon **ADL : enregistrer l’Assembly via la Configuration** commande est le fichier clic tooright hello dans l’Explorateur de fichiers.</span><span class="sxs-lookup"><span data-stu-id="28277-268">Another way tootrigger hello **ADL: Register Assembly through Configuration** command is tooright-click hello .dll file in File Explorer.</span></span> 

<span data-ttu-id="28277-269">Hello après U-SQL de code montre comment toocall un assembly.</span><span class="sxs-lookup"><span data-stu-id="28277-269">hello following U-SQL code demonstrates how toocall an assembly.</span></span> <span data-ttu-id="28277-270">Dans l’exemple hello, nom de l’assembly hello est *test*.</span><span class="sxs-lookup"><span data-stu-id="28277-270">In hello sample, hello assembly name is *test*.</span></span>

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
    too@"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-hello-data-lake-analytics-catalog"></a><span data-ttu-id="28277-271">Catalogue de données Lake Analytique hello accès</span><span class="sxs-lookup"><span data-stu-id="28277-271">Access hello Data Lake Analytics catalog</span></span>

<span data-ttu-id="28277-272">Après que vous être connecté tooAzure, vous pouvez utiliser hello suivant du catalogue des étapes tooaccess hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="28277-272">After you have connected tooAzure, you can use hello following steps tooaccess hello U-SQL catalog.</span></span>

<span data-ttu-id="28277-273">**métadonnées de tooaccess hello Analytique de LAC de données Azure**</span><span class="sxs-lookup"><span data-stu-id="28277-273">**tooaccess hello Azure Data Lake Analytics metadata**</span></span>

1.  <span data-ttu-id="28277-274">Sélectionnez Ctrl+Maj+P et entrez **ADL: List Tables**.</span><span class="sxs-lookup"><span data-stu-id="28277-274">Select Ctrl+Shift+P, and then enter **ADL: List Tables**.</span></span>
2.  <span data-ttu-id="28277-275">Sélectionnez un des comptes de données Lake Analytique hello.</span><span class="sxs-lookup"><span data-stu-id="28277-275">Select one of hello Data Lake Analytics accounts.</span></span>
3.  <span data-ttu-id="28277-276">Sélectionnez une des bases de données hello Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="28277-276">Select one of hello Data Lake Analytics databases.</span></span>
4.  <span data-ttu-id="28277-277">Sélectionnez un des schémas de hello.</span><span class="sxs-lookup"><span data-stu-id="28277-277">Select one of hello schemas.</span></span> <span data-ttu-id="28277-278">Vous pouvez voir la liste hello des tables.</span><span class="sxs-lookup"><span data-stu-id="28277-278">You can see hello list of tables.</span></span>

## <a name="view-data-lake-analytics-jobs"></a><span data-ttu-id="28277-279">Afficher les travaux Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="28277-279">View Data Lake Analytics jobs</span></span>

<span data-ttu-id="28277-280">**travaux de tooview Analytique lac de données**</span><span class="sxs-lookup"><span data-stu-id="28277-280">**tooview Data Lake Analytics jobs**</span></span>
1.  <span data-ttu-id="28277-281">Ouvrez la palette de commandes hello (Ctrl + Maj + P), puis sélectionnez **ADL : afficher le travail**.</span><span class="sxs-lookup"><span data-stu-id="28277-281">Open hello command palette (Ctrl+Shift+P) and select **ADL: Show Job**.</span></span> 
2.  <span data-ttu-id="28277-282">Sélectionnez un compte local ou Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="28277-282">Select a Data Lake Analytics or local account.</span></span> 
3.  <span data-ttu-id="28277-283">Attendez la liste des travaux hello pour hello compte tooappear.</span><span class="sxs-lookup"><span data-stu-id="28277-283">Wait for hello jobs list for hello account tooappear.</span></span>
4.  <span data-ttu-id="28277-284">Sélectionnez une tâche à partir de la liste des travaux, Data Lake Tools ouvre les détails d’une tâche hello Bonjour portail Azure et affiche le fichier de JobInfo hello dans VS Code.</span><span class="sxs-lookup"><span data-stu-id="28277-284">Select a job from job list, Data Lake Tools opens hello job details in hello Azure portal and displays hello JobInfo file in VS Code.</span></span>

![Data Lake Tools pour Visual Studio Code - Types d’objets IntelliSense](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a><span data-ttu-id="28277-286">Intégration d’Azure Data Lake Storage</span><span class="sxs-lookup"><span data-stu-id="28277-286">Azure Data Lake Storage integration</span></span>

<span data-ttu-id="28277-287">Vous pouvez utiliser les commandes Azure Data Lake Storage pour :</span><span class="sxs-lookup"><span data-stu-id="28277-287">You can use Azure Data Lake Storage-related commands to:</span></span>
 - <span data-ttu-id="28277-288">Rechercher les ressources de stockage de LAC de données Azure hello.</span><span class="sxs-lookup"><span data-stu-id="28277-288">Browse through hello Azure Data Lake Storage resources.</span></span> 
 - <span data-ttu-id="28277-289">Fichier de stockage de LAC de données Azure hello aperçu.</span><span class="sxs-lookup"><span data-stu-id="28277-289">Preview hello Azure Data Lake Storage file.</span></span>  
 - <span data-ttu-id="28277-290">Télécharger hello du fichier directement tooAzure stockage lac de données dans le Code de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="28277-290">Upload hello file directly tooAzure Data Lake Storage in VS Code.</span></span> 

### <a name="list-hello-storage-path"></a><span data-ttu-id="28277-291">Chemin d’accès de stockage liste hello</span><span class="sxs-lookup"><span data-stu-id="28277-291">List hello storage path</span></span> 
<span data-ttu-id="28277-292">Vous pouvez afficher le chemin d’accès du stockage hello via la palette de commandes hello ou avec le bouton droit.</span><span class="sxs-lookup"><span data-stu-id="28277-292">You can list hello storage path through hello command palette or through right-click.</span></span>

<span data-ttu-id="28277-293">**chemin d’accès de stockage de hello toolist via la palette de commandes hello**</span><span class="sxs-lookup"><span data-stu-id="28277-293">**toolist hello storage path through hello command palette**</span></span>

1.  <span data-ttu-id="28277-294">Ouvrez la palette de commandes hello (Ctrl + Maj + P), puis entrez **ADL : chemin d’accès de stockage de liste**.</span><span class="sxs-lookup"><span data-stu-id="28277-294">Open hello command palette (Ctrl+Shift+P) and enter **ADL: List Storage Path**.</span></span>

    ![Data Lake Tools pour Visual Studio Code - Répertorier le chemin de stockage](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  <span data-ttu-id="28277-296">Sélectionnez votre meilleur moyen pour répertorier les chemin d’accès de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="28277-296">Select your preferred way for listing hello storage path.</span></span> <span data-ttu-id="28277-297">Cette section utilise **Entrer un chemin d’accès** comme exemple.</span><span class="sxs-lookup"><span data-stu-id="28277-297">This passage uses **Enter a path** as an example.</span></span>

    ![Data Lake Tools pour Visual Studio Code chemin d’accès de stockage de hello toolist unidirectionnel](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- <span data-ttu-id="28277-299">VS Code conserve le chemin d’accès de hello visité en dernier dans chaque compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="28277-299">VS Code keeps hello last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="28277-300">Par exemple : /tt/ss.</span><span class="sxs-lookup"><span data-stu-id="28277-300">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="28277-301">Navigateur à partir du chemin d’accès racine : chemin d’accès de la racine hello liste à partir de votre compte Analytique lac de données sélectionné ou un chemin d’accès local.</span><span class="sxs-lookup"><span data-stu-id="28277-301">Browser from root path: hello list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="28277-302">Enter a path : indiquez un chemin spécifié à partir de votre compte Data Lake Analytics sélectionné ou un chemin local.</span><span class="sxs-lookup"><span data-stu-id="28277-302">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>
    
3. <span data-ttu-id="28277-303">Sélectionnez un compte à partir de chemin d’accès local de hello ou un compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="28277-303">Select an account from hello local path or a Data Lake Analytics account.</span></span>

    ![Data Lake Tools pour Visual Studio Code - Sélectionner Plus](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. <span data-ttu-id="28277-305">Sélectionnez **plus** toolist plusieurs comptes d’Analytique lac de données et sélectionnez un compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="28277-305">Select **more** toolist more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

    ![Data Lake Tools pour Visual Studio Code - Sélectionner un compte](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  <span data-ttu-id="28277-307">Entrez un chemin de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="28277-307">Enter an Azure storage path.</span></span> <span data-ttu-id="28277-308">Par exemple : /output.</span><span class="sxs-lookup"><span data-stu-id="28277-308">For example, /output.</span></span>

    ![Data Lake Tools pour Visual Studio Code - Entrer le chemin de stockage](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  <span data-ttu-id="28277-310">Résultats : palette de commandes hello répertorie des informations de chemin d’accès de hello en fonction de vos entrées.</span><span class="sxs-lookup"><span data-stu-id="28277-310">Results: hello command palette lists hello path information based on your entries.</span></span>

    ![Data Lake Tools pour Visual Studio Code - Répertorier le chemin de stockage, résultats](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

<span data-ttu-id="28277-312">Un chemin d’accès relatif de toolist hello est via hello plus pratique d’utiliser avec le bouton droit de menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="28277-312">A more convenient way toolist hello relative path is through hello right-click context menu.</span></span>

<span data-ttu-id="28277-313">**Cliquez sur le chemin d’accès de stockage de hello toolist via**</span><span class="sxs-lookup"><span data-stu-id="28277-313">**toolist hello storage path through right-click**</span></span>

1.  <span data-ttu-id="28277-314">Avec le bouton droit tooselect de chaîne de chemin d’accès hello **chemin d’accès de stockage de liste**.</span><span class="sxs-lookup"><span data-stu-id="28277-314">Right-click hello path string tooselect **List Storage Path**.</span></span>

       ![Data Lake Tools pour Visual Studio Code - Menu contextuel accessible par un clic droit](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. <span data-ttu-id="28277-316">chemin d’accès relatif Hello sélectionné s’affiche dans la palette de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="28277-316">hello selected relative path appears in hello command palette.</span></span>

   ![Data Lake Tools pour Visual Studio Code - Chemin relatif sélectionné](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  <span data-ttu-id="28277-318">Sélectionnez un compte à partir de chemin d’accès local de hello ou un compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="28277-318">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools pour Visual Studio Code - Sélectionner un compte](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  <span data-ttu-id="28277-320">Résultats : palette de commandes hello répertorie les dossiers de hello et des fichiers pour le chemin d’accès actuel de hello.</span><span class="sxs-lookup"><span data-stu-id="28277-320">Results: hello command palette lists hello folders and files for hello current path.</span></span>

       ![Outils de LAC de données pour la liste de Code de Visual Studio à partir du chemin d’accès actuel de hello](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-hello-storage-file"></a><span data-ttu-id="28277-322">Fichier de stockage hello Preview</span><span class="sxs-lookup"><span data-stu-id="28277-322">Preview hello storage file</span></span>
<span data-ttu-id="28277-323">Vous pouvez afficher un aperçu des fichiers de stockage hello via la palette de commandes hello ou avec le bouton droit.</span><span class="sxs-lookup"><span data-stu-id="28277-323">You can preview hello storage file through hello command palette or through right-click.</span></span>

<span data-ttu-id="28277-324">**fichier de stockage toopreview hello via la palette de commandes hello**</span><span class="sxs-lookup"><span data-stu-id="28277-324">**toopreview hello storage file through hello command palette**</span></span>

1.  <span data-ttu-id="28277-325">Ouvrez la palette de commandes hello (Ctrl + Maj + P), puis entrez **ADL : fichier de stockage aperçu**.</span><span class="sxs-lookup"><span data-stu-id="28277-325">Open hello command palette (Ctrl+Shift+P) and enter **ADL: Preview Storage File**.</span></span>

       ![Data Lake Tools pour Visual Studio Code - Aperçu du fichier de stockage](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  <span data-ttu-id="28277-327">Sélectionnez un compte à partir de chemin d’accès local de hello ou un compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="28277-327">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools pour Visual Studio Code - Répertorier un compte](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="28277-329">Sélectionnez **plus** toolist plusieurs comptes d’Analytique lac de données et sélectionnez un compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="28277-329">Select **more** toolist more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

       ![Data Lake Tools pour Visual Studio Code - Sélectionner un compte](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  <span data-ttu-id="28277-331">Entrez un fichier ou chemin de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="28277-331">Enter an Azure storage path or file.</span></span> <span data-ttu-id="28277-332">Par exemple : /output/SearchLog.txt.</span><span class="sxs-lookup"><span data-stu-id="28277-332">For example, /output/SearchLog.txt.</span></span>

       ![Data Lake Tools pour Visual Studio Code - Entrer le fichier et le chemin de stockage](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  <span data-ttu-id="28277-334">Résultats : palette de commandes hello répertorie des informations de chemin d’accès de hello en fonction de vos entrées.</span><span class="sxs-lookup"><span data-stu-id="28277-334">Results: hello command palette lists hello path information based on your entries.</span></span>

       ![Data Lake Tools pour Visual Studio Code - Aperçu du fichier, résultats](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

<span data-ttu-id="28277-336">**Cliquez sur le chemin d’accès de stockage de hello toolist via**</span><span class="sxs-lookup"><span data-stu-id="28277-336">**toolist hello storage path through right-click**</span></span>

1.  <span data-ttu-id="28277-337">toopreview un fichier, avec le bouton droit de la CheminAccèsFichier hello.</span><span class="sxs-lookup"><span data-stu-id="28277-337">toopreview a file, right-click hello file path.</span></span>

   ![Data Lake Tools pour Visual Studio Code - Menu contextuel accessible par un clic droit](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  <span data-ttu-id="28277-339">Sélectionnez un compte à partir de chemin d’accès local de hello ou un compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="28277-339">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools pour Visual Studio Code - Sélectionner un compte](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="28277-341">Résultats : VS Code affiche hello aperçu des résultats pour les fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="28277-341">Results: VS Code displays hello preview results of hello file.</span></span>

       ![Data Lake Tools pour Visual Studio Code - Aperçu du fichier, résultats](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a><span data-ttu-id="28277-343">Charger un fichier</span><span class="sxs-lookup"><span data-stu-id="28277-343">Upload a file</span></span> 

<span data-ttu-id="28277-344">Vous pouvez télécharger des fichiers en entrant les commandes hello **ADL : télécharger un fichier** ou **ADL : télécharger un fichier via la Configuration**.</span><span class="sxs-lookup"><span data-stu-id="28277-344">You can upload files by entering hello commands **ADL: Upload File** or **ADL: Upload File through Configuration**.</span></span>

<span data-ttu-id="28277-345">**les fichiers tooupload hello cependant ADL : télécharger un fichier (commande)**</span><span class="sxs-lookup"><span data-stu-id="28277-345">**tooupload files though hello ADL: Upload File command**</span></span>
1. <span data-ttu-id="28277-346">Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello ou éditeur de script hello et puis entrez **télécharger le fichier**.</span><span class="sxs-lookup"><span data-stu-id="28277-346">Select Ctrl+Shift+P tooopen hello command palette or right-click hello script editor, and then enter **Upload File**.</span></span>
2.  <span data-ttu-id="28277-347">hello de tooupload de fichier, entrez un chemin d’accès local.</span><span class="sxs-lookup"><span data-stu-id="28277-347">tooupload hello file, enter a local path.</span></span>

    ![Data Lake Tools pour Visual Studio Code - Entrer un chemin local](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. <span data-ttu-id="28277-349">Sélectionnez une des façons de hello du chemin d’accès de stockage annonce hello.</span><span class="sxs-lookup"><span data-stu-id="28277-349">Select one of hello ways of listing hello storage path.</span></span> <span data-ttu-id="28277-350">Cette section utilise **Entrer un chemin d’accès** comme exemple.</span><span class="sxs-lookup"><span data-stu-id="28277-350">This passage uses **Enter a path** as an example.</span></span>

    ![Data Lake Tools pour Visual Studio Code - Répertorier le chemin de stockage](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- <span data-ttu-id="28277-352">VS Code conserve le chemin d’accès de hello visité en dernier dans chaque compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="28277-352">VS Code keeps hello last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="28277-353">Par exemple : /tt/ss.</span><span class="sxs-lookup"><span data-stu-id="28277-353">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="28277-354">Navigateur à partir du chemin d’accès racine : chemin d’accès de la racine hello liste à partir de votre compte Analytique lac de données sélectionné ou un chemin d’accès local.</span><span class="sxs-lookup"><span data-stu-id="28277-354">Browser from root path: hello list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="28277-355">Enter a path : indiquez un chemin spécifié à partir de votre compte Data Lake Analytics sélectionné ou un chemin local.</span><span class="sxs-lookup"><span data-stu-id="28277-355">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>

4. <span data-ttu-id="28277-356">Sélectionnez un compte à partir de chemin d’accès local de hello ou un compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="28277-356">Select an account from hello local path or a Data Lake Analytics account.</span></span>

    ![Data Lake Tools pour Visual Studio Code - Stockage accessible par un clic droit](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. <span data-ttu-id="28277-358">Entrez un chemin de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="28277-358">Enter an Azure storage path.</span></span> <span data-ttu-id="28277-359">Par exemple : /output.</span><span class="sxs-lookup"><span data-stu-id="28277-359">For example: /output.</span></span>

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. <span data-ttu-id="28277-360">Recherchez votre chemin de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="28277-360">Find your Azure storage path.</span></span> <span data-ttu-id="28277-361">Sélectionnez **Choisir le dossier actuel**.</span><span class="sxs-lookup"><span data-stu-id="28277-361">Select **Choose current folder**.</span></span>

    ![Data Lake Tools pour Visual Studio Code - Sélectionner un dossier](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  <span data-ttu-id="28277-363">Résultats : hello **sortie** fenêtre affiche l’état de téléchargement de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="28277-363">Results: hello **Output** window displays hello file upload status.</span></span>

       ![Data Lake Tools pour Visual Studio Code - État du chargement](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

<span data-ttu-id="28277-365">**les fichiers tooupload hello cependant ADL : télécharger un fichier via la commande de Configuration**</span><span class="sxs-lookup"><span data-stu-id="28277-365">**tooupload files though hello ADL: Upload File through Configuration command**</span></span>
1.  <span data-ttu-id="28277-366">Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello ou éditeur de script hello et puis entrez **télécharger un fichier via la Configuration**.</span><span class="sxs-lookup"><span data-stu-id="28277-366">Select Ctrl+Shift+P tooopen hello command palette or right-click hello script editor, and then enter **Upload File through Configuration**.</span></span>
2.  <span data-ttu-id="28277-367">VS Code affiche un fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="28277-367">VS Code displays a JSON file.</span></span> <span data-ttu-id="28277-368">Vous pouvez entrer des chemins d’accès de fichier et télécharger plusieurs fichiers à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="28277-368">You can enter file paths and upload multiple files at hello same time.</span></span> <span data-ttu-id="28277-369">Instructions qui s’affichent dans hello **sortie** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="28277-369">Instructions are displayed in hello **Output** window.</span></span> <span data-ttu-id="28277-370">fichiers de hello tooupload tooproceed, enregistrez le fichier JSON de hello (Ctrl + S).</span><span class="sxs-lookup"><span data-stu-id="28277-370">tooproceed tooupload hello file, save (Ctrl+S) hello JSON file.</span></span>

       ![Chemin de fichier Data Lake Tools pour Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  <span data-ttu-id="28277-372">Résultats : hello **sortie** fenêtre affiche l’état de téléchargement de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="28277-372">Results: hello **Output** window displays hello file upload status.</span></span>

       ![Data Lake Tools pour Visual Studio Code - État du chargement](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

<span data-ttu-id="28277-374">Un autre tooupload de façon hello est un toostorage de fichier avec le bouton droit de menu sur les chemin d’accès complet du fichier hello ou un chemin relatif du fichier hello éditeur de script hello.</span><span class="sxs-lookup"><span data-stu-id="28277-374">Another way tooupload a file toostorage is through hello right-click menu on hello file's full path or hello file's relative path in hello script editor.</span></span> <span data-ttu-id="28277-375">Entrez le chemin d’accès du fichier local hello, puis sélectionnez le compte hello.</span><span class="sxs-lookup"><span data-stu-id="28277-375">Enter hello local file path, and then select hello account.</span></span> <span data-ttu-id="28277-376">Hello **sortie** fenêtre affiche l’état de téléchargement hello.</span><span class="sxs-lookup"><span data-stu-id="28277-376">hello **Output** window displays hello upload status.</span></span> 

### <a name="open-azure-storage-explorer"></a><span data-ttu-id="28277-377">Ouvrir l’Explorateur de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="28277-377">Open Azure Storage Explorer</span></span>
<span data-ttu-id="28277-378">Vous pouvez ouvrir **Azure Storage Explorer** en entrant la commande hello **ADL : Ouvrez l’Explorateur de stockage Azure Web** ou en le sélectionnant dans le menu contextuel hello.</span><span class="sxs-lookup"><span data-stu-id="28277-378">You can open **Azure Storage Explorer** by entering hello command **ADL: Open Web Azure Storage Explorer** or by selecting it from hello right-click context menu.</span></span>

<span data-ttu-id="28277-379">**tooopen Explorateur de stockage Azure**</span><span class="sxs-lookup"><span data-stu-id="28277-379">**tooopen Azure Storage Explorer**</span></span>

1. <span data-ttu-id="28277-380">Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="28277-380">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2. <span data-ttu-id="28277-381">Entrez **ouvrir Explorateur de stockage Azure Web** ou avec le bouton droit sur un chemin d’accès relatif ou un chemin d’accès complet de hello dans l’éditeur de script hello, puis sélectionnez **ouvrir Explorateur de stockage Azure Web**.</span><span class="sxs-lookup"><span data-stu-id="28277-381">Enter **Open Web Azure Storage Explorer** or right-click on a relative path or hello full path in hello script editor, and then select **Open Web Azure Storage Explorer**.</span></span>
3. <span data-ttu-id="28277-382">Sélectionnez un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="28277-382">Select a Data Lake Analytics account.</span></span>

<span data-ttu-id="28277-383">Outils de LAC de données ouvre le chemin d’accès de stockage Azure hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="28277-383">Data Lake Tools opens hello Azure storage path in hello Azure portal.</span></span> <span data-ttu-id="28277-384">Vous pouvez trouver hello chemin d’accès et aperçu hello le fichier à partir du web de hello.</span><span class="sxs-lookup"><span data-stu-id="28277-384">You can find hello path and preview hello file from hello web.</span></span>

### <a name="local-run-and-local-debug-for-windows-users"></a><span data-ttu-id="28277-385">Exécution locale et débogage local pour les utilisateurs de Windows</span><span class="sxs-lookup"><span data-stu-id="28277-385">Local run and local debug for Windows users</span></span>
<span data-ttu-id="28277-386">Exécution locale de U-SQL teste vos données locales et valide votre script localement, avant que votre code soit publié tooData Lake Analytique.</span><span class="sxs-lookup"><span data-stu-id="28277-386">U-SQL local run tests your local data and validates your script locally, before your code is published tooData Lake Analytics.</span></span> <span data-ttu-id="28277-387">Hello débogage local grâce à hello toocomplete vous tâches suivantes avant de votre code est soumis tooData Lake Analytique :</span><span class="sxs-lookup"><span data-stu-id="28277-387">hello local debug feature enables you toocomplete hello following tasks before your code is submitted tooData Lake Analytics:</span></span> 
- <span data-ttu-id="28277-388">Déboguer votre code-behind C#</span><span class="sxs-lookup"><span data-stu-id="28277-388">Debug your C# code-behind.</span></span> 
- <span data-ttu-id="28277-389">Parcourir le code de hello.</span><span class="sxs-lookup"><span data-stu-id="28277-389">Step through hello code.</span></span> 
- <span data-ttu-id="28277-390">Valider votre script localement</span><span class="sxs-lookup"><span data-stu-id="28277-390">Validate your script locally.</span></span>

<span data-ttu-id="28277-391">Pour obtenir des instructions sur l’exécution locale et le débogage local, consultez [Exécution locale et débogage local U-SQL avec Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="28277-391">For instructions on local run and local debug, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>

## <a name="additional-features"></a><span data-ttu-id="28277-392">Fonctionnalités supplémentaires</span><span class="sxs-lookup"><span data-stu-id="28277-392">Additional features</span></span>

<span data-ttu-id="28277-393">Data Lake Tools pour Visual Studio Code prend en charge hello suivant de fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="28277-393">Data Lake Tools for VS Code supports hello following features:</span></span>

-   <span data-ttu-id="28277-394">Saisie semi-automatique IntelliSense : des suggestions s’affichent dans des fenêtres indépendantes autour des éléments tels que les mots clés, les méthodes et les variables.</span><span class="sxs-lookup"><span data-stu-id="28277-394">IntelliSense auto-complete: Suggestions appear in pop-up windows around items, such as keywords, methods, and variables.</span></span> <span data-ttu-id="28277-395">Les icônes représentent différents types d’objets de hello :</span><span class="sxs-lookup"><span data-stu-id="28277-395">Different icons represent different types of hello objects:</span></span>

    - <span data-ttu-id="28277-396">Type de données Scala</span><span class="sxs-lookup"><span data-stu-id="28277-396">Scala data type</span></span>
    - <span data-ttu-id="28277-397">Type de données complexe</span><span class="sxs-lookup"><span data-stu-id="28277-397">Complex data type</span></span>
    - <span data-ttu-id="28277-398">Types définis par l’utilisateur (UDT) intégrés</span><span class="sxs-lookup"><span data-stu-id="28277-398">Built-in UDTs</span></span>
    - <span data-ttu-id="28277-399">Classes et collection .NET</span><span class="sxs-lookup"><span data-stu-id="28277-399">.NET collection and classes</span></span>
    - <span data-ttu-id="28277-400">Expressions C#</span><span class="sxs-lookup"><span data-stu-id="28277-400">C# expressions</span></span>
    - <span data-ttu-id="28277-401">UDF, UDO et UDAAG C# intégrés</span><span class="sxs-lookup"><span data-stu-id="28277-401">Built-in C# UDFs, UDOs, and UDAAGs</span></span> 
    - <span data-ttu-id="28277-402">Fonctions U-SQL</span><span class="sxs-lookup"><span data-stu-id="28277-402">U-SQL functions</span></span>
    - <span data-ttu-id="28277-403">Fonction de fenêtrage U-SQL</span><span class="sxs-lookup"><span data-stu-id="28277-403">U-SQL windowing function</span></span>
 
    ![Data Lake Tools pour Visual Studio Code - Types d’objets IntelliSense](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   <span data-ttu-id="28277-405">IntelliSense de saisie semi-automatique sur les métadonnées des données Lake Analytique : Data Lake Tools télécharge localement des informations de métadonnées Analytique lac de données hello.</span><span class="sxs-lookup"><span data-stu-id="28277-405">IntelliSense auto-complete on Data Lake Analytics metadata: Data Lake Tools downloads hello Data Lake Analytics metadata information locally.</span></span> <span data-ttu-id="28277-406">fonctionnalité IntelliSense de Hello remplit automatiquement les objets, y compris la base de données hello, schéma, table, vue, une fonction table, procédures et c# assemblys, à partir des métadonnées de données Lake Analytique hello.</span><span class="sxs-lookup"><span data-stu-id="28277-406">hello IntelliSense feature automatically populates objects, including hello database, schema, table, view, table-valued function, procedures, and C# assemblies, from hello Data Lake Analytics metadata.</span></span>
 
    ![Data Lake Tools pour Visual Studio Code - Métadonnées IntelliSense](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   <span data-ttu-id="28277-408">IntelliSense erroné : Data Lake Tools souligne hello édition d’erreurs pour U-SQL et c#.</span><span class="sxs-lookup"><span data-stu-id="28277-408">IntelliSense error marker: Data Lake Tools underlines hello editing errors for U-SQL and C#.</span></span> 
-   <span data-ttu-id="28277-409">Met en surbrillance de syntaxe : Data Lake Tools utilise des éléments de toodifferentiate des couleurs différentes, telles que les variables, les mots clés, les type de données et les fonctions.</span><span class="sxs-lookup"><span data-stu-id="28277-409">Syntax highlights: Data Lake Tools uses different colors toodifferentiate items, such as variables, keywords, data type, and functions.</span></span> 

    ![Data Lake Tools pour Visual Studio Code - Points clés de la syntaxe](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a><span data-ttu-id="28277-411">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="28277-411">Next steps</span></span>

- <span data-ttu-id="28277-412">Pour l’exécution locale et le débogage local U-SQL avec Visual Studio Code, consultez [Exécution locale et débogage local U-SQL avec Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="28277-412">For U-SQL local run and local debug with Visual Studio Code, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>
- <span data-ttu-id="28277-413">Pour obtenir des informations sur la prise en main de Data Lake Analytics, consultez [Didacticiel : bien démarrer avec Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="28277-413">For getting-started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="28277-414">Pour obtenir des informations sur l’utilisation de Data Lake Tools pour Visual Studio, consultez [Didacticiel : développer des scripts U-SQL avec Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="28277-414">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="28277-415">Pour plus d’informations sur le développement d’assemblys, consultez [Développement d’assemblys U-SQL pour les tâches d’Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="28277-415">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>



