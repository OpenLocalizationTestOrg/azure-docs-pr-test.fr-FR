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
# <a name="troubleshooting-hello-access-panel-extension-for-internet-explorer"></a>Résolution des problèmes de hello Extension volet d’accès pour Internet Explorer
Cet article vous aidera à résoudre les problèmes de hello les problèmes suivants :

* Vous êtes tooaccess Impossible de vos applications via le portail de mes applications hello lors de l’utilisation d’Internet Explorer.
* Vous consultez hello « Installer le logiciel » message même si vous avez déjà installé le logiciel de hello.

Si vous êtes un administrateur, voir aussi : [comment tooDeploy hello Extension volet d’accès pour Internet Explorer à l’aide de la stratégie de groupe](active-directory-saas-ie-group-policy.md)

## <a name="run-hello-diagnostic-tool"></a>Exécuter l’outil de Diagnostic de hello
Vous pouvez diagnostiquer les problèmes d’installation avec hello Extension volet d’accès en téléchargeant et en exécutant l’outil de diagnostic hello volet d’accès :

1. [Cliquez sur l’outil de diagnostic du hello toodownload.](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. Hello ouvrir, puis appuyez sur **extraire tout** bouton.
   
    ![Appuyer sur Extraire tout](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. Appuyez sur hello **extraire** toocontinue du bouton.
   
    ![Appuyer sur Extraire](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. outil de hello toorun, fichier de hello avec le bouton nommé **AccessPanelExtensionDiagnosticTool**, puis sélectionnez **ouvrir avec > Microsoft Script ordinateur hôte Windows**.
   
    ![Ouvrir avec > Microsoft Windows Based Script Host](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. Vous verrez ensuite hello suivant la fenêtre de diagnostic qui décrit ce qui peut être un problème avec votre installation.
   
    ![Un exemple de fenêtre de diagnostic hello](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. Cliquez sur «**Oui**« toolet hello programme correctif hello problèmes qui ont été trouvés.
7. toosave ces modifications, fermez chaque fenêtre Internet Explorer, puis rouvrez Internet Explorer.<br />Si vous ne pouvez toujours pas accéder à vos applications, essayez les étapes de hello ci-dessous.

## <a name="check-that-hello-access-panel-extension-is-enabled"></a>Vérifiez que hello Qu'extension volet d’accès est activée.
tooverify qui hello Extension volet d’accès est activée dans Internet Explorer :

1. Dans Internet Explorer, cliquez sur hello **icône d’engrenage** sur hello coin supérieur droit de la fenêtre hello. Puis sélectionnez **Options Internet**.<br />(Dans les versions antérieures d’Internet Explorer, ce menu se trouve dans **Outils > Options Internet**.
   
    ![Accédez tooTools > Options Internet](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. Cliquez sur hello **programmes** onglet, puis cliquez sur hello **gérer les modules complémentaires** bouton.
   
    ![Cliquer sur Gérer les modules complémentaires](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. Dans cette boîte de dialogue, sélectionnez **Extension volet d’accès** puis cliquez sur hello **activer** bouton.
   
    ![Cliquer sur Activer](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. toosave ces modifications, fermez chaque fenêtre Internet Explorer et puis rouvrez Internet Explorer.

## <a name="enable-extensions-for-inprivate-browsing"></a>Activation des extensions pour la navigation InPrivate
Si vous utilisez le mode de navigation InPrivate hello :

1. Dans Internet Explorer, cliquez sur hello **icône d’engrenage** sur hello coin supérieur droit de la fenêtre hello. Puis sélectionnez **Options Internet**.<br />(Dans les versions antérieures d’Internet Explorer, ce menu se trouve dans **Outils > Options Internet**.
   
    ![Un exemple de fenêtre de diagnostic hello](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. Accédez toohello **confidentialité** sous l’onglet puis **Décochez** hello case à cocher **désactiver les barres d’outils et extensions au démarrage de la navigation InPrivate**</p>
   
    ![Décocher Désactiver les barres d’outils et les extensions lors du démarrage de la navigation InPrivate](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. toosave ces modifications, fermez chaque fenêtre Internet Explorer et puis rouvrez Internet Explorer.

## <a name="uninstall-hello-access-panel-extension"></a>Désinstaller hello Extension volet d’accès
hello toouninstall extension volet d’accès de votre ordinateur :

1. Sur votre clavier, appuyez sur hello **clé Windows** menu Démarrer de hello tooopen. Lorsque le menu de hello est ouvert, vous pouvez taper quoi que ce soit toodo une recherche. Tapez « Panneau », puis ouvrez hello **le panneau de configuration** lorsqu’il apparaît dans les résultats de recherche hello.
   
    ![Rechercher le Panneau de configuration](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. Dans hello coin supérieur droit de hello le panneau de configuration, modifiez hello **afficher par** option trop**grandes icônes**. Rechercher, puis cliquez sur hello **programmes et fonctionnalités** bouton.
   
    ![Suivi modifications hello vue tooshow grandes icônes](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. Dans la liste hello, sélectionnez **Extension volet d’accès**et cliquez sur hello de hello **désinstallation** bouton.
   
    ![Cliquer sur Désinstaller](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. Vous pouvez ensuite essayer d’extension de hello tooinstall toosee à nouveau si hello problème a été résolu.

Si vous rencontrez des problèmes de désinstallation hello extension, vous pouvez également supprimer à l’aide de hello [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) outil.

## <a name="related-articles"></a>Articles connexes
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
* [Accès aux applications et authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Comment tooDeploy hello Extension volet d’accès pour Internet Explorer à l’aide de la stratégie de groupe](active-directory-saas-ie-group-policy.md)

