---
title: "Didacticiel : Créer un pipeline à l’aide de l’Assistant de copie | Microsoft Docs"
description: "Dans ce didacticiel, vous créez un pipeline Azure Data Factory avec une activité de copie à l’aide de hello Assistant copie de prise en charge par la fabrique de données"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b87afb8e-53b7-4e1b-905b-0343dd096198
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 567b89e7a54c245c134cd0674690e6f3499b46d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a>Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy
> [!div class="op_single_selector"]
> * [Vue d’ensemble et étapes préalables requises](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Assistant de copie](data-factory-copy-data-wizard-tutorial.md)
> * [Portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Modèle Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

Ce didacticiel vous montre comment toouse hello **Assistant copie de** toocopy des données à partir d’une base de données SQL Azure de tooan stockage blob Azure. 

Bonjour Azure Data Factory **Assistant copie de** vous permet de tooquickly créer un pipeline de données qui copie les données à partir d’un magasin de données de destination source prise en charge données magasin tooa pris en charge. Par conséquent, nous vous recommandons d’utiliser l’Assistant de hello comme une première toocreate d’étape un exemple de pipeline pour votre scénario de déplacement des données. Pour obtenir la liste des magasins de données pris en charge en tant que sources et destinations, consultez [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) .  

Ce didacticiel vous montre comment toocreate une fabrique de données Azure, lancement hello, Assistant copie de parcourir les détails de tooprovide étapes sur votre scénario de réception/le déplacement des données. Lorsque vous avez terminé les étapes décrites dans l’Assistant de hello, hello crée automatiquement un pipeline comportant des données toocopy d’activité de copie à partir d’une base de données SQL Azure de tooan stockage blob Azure. Pour plus d’informations sur l’activité de copie, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md).

