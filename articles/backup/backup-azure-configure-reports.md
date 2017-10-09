---
title: Rapports aaaConfigure pour la sauvegarde Azure
description: "Cet article traite de la configuration des rapports Power BI pour la Sauvegarde Azure à l’aide d’un coffre Recovery Services."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 86e465f1-8996-4a40-b582-ccf75c58ab87
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 503a240b36ea999e0fea434b6a50d26ddf7677bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-backup-reports"></a>Configurer les rapports de la Sauvegarde Azure
Cet article traite à propos des rapports de tooconfigure étapes pour la sauvegarde Azure à l’aide du coffre Recovery Services et tooaccess ces rapports à l’aide de Power BI. Après avoir effectué ces étapes, vous pouvez directement accéder tooPower BI tooview tous les rapports de hello, personnaliser et créer des rapports. 

## <a name="supported-scenarios"></a>Scénarios pris en charge
1. Les rapports de sauvegarde Azure sont pris en charge pour la machine virtuelle Azure sauvegarde et fichier/dossier sauvegarde toocloud à l’aide d’Azure Recovery Services Agent.
2. Pour l’instant, les rapports ne sont pas pris en charge pour SQL Azure, DPM et le serveur de sauvegarde Azure.
3. Vous pouvez afficher des rapports sur les coffres et les abonnements, si le même compte de stockage est configuré pour chacun des coffres de hello. Compte de stockage sélectionné doit être Bonjour même région que la récupération des services coffre.
4. fréquence de Hello d’actualisation planifiée pour les rapports de hello est de 24 heures dans Power BI. Vous pouvez également effectuer une actualisation ad hoc de hello rapports dans Power BI, dans lequel les données les plus récentes cas dans le compte de stockage sont utilisées pour le rendu des rapports. 

