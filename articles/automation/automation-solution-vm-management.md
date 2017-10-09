---
title: "aaaStart/arrêter les machines virtuelles pendant les heures creuses [Aperçu] Solution | Documents Microsoft"
description: "solutions de gestion de la machine virtuelle Hello démarre et arrête le Gestionnaire de ressources des Machines virtuelles Azure selon une planification et surveiller de manière proactive à partir de l’Analytique des journaux."
services: automation
documentationCenter: 
authors: mgoedtel
manager: carmonm
editor: 
ms.assetid: 06c27f72-ac4c-4923-90a6-21f46db21883
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: magoedte
ms.openlocfilehash: 6cbe16dfb40bf13f29d9e58ca0bc8c5c7979879d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="startstop-vms-during-off-hours-preview-solution-in-automation"></a>Solution Start/Stop VMs during off-hours (Preview) (Démarrer/arrêter des machines virtuelles durant les heures creuses [version préliminaire]) dans Automation

Hello machines virtuelles de démarrage/arrêt au cours de la solution d’heures creuses [Aperçu] démarre et arrête vos machines virtuelles de Azure Resource Manager selon une planification définie par l’utilisateur et fournit un aperçu de la réussite de hello de tâches d’automatisation hello qui démarrent et arrêtent vos machines virtuelles avec OMS Analytique de journal.  

## <a name="prerequisites"></a>Composants requis

