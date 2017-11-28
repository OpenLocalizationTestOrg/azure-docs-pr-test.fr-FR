---
title: "aaaTroubleshooting hello Extension volet d’accès Azure pour Internet Explorer | Documents Microsoft"
description: "Comment toouse groupe module complémentaire stratégie toodeploy hello Internet Explorer pour le portail de mes applications hello."
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
ms.openlocfilehash: 23cbb6117f34759330206de3a26f1397486acedb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-access-panel-extension-for-internet-explorer"></a><span data-ttu-id="d0dbe-103">Résolution des problèmes de hello Extension volet d’accès pour Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="d0dbe-103">Troubleshooting hello Access Panel Extension for Internet Explorer</span></span>
<span data-ttu-id="d0dbe-104">Cet article vous aidera à résoudre les problèmes de hello les problèmes suivants :</span><span class="sxs-lookup"><span data-stu-id="d0dbe-104">This article helps you troubleshoot hello following problems:</span></span>

* <span data-ttu-id="d0dbe-105">Vous êtes tooaccess Impossible de vos applications via le portail de mes applications hello lors de l’utilisation d’Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-105">You're unable tooaccess your apps through hello My Apps portal while using Internet Explorer.</span></span>
* <span data-ttu-id="d0dbe-106">Vous consultez hello « Installer le logiciel » message même si vous avez déjà installé le logiciel de hello.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-106">You see hello "Install Software" message even though you've already installed hello software.</span></span>

<span data-ttu-id="d0dbe-107">Si vous êtes un administrateur, voir aussi : [comment tooDeploy hello Extension volet d’accès pour Internet Explorer à l’aide de la stratégie de groupe](active-directory-saas-ie-group-policy.md)</span><span class="sxs-lookup"><span data-stu-id="d0dbe-107">If you are an admin, see also: [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md)</span></span>

## <a name="run-hello-diagnostic-tool"></a><span data-ttu-id="d0dbe-108">Exécuter l’outil de Diagnostic de hello</span><span class="sxs-lookup"><span data-stu-id="d0dbe-108">Run hello Diagnostic Tool</span></span>
<span data-ttu-id="d0dbe-109">Vous pouvez diagnostiquer les problèmes d’installation avec hello Extension volet d’accès en téléchargeant et en exécutant l’outil de diagnostic hello volet d’accès :</span><span class="sxs-lookup"><span data-stu-id="d0dbe-109">You can diagnose installation problems with hello Access Panel Extension by downloading and running hello Access Panel diagnostic tool:</span></span>

