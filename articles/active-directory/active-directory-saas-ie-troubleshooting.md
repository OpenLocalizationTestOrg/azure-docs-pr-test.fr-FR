---
title: "Résolution des problèmes liés à l’extension Volet d’accès Azure pour IE| Microsoft Docs"
description: "Comment utiliser la stratégie de groupe pour déployer le module complémentaire Internet Explorer du portail Mes applications."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56b3230-26fd-42ec-9e3d-2c12daf15479
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 938d0b4046afa8c80eabe542f4541d0554948f5d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshooting-the-access-panel-extension-for-internet-explorer"></a><span data-ttu-id="5c808-103">Résolution des problèmes liés à l’extension Volet d’accès pour Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="5c808-103">Troubleshooting the Access Panel Extension for Internet Explorer</span></span>
<span data-ttu-id="5c808-104">Cet article vous aide à résoudre les problèmes suivants :</span><span class="sxs-lookup"><span data-stu-id="5c808-104">This article helps you troubleshoot the following problems:</span></span>

* <span data-ttu-id="5c808-105">Vous ne parvenez pas à accéder à vos applications par le biais du portail Mes applications quand vous utilisez Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="5c808-105">You're unable to access your apps through the My Apps portal while using Internet Explorer.</span></span>
* <span data-ttu-id="5c808-106">Le message « Installer le logiciel » s’affiche même si vous avez déjà installé le logiciel.</span><span class="sxs-lookup"><span data-stu-id="5c808-106">You see the "Install Software" message even though you've already installed the software.</span></span>

<span data-ttu-id="5c808-107">Si vous êtes administrateur, consultez aussi : [Déploiement de l’extension Volet d’accès pour Internet Explorer à l’aide de la stratégie de groupe](active-directory-saas-ie-group-policy.md)</span><span class="sxs-lookup"><span data-stu-id="5c808-107">If you are an admin, see also: [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md)</span></span>

## <a name="run-the-diagnostic-tool"></a><span data-ttu-id="5c808-108">Exécution de l’outil de diagnostic</span><span class="sxs-lookup"><span data-stu-id="5c808-108">Run the Diagnostic Tool</span></span>
<span data-ttu-id="5c808-109">Vous pouvez diagnostiquer les problèmes d’installation de l’extension Volet d’accès en téléchargeant et en exécutant l’outil de diagnostic du volet d’accès :</span><span class="sxs-lookup"><span data-stu-id="5c808-109">You can diagnose installation problems with the Access Panel Extension by downloading and running the Access Panel diagnostic tool:</span></span>

