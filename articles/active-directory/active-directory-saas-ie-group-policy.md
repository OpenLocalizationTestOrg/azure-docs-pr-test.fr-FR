---
title: "Déployer l’extension Volet d’accès Azure pour IE à l’aide d’un GPO | Microsoft Docs"
description: "Comment utiliser la stratégie de groupe pour déployer le module complémentaire Internet Explorer du portail Mes applications."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 7c2d49c8-5be0-4e7e-abac-332f9dfda736
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b402ae326ab34ec71ad9de966e22be00045fee3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-deploy-the-access-panel-extension-for-internet-explorer-using-group-policy"></a><span data-ttu-id="d7c55-103">Déploiement de l’extension Volet d’accès pour Internet Explorer à l’aide de la stratégie de groupe</span><span class="sxs-lookup"><span data-stu-id="d7c55-103">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span></span>
<span data-ttu-id="d7c55-104">Ce didacticiel montre comment utiliser la stratégie de groupe pour installer à distance l’extension Volet d’accès pour Internet Explorer sur les ordinateurs de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d7c55-104">This tutorial shows how to use group policy to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span> <span data-ttu-id="d7c55-105">Cette extension est requise pour les utilisateurs d’Internet Explorer qui ont besoin de se connecter à des applications configurées à l’aide de l’ [authentification unique par mot de passe](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="d7c55-105">This extension is required for Internet Explorer users who need to sign into apps that are configured using [password-based single sign-on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span></span>

<span data-ttu-id="d7c55-106">Il est recommandé que les administrateurs automatisent le déploiement de cette extension.</span><span class="sxs-lookup"><span data-stu-id="d7c55-106">It is recommended that admins automate the deployment of this extension.</span></span> <span data-ttu-id="d7c55-107">Dans le cas contraire, les utilisateurs doivent télécharger et installer l’extension eux-mêmes, ce qui peut entraîner des erreurs des utilisateurs et nécessite des autorisations d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d7c55-107">Otherwise, users have to download and install the extension themselves, which is prone to user error and requires administrator permissions.</span></span> <span data-ttu-id="d7c55-108">Ce didacticiel présente une méthode d’automatisation des déploiements de logiciels à l’aide d’une stratégie de groupe.</span><span class="sxs-lookup"><span data-stu-id="d7c55-108">This tutorial covers one method of automating software deployments by using group policy.</span></span> [<span data-ttu-id="d7c55-109">En savoir plus sur la stratégie de groupe.</span><span class="sxs-lookup"><span data-stu-id="d7c55-109">Learn more about group policy.</span></span>](https://technet.microsoft.com/windowsserver/bb310732.aspx)