## <a name="prerequisites"></a>Composants requis
1. Créer un [compte de stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) tooconfigure pour des rapports. Il est utilisé pour stocker les données associées aux rapports.
2. [Créer un compte Power BI](https://powerbi.microsoft.com/landing/signin/) tooview, personnaliser et créer vos propres rapports à l’aide du portail Power BI.
3. Inscrire le fournisseur de ressources hello **Microsoft.insights** si ne pas déjà inscrit, avec un abonnement hello de compte de stockage et également avec un abonnement hello de Services de récupération de coffre de tooenable toohello tooflow de données de création de rapports compte de stockage. toodo hello même, vous devez tooAzure portal > abonnement > fournisseurs de ressources et vérifiez cette tooregister fournisseur il. 

## <a name="configure-storage-account-for-reports"></a>Configurer le compte de stockage pour les rapports
Utilisez hello suivant du compte de stockage suit tooconfigure hello pour le coffre recovery services à l’aide du portail Azure. Il s’agit d’une configuration unique et une fois que le compte de stockage est configuré, vous pouvez accéder tooPower BI directement tooview pack de contenu et de tirer parti des rapports.
1. Si vous avez déjà ouvert un coffre Recovery Services, passez toonext étape. Si vous n’avez pas d’un coffre Recovery Services est ouvert, mais sont Bonjour portail Azure, dans le menu du Hub hello, cliquez sur **Parcourir**.

   * Dans la liste de hello des ressources, tapez **Recovery Services**.
   * Comme vous commencez à taper, hello filtres de la liste en fonction de votre entrée. Lorsque vous voyez **Coffres Recovery Services**, cliquez dessus.

      ![Créer un archivage de Recovery Services - Étape 1](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     liste Hello des archivages de Recovery Services s’affiche. À partir de la liste de hello des archivages de Recovery Services, sélectionnez un coffre.

     tableau de bord Hello coffre-fort sélectionné s’ouvre.
2. À partir de la liste hello des éléments qui s’affiche sous le coffre, cliquez sur **sauvegarde rapports** sous surveillance et rapports section tooconfigure hello compte de stockage pour les rapports.

      ![Sélectionner l’élément de menu Rapports de sauvegarde - Étape 2](./media/backup-azure-configure-reports/backup-reports-settings.PNG)
3. Panneau des rapports de sauvegarde hello, cliquez sur **configurer** bouton. Cela ouvre le panneau des Application Azure Insights hello qui est utilisée pour pousser le compte de stockage de données toocustomer.

      ![Configurer le compte de stockage - Étape 3](./media/backup-azure-configure-reports/configure-storage-account.PNG)
4. Définir le bouton bascule du statut hello trop**sur** et sélectionnez **archiver tooa compte de stockage** case à cocher pour que les rapports de données peuvent démarrer circulent dans le compte de stockage toohello.

      ![Activer les diagnostics - Étape 4](./media/backup-azure-configure-reports/set-status-on.png)
5. Cliquez sur le sélecteur de compte de stockage et le compte de stockage hello select à partir de la liste de hello pour stocker les rapports des données et cliquez sur **OK**.

      ![Sélectionner le compte de stockage - Étape 5](./media/backup-azure-configure-reports/select-storage-account.png)
6. Sélectionnez **AzureBackupReport** case à cocher et également déplacer période de rétention hello curseur tooselect pour cela les données de rapport. Les données dans le compte de stockage hello de rapport sont conservée pendant période hello sélectionnée à l’aide de ce curseur.

      ![Sélectionner le compte de stockage - Étape 6](./media/backup-azure-configure-reports/save-configuration.png)
7. Passez en revue toutes les modifications de hello et cliquez sur **enregistrer** bouton en haut, comme indiqué dans la figure hello ci-dessus. Cette action garantit que toutes vos modifications sont enregistrées et que le compte de stockage est maintenant configuré de façon à stocker les données de rapports.

> [!NOTE]
> Une fois que vous configurez des rapports à l’enregistrement de compte de stockage, vous devez **attendre 24 heures** pour toocomplete de push de données initiale. Vous devez importer le pack de contenu Azure Backup dans Power BI uniquement après cette heure. Consultez [la section FAQ](#frequently-asked-questions) pour plus de détails. 
>
>

## <a name="view-reports-in-power-bi"></a>Afficher les rapports dans Power BI 
Une fois la configuration du compte de stockage pour des rapports à l’aide du coffre recovery services, il prend environ 24 heures pour les rapports toostart données circulent dans. Après 24 heures de la configuration d’un compte de stockage, suivi de hello utilisez les étapes tooview des rapports dans Power BI :
1. [Connectez-vous](https://powerbi.microsoft.com/landing/signin/) tooPower BI.
2. Cliquez sur **Obtenir les données** et cliquez sur Obtenir sous **Services** dans la bibliothèque de packs de contenu. Utilisez les étapes indiquées dans [pack de contenu Power BI documentation tooaccess](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-packs-services/).

     ![Importer un pack de contenu](./media/backup-azure-configure-reports/content-pack-import.png)
3. Tapez **Sauvegarde Azure** dans la barre de recherche et cliquez sur **Obtenir maintenant**.

      ![Obtenir un pack de contenu](./media/backup-azure-configure-reports/content-pack-get.png)
4. Entrez le nom de compte de stockage hello configuré à l’étape 5 ci-dessus, cliquez sur **suivant** bouton.

    ![Entrer le nom du compte de stockage](./media/backup-azure-configure-reports/content-pack-storage-account-name.png)    
5. Entrez la clé de compte de stockage hello pour ce compte de stockage. Vous pouvez [afficher et copier les clés d’accès de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-account) en naviguant tooyour compte de stockage dans le portail Azure. 

     ![Entrer le compte de stockage](./media/backup-azure-configure-reports/content-pack-storage-account-key.png) <br/>
     
6. Cliquez sur le bouton **Se connecter**. Lorsque la connexion est établie, vous obtenez une notification **Importation de données**.

    ![Importer un pack de contenu](./media/backup-azure-configure-reports/content-pack-importing-data.png) <br/>
    
    Après un certain temps, vous obtenez **réussite** notification une fois l’importation hello est terminée. S’il existe une grande quantité de données dans le compte de stockage hello peut prendre un peu plus de temps tooimport hello pack de contenu.
    
    ![Importer le pack de contenu - Réussite](./media/backup-azure-configure-reports/content-pack-import-success.png) <br/>
    
7. Une fois que les données sont importées avec succès, **Azure Backup** pack de contenu est visible dans **applications** dans le volet de navigation hello. liste de Hello affiche maintenant Azure Backup de tableau de bord, rapports et jeu de données avec une étoile jaune, indiquant les rapports nouvellement importés. 

     ![Pack de contenu de la Sauvegarde Azure](./media/backup-azure-configure-reports/content-pack-azure-backup.png) <br/>
     
8. Cliquez sur **Sauvegarde Azure** sous Tableaux de bord ; un ensemble de rapports clés épinglés s’affiche.

      ![Tableau de bord de la Sauvegarde Azure](./media/backup-azure-configure-reports/azure-backup-dashboard.png) <br/>
9. ensemble complet de hello tooview de rapports, cliquez sur n’importe quel rapport dans le tableau de bord hello.

      ![Intégrité des travaux de la Sauvegarde Azure](./media/backup-azure-configure-reports/azure-backup-job-health.png) <br/>
10. Cliquez sur chaque onglet tooview rapports hello dans cette zone.

      ![Onglets des rapports de la Sauvegarde Azure](./media/backup-azure-configure-reports/reports-tab-view.png)


## <a name="frequently-asked-questions"></a>Forum Aux Questions
1. **Comment vérifier si les données de création de rapports a démarré circulent dans toostorage compte ?**
    
    Vous pouvez accéder toohello stockage configurés et sélectionnez les conteneurs du compte. Si le conteneur de hello comporte une entrée pour insights-journaux-azurebackupreport, il indique que les données de rapport a démarré circulent.

2. **Quelle est la fréquence de hello du compte de toostorage de push de données et le pack de contenu Azure Backup dans Power BI ?**

   Pour les utilisateurs de jour 0, il faudrait compte de toostorage des données toopush environ 24 heures. Une fois cette opération push initiale aboutit, les données sont actualisées avec hello suivant fréquence illustré hello ci-dessous. 
      * Les données relatives trop**travaux, alertes, des éléments de sauvegarde, coffres, serveurs protégés et des stratégies** est transmise compte de stockage toocustomer et lorsqu’il est connecté.
      * Les données relatives trop**stockage** est transmise compte de stockage toocustomer toutes les 24 heures.
   
    ![Fréquence des Push de données des rapports de la Sauvegarde Azure](./media/backup-azure-configure-reports/reports-data-refresh-cycle.png)

  Power BI effectue une [actualisation planifiée une fois par jour](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/#what-can-be-refreshed). Vous pouvez effectuer une actualisation manuelle des données de salutation dans Power BI hello pack de contenu.

3. **Combien puis-je conserver hello rapports ?** 

   Lorsque vous configurez le compte de stockage, vous pouvez sélectionner la période de rétention de données de rapports hello compte de stockage (à l’aide de l’étape 6 de configurer le compte de stockage pour la section rapports ci-dessus). En outre, vous pouvez [Analyser les rapports sous Excel](https://powerbi.microsoft.com/documentation/powerbi-service-analyze-in-excel/) et les enregistrer pour allonger la période de rétention en fonction de vos besoins. 

4. **Je vois toutes mes données dans les rapports après avoir configuré le compte de stockage hello ?**

   Tous les hello données générées après **« compte de stockage de configuration »** sera poussée de compte de stockage toohello et sera disponible dans les rapports. Toutefois, **les travaux En cours ne sont pas transmis** pour la création de rapports. Une fois le travail de hello se termine ou échoue, il est envoyé tooreports.

5. **Si j’ai déjà configuré des rapports de tooview de compte de stockage hello, puis-je modifier hello configuration toouse un autre compte de stockage ?** 

   Oui, vous pouvez modifier hello configuration toopoint tooa autre compte de stockage. Vous devez utiliser le compte de stockage hello qui vient d’être configuré lors de la connexion tooAzure pack de contenu de sauvegarde. En outre, une fois qu’un autre compte de stockage est configuré, les nouvelles données arrivent dans ce compte de stockage. Mais les données plus anciennes (avant la modification de configuration de hello) devrait rester dans le compte de stockage hello plus anciens.

6. **Puis-je afficher des rapports sur différents coffres et différents abonnements ?** 

   Oui, vous pouvez configurer hello même compte de stockage entre les différents rapports d’entre-coffre tooview les coffres. En outre, vous pouvez configurer hello du même compte de stockage pour les coffres entre abonnements. Vous pouvez ensuite utiliser ce compte de stockage lors de la connexion du pack de contenu de sauvegarde tooAzure dans les rapports de hello tooview Power BI. Toutefois, le compte de stockage hello sélectionné doit être Bonjour même région que la récupération des services coffre.
   
## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez configuré le compte de stockage hello et importé pack de contenu de sauvegarde Azure, dans l’étape suivante de hello est toocustomize ces rapports et l’utilisation de rapports de toocreate de modèle de données. Voir la rubrique hello suivant des articles pour plus d’informations.

* [Utiliser le modèle de données de rapports de la Sauvegarde Azure](backup-azure-reports-data-model.md)
* [Filtrer les rapports dans Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-about-filters-and-highlighting-in-reports/)
* [Créer des rapports dans Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/)

