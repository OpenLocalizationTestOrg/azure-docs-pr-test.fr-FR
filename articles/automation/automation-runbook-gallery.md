---
title: "galeries aaaRunbook et le module d’automatisation Azure | Documents Microsoft"
description: "Procédures opérationnelles et modules à partir de la Communauté Microsoft et hello sont disponibles pour vous tooinstall et utilisent dans votre environnement Azure Automation.  Cet article décrit comment vous pouvez accéder à ces ressources et les toocontribute votre galerie toohello de runbooks."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d3fee7b4-630a-4c10-8425-9bf51d7c9e58
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 10b634460edf66dd7548017e3a2f7111b7125f30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-and-module-galleries-for-azure-automation"></a>Galeries de runbooks et de modules pour Azure Automation
Au lieu de créer vos propres runbooks et des modules dans Azure Automation, vous pouvez accéder à un éventail de scénarios qui ont déjà été générés par la Communauté Microsoft et hello.  Vous pouvez utiliser ces scénarios sans les modifier ou les utiliser comme point de départ, puis les modifier selon vos besoins spécifiques.

Vous pouvez obtenir des runbooks à partir de hello [galerie de runbooks](#runbooks-in-runbook-gallery) et les modules de hello [PowerShell Gallery](#modules-in-powerShell-gallery).  Vous pouvez également contribuer toohello Communauté en partageant des scénarios que vous développez.

## <a name="runbooks-in-runbook-gallery"></a>Runbooks dans la galerie de runbooks
Hello [galerie de runbooks](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=RootCategory&f\[0\].Value=WindowsAzure&f\[1\].Type=SubCategory&f\[1\].Value=WindowsAzure_automation&f\[1\].Text=Automation) fournit divers runbooks à partir de la Communauté Microsoft et hello que vous pouvez importer dans Azure Automation. Vous pouvez télécharger un runbook à partir de la galerie hello qui est hébergée dans hello [centre de scripts TechNet](https://gallery.technet.microsoft.com/scriptcenter/site/upload), ou vous pouvez importer directement les runbook à partir de la galerie de hello à partir de hello portail Azure classic ou portail Azure.

Vous ne pouvez importer directement à partir de la galerie de runbooks hello à l’aide de hello portail Azure classic ou le portail Azure. Vous ne pouvez pas exécuter cette fonction à l’aide de Windows PowerShell.

> [!NOTE]
> Vous devez valider le contenu de hello de tout runbook que vous obtenez à partir de la galerie de runbooks de hello et précautionneux lors de l’installation et à les exécuter dans un environnement de production. |
> 
> 

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-classic-portal"></a>tooimport un runbook à partir de la galerie de runbooks de hello avec hello portail Azure classic
1. Bonjour portail Azure, cliquez sur, **nouveau**, **des Services d’application**, **Automation**, **Runbook**, **à partir de la galerie**.
2. Sélectionnez une catégorie de tooview liées procédures opérationnelles, puis sélectionnez un tooview runbook ses détails. Lorsque vous sélectionnez runbook hello souhaité, cliquez sur le bouton de flèche droite hello.
   
    ![galerie de runbooks](media/automation-runbook-gallery/runbook-gallery.png)
3. Passez en revue le contenu hello du runbook de hello et notez toutes les conditions requises dans la description de hello. Lorsque vous avez terminé, cliquez sur bouton de flèche droite hello.
4. Entrez les détails de runbook de hello, puis cliquez sur la coche hello. nom du runbook Hello est déjà renseigné.
5. Hello runbook apparaîtra sur hello **Runbooks** onglet hello compte Automation.

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-portal"></a>tooimport un runbook à partir de la galerie de runbooks de hello avec hello portail Azure
1. Bonjour portail Azure, ouvrez votre compte Automation.
2. Cliquez sur hello **Runbooks** vignette tooopen hello liste des runbooks.
3. Cliquez sur le bouton **Parcourir la galerie** .
   
    ![Bouton Parcourir la galerie](media/automation-runbook-gallery/browse-gallery-button.png)
4. Localiser l’élément de galerie hello souhaitées et sélectionnez il tooview ses détails.
   
    ![Parcourir la galerie](media/automation-runbook-gallery/browse-gallery.png)
5. Cliquez sur **projet source de vue** élément hello tooview hello [centre de scripts TechNet](http://gallery.technet.microsoft.com/).
6. tooimport un élément, cliquez dessus tooview ses détails, puis hello **importation** bouton.
   
    ![Bouton Importer](media/automation-runbook-gallery/gallery-item-detail.png)
7. Si vous le souhaitez, modifier le nom hello de hello runbook, puis **OK** tooimport hello runbook.
8. Hello runbook apparaîtra sur hello **Runbooks** onglet hello compte Automation.

### <a name="adding-a-runbook-toohello-runbook-gallery"></a>Ajout d’une galerie de runbooks toohello runbook
Microsoft vous encourage tooadd runbooks toohello galerie de runbooks que vous pensez être utiles tooother clients.  Vous pouvez ajouter un runbook par [télécharger toohello centre de scripts](http://gallery.technet.microsoft.com/site/upload) tenant hello compte les détails suivants.

* Vous devez spécifier *Windows Azure* pour hello **catégorie** et *Automation* pour hello **sous-catégorie** pour toobe de runbook hello affiché dans l’Assistant hello.  
* téléchargement de Hello doit être un seul fichier .ps1 ou .graphrunbook.  Si hello runbook nécessite des modules, les runbooks enfants ou des ressources, puis vous devez les répertorier dans description hello de soumission de hello et dans la section commentaires hello hello runbook.  Si vous avez un scénario nécessitant plusieurs runbooks, chaque télécharger séparément et Lister les noms de hello Hello liées procédures opérationnelles dans chacun de leurs descriptions. Assurez-vous que vous utilisez hello même balises afin qu’ils seront afficheront dans hello même catégorie. Un utilisateur a tooread hello description tooknow que d’autres runbooks sont toowork de scénario hello requis.
* Ajouter la balise de hello « GraphicalPS » si vous publiez un **runbook graphique** (pas un flux de travail graphique). 
* Insérer un PowerShell ou le flux de travail PowerShell extrait de code dans l’aide de description hello **insérer la section de code** icône.
* Hello résumé pour le téléchargement de hello s’affichera dans hello que galerie de runbooks des résultats, fournissez des informations détaillées qui vous aidera un utilisateur fonctionnalité hello de hello runbook.
* Vous devez attribuer un toothree Hello suivant le téléchargement de toohello de balises.  Hello runbook sera répertorié dans l’Assistant hello sous les catégories hello correspondant à ces balises.  Aucune balise pas dans cette liste sera ignoré par l’Assistant de hello. Si vous ne spécifiez pas de balises correspondantes, hello runbook sera répertorié sous hello autre catégorie.
  
  * Sauvegarde
  * Gestion de la capacité
  * Contrôle des modifications
  * Conformité
  * Environnements de développement / test
  * Récupération d’urgence
  * Analyse
  * Application de correctifs
  * Approvisionnement
  * Correction
  * Gestion du cycle de vie des machines virtuelles
* Automation met à jour hello galerie une fois par heure, donc vous ne voyez pas vos contributions immédiatement.

## <a name="modules-in-powershell-gallery"></a>Modules dans PowerShell Gallery
Modules PowerShell contiennent des applets de commande que vous pouvez utiliser dans vos runbook, et des modules que vous pouvez installer dans Azure Automation sont disponibles dans hello [PowerShell Gallery](http://www.powershellgallery.com).  Vous pouvez lancer cette galerie à partir de hello portail Azure et les installer directement dans Azure Automation, ou vous pouvez les télécharger et installer manuellement.  Vous ne pouvez pas installer les modules hello directement à partir de hello portail Azure classic, mais vous pouvez les télécharger à les installer comme vous le feriez pour n’importe quel autre module.

### <a name="tooimport-a-module-from-hello-automation-module-gallery-with-hello-azure-portal"></a>tooimport un module à partir de hello galerie des modules Automation avec hello portail Azure
1. Bonjour portail Azure, ouvrez votre compte Automation.
2. Cliquez sur hello **actifs** vignette tooopen hello liste de ressources.
3. Cliquez sur hello **Modules** vignette tooopen hello liste des modules.
4. Cliquez sur hello **parcourir la galerie** Panneau de la galerie de parcourir bouton et hello est lancée.
   
    ![Galerie du module](media/automation-runbook-gallery/modules-blade.png) <br>
5. Une fois que vous avez lancé le panneau de hello parcourir la galerie, vous pouvez rechercher en hello champs qui suivent :
   
   * Nom du module
   * Tags
   * Auteur
   * Nom Applet de commande/Ressource DSC
6. Recherchez un module que vous intéresse et sélectionnez tooview ses détails.  
   Lorsque vous explorez un module spécifique, vous pouvez afficher plus d’informations sur le module hello, y compris un toohello précédent lien PowerShell Gallery, les dépendances requises, et toutes les applets de commande hello et/ou les ressources DSC qui hello module contient.
   
    ![Détails du module PowerShell](media/automation-runbook-gallery/gallery-item-details-blade.png) <br>
7. module de hello tooinstall directement dans Azure Automation, cliquez sur hello **importation** bouton.
   
    ![Bouton Importer le module](media/automation-runbook-gallery/module-import-button.png)
8. Lorsque vous cliquez sur le bouton Importer de hello, vous verrez le nom du module hello que vous allez tooimport. Si toutes les dépendances de hello sont installées, hello **OK** bouton est activé. S’il manque des dépendances, vous devez tooimport celles avant de pouvoir importer ce module.
9. Cliquez sur **OK** tooimport hello module et panneau de module hello seront lancée. Lorsque Azure Automation importe un compte tooyour de module, il extrait les métadonnées sur le module de hello et les applets de commande hello.
   
    ![Panneau Importer le module](media/automation-runbook-gallery/module-import-blade.png)
   
    Cette opération peut prendre quelques minutes étant donné que chaque activité doit toobe extraite.
10. Vous recevrez une notification que le module hello est en cours de déploiement et une notification lorsqu’elle est terminée.
11. Après avoir importé le module de hello, vous voyez les activités disponibles hello, et vous pouvez utiliser ses ressources dans vos procédures opérationnelles et de la Configuration d’état souhaité.

## <a name="requesting-a-runbook-or-module"></a>Demande d’un runbook ou d’un module
Vous pouvez envoyer des demandes trop[User Voice](https://feedback.azure.com/forums/246290-azure-automation/).  Si vous avez besoin aider à écrire un runbook, ou vous avez une question à propos de PowerShell, publiez une question tooour [forum](http://social.msdn.microsoft.com/Forums/windowsazure/en-US/home?forum=azureautomation&filter=alltypes&sort=lastpostdesc).

## <a name="next-steps"></a>Étapes suivantes
* tooget a démarré avec des runbooks, consultez [création ou importation d’un runbook dans Azure Automation](automation-creating-importing-runbook.md)
* différences de hello toounderstand entre PowerShell et les flux de travail PowerShell avec des runbooks, consultez [Learning PowerShell workflow](automation-powershell-workflow.md)