<span data-ttu-id="d7c55-110">L’extension Volet d’accès est également disponible pour [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) et [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998) qui ne requièrent pas d’autorisations d’administrateur pour l’installation.</span><span class="sxs-lookup"><span data-stu-id="d7c55-110">The Access Panel extension is also available for [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) and [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), neither of which require administrator permissions to install.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7c55-111">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="d7c55-111">Prerequisites</span></span>
* <span data-ttu-id="d7c55-112">Vous avez configuré les [services de domaine Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)et vous avez joint les ordinateurs de vos utilisateurs à votre domaine.</span><span class="sxs-lookup"><span data-stu-id="d7c55-112">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>
* <span data-ttu-id="d7c55-113">Vous devez disposer de l’autorisation « Modifier les paramètres » pour modifier l’objet de stratégie de groupe (GPO).</span><span class="sxs-lookup"><span data-stu-id="d7c55-113">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="d7c55-114">Par défaut, les membres des groupes de sécurité suivants jouissent de cette autorisation : administrateurs de domaine, administrateurs d’entreprise et propriétaires créateurs de la stratégie de groupe.</span><span class="sxs-lookup"><span data-stu-id="d7c55-114">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> [<span data-ttu-id="d7c55-115">En savoir plus.</span><span class="sxs-lookup"><span data-stu-id="d7c55-115">Learn more.</span></span>](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-the-distribution-point"></a><span data-ttu-id="d7c55-116">Étape 1 : Créer le point de distribution</span><span class="sxs-lookup"><span data-stu-id="d7c55-116">Step 1: Create the Distribution Point</span></span>
<span data-ttu-id="d7c55-117">Tout d’abord, vous devez placer le package d’installation sur un emplacement réseau accessible à tous les ordinateurs sur lesquels vous souhaitez installer l’extension à distance.</span><span class="sxs-lookup"><span data-stu-id="d7c55-117">First, you must place the installer package on a network location that can be accessed by the machines that you wish to remotely install the extension on.</span></span> <span data-ttu-id="d7c55-118">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d7c55-118">To do this, follow these steps:</span></span>

1. <span data-ttu-id="d7c55-119">Connectez-vous au serveur en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d7c55-119">Log on to the server as an administrator</span></span>
2. <span data-ttu-id="d7c55-120">Dans la fenêtre **Gestionnaire de serveur**, accédez à **Services de fichiers et de stockage**.</span><span class="sxs-lookup"><span data-stu-id="d7c55-120">In the **Server Manager** window, go to **Files and Storage Services**.</span></span>
   
    ![Ouvrir Services de fichiers et de stockage](./media/active-directory-saas-ie-group-policy/files-services.png)
3. <span data-ttu-id="d7c55-122">Accédez à l’onglet **Partages** . Ensuite, cliquez sur **Tâches** > **Nouveau partage...**</span><span class="sxs-lookup"><span data-stu-id="d7c55-122">Go to the **Shares** tab. Then click **Tasks** > **New Share...**</span></span>
   
    ![Ouvrir Services de fichiers et de stockage](./media/active-directory-saas-ie-group-policy/shares.png)
4. <span data-ttu-id="d7c55-124">Terminez l’ **Assistant Nouveau partage** et définissez des autorisations pour garantir l’accès à partir des ordinateurs de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d7c55-124">Complete the **New Share Wizard** and set permissions to ensure that it can be accessed from your users' machines.</span></span> [<span data-ttu-id="d7c55-125">En savoir plus sur les partages.</span><span class="sxs-lookup"><span data-stu-id="d7c55-125">Learn more about shares.</span></span>](https://technet.microsoft.com/library/cc753175.aspx)
5. <span data-ttu-id="d7c55-126">Téléchargez le package Microsoft Windows Installer (fichier .msi) suivant : [Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi) (Panel Extension.msi)</span><span class="sxs-lookup"><span data-stu-id="d7c55-126">Download the following Microsoft Windows Installer package (.msi file): [Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span></span>
6. <span data-ttu-id="d7c55-127">Copiez le package d’installation vers l’emplacement souhaité sur le partage.</span><span class="sxs-lookup"><span data-stu-id="d7c55-127">Copy the installer package to a desired location on the share.</span></span>
   
    ![Copiez le fichier .msi dans le partage.](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. <span data-ttu-id="d7c55-129">Vérifiez que vos ordinateurs client sont en mesure d’accéder au package d’installation à partir du partage.</span><span class="sxs-lookup"><span data-stu-id="d7c55-129">Verify that your client machines are able to access the installer package from the share.</span></span> 

## <a name="step-2-create-the-group-policy-object"></a><span data-ttu-id="d7c55-130">Étape 2 : Créer l’objet de stratégie de groupe</span><span class="sxs-lookup"><span data-stu-id="d7c55-130">Step 2: Create the Group Policy Object</span></span>
1. <span data-ttu-id="d7c55-131">Ouvrez une session sur le serveur qui héberge votre installation AD DS (services de domaine Active Directory).</span><span class="sxs-lookup"><span data-stu-id="d7c55-131">Log on to the server that hosts your Active Directory Domain Services (AD DS) installation.</span></span>
2. <span data-ttu-id="d7c55-132">Dans le Gestionnaire de serveur, accédez à **Outils** > **Gestion des stratégies de groupe**.</span><span class="sxs-lookup"><span data-stu-id="d7c55-132">In the Server Manager, go to **Tools** > **Group Policy Management**.</span></span>
   
    ![Accéder à Outils > Gestion des stratégies de groupe](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. <span data-ttu-id="d7c55-134">Dans le volet gauche de la fenêtre **Gestion des stratégies de groupe**, affichez votre hiérarchie des unités d’organisation (UO) et déterminez l’étendue selon laquelle vous aimeriez appliquer la stratégie de groupe.</span><span class="sxs-lookup"><span data-stu-id="d7c55-134">In the left pane of the **Group Policy Management** window, view your Organizational Unit (OU) hierarchy and determine at which scope you would like to apply the group policy.</span></span> <span data-ttu-id="d7c55-135">Par exemple, vous pouvez décider de sélectionner une petite UO à déployer pour quelques utilisateurs à des fins de test. Vous pouvez également choisir une UO de niveau supérieur à déployer dans toute votre organisation.</span><span class="sxs-lookup"><span data-stu-id="d7c55-135">For instance, you may decide to pick a small OU to deploy to a few users for testing, or you may pick a top-level OU to deploy to your entire organization.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d7c55-136">Si vous souhaitez créer ou modifier vos unités d’organisation (UO), revenez au Gestionnaire de serveur et accédez à **Outils** > **Utilisateurs et ordinateurs Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d7c55-136">If you would like to create or edit your Organization Units (OUs), switch back to the Server Manager and go to **Tools** > **Active Directory Users and Computers**.</span></span>
   > 
   > 
4. <span data-ttu-id="d7c55-137">Une fois que vous avez sélectionné une UO, cliquez dessus avec le bouton droit et sélectionnez **Créer un objet GPO dans ce domaine, et le lier ici...**</span><span class="sxs-lookup"><span data-stu-id="d7c55-137">Once you have selected an OU, right-click it and select **Create a GPO in this domain, and Link it here...**</span></span>
   
    ![Créer un objet GPO](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. <span data-ttu-id="d7c55-139">Dans l’invite **Nouvel objet GPO** , tapez un nom pour le nouvel objet de stratégie de groupe.</span><span class="sxs-lookup"><span data-stu-id="d7c55-139">In the **New GPO** prompt, type in a name for the new Group Policy Object.</span></span>
   
    ![Nommer le nouvel objet GPO](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. <span data-ttu-id="d7c55-141">Cliquez avec le bouton droit sur l’objet de stratégie de groupe que vous avez créé, puis sélectionnez **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="d7c55-141">Right-click the Group Policy Object that you created, and select **Edit**.</span></span>
   
    ![Modifier le nouvel objet GPO](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-the-installation-package"></a><span data-ttu-id="d7c55-143">Étape 3 : Assigner le package d’installation</span><span class="sxs-lookup"><span data-stu-id="d7c55-143">Step 3: Assign the Installation Package</span></span>
1. <span data-ttu-id="d7c55-144">Déterminez si vous souhaitez déployer l’extension selon la **Configuration ordinateur** ou la **Configuration utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="d7c55-144">Determine whether you would like to deploy the extension based on **Computer Configuration** or **User Configuration**.</span></span> <span data-ttu-id="d7c55-145">Lorsque vous utilisez la [Configuration ordinateur](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), l’extension est installée sur l’ordinateur, quels que soient les utilisateurs qui s’y connectent.</span><span class="sxs-lookup"><span data-stu-id="d7c55-145">When using [computer configuration](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), the extension is installed on the computer regardless of which users log on to it.</span></span> <span data-ttu-id="d7c55-146">Avec la [Configuration utilisateur](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), l’extension est installée pour les utilisateurs, quels que soient les ordinateurs auxquels ils se connectent.</span><span class="sxs-lookup"><span data-stu-id="d7c55-146">With [user configuration](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), users have the extension installed for them regardless of which computers they log on to.</span></span>
2. <span data-ttu-id="d7c55-147">Dans le volet gauche de la fenêtre **Éditeur de gestion des stratégies de groupe** , accédez à l’un des chemins de dossier suivants, selon le type de configuration que vous avez choisi :</span><span class="sxs-lookup"><span data-stu-id="d7c55-147">In the left pane of the **Group Policy Management Editor** window, go to either of the following folder paths, depending on which type of configuration you chose:</span></span>
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. <span data-ttu-id="d7c55-148">Cliquez avec le bouton droit sur **Installation de logiciel**, puis sélectionnez **Nouveau** > **Package...**</span><span class="sxs-lookup"><span data-stu-id="d7c55-148">Right-click **Software installation**, then select **New** > **Package...**</span></span>
   
    ![Créer un package d’installation de logiciel](./media/active-directory-saas-ie-group-policy/new-package.png)
4. <span data-ttu-id="d7c55-150">Accédez au dossier partagé qui contient le package d’installation dans [Étape 1 : Créer le point de distribution](#step-1-create-the-distribution-point), sélectionnez le fichier .msi, puis cliquez sur **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="d7c55-150">Go to the shared folder that contains the installer package from [Step 1: Create the Distribution Point](#step-1-create-the-distribution-point), select the .msi file, and click **Open**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="d7c55-151">Si le partage se trouve sur le même serveur, vérifiez que vous accédez au fichier .msi via le chemin d’accès du fichier réseau, et non via le chemin d’accès du fichier local.</span><span class="sxs-lookup"><span data-stu-id="d7c55-151">If the share is located on this same server, verify that you are accessing the .msi through the network file path, rather than the local file path.</span></span>
   > 
   > 
   
    ![Sélectionnez le package d’installation à partir du dossier partagé.](./media/active-directory-saas-ie-group-policy/select-package.png)
5. <span data-ttu-id="d7c55-153">Dans l’invite **Déploiement du logiciel**, sélectionnez **Affecté** pour votre méthode de déploiement.</span><span class="sxs-lookup"><span data-stu-id="d7c55-153">In the **Deploy Software** prompt, select **Assigned** for your deployment method.</span></span> <span data-ttu-id="d7c55-154">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d7c55-154">Then click **OK**.</span></span>
   
    ![Sélectionnez Affecté, puis cliquez sur OK.](./media/active-directory-saas-ie-group-policy/deployment-method.png)

<span data-ttu-id="d7c55-156">L’extension est désormais déployée sur l’UO que vous avez sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="d7c55-156">The extension is now deployed to the OU that you selected.</span></span> [<span data-ttu-id="d7c55-157">En savoir plus sur l’installation des logiciels de la stratégie de groupe.</span><span class="sxs-lookup"><span data-stu-id="d7c55-157">Learn more about Group Policy Software Installation.</span></span>](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-the-extension-for-internet-explorer"></a><span data-ttu-id="d7c55-158">Étape 4 : Activer automatiquement l’extension pour Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="d7c55-158">Step 4: Auto-Enable the Extension for Internet Explorer</span></span>
<span data-ttu-id="d7c55-159">Outre l’exécution du programme d’installation, toutes les extensions pour Internet Explorer doivent être explicitement activées avant de pouvoir être utilisées.</span><span class="sxs-lookup"><span data-stu-id="d7c55-159">In addition to running the installer, every extension for Internet Explorer must be explicitly enabled before it can be used.</span></span> <span data-ttu-id="d7c55-160">Suivez les étapes ci-dessous pour activer l’extension Volet d’accès à l’aide de la stratégie de groupe :</span><span class="sxs-lookup"><span data-stu-id="d7c55-160">Follow the steps below to enable the Access Panel Extension using group policy:</span></span>

1. <span data-ttu-id="d7c55-161">Dans la fenêtre **Éditeur de gestion des stratégies de groupe** , accédez à l’un des chemins suivants, selon le type de configuration que vous avez choisi dans [Étape 3 : Assigner le package d’installation](#step-3-assign-the-installation-package):</span><span class="sxs-lookup"><span data-stu-id="d7c55-161">In the **Group Policy Management Editor** window, go to either of the following paths, depending on which type of configuration you chose in [Step 3: Assign the Installation Package](#step-3-assign-the-installation-package):</span></span>
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. <span data-ttu-id="d7c55-162">Cliquez avec le bouton droit sur **Liste des modules complémentaires**, puis sélectionnez **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="d7c55-162">Right-click **Add-on List**, and select **Edit**.</span></span>
    <span data-ttu-id="d7c55-163">![Modifiez la liste des modules complémentaires.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span><span class="sxs-lookup"><span data-stu-id="d7c55-163">![Edit Add-on List.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span></span>
3. <span data-ttu-id="d7c55-164">Dans la fenêtre **Liste des modules complémentaires**, sélectionnez **Activé**.</span><span class="sxs-lookup"><span data-stu-id="d7c55-164">In the **Add-on List** window, select **Enabled**.</span></span> <span data-ttu-id="d7c55-165">Ensuite, sous la section **Options** cliquez sur **Afficher...**.</span><span class="sxs-lookup"><span data-stu-id="d7c55-165">Then, under the **Options** section, click **Show...**.</span></span>
   
    ![Cliquez sur Activer, puis sur Afficher...](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. <span data-ttu-id="d7c55-167">Dans la fenêtre **Afficher le contenu** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d7c55-167">In the **Show Contents** window, perform the following steps:</span></span>
   
   1. <span data-ttu-id="d7c55-168">Pour la première colonne (champ **Nom de la valeur**), copiez et collez l’ID de classe suivant : `{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span><span class="sxs-lookup"><span data-stu-id="d7c55-168">For the first column (the **Value Name** field), copy and paste the following Class ID: `{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span></span>
   2. <span data-ttu-id="d7c55-169">Pour la deuxième colonne (champ **Valeur**), tapez la valeur suivante : `1`</span><span class="sxs-lookup"><span data-stu-id="d7c55-169">For the second column (the **Value** field), type in the following value: `1`</span></span>
   3. <span data-ttu-id="d7c55-170">Cliquez sur **OK** pour fermer la fenêtre **Afficher le contenu**.</span><span class="sxs-lookup"><span data-stu-id="d7c55-170">Click **OK** to close the **Show Contents** window.</span></span>
      
      ![Remplissez les valeurs comme indiqué ci-dessus.](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. <span data-ttu-id="d7c55-172">Cliquez sur **OK** pour appliquer vos modifications et fermer la fenêtre **Liste des modules complémentaires**.</span><span class="sxs-lookup"><span data-stu-id="d7c55-172">Click **OK** to apply your changes and close the **Add-on List** window.</span></span>

<span data-ttu-id="d7c55-173">L’extension doit désormais être activée pour les ordinateurs dans l’UO sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="d7c55-173">The extension should now be enabled for the machines in the selected OU.</span></span> [<span data-ttu-id="d7c55-174">En savoir plus sur l’utilisation de la stratégie de groupe pour activer ou désactiver les modules complémentaires d’Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="d7c55-174">Learn more about using group policy to enable or disable Internet Explorer add-ons.</span></span>](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a><span data-ttu-id="d7c55-175">Étape 5 (Facultatif) : Désactiver l’invite « Mémoriser le mot de passe »</span><span class="sxs-lookup"><span data-stu-id="d7c55-175">Step 5 (Optional): Disable "Remember Password" Prompt</span></span>
<span data-ttu-id="d7c55-176">Lorsque les utilisateurs se connectent à des sites Web à l'aide de l'Extension Volet d'accès, Internet Explorer peut afficher le message suivant : « Souhaitez-vous enregistrer votre mot de passe ? »</span><span class="sxs-lookup"><span data-stu-id="d7c55-176">When users sign-in to websites using the Access Panel Extension, Internet Explorer may show the following prompt asking "Would you like to store your password?"</span></span>

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

<span data-ttu-id="d7c55-177">Si vous ne souhaitez pas que les utilisateurs puissent accéder à ce message, suivez les étapes mentionnées ci-dessous pour que la saisie semi-automatique ne procède pas à la mémorisation de mots de passe :</span><span class="sxs-lookup"><span data-stu-id="d7c55-177">If you wish to prevent your users from seeing this prompt, then follow the steps below to prevent auto-complete from remembering passwords:</span></span>

1. <span data-ttu-id="d7c55-178">Dans la fenêtre **Éditeur de gestion des stratégies de groupe** , accédez au chemin d'accès ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d7c55-178">In the **Group Policy Management Editor** window, go to the path listed below.</span></span> <span data-ttu-id="d7c55-179">Ce paramètre de configuration n’est disponible que sous **Configuration utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="d7c55-179">This configuration setting is only available under **User Configuration**.</span></span>
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. <span data-ttu-id="d7c55-180">Recherchez le paramètre nommé **Activer la saisie semi-automatique des noms d'utilisateur et des mots de passe dans les formulaires**.</span><span class="sxs-lookup"><span data-stu-id="d7c55-180">Find the setting named **Turn on the auto-complete feature for user names and passwords on forms**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d7c55-181">Les versions précédentes d'Active Directory peuvent répertorier ce paramètre via le nom **Ne pas autoriser la saisie semi-automatique à enregistrer des mots de passe**.</span><span class="sxs-lookup"><span data-stu-id="d7c55-181">Previous versions of Active Directory may list this setting with the name **Do not allow auto-complete to save passwords**.</span></span> <span data-ttu-id="d7c55-182">La configuration de ce paramètre diffère du paramètre décrit dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d7c55-182">The configuration for that setting differs from the setting described in this tutorial.</span></span>
   > 
   > 
   
    ![N'oubliez pas de le rechercher sous Paramètres utilisateur.](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. <span data-ttu-id="d7c55-184">Cliquez avec le bouton droit sur le paramètre ci-dessus, puis sélectionnez **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="d7c55-184">Right click the above setting, and select **Edit**.</span></span>
4. <span data-ttu-id="d7c55-185">Dans la fenêtre intitulée **Activer la saisie semi-automatique des noms d'utilisateur et des mots de passe dans les formulaires**, sélectionnez **Désactivé**.</span><span class="sxs-lookup"><span data-stu-id="d7c55-185">In the window titled **Turn on the auto-complete feature for user names and passwords on forms**, select **Disabled**.</span></span>
   
    ![Sélectionner Désactiver](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. <span data-ttu-id="d7c55-187">Cliquez sur **OK** pour appliquer ces modifications et fermer la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="d7c55-187">Click **OK** to apply these changes and close the window.</span></span>

<span data-ttu-id="d7c55-188">Les utilisateurs ne seront plus en mesure d’enregistrer leurs informations d'identification ou d’utiliser la saisie semi-automatique pour accéder aux informations d'identification enregistrées précédemment.</span><span class="sxs-lookup"><span data-stu-id="d7c55-188">Users will no longer be able to store their credentials or use auto-complete to access previously stored credentials.</span></span> <span data-ttu-id="d7c55-189">Toutefois, cette stratégie permet aux utilisateurs de continuer à utiliser la saisie semi-automatique pour les autres types de champs de formulaire, tels que les champs de recherche.</span><span class="sxs-lookup"><span data-stu-id="d7c55-189">However, this policy does allow users to continue to use auto-complete for other types of form fields, such as search fields.</span></span>

> [!WARNING]
> <span data-ttu-id="d7c55-190">Si cette stratégie est activée après que les utilisateurs aient choisi de stocker certaines informations d'identification, cette stratégie n’effacera *pas* les informations d'identification qui ont déjà été enregistrées.</span><span class="sxs-lookup"><span data-stu-id="d7c55-190">If this policy is enabled after users have chosen to store some credentials, this policy will *not* clear the credentials that have already been stored.</span></span>
> 
> 

## <a name="step-6-testing-the-deployment"></a><span data-ttu-id="d7c55-191">Étape 6 : tester le déploiement</span><span class="sxs-lookup"><span data-stu-id="d7c55-191">Step 6: Testing the Deployment</span></span>
<span data-ttu-id="d7c55-192">Suivez les étapes ci-dessous pour vérifier si le déploiement de l’extension a réussi :</span><span class="sxs-lookup"><span data-stu-id="d7c55-192">Follow the steps below to verify if the extension deployment was successful:</span></span>

1. <span data-ttu-id="d7c55-193">Si vous avez effectué le déploiement à l’aide de la **Configuration ordinateur**, connectez-vous à un ordinateur client appartenant à l’UO que vous avez sélectionnée dans [Étape 2 : Créer l’objet de stratégie de groupe](#step-2-create-the-group-policy-object).</span><span class="sxs-lookup"><span data-stu-id="d7c55-193">If you deployed using **Computer Configuration**, sign into a client machine that belongs to the OU that you selected in [Step 2: Create the Group Policy Object](#step-2-create-the-group-policy-object).</span></span> <span data-ttu-id="d7c55-194">Si vous avez effectué le déploiement à l’aide de la **Configuration utilisateur**, veillez à vous connecter en tant qu’utilisateur appartenant à cette UO.</span><span class="sxs-lookup"><span data-stu-id="d7c55-194">If you deployed using **User Configuration**, make sure to sign in as a user who belongs to that OU.</span></span>
2. <span data-ttu-id="d7c55-195">Les modifications de la stratégie de groupe peuvent nécessiter plusieurs connexions pour s’appliquer sur cet ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d7c55-195">It may take a couple sign ins for the group policy changes to fully update with this machine.</span></span> <span data-ttu-id="d7c55-196">Pour forcer la mise à jour, ouvrez une fenêtre **d’invite de commande** et exécutez la commande suivante : `gpupdate /force`</span><span class="sxs-lookup"><span data-stu-id="d7c55-196">To force the update, open a **Command Prompt** window and run the following command: `gpupdate /force`</span></span>
3. <span data-ttu-id="d7c55-197">Vous devez redémarrer l’ordinateur pour lancer l’installation.</span><span class="sxs-lookup"><span data-stu-id="d7c55-197">You must restart the machine for the installation to take place.</span></span> <span data-ttu-id="d7c55-198">Le démarrage peut prendre beaucoup plus de temps que d’habitude lors de l’installation de l’extension.</span><span class="sxs-lookup"><span data-stu-id="d7c55-198">Bootup may take significantly more time than usual while the extension installs.</span></span>
4. <span data-ttu-id="d7c55-199">Après avoir redémarré, ouvrez **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="d7c55-199">After restarting, open **Internet Explorer**.</span></span> <span data-ttu-id="d7c55-200">Dans le coin supérieur droit de la fenêtre, cliquez sur **Outils** (l’icône d’engrenage), puis sélectionnez **Gérer les modules complémentaires**.</span><span class="sxs-lookup"><span data-stu-id="d7c55-200">On the upper-right corner of the window, click **Tools** (the gear icon), and then select **Manage add-ons**.</span></span>
   
    ![Accéder à Outils > Gérer les modules complémentaires](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. <span data-ttu-id="d7c55-202">Dans la fenêtre **Gérer les modules complémentaires**, vérifiez que l’**extension Volet d’accès** a été installée et que son **État** a été défini sur **Activé**.</span><span class="sxs-lookup"><span data-stu-id="d7c55-202">In the **Manage Add-ons** window, verify that the **Access Panel Extension** has been installed and that its **Status** has been set to **Enabled**.</span></span>
   
    ![Vérifiez que l’extension Volet d’accès est installée et activée.](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a><span data-ttu-id="d7c55-204">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="d7c55-204">Related Articles</span></span>
* [<span data-ttu-id="d7c55-205">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7c55-205">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="d7c55-206">Accès aux applications et authentification unique avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7c55-206">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="d7c55-207">Résolution des problèmes liés à l'extension du volet d'accès pour Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="d7c55-207">Troubleshooting the Access Panel Extension for Internet Explorer</span></span>](active-directory-saas-ie-troubleshooting.md)