- Hello runbooks fonctionnent avec un [Azure exécuter en tant que compte](automation-offering-get-started.md#authentication-methods).  Hello compte d’identification est la méthode d’authentification de hello préférée, car elle utilise l’authentification par certificat au lieu d’un mot de passe peut expirer ou changent fréquemment.  

- Cette solution peut uniquement gérer des machines virtuelles qui se trouvent dans hello même abonnement qu’où hello compte Automation réside.  

- Cette solution déploie uniquement toohello suivant des régions Azure - sud-est de l’Australie, est des États-Unis, Asie du Sud-est et Europe de l’ouest.  procédures opérationnelles Hello gérer hello VM planification peuvent cibler des machines virtuelles dans n’importe quelle région.  

- les notifications par courrier électronique toosend lorsque hello démarrer et arrêter des runbook de la machine virtuelle terminée, un abonnement de la classe d’entreprise Office 365 est requis.  

## <a name="solution-components"></a>Composants de la solution

Cette solution se compose de hello suivant des ressources qui seront importés et ajoutaient le compte d’automatisation tooyour.

### <a name="runbooks"></a>Runbooks

Runbook | Description|
--------|------------|
CleanSolution-MS-Mgmt-VM | Ce runbook supprimera tous ses ressources et les planifications lorsque vous passez des solutions de hello toodelete de votre abonnement.|  
SendMailO365-MS-Mgmt | Ce runbook envoie un message électronique via Office 365 Exchange.|
StartByResourceGroup-MS-Mgmt-VM | Ce runbook est prévue toostart VMs (les deux classique et les machines virtuelles basés sur ARM) qui se trouve dans une liste donnée de groupes de ressources Azure.
StopByResourceGroup-MS-Mgmt-VM | Ce runbook est prévue toostop VMs (les deux classique et les machines virtuelles basés sur ARM) qui se trouve dans une liste donnée de groupes de ressources Azure.|
<br>

### <a name="variables"></a>variables

Variable | Description|
---------|------------|
Runbook **SendMailO365-MS-Mgmt** ||
SendMailO365-IsSendEmail-MS-Mgmt | Indique si les runbooks StartByResourceGroup-MS-Mgmt-VM et StopByResourceGroup-MS-Mgmt-VM peuvent envoyer une notification par courrier électronique une fois l’opération associée terminée.  Sélectionnez **True** tooenable et **False** toodisable génération d’alertes par courrier électronique. La valeur par défaut est **False**.| 
Runbook **StartByResourceGroup-MS-Mgmt-VM** ||
StartByResourceGroup-ExcludeList-MS-Mgmt-VM | Entrez toobe de noms de machine virtuelle exclu de l’opération de gestion ; Séparez les noms en utilisant un point-virgule ( ;) sans espaces. Les valeurs respectent la casse et le caractère générique (astérisque) est pris en charge.|
StartByResourceGroup-SendMailO365-EmailBodyPreFix-MS-Mgmt | Texte qui peut être ajouté début toohello hello par courrier électronique du corps du message.|
StartByResourceGroup-SendMailO365-EmailRunBookAccount-MS-Mgmt | Spécifie le nom hello Hello compte Automation contenant un runbook de messagerie hello.  **Ne modifiez pas cette variable.**|
StartByResourceGroup-SendMailO365-EmailRunbookName-MS-Mgmt | Spécifie le nom hello du runbook de messagerie hello.  Il est utilisé par hello StartByResourceGroup-MS-Mgmt-VM et de la messagerie de toosend runbooks StopByResourceGroup-MS-Mgmt-VM.  **Ne modifiez pas cette variable.**|
StartByResourceGroup-SendMailO365-EmailRunbookResourceGroup-MS-Mgmt | Spécifie le nom hello hello du groupe de ressources qui contient des runbook de messagerie hello.  **Ne modifiez pas cette variable.**|
StartByResourceGroup-SendMailO365-EmailSubject-MS-Mgmt | Spécifie le texte hello pour la ligne d’objet hello de courrier électronique de hello.|  
StartByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt | Spécifie l’ou les destinataires de courrier électronique de hello hello.  Séparez les noms à l’aide de points-virgules (;), sans espaces.|
StartByResourceGroup-TargetResourceGroups-MS-Mgmt-VM | Entrez toobe de noms de machine virtuelle exclu de l’opération de gestion ; Séparez les noms en utilisant un point-virgule ( ;) sans espaces. Les valeurs respectent la casse et le caractère générique (astérisque) est pris en charge.  Par défaut (astérisque) inclut tous les groupes de ressources dans l’abonnement de hello.|
StartByResourceGroup-TargetSubscriptionID-MS-Mgmt-VM | Spécifie l’abonnement hello contenant toobe d’ordinateurs virtuels géré par cette solution.  Il doit s’agir hello même abonnement où se trouve hello compte Automation de cette solution.|
Runbook **StopByResourceGroup-MS-Mgmt-VM** ||
StopByResourceGroup-ExcludeList-MS-Mgmt-VM | Entrez toobe de noms de machine virtuelle exclu de l’opération de gestion ; Séparez les noms en utilisant un point-virgule ( ;) sans espaces. Les valeurs respectent la casse et le caractère générique (astérisque) est pris en charge.|
StopByResourceGroup-SendMailO365-EmailBodyPreFix-MS-Mgmt | Texte qui peut être ajouté début toohello hello par courrier électronique du corps du message.|
StopByResourceGroup-SendMailO365-EmailRunBookAccount-MS-Mgmt | Spécifie le nom hello Hello compte Automation contenant un runbook de messagerie hello.  **Ne modifiez pas cette variable.**|
StopByResourceGroup-SendMailO365-EmailRunbookResourceGroup-MS-Mgmt | Spécifie le nom hello hello du groupe de ressources qui contient des runbook de messagerie hello.  **Ne modifiez pas cette variable.**|
StopByResourceGroup-SendMailO365-EmailSubject-MS-Mgmt | Spécifie le texte hello pour la ligne d’objet hello de courrier électronique de hello.|  
StopByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt | Spécifie l’ou les destinataires de courrier électronique de hello hello.  Séparez les noms à l’aide de points-virgules (;), sans espaces.|
StopByResourceGroup-TargetResourceGroups-MS-Mgmt-VM | Entrez toobe de noms de machine virtuelle exclu de l’opération de gestion ; Séparez les noms en utilisant un point-virgule ( ;) sans espaces. Les valeurs respectent la casse et le caractère générique (astérisque) est pris en charge.  Par défaut (astérisque) inclut tous les groupes de ressources dans l’abonnement de hello.|
StopByResourceGroup-TargetSubscriptionID-MS-Mgmt-VM | Spécifie l’abonnement hello contenant toobe d’ordinateurs virtuels géré par cette solution.  Il doit s’agir hello même abonnement où se trouve hello compte Automation de cette solution.|  
<br>

### <a name="schedules"></a>Planifications

Planification | Description|
---------|------------|
StartByResourceGroup-Schedule-MS-Mgmt | Planification de runbook StartByResourceGroup, qui effectue le démarrage hello d’ordinateurs virtuels gérés par cette solution. Lors de la création, la valeur par défaut tooUTC horaire.|
StopByResourceGroup-Schedule-MS-Mgmt | Planification de runbook StopByResourceGroup, qui effectue un arrêt hello d’ordinateurs virtuels gérés par cette solution. Lors de la création, la valeur par défaut tooUTC horaire.|

### <a name="credentials"></a>Informations d'identification

Informations d'identification | Description|
-----------|------------|
O365Credential | Spécifie un e-mail de toosend du compte d’utilisateur Office 365 valid.  Uniquement requis si la valeur de variable SendMailO365-IsSendEmail-MS-Mgmt est trop**True**.

## <a name="configuration"></a>Configuration

Effectuer hello suivant les étapes tooadd hello machines virtuelles de démarrage/arrêt pendant les heures creuses [Aperçu] solution tooyour compte Automation, puis configurez solution de hello toocustomize hello variables.

1. À partir de hello-écran d’accueil Bonjour portail Azure, sélectionnez hello **Marketplace** vignette.  Si la vignette de hello n’est plus épinglé tooyour-écran d’accueil, à partir du volet de navigation gauche hello, sélectionnez **nouveau**.  
2. Dans le panneau de Marketplace hello, tapez **démarrer un ordinateur virtuel** dans la zone de recherche hello et de la solution de hello puis **machines virtuelles de démarrage/arrêt pendant les heures creuses [Aperçu]** hello résultats de recherche.  
3. Bonjour **machines virtuelles de démarrage/arrêt pendant les heures creuses [Aperçu]** panneau pour hello sélectionné la solution, passez en revue les informations de résumé hello, puis sur **créer**.  
4. Hello **ajouter la Solution** panneau s’affiche où vous êtes invité à tooconfigure hello solution avant de pouvoir l’importer dans votre abonnement Automation.<br><br> ![Panneau Ajouter une solution de VM Management (Gestion de machines virtuelles)](media/automation-solution-vm-management/vm-management-solution-add-solution-blade.png)<br><br>
5.  Sur hello **ajouter la Solution** panneau, sélectionnez **espace de travail** et vous sélectionnez ici un espace de travail OMS qui est lié toohello même abonnement Azure hello compte Automation est dans ou créer un espace de travail OMS.  Si vous n’avez pas un espace de travail OMS, vous pouvez sélectionner **créer un nouvel espace de travail** et hello **espace de travail OMS** panneau, exécutez les opérations hello : 
   - Spécifiez un nom pour hello nouvelle **espace de travail OMS**.
   - Sélectionnez un **abonnement** toolink tooby en sélectionnant à partir de la liste déroulante de hello si la valeur par défaut hello sélectionnée n’est pas appropriée.
   - Pour **Groupe de ressources**, vous pouvez créer un groupe de ressources ou sélectionner un groupe de ressources existant.  
   - Sélectionnez un **emplacement**.  Actuellement hello seuls emplacements fournis pour la sélection sont **sud-est de l’Australie**, **États-Unis**, **Asie du Sud-est**, et **Europe de l’ouest**.
   - Sélectionner un **niveau de tarification**.  Hello est disponible dans deux niveaux : libérer et OMS payé couche.  niveau gratuit de Hello a une limite de quantité hello de données collectées quotidiennement, période de rétention et minutes de runtime de travail de runbook.  Hello OMS payé couche n’a pas une limite de quantité hello de données collectées quotidiennement.  

        > [!NOTE]
        > Hello autonome payée couche est affichée en tant qu’option, il n’est pas applicable.  Si vous sélectionnez et poursuivez la création de hello de cette solution dans votre abonnement, il échouera.  Ce problème sera résolu lors de la sortie officielle de cette solution.<br>Si vous utilisez cette solution, elle utilise uniquement les minutes du travail d’automatisation et l’ingestion du journal.  solution de Hello n’ajoute pas l’environnement tooyour de nœuds supplémentaires OMS.  

6. Après avoir entré des informations de hello requis sur hello **espace de travail OMS** panneau, cliquez sur **créer**.  Alors que les informations de hello sont vérifiées et espace de travail hello est créé, vous pouvez suivre sa progression sous **Notifications** à partir du menu de hello.  Vous serez renvoyé toohello **ajouter la Solution** panneau.  
7. Sur hello **ajouter la Solution** panneau, sélectionnez **compte Automation**.  Si vous créez un nouvel espace de travail OMS, vous serez requis tooalso créer un nouveau compte Automation qui sera associée à hello nouvel espace de travail OMS spécifié précédemment, y compris votre abonnement Azure, le groupe de ressources et la région.  Vous pouvez sélectionner **créer un compte Automation** et hello **compte Automation d’ajouter** panneau, fournir hello suivantes : 
  - Bonjour **nom** , entrez le nom hello Hello compte Automation.

    Toutes les autres options sont automatiquement remplies en fonction de l’espace de travail OMS hello sélectionné et ces options ne peut pas être modifiées.  Un compte d’identification Azure est la méthode d’authentification par défaut hello pour les runbooks hello inclus dans cette solution.  Une fois que vous cliquez sur **OK**, options de configuration hello sont validées et hello compte Automation est créé.  Vous pouvez suivre sa progression sous **Notifications** à partir du menu de hello. 

    Sinon, vous pouvez sélectionner un compte d’identification Automation existant.  Notez que compte hello sélectionné ne peut pas être déjà lié tooanother espace de travail OMS, sinon un message s’affiche dans hello panneau tooinform vous.  Si elle est déjà lié, vous serez peut-être tooselect un autre compte Automation exécuter en tant qu’ou créez-en un.<br><br> ![Automation tooOMS compte déjà lié espace de travail](media/automation-solution-vm-management/vm-management-solution-add-solution-blade-autoacct-warning.png)<br>

8. Pour finir sur hello **ajouter la Solution** panneau, sélectionnez **Configuration** et hello **paramètres** panneau s’affiche.  Sur hello **paramètres** panneau, vous êtes invité à :  
   - Spécifiez hello **les noms de groupe de ressources cible**, qui est un nom de groupe de ressources qui contient les toobe d’ordinateurs virtuels géré par cette solution.  Vous pouvez entrer plusieurs noms en les séparant à l’aide de points-virgules (les valeurs respectent la casse).  À l’aide d’un caractère générique est pris en charge si vous souhaitez que les machines virtuelles de tootarget dans tous les groupes de ressources dans l’abonnement de hello.
   - Sélectionnez un **planification** qui est une périodique de date et heure de démarrage et arrêt hello la machine virtuelle Bonjour ciblent des groupes de ressources.  Par défaut, la planification de hello est horaire configuré toohello UTC et en sélectionnant une autre région n’est pas disponible.  Si vous le souhaitez tooconfigure hello tooyour spécifique fuseau horaire de planification après la configuration de solution de hello, consultez [planification de démarrage et d’arrêt de hello modification](#modifying-the-startup-and-shutdown-schedule) ci-dessous.    

10. Une fois que vous avez terminé la configuration hello initiale des paramètres requis pour la solution de hello, sélectionnez **créer**.  Tous les paramètres seront validés et puis il tentera de solution de hello toodeploy dans votre abonnement.  Ce processus peut prendre plusieurs secondes toocomplete et que vous pouvez suivre sa progression sous **Notifications** à partir du menu de hello. 

## <a name="collection-frequency"></a>Fréquence de collecte

Automation journal et la tâche de flux de données données de la tâche sont intégrées dans le référentiel d’OMS hello toutes les cinq minutes.  

## <a name="using-hello-solution"></a>À l’aide de la solution de hello

Lorsque vous ajoutez la solution de gestion de la machine virtuelle de hello, dans votre hello d’espace de travail OMS **StartStopVM vue** vignette sera ajoutée tooyour du tableau de bord OMS.  Cette vignette affiche un nombre et une représentation graphique des travaux de runbooks hello pour les solutions hello qui ont démarré et ont abouti.<br><br> ![Vignette StartStopVMView de VM Management (Gestion de machines virtuelles)](media/automation-solution-vm-management/vm-management-solution-startstopvm-view-tile.png)  

Dans votre compte Automation, vous pouvez accéder et gérer des solutions de hello en sélectionnant hello **Solutions** vignette dans hello **Solutions** panneau, en sélectionnant la solution hello **[[[début-Stop-VM Espace de travail]** à partir de la liste de hello.<br><br> ![Liste Solutions d’Automation](media/automation-solution-vm-management/vm-management-solution-autoaccount-solution-list.png)  

Sélectionnez les solutions hello afficher hello **Start-Stop-VM [espace de travail]** Panneau de la solution, où vous pouvez consulter des informations importantes telles que hello **StartStopVM** vignette, comme dans votre espace de travail OMS, qui affiche un nombre et une représentation graphique des travaux de runbooks hello pour les solutions hello qui ont démarré et ont abouti.<br><br> ![Panneau Solution d’Automation](media/automation-solution-vm-management/vm-management-solution-solution-blade.png)  

À ce stade, vous pouvez également ouvrir votre espace de travail OMS et approfondir l’analyse des enregistrements de tâche hello.  Cliquez simplement sur **tous les paramètres**et Bonjour **paramètres** panneau, sélectionnez **Quick Start** , puis dans hello **démarrage rapide** sélectionnez du panneau  **Portail OMS**.   Cela a pour effet d’ouvrir un nouvel onglet ou une nouvelle session de navigateur et de présenter votre espace de travail OMS associé à votre compte et votre abonnement Automation.  


### <a name="configuring-e-mail-notifications"></a>Configuration des notifications par courrier électronique

tooenable les notifications par courrier électronique lorsque hello démarrer et arrêter des runbooks de machine virtuelle terminée, vous devez toomodify hello **O365Credential** des informations d’identification et au minimum, hello variables suivantes :

 - SendMailO365-IsSendEmail-MS-Mgmt
 - StartByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt
 - StopByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt

tooconfigure hello **O365Credential** informations d’identification, effectuer hello comme suit :

1. À partir de votre compte automation, cliquez sur **tous les paramètres** haut hello de fenêtre hello. 
2. Sur hello **paramètres** panneau section hello **ressources Automation**, sélectionnez **actifs**. 
3. Sur hello **actifs** panneau, sélectionnez hello **informations d’identification** vignette et de hello **informations d’identification** panneau, sélectionnez hello **O365Credential**.  
4. Entrez un nom d’utilisateur valide de Office 365 et le mot de passe, puis **enregistrer** toosave vos modifications.  

les variables de hello tooconfigure mis en surbrillance, effectuez hello comme suit :

1. À partir de votre compte automation, cliquez sur **tous les paramètres** haut hello de fenêtre hello. 
2. Sur hello **paramètres** panneau section hello **ressources Automation**, sélectionnez **actifs**. 
3. Sur hello **actifs** panneau, sélectionnez hello **Variables** vignette et de hello **Variables** panneau, sélectionnez variable hello répertorié ci-dessus et modifiez sa valeur suivante hello Description pour qu’il est spécifié dans hello [variable](##variables) section précédemment.  
4. Cliquez sur **enregistrer** variable de toohello modifications toosave hello.   

### <a name="modifying-hello-startup-and-shutdown-schedule"></a>Modification planification hello de démarrage et d’arrêt

Planification de démarrage et d’arrêt hello gestion dans cette solution suit hello même les étapes décrites dans [planification d’un runbook dans Azure Automation](automation-schedules.md).  N’oubliez pas, vous ne pouvez pas modifier la configuration de la planification hello.  Vous devez toodisable hello planification existante, puis créez-en un et puis liez toohello **StartByResourceGroup-MS-Mgmt-VM** ou **StopByResourceGroup-MS-Mgmt-VM** runbook que vous souhaitez hello planifier tooapply à.   

## <a name="log-analytics-records"></a>Enregistrements Log Analytics

Automation crée deux types d’enregistrements dans le référentiel d’OMS hello.

### <a name="job-logs"></a>Journaux de tâches

Propriété | Description|
----------|----------|
Appelant |  Qui a lancé une opération hello.  Les valeurs possibles sont une adresse de messagerie ou un système pour les travaux planifiés.|
Catégorie | Classification de type hello de données.  Pour l’automatisation, la valeur de hello est JobLogs.|
CorrelationId | GUID qui est hello Id de corrélation de tâche du runbook hello.|
JobId | GUID qui est hello Id de tâche du runbook hello.|
operationName | Spécifie le type hello d’opération exécutée dans Azure.  Pour l’automatisation, hello aura travail.|
resourceId | Spécifie le type de ressource hello dans Azure.  Pour l’automatisation, valeur de hello est compte d’automatisation hello associé hello runbook.|
ResourceGroup | Spécifie le nom du groupe de ressources de la tâche du runbook hello hello.|
ResourceProvider | Spécifie les hello service Azure qui fournit des ressources hello vous pouvez déployer et gérer.  Pour l’automatisation, la valeur de hello est Azure Automation.|
ResourceType | Spécifie le type de ressource hello dans Azure.  Pour l’automatisation, valeur de hello est compte d’automatisation hello associé hello runbook.|
resultType | état de Hello de tâche du runbook hello.  Les valeurs possibles sont les suivantes :<br>Démarré<br>Arrêté<br>Interrompu<br>Échec<br>- Succeeded|
resultDescription | Décrit l’état de résultat du travail de runbook hello.  Les valeurs possibles sont les suivantes :<br>- Job is started<br>- Job Failed<br>- Job Completed|
RunbookName | Spécifie le nom hello de hello runbook.|
SourceSystem | Spécifie le système de source de hello pour les données hello soumises.  Pour l’automatisation, hello aura : OpsManager|
StreamType | Spécifie le type hello d’événement. Les valeurs possibles sont les suivantes :<br>- Verbose<br>Sortie<br>Error<br>Avertissement|
SubscriptionId | Spécifie l’ID d’abonnement hello du travail de hello.
Temps | Date et heure à l’exécution de tâche du runbook hello.|


### <a name="job-streams"></a>Flux de tâches

Propriété | Description|
----------|----------|
Appelant |  Qui a lancé une opération hello.  Les valeurs possibles sont une adresse de messagerie ou un système pour les travaux planifiés.|
Catégorie | Classification de type hello de données.  Pour l’automatisation, la valeur de hello est JobStreams.|
JobId | GUID qui est hello Id de tâche du runbook hello.|
operationName | Spécifie le type hello d’opération exécutée dans Azure.  Pour l’automatisation, hello aura travail.|
ResourceGroup | Spécifie le nom du groupe de ressources de la tâche du runbook hello hello.|
resourceId | Spécifie l’Id de ressource hello dans Azure.  Pour l’automatisation, valeur de hello est compte d’automatisation hello associé hello runbook.|
ResourceProvider | Spécifie les hello service Azure qui fournit des ressources hello vous pouvez déployer et gérer.  Pour l’automatisation, la valeur de hello est Azure Automation.|
ResourceType | Spécifie le type de ressource hello dans Azure.  Pour l’automatisation, valeur de hello est compte d’automatisation hello associé hello runbook.|
resultType | résultat de Hello de tâche du runbook à l’événement hello hello hello a été généré.  Les valeurs possibles sont les suivantes :<br>- InProgress|
resultDescription | Inclut le flux de sortie hello hello runbook.|
RunbookName | nom de Hello de hello runbook.|
SourceSystem | Spécifie le système de source de hello pour les données hello soumises.  Pour l’automatisation, hello aura OpsManager|
StreamType | type de Hello du flux de travail. Les valeurs possibles sont les suivantes :<br>progress<br>Sortie<br>Avertissement<br>error<br>DEBUG<br>- Verbose|
Temps | Date et heure à l’exécution de tâche du runbook hello.|

Lorsque vous effectuez une recherche de journal qui retourne des enregistrements de la catégorie de **JobLogs** ou **JobStreams**, vous pouvez sélectionner hello **JobLogs** ou **JobStreams** vue qui affiche un ensemble de vignettes de résumé des mises à jour hello retournées par la recherche de hello.

## <a name="sample-log-searches"></a>Exemples de recherches dans les journaux

Hello tableau suivant fournit des exemples des recherches de journaux pour les enregistrements de tâche collectées par cette solution. 

Interroger | Description|
----------|----------|
Rechercher les tâches du runbook StartVM exécutées avec succès | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" ResultType=Succeeded &#124; measure count() by JobId_g|
Rechercher les tâches du runbook StopVM exécutées avec succès | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" ResultType=Failed &#124; measure count() by JobId_g
Afficher l’état des tâches au fil du temps pour les runbooks StartVM et StopVM | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" OR "StopByResourceGroup-MS-Mgmt-VM" NOT(ResultType="started") | measure Count() by ResultType interval 1day|

## <a name="removing-hello-solution"></a>Suppression de solution de hello

Si vous décidez que vous n’avez plus besoin solution de hello toouse tout davantage, vous pouvez le supprimer à partir de hello compte Automation.  Suppression de la solution de hello supprime uniquement les procédures opérationnelles de hello, elle ne supprime pas les planifications hello ou des variables qui ont été créés lors de la solution de hello a été ajoutée.  Ces composants vous devez toodelete manuellement si vous ne les utilisez pas avec les autres runbooks.  

toodelete hello solution, effectuer hello comme suit :

1.  À partir de votre compte automation, sélectionnez hello **Solutions** vignette.  
2.  Sur hello **Solutions** les lames, les solutions hello sélectionnez **Start-Stop-VM [espace de travail]**.  Sur hello **VMManagementSolution [espace de travail]** panneau, cliquez sur le menu hello **supprimer**.<br><br> ![Supprimer la solution de gestion de machine virtuelle](media/automation-solution-vm-management/vm-management-solution-delete.png)
3.  Bonjour **supprimer la Solution** fenêtre, confirmer la solution de hello toodelete.
4.  Alors que les informations de hello sont vérifiées et les solutions hello sont supprimée, vous pouvez suivre sa progression sous **Notifications** à partir du menu de hello.  Vous serez renvoyé toohello **VMManagementSolution [espace de travail]** panneau après le démarrage de la solution tooremove des processus hello.  

compte d’automatisation Hello et espace de travail OMS ne sont pas supprimés dans le cadre de ce processus.  Si vous ne souhaitez pas l’espace de travail tooretain hello OMS, vous devez supprimer toomanually.  Il est possible également de hello portail Azure.   Hello-écran d’accueil Bonjour portail Azure, sélectionnez **Analytique de journal** et puis sur hello **Analytique de journal** panneau, espace de travail hello sélectionnez et cliquez sur **supprimer** à partir du menu hello Panneau de paramètres d’espace de travail de Hello.  
      
## <a name="next-steps"></a>Étapes suivantes

- toolearn en savoir plus sur la façon dont des journaux d’Analytique de journal, de travail de tooconstruct les requêtes de recherche différente et révision hello Automation voir [connectez-vous recherche Analytique de journal](../log-analytics/log-analytics-log-searches.md)
- toolearn plus d’informations sur l’exécution du runbook, comment les tâches de runbook toomonitor et d’autres détails techniques, consultez [suivre un travail de runbook](automation-runbook-execution.md)
- toolearn en savoir plus sur l’Analytique des journaux OMS et les sources de collection de données, consultez [les données de stockage Azure de collecte dans la vue d’ensemble Analytique de journal](../log-analytics/log-analytics-azure-storage.md)






   