1. [<span data-ttu-id="5c808-110">Cliquez ici pour télécharger l’outil de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="5c808-110">Click here to download the diagnostic tool.</span></span>](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. <span data-ttu-id="5c808-111">Ouvrez le fichier, puis appuyez sur le bouton **Extraire tout** .</span><span class="sxs-lookup"><span data-stu-id="5c808-111">Open the file, and press **Extract all** button.</span></span>
   
    ![Appuyer sur Extraire tout](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. <span data-ttu-id="5c808-113">Appuyez sur le bouton **Extraire** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="5c808-113">Then press the **Extract** button to continue.</span></span>
   
    ![Appuyer sur Extraire](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. <span data-ttu-id="5c808-115">Pour exécuter l’outil, cliquez sur le fichier nommé **AccessPanelExtensionDiagnosticTool**, puis sélectionnez **Ouvrir avec > Microsoft Windows Based Script Host**.</span><span class="sxs-lookup"><span data-stu-id="5c808-115">To run the tool, right-click the file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.</span></span>
   
    ![Ouvrir avec > Microsoft Windows Based Script Host](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. <span data-ttu-id="5c808-117">La fenêtre de diagnostic suivante s’ouvre, qui décrit les éventuels problèmes liés à votre installation.</span><span class="sxs-lookup"><span data-stu-id="5c808-117">You will then see the following diagnostic window, which describes what might be wrong with your installation.</span></span>
   
    ![Exemple de fenêtre de diagnostic](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. <span data-ttu-id="5c808-119">Cliquez sur**Oui**pour autoriser le programme à résoudre les problèmes identifiés.</span><span class="sxs-lookup"><span data-stu-id="5c808-119">Click "**YES**" to let the program fix the issues that have been found.</span></span>
7. <span data-ttu-id="5c808-120">Pour enregistrer ces modifications, fermez toutes les fenêtres d’Internet Explorer, puis rouvrez Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="5c808-120">To save these changes, close every Internet Explorer window, and then open Internet Explorer again.</span></span><br /><span data-ttu-id="5c808-121">Si vous ne pouvez toujours pas accéder à vos applications, essayez les étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="5c808-121">If you still can't access your apps, try the steps below.</span></span>

## <a name="check-that-the-access-panel-extension-is-enabled"></a><span data-ttu-id="5c808-122">Vérifiez que l’extension Volet d’accès est activée.</span><span class="sxs-lookup"><span data-stu-id="5c808-122">Check that the Access Panel Extension is enabled</span></span>
<span data-ttu-id="5c808-123">Pour vérifier que l’extension Volet d’accès est activée dans Internet Explorer :</span><span class="sxs-lookup"><span data-stu-id="5c808-123">To verify that the Access Panel Extension is enabled in Internet Explorer:</span></span>

1. <span data-ttu-id="5c808-124">Dans Internet Explorer, cliquez sur l’**icône d’engrenage** en haut à droite de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="5c808-124">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span></span> <span data-ttu-id="5c808-125">Puis sélectionnez **Options Internet**.</span><span class="sxs-lookup"><span data-stu-id="5c808-125">Then select **Internet options**.</span></span><br /><span data-ttu-id="5c808-126">(Dans les versions antérieures d’Internet Explorer, ce menu se trouve dans **Outils > Options Internet**.</span><span class="sxs-lookup"><span data-stu-id="5c808-126">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Accéder à Outils > Options Internet](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. <span data-ttu-id="5c808-128">Cliquez sur l’onglet **Programmes**, puis sur le bouton **Gérer les modules complémentaires**.</span><span class="sxs-lookup"><span data-stu-id="5c808-128">Click the **Programs** tab, then click the **Manage add-ons** button.</span></span>
   
    ![Cliquer sur Gérer les modules complémentaires](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. <span data-ttu-id="5c808-130">Dans cette boîte de dialogue, sélectionnez **Extension Volet d’accès**, puis cliquez sur le bouton **Activer**.</span><span class="sxs-lookup"><span data-stu-id="5c808-130">In this dialog, select **Access Panel Extension** and then click the **Enable** button.</span></span>
   
    ![Cliquer sur Activer](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. <span data-ttu-id="5c808-132">Pour enregistrer ces modifications, fermez toutes les fenêtres d’Internet Explorer, puis rouvrez Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="5c808-132">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="enable-extensions-for-inprivate-browsing"></a><span data-ttu-id="5c808-133">Activation des extensions pour la navigation InPrivate</span><span class="sxs-lookup"><span data-stu-id="5c808-133">Enable Extensions for InPrivate Browsing</span></span>
<span data-ttu-id="5c808-134">Si vous utilisez le mode de navigation InPrivate :</span><span class="sxs-lookup"><span data-stu-id="5c808-134">If you are using the InPrivate Browsing mode:</span></span>

1. <span data-ttu-id="5c808-135">Dans Internet Explorer, cliquez sur l’**icône d’engrenage** en haut à droite de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="5c808-135">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span></span> <span data-ttu-id="5c808-136">Puis sélectionnez **Options Internet**.</span><span class="sxs-lookup"><span data-stu-id="5c808-136">Then select **Internet options**.</span></span><br /><span data-ttu-id="5c808-137">(Dans les versions antérieures d’Internet Explorer, ce menu se trouve dans **Outils > Options Internet**.</span><span class="sxs-lookup"><span data-stu-id="5c808-137">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Exemple de fenêtre de diagnostic](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. <span data-ttu-id="5c808-139">Accédez à l’onglet **Confidentialité**, puis **décochez** la case **Désactiver les barres d’outils et les extensions lors du démarrage de la navigation InPrivate**</span><span class="sxs-lookup"><span data-stu-id="5c808-139">Go to the **Privacy** tab, then **uncheck** the checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</span></span></p>
   
    ![Décocher Désactiver les barres d’outils et les extensions lors du démarrage de la navigation InPrivate](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. <span data-ttu-id="5c808-141">Pour enregistrer ces modifications, fermez toutes les fenêtres d’Internet Explorer, puis rouvrez Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="5c808-141">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="uninstall-the-access-panel-extension"></a><span data-ttu-id="5c808-142">Désinstallation de l’extension Volet d’accès</span><span class="sxs-lookup"><span data-stu-id="5c808-142">Uninstall the Access Panel Extension</span></span>
<span data-ttu-id="5c808-143">Pour désinstaller l’extension Volet d’accès de votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="5c808-143">To uninstall the Access Panel extension from your computer:</span></span>

1. <span data-ttu-id="5c808-144">Sur votre clavier, appuyez sur la **touche Windows** pour ouvrir le menu Démarrer.</span><span class="sxs-lookup"><span data-stu-id="5c808-144">On your keyboard, press the **Windows key** to open the Start menu.</span></span> <span data-ttu-id="5c808-145">Ce menu vous permet de rechercher une application.</span><span class="sxs-lookup"><span data-stu-id="5c808-145">When the menu is open, you can type anything to do a search.</span></span> <span data-ttu-id="5c808-146">Tapez « Panneau de configuration », puis ouvrez le **Panneau de configuration** quand il apparaît dans les résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="5c808-146">Type "Control Panel" and then open the **Control Panel** when it appears in the search results.</span></span>
   
    ![Rechercher le Panneau de configuration](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. <span data-ttu-id="5c808-148">En haut à droite du Panneau de configuration, choisissez **Grandes icônes** sous l’option **Afficher par**.</span><span class="sxs-lookup"><span data-stu-id="5c808-148">In the top right corner of the Control Panel, change the **View by** option to **Large icons**.</span></span> <span data-ttu-id="5c808-149">Recherchez et sélectionnez le bouton **Programmes et fonctionnalités**.</span><span class="sxs-lookup"><span data-stu-id="5c808-149">Then find and click the **Programs and Features** button.</span></span>
   
    ![Modifier l’affichage pour afficher les Grandes icônes](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. <span data-ttu-id="5c808-151">Dans la liste, sélectionnez **Extension Volet d’accès**, puis cliquez sur le bouton **Désinstaller**.</span><span class="sxs-lookup"><span data-stu-id="5c808-151">From the list, select **Access Panel Extension**, and the click the **Uninstall** button.</span></span>
   
    ![Cliquer sur Désinstaller](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. <span data-ttu-id="5c808-153">Essayez ensuite de réinstaller l’extension pour vérifier que le problème a été résolu.</span><span class="sxs-lookup"><span data-stu-id="5c808-153">You can then try to install the extension again to see if the problem has been resolved.</span></span>

<span data-ttu-id="5c808-154">Si vous rencontrez des problèmes pour désinstaller l’extension, vous pouvez également la supprimer à l’aide de l’outil [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) .</span><span class="sxs-lookup"><span data-stu-id="5c808-154">If you encounter issues uninstalling the extension, you can also remove it using the [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.</span></span>

## <a name="related-articles"></a><span data-ttu-id="5c808-155">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="5c808-155">Related Articles</span></span>
* [<span data-ttu-id="5c808-156">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c808-156">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="5c808-157">Accès aux applications et authentification unique avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c808-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="5c808-158">Déploiement de l'extension du volet d'accès pour Internet Explorer à l'aide de la stratégie de groupe</span><span class="sxs-lookup"><span data-stu-id="5c808-158">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span></span>](active-directory-saas-ie-group-policy.md)