1. [<span data-ttu-id="d0dbe-110">Cliquez sur l’outil de diagnostic du hello toodownload.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-110">Click here toodownload hello diagnostic tool.</span></span>](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. <span data-ttu-id="d0dbe-111">Hello ouvrir, puis appuyez sur **extraire tout** bouton.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-111">Open hello file, and press **Extract all** button.</span></span>
   
    ![Appuyer sur Extraire tout](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. <span data-ttu-id="d0dbe-113">Appuyez sur hello **extraire** toocontinue du bouton.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-113">Then press hello **Extract** button toocontinue.</span></span>
   
    ![Appuyer sur Extraire](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. <span data-ttu-id="d0dbe-115">outil de hello toorun, fichier de hello avec le bouton nommé **AccessPanelExtensionDiagnosticTool**, puis sélectionnez **ouvrir avec > Microsoft Script ordinateur hôte Windows**.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-115">toorun hello tool, right-click hello file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.</span></span>
   
    ![Ouvrir avec > Microsoft Windows Based Script Host](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. <span data-ttu-id="d0dbe-117">Vous verrez ensuite hello suivant la fenêtre de diagnostic qui décrit ce qui peut être un problème avec votre installation.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-117">You will then see hello following diagnostic window, which describes what might be wrong with your installation.</span></span>
   
    ![Un exemple de fenêtre de diagnostic hello](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. <span data-ttu-id="d0dbe-119">Cliquez sur «**Oui**« toolet hello programme correctif hello problèmes qui ont été trouvés.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-119">Click "**YES**" toolet hello program fix hello issues that have been found.</span></span>
7. <span data-ttu-id="d0dbe-120">toosave ces modifications, fermez chaque fenêtre Internet Explorer, puis rouvrez Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-120">toosave these changes, close every Internet Explorer window, and then open Internet Explorer again.</span></span><br /><span data-ttu-id="d0dbe-121">Si vous ne pouvez toujours pas accéder à vos applications, essayez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-121">If you still can't access your apps, try hello steps below.</span></span>

## <a name="check-that-hello-access-panel-extension-is-enabled"></a><span data-ttu-id="d0dbe-122">Vérifiez que hello Qu'extension volet d’accès est activée.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-122">Check that hello Access Panel Extension is enabled</span></span>
<span data-ttu-id="d0dbe-123">tooverify qui hello Extension volet d’accès est activée dans Internet Explorer :</span><span class="sxs-lookup"><span data-stu-id="d0dbe-123">tooverify that hello Access Panel Extension is enabled in Internet Explorer:</span></span>

1. <span data-ttu-id="d0dbe-124">Dans Internet Explorer, cliquez sur hello **icône d’engrenage** sur hello coin supérieur droit de la fenêtre hello.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-124">In Internet Explorer, click hello **Gear icon** on hello top right corner of hello window.</span></span> <span data-ttu-id="d0dbe-125">Puis sélectionnez **Options Internet**.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-125">Then select **Internet options**.</span></span><br /><span data-ttu-id="d0dbe-126">(Dans les versions antérieures d’Internet Explorer, ce menu se trouve dans **Outils > Options Internet**.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-126">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Accédez tooTools > Options Internet](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. <span data-ttu-id="d0dbe-128">Cliquez sur hello **programmes** onglet, puis cliquez sur hello **gérer les modules complémentaires** bouton.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-128">Click hello **Programs** tab, then click hello **Manage add-ons** button.</span></span>
   
    ![Cliquer sur Gérer les modules complémentaires](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. <span data-ttu-id="d0dbe-130">Dans cette boîte de dialogue, sélectionnez **Extension volet d’accès** puis cliquez sur hello **activer** bouton.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-130">In this dialog, select **Access Panel Extension** and then click hello **Enable** button.</span></span>
   
    ![Cliquer sur Activer](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. <span data-ttu-id="d0dbe-132">toosave ces modifications, fermez chaque fenêtre Internet Explorer et puis rouvrez Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-132">toosave these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="enable-extensions-for-inprivate-browsing"></a><span data-ttu-id="d0dbe-133">Activation des extensions pour la navigation InPrivate</span><span class="sxs-lookup"><span data-stu-id="d0dbe-133">Enable Extensions for InPrivate Browsing</span></span>
<span data-ttu-id="d0dbe-134">Si vous utilisez le mode de navigation InPrivate hello :</span><span class="sxs-lookup"><span data-stu-id="d0dbe-134">If you are using hello InPrivate Browsing mode:</span></span>

1. <span data-ttu-id="d0dbe-135">Dans Internet Explorer, cliquez sur hello **icône d’engrenage** sur hello coin supérieur droit de la fenêtre hello.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-135">In Internet Explorer, click hello **Gear icon** on hello top right corner of hello window.</span></span> <span data-ttu-id="d0dbe-136">Puis sélectionnez **Options Internet**.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-136">Then select **Internet options**.</span></span><br /><span data-ttu-id="d0dbe-137">(Dans les versions antérieures d’Internet Explorer, ce menu se trouve dans **Outils > Options Internet**.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-137">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Un exemple de fenêtre de diagnostic hello](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. <span data-ttu-id="d0dbe-139">Accédez toohello **confidentialité** sous l’onglet puis **Décochez** hello case à cocher **désactiver les barres d’outils et extensions au démarrage de la navigation InPrivate**</span><span class="sxs-lookup"><span data-stu-id="d0dbe-139">Go toohello **Privacy** tab, then **uncheck** hello checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</span></span></p>
   
    ![Décocher Désactiver les barres d’outils et les extensions lors du démarrage de la navigation InPrivate](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. <span data-ttu-id="d0dbe-141">toosave ces modifications, fermez chaque fenêtre Internet Explorer et puis rouvrez Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-141">toosave these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="uninstall-hello-access-panel-extension"></a><span data-ttu-id="d0dbe-142">Désinstaller hello Extension volet d’accès</span><span class="sxs-lookup"><span data-stu-id="d0dbe-142">Uninstall hello Access Panel Extension</span></span>
<span data-ttu-id="d0dbe-143">hello toouninstall extension volet d’accès de votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="d0dbe-143">toouninstall hello Access Panel extension from your computer:</span></span>

1. <span data-ttu-id="d0dbe-144">Sur votre clavier, appuyez sur hello **clé Windows** menu Démarrer de hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-144">On your keyboard, press hello **Windows key** tooopen hello Start menu.</span></span> <span data-ttu-id="d0dbe-145">Lorsque le menu de hello est ouvert, vous pouvez taper quoi que ce soit toodo une recherche.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-145">When hello menu is open, you can type anything toodo a search.</span></span> <span data-ttu-id="d0dbe-146">Tapez « Panneau », puis ouvrez hello **le panneau de configuration** lorsqu’il apparaît dans les résultats de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-146">Type "Control Panel" and then open hello **Control Panel** when it appears in hello search results.</span></span>
   
    ![Rechercher le Panneau de configuration](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. <span data-ttu-id="d0dbe-148">Dans hello coin supérieur droit de hello le panneau de configuration, modifiez hello **afficher par** option trop**grandes icônes**.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-148">In hello top right corner of hello Control Panel, change hello **View by** option too**Large icons**.</span></span> <span data-ttu-id="d0dbe-149">Rechercher, puis cliquez sur hello **programmes et fonctionnalités** bouton.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-149">Then find and click hello **Programs and Features** button.</span></span>
   
    ![Suivi modifications hello vue tooshow grandes icônes](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. <span data-ttu-id="d0dbe-151">Dans la liste hello, sélectionnez **Extension volet d’accès**et cliquez sur hello de hello **désinstallation** bouton.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-151">From hello list, select **Access Panel Extension**, and hello click hello **Uninstall** button.</span></span>
   
    ![Cliquer sur Désinstaller](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. <span data-ttu-id="d0dbe-153">Vous pouvez ensuite essayer d’extension de hello tooinstall toosee à nouveau si hello problème a été résolu.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-153">You can then try tooinstall hello extension again toosee if hello problem has been resolved.</span></span>

<span data-ttu-id="d0dbe-154">Si vous rencontrez des problèmes de désinstallation hello extension, vous pouvez également supprimer à l’aide de hello [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) outil.</span><span class="sxs-lookup"><span data-stu-id="d0dbe-154">If you encounter issues uninstalling hello extension, you can also remove it using hello [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.</span></span>

## <a name="related-articles"></a><span data-ttu-id="d0dbe-155">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="d0dbe-155">Related Articles</span></span>
* [<span data-ttu-id="d0dbe-156">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0dbe-156">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="d0dbe-157">Accès aux applications et authentification unique avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0dbe-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="d0dbe-158">Comment tooDeploy hello Extension volet d’accès pour Internet Explorer à l’aide de la stratégie de groupe</span><span class="sxs-lookup"><span data-stu-id="d0dbe-158">How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy</span></span>](active-directory-saas-ie-group-policy.md)