## <a name="prerequisites"></a>Composants requis
Terminer la configuration requise indiquée dans hello [vue d’ensemble du didacticiel](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article avant d’effectuer ce didacticiel.

## <a name="create-data-factory"></a>Créer une fabrique de données
Dans cette étape, vous utilisez hello toocreate portail Azure une fabrique de données Azure nommée **ADFTutorialDataFactory**.

1. Connectez-vous trop[portail Azure](https://portal.azure.com).
2. Cliquez sur **+ nouveau** à partir de l’angle supérieur gauche de hello, cliquez sur **données + analytique**, puis cliquez sur **Data Factory**. 
   
   ![Nouveau -> DataFactory](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. Bonjour **nouvelle fabrique de données** panneau :
   
   1. Entrez **ADFTutorialDataFactory** pour hello **nom**.
       nom de Hello de fabrique de données Azure hello doit être globalement unique. Si vous recevez une erreur de hello : `Data factory name “ADFTutorialDataFactory” is not available`, de modifier le nom hello hello fabrique de données (par exemple, yournameADFTutorialDataFactoryYYYYMMDD) et essayez à nouveau de créer. Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.  
      
       ![Nom de la fabrique de données indisponible](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. Sélectionnez votre **abonnement**Azure.
   3. Pour le groupe de ressources, effectuez l’une des hello comme suit : 
      
      - Sélectionnez **utiliser l’existante** tooselect un groupe de ressources existant.
      - Sélectionnez **nouvel** tooenter un nom pour un groupe de ressources.
          
        Certaines des étapes hello dans ce didacticiel supposent que vous utilisez hello nom : **ADFTutorialResourceGroup** pour le groupe de ressources hello. toolearn sur les groupes de ressources, consultez [à l’aide de la ressource groupes toomanage vos ressources Azure](../azure-resource-manager/resource-group-overview.md).
   4. Sélectionnez un **emplacement** de fabrique de données hello.
   5. Sélectionnez **toodashboard du code confidentiel** bas hello du Panneau de hello de case à cocher.  
   6. Cliquez sur **Créer**.
      
       ![Panneau Nouvelle fabrique de données](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. Après la création de hello est terminée, vous voyez hello **Data Factory** panneau comme indiqué dans hello suivant image :
   
   ![Page d'accueil Data Factory](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a>Lancer l’Assistant Copie
1. Dans le panneau de la fabrique de données hello, cliquez sur **copier des données [Aperçu]** toolaunch hello **Assistant copie de**. 
   
   > [!NOTE]
   > Si vous voyez ce navigateur hello est bloqué au niveau de « Autorisation... », désactiver/Décochez **bloquer les cookies tiers et les données de site** définition dans les paramètres du navigateur hello (ou) conserver cette option activée et créer une exception pour  **Login.microsoftonline.com** , puis essayez de lancer les Assistant hello à nouveau.
2. Bonjour **propriétés** page :
   
   1. Saisissez **CopyFromBlobToAzureSql** dans **Nom de la tâche**.
   2. Saisissez une **Description** (facultative).
   3. Hello de modification **date heure de début** et hello **date heure de fin** afin que la date de fin hello est définie tootoday date toofive jours précédemment.  
   4. Cliquez sur **Suivant**.  
      
      ![Outil de copie - page Propriétés](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. Sur hello **magasin de données Source** , cliquez sur **stockage d’objets Blob Azure** vignette. Vous utilisez cette banque de données de page toospecify hello source pour la tâche de copie hello. 
   
    ![Outil de copie - page Source data store (Magasin de données source)](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. Sur hello **spécifier le compte de stockage d’objets Blob Azure hello** page :
   
   1. Saisissez **AzureStorageLinkedService** dans **Nom du service lié**.
   2. Vérifiez que l’option **À partir des abonnements** est sélectionnée pour **Account selection method** (Méthode de sélection du compte).
   3. Sélectionnez votre **abonnement**Azure.  
   4. Sélectionnez un **compte de stockage Azure** hello à partir de la liste de stockage Azure comptes disponible dans l’abonnement de hello sélectionné. Vous pouvez également choisir tooenter les paramètres de compte de stockage manuellement en sélectionnant **entrer manuellement** option hello **méthode de sélection du compte**, puis cliquez sur **suivant**. 
      
      ![Outil Copier - spécifiez le compte de stockage d’objets Blob Azure hello](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. Sur **choisir un fichier d’entrée hello ou un dossier** page :
   
   1. Double-cliquez sur **adftutorial** (dossier).
   2. Sélectionnez **emp.txt**, puis cliquez sur **Choisir**.
      
      ![Outil Copier - choisir un fichier d’entrée de hello ou un dossier](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. Sur hello **choisir un fichier d’entrée hello ou un dossier** , cliquez sur **suivant**. Ne sélectionnez pas **copie binaire**. 
   
    ![Outil Copier - choisir un fichier d’entrée de hello ou un dossier](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. Sur hello **les paramètres de format de fichier** page, vous voyez les délimiteurs hello et schéma de hello est détecté automatiquement par l’Assistant de hello par l’analyse du fichier de hello. Vous pouvez également entrer manuellement des délimiteurs de hello pour hello copie Assistant toostop détection automatique ou toooverride. Cliquez sur **suivant** une fois que vous passez en revue les délimiteurs hello et afficher un aperçu des données. 
   
    ![Outil de copie - Paramètres de format de fichier](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. Sur les données de Destination hello Boutique, sélectionnez **base de données SQL Azure**, puis cliquez sur **suivant**.
   
    ![Outil de copie - Choisir une banque de destination](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. Sur **base de données SQL Azure spécifiez hello** page :
   
   1. Entrez **AzureSqlLinkedService** pour hello **nom de la connexion** champ.
   2. Vérifiez que l’option **À partir des abonnements** est sélectionnée pour **Server / database selection method** (Méthode de sélection du serveur/de la base de données).
   3. Sélectionnez votre **abonnement**Azure.  
   4. Sélectionnez le **Nom du serveur** et la **Base de données**.
   5. Saisissez le **Nom d’utilisateur** et le **Mot de passe**.
   6. Cliquez sur **Suivant**.  
      
      ![Outil de copie - Spécifier la base de données SQL Azure](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. Sur hello **mappage de Table** page, sélectionnez **emp** pour hello **Destination** à partir de la liste déroulante de hello, cliquez sur **bas** (facultatif) toosee hello schéma et toopreview hello les données.
    
     ![Outil de copie - Mappage de Table](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. Sur hello **le mappage de schéma** , cliquez sur **suivant**.
    
    ![Outil de copie - Mappage de schéma](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. Sur hello **les paramètres de performances** , cliquez sur **suivant**. 
    
    ![Outil de copie - Paramètres de performances](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. Passez en revue les informations contenues dans hello **Résumé** page, puis cliquez sur **Terminer**. Assistant de Hello crée deux services liés, les deux jeux de données (entrées et sorties) et un seul pipeline dans la fabrique de données hello (à partir de lancement de hello Assistant copie de). 
    
    ![Outil de copie - Paramètres de performances](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a>Lancer l’application Surveiller et gérer
1. Sur hello **déploiement** , cliquez sur le lien de hello : `Click here toomonitor copy pipeline`.
   
   ![Outil de copie - Déploiement réussi](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. Hello analyse de l’application est lancée dans un onglet distinct dans votre navigateur web.   
   
   ![Application de surveillance](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. état le plus récent hello toosee de tranches horaires, cliquez sur **Actualiser** bouton Bonjour **WINDOWS de l’activité** liste à la fin de hello. Vous voyez cinq windows d’activité pendant cinq jours entre les heures de début et de fin de pipeline de hello. liste de Hello n’est pas automatiquement actualisée, donc vous pouvez peut-être tooclick actualiser plusieurs fois avant de voir toutes les fenêtres d’activité hello prêt hello. 
4. Sélectionnez une fenêtre d’activité dans la liste de hello. Afficher les détails de hello concernant Bonjour **activité fenêtre Explorateur** sur hello droite.

    ![Détails de la fenêtre d’activité](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    Notez que les dates de hello 11, 12, 13, 14 et 15 sont au vert, ce qui signifie que hello quotidienne des tranches de sortie pour ces dates ont déjà été générés. Vous consultez ce codage en couleurs dans le pipeline de hello et hello du jeu de données de sortie dans la vue de diagramme hello. Dans étape précédente de hello, notez que deux tranches ont déjà été produits, une tranche est en cours de traitement, et hello deux autres attendent toobe traité (basé sur le codage en couleurs hello). 

    Pour plus d’informations sur l’utilisation de cette application, consultez l’article [Surveiller et gérer les pipelines Azure Data Factory à l’aide de la nouvelle application de surveillance et de gestion](data-factory-monitor-manage-app.md).

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez utilisé le stockage Blob Azure comme magasin de données source et une base de données SQL Azure comme banque de données de destination dans une opération de copie. Hello tableau suivant fournit une liste de banques de données pris en charge en tant que sources et destinations par l’activité de copie hello : 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

Pour plus d’informations sur les champs et propriétés que vous voyez dans l’Assistant copie de hello pour un magasin de données, cliquez sur lien hello hello magasin de données dans la table de hello. 
