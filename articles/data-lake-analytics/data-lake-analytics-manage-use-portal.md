---
title: "aaaManage Analytique de LAC de données Azure à l’aide de hello portail Azure | Documents Microsoft"
description: "Découvrez comment toomanage acounts Analytique lac de données, données sources, les utilisateurs et des travaux."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: a0e045f1-73d6-427f-868d-7b55c10f811b
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: f63ccdfae79772c92e92462194e8cdc636a73dc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-hello-azure-portal"></a>Gérer Analytique de LAC de données Azure à l’aide de hello portail Azure
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Découvrez comment des comptes toomanage Analytique de LAC de données Azure, des sources de données de compte, des utilisateurs et des travaux à l’aide de hello portail Azure. les rubriques de gestion toosee sur l’utilisation d’autres outils, cliquez sur un onglet en hello haut hello.

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a>Gérer les comptes Data Lake Analytics

### <a name="create-an-account"></a>Créer un compte

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **Nouveau** > **Intelligence + analyse** > **Data Lake Analytics**.
3. Sélectionnez les valeurs de hello éléments suivants : 
   1. **Nom**: nom hello Hello compte d’Analytique lac de données.
   2. **Abonnement**: hello abonnement Azure utilisé pour le compte de hello.
   3. **Groupe de ressources**: groupe de ressources Azure hello dans quel compte de hello toocreate. 
   4. **Emplacement**: hello du centre de données Azure pour compte Analytique lac de données de hello. 
   5. **Data Lake Store**: hello toobe de magasin par défaut utilisé pour hello Analytique lac de données compte. compte d’Azure Data Lake Store Hello et hello Analytique lac de données compte doit être dans hello même emplacement.
4. Cliquez sur **Créer**. 

### <a name="delete-a-data-lake-analytics-account"></a>Supprimer un compte Data Lake Analytics

Avant de supprimer un compte Data Lake Analytics, vous devez supprimer le compte Data Lake Store dépendant.

1. Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.
2. Cliquez sur **Supprimer**.
3. Nom du compte type hello.
4. Cliquez sur **Supprimer**.

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a>Gérer les sources de données

Analytique de LAC de données prend en charge hello les sources de données suivantes :

* Data Lake Store
* Azure Storage

Vous pouvez utiliser des sources de données toobrowse Explorateur de données et effectuer des opérations de gestion de fichiers de base. 

### <a name="add-a-data-source"></a>Ajouter une source de données

1. Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.
2. Cliquez sur **Sources de données**.
3. Cliquez sur **Ajouter une source de données**.
    
   * tooadd un compte Data Lake Store, vous devez compte hello toohello d’accès et le nom de compte tooquery en mesure de toobe il.
   * tooadd stockage d’objets Blob Azure, vous devez compte de stockage hello et clé de compte hello. toofind compte de stockage toohello leur, allez dans le portail de hello.

## <a name="set-up-firewall-rules"></a>Configurer des règles de pare-feu

Vous pouvez utiliser les données Lake Analytique toofurther verrouiller accès tooyour compte d’Analytique lac de données au niveau du réseau hello. Vous pouvez activer un pare-feu, spécifier une adresse IP ou définir une plage d’adresses IP pour vos clients approuvés. Une fois que ces mesures, seuls les clients qui ont des adresses IP de hello plage hello défini peuvent se connecter toohello magasin.

Si d’autres services Azure, comme Azure Data Factory ou des machines virtuelles, vous connecter compte Analytique lac de données de toohello, assurez-vous que **autoriser les Services Azure** est activé **sur**. 

### <a name="set-up-a-firewall-rule"></a>Configurer une règle de pare-feu

1. Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.
2. Dans le menu hello hello gauche, cliquez sur **pare-feu**.

## <a name="add-a-new-user"></a>Ajouter un nouvel utilisateur

Vous pouvez utiliser hello **Assistant Ajout d’utilisateur** tooeasily configurer de nouveaux utilisateurs lac de données.

1. Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.
2. Sur hello de gauche, sous **mise en route**, cliquez sur **Assistant Ajout d’utilisateur**.
3. Sélectionnez un utilisateur, puis cliquez sur **Enregistrer**.
4. Sélectionnez un rôle, puis cliquez sur **Enregistrer**. tooset d’un nouveau toouse de développeur Azure Data Lake, sélectionnez hello **données Lake Analytique développeur** rôle.
5. Sélectionnez les listes de contrôle d’accès hello (ACL) pour les bases de données hello U-SQL. Lorsque vous êtes satisfait de vos choix, cliquez sur **Sélectionner**.
6. Sélectionnez les ACL hello pour les fichiers. Hello banque par défaut, ne modifiez pas les ACL hello pour le dossier racine de hello « / » et pour hello/System dossier. Cliquez sur **Sélectionner**.
7. Passez en revue toutes vos sélections, puis cliquez sur **Exécuter**.
8. Hello Assistant terminé, cliquez sur **fait**.

## <a name="manage-role-based-access-control"></a>Gérer le contrôle d’accès en fonction du rôle

Comme d’autres services Azure, vous pouvez utiliser toocontrol de contrôle d’accès en fonction du rôle (RBAC) comment les utilisateurs interagissent avec le service de hello.

les rôles RBAC standards Hello ont hello suivant de fonctionnalités :
* **Propriétaire**: peut envoyer des travaux, surveillez les travaux, annuler les travaux à partir de n’importe quel utilisateur et configurer le compte de hello.
* **Collaborateur**: peut envoyer des travaux, surveillez les travaux, annuler les travaux à partir de n’importe quel utilisateur et configurer le compte de hello.
* **Lecteur** : peut surveiller des travaux.

Utilisez hello données Lake Analytique développeur rôle tooenable U-SQL développeurs toouse hello Analytique lac de données service. Vous pouvez utiliser le rôle de développeur du lac de données Analytique hello pour :
* Envoyer des travaux.
* Surveiller la progression de statut et hello travail soumis par n’importe quel utilisateur.
* Consultez hello U-SQL de scripts de travaux soumis par les utilisateurs.
* Annuler uniquement vos propres travaux.

### <a name="add-users-or-security-groups-tooa-data-lake-analytics-account"></a>Ajouter des utilisateurs ou des groupes de sécurité tooa compte d’Analytique lac de données

1. Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.
2. Cliquez sur **Contrôle d’accès (IAM)** > **Ajouter**.
3. Sélectionnez un rôle
4. Ajoutez un utilisateur.
5. Cliquez sur **OK**.

>[!NOTE]
>Si un utilisateur ou un groupe de sécurité doit toosubmit travaux, ils doivent également l’autorisation sur le compte du magasin hello. Pour plus d’informations, consultez [Sécuriser les données stockées dans Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a>Gestion des travaux

### <a name="submit-a-job"></a>Soumettre un travail

1. Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.

2. Cliquez sur **Nouveau travail**. Pour chaque travail, configurez les éléments suivants :

    1. **Nom de la tâche**: nom hello du travail de hello.
    2. **Priorité** : les nombres inférieurs ont une priorité supérieure. Si deux travaux est en attente, hello une valeur de priorité inférieure s’exécute en premier.
    3. **Parallélisme**: nombre maximal de hello de compute traite tooreserve pour ce travail.

3. Cliquez sur **Envoyer le travail**.

### <a name="monitor-jobs"></a>Surveiller des travaux

1. Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.
2. Cliquez sur **Afficher tous les travaux**. Une liste de tous les travaux actifs et récemment terminé hello dans le compte de hello s’affiche.
3. Si vous le souhaitez, cliquez sur **filtre** toohelp vous recherchez les travaux de hello par **période**, **nom de la tâche**, et **auteur** valeurs. 

### <a name="monitoring-pipeline-jobs"></a>Surveillance des tâches de pipeline
Les travaux qui font partie d’un pipeline fonctionnent ensemble, généralement séquentiellement, tooaccomplish un scénario spécifique. Par exemple, vous pouvez avoir un pipeline qui nettoie, extrait, transforme, regroupe l’utilisation des informations du client. Travaux de pipeline est identifiés à l’aide de la propriété « Pipeline » de hello lors de la soumission de la tâche hello. Les tâches planifiées à l’aide du fichier de définition d’application V2 auront automatiquement cette propriété remplie. 

tooview une liste des tâches U-SQL qui font partie de pipelines : 

1. Bonjour portail Azure, accédez à des comptes tooyour Analytique lac de données.
2. Cliquez sur **Informations sur les tâches**. Bonjour qu'onglet « Toutes les tâches » prendra par défaut, qui contient la liste en cours d’exécution, en file d’attente et fin des tâches.
3. Cliquez sur hello **Pipeline travaux** onglet. Une liste des tâches de pipeline s’affiche, ainsi que des statistiques agrégées pour chaque pipeline.

### <a name="monitoring-recurring-jobs"></a>Surveillance des tâches récurrentes
Un abonnement est un travail qui a hello même logique métier mais utilise les données d’entrée différente chaque fois qu’il exécute. Dans l’idéal, tâches périodiques doivent toujours réussir et ont relativement stable exécution ; Ces comportements d’analyse afin de garantir le travail de hello est intègre. Tâches périodiques sont identifiés à l’aide de la propriété « Recurrence » de hello. Les tâches planifiées à l’aide du fichier de définition d’application V2 auront automatiquement cette propriété remplie.

tooview une liste des tâches U-SQL qui sont récurrents : 

1. Bonjour portail Azure, accédez à des comptes tooyour Analytique lac de données.
2. Cliquez sur **Informations sur les tâches**. Bonjour qu'onglet « Toutes les tâches » prendra par défaut, qui contient la liste en cours d’exécution, en file d’attente et fin des tâches.
3. Cliquez sur hello **périodique des travaux** onglet. Une liste des tâches récurrentes s’affiche, ainsi que des statistiques agrégées pour chaque tâche récurrente.

## <a name="manage-policies"></a>Gérer les stratégies

### <a name="account-level-policies"></a>Stratégies au niveau du compte

Ces stratégies s’appliquent à des travaux de tooall dans un compte Analytique lac de données.

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a>Nombre maximal d’unités Analytics dans un compte Data Lake Analytics
Une stratégie de contrôle le nombre total de hello d’Analytique unités (AUs), votre compte Analytique lac de données peut utiliser. Par défaut, hello est la valeur too250. Par exemple, si cette valeur est définie à too250 AUs, vous pouvez avoir une tâche est exécutée avec 250 AUs affectés tooit ou 10 travaux en cours d’exécution avec 25 AUs chaque. Tâches supplémentaires qui sont envoyées sont en file d’attente jusqu'à ce que les travaux en cours d’exécution hello. Lorsque des travaux en cours d’exécution sont terminées, AUs sont libérer hello en file d’attente des travaux toorun.

nombre de hello toochange de AUs pour votre compte Analytique lac de données :

1. Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.
2. Cliquez sur **Propriétés**.
3. Sous **AUs maximale**, déplacer hello curseur tooselect une valeur ou entrez la valeur de hello dans la zone de texte hello. 
4. Cliquez sur **Enregistrer**.

> [!NOTE]
> Si vous avez besoin de plus de hello par défaut (250) AUs, dans le portail hello, cliquez sur **aide + Support** toosubmit une demande de support. nombre de Hello de AUs disponibles dans votre compte Analytique lac de données peut être augmenté.
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a>Nombre maximal de travaux pouvant s’exécuter simultanément
Une stratégie de contrôle le nombre de travaux peut exécuter à hello même temps. Par défaut, cette valeur est définie à too20. Si votre Analytique lac de données a AUs disponibles, nouvelles tâches sont planifiée toorun immédiatement tant que le nombre total de hello de travaux en cours d’exécution atteint la valeur hello de cette stratégie. Lorsque vous atteignez le nombre maximal de hello de tâches pouvant être exécutés simultanément, les tâches suivantes sont en attente dans l’ordre de priorité jusqu'à ce que la fin d’une ou plusieurs tâches en cours d’exécution (selon la disponibilité de l’Australie).

nombre de hello toochange de tâches qui peuvent s’exécuter simultanément :

1. Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.
2. Cliquez sur **Propriétés**.
3. Sous **nombre maximal de travaux d’en cours d’exécution**, déplacer hello curseur tooselect une valeur ou entrez la valeur de hello dans la zone de texte hello. 
4. Cliquez sur **Enregistrer**.

> [!NOTE]
> Si vous avez besoin de toorun plus que hello par défaut (20) nombre de travaux, dans le portail de hello, cliquez sur **aide + Support** toosubmit une demande de support. nombre de Hello de travaux pouvant s’exécuter simultanément dans votre compte Analytique lac de données peut être augmenté.
>

#### <a name="how-long-tookeep-job-metadata-and-resources"></a>La durée pendant laquelle les métadonnées de tâche tookeep et ressources 
Lorsque les utilisateurs exécutent des travaux U-SQL, hello service de données Lake Analytique conserve tous les fichiers associés. Les fichiers associés incluent un script de hello U-SQL, les fichiers DLL hello référencés dans le script de hello U-SQL, les ressources compilées et les statistiques. les fichiers de Hello sont dans le dossier de /system/ hello du compte de stockage de LAC de données Azure hello par défaut. Cette stratégie contrôle la durée pendant laquelle ces ressources sont stockées avant d’être automatiquement supprimés (valeur par défaut hello est de 30 jours). Vous pouvez utiliser ces fichiers pour le débogage et pour régler les performances des tâches que vous devez réexécuter Bonjour futures.

toochange la durée pendant laquelle les métadonnées de tâche tookeep et ressources :

1. Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.
2. Cliquez sur **Propriétés**.
3. Sous **jours tooRetain travail interroge**, déplacer hello curseur tooselect une valeur ou entrez la valeur de hello dans la zone de texte hello.  
4. Cliquez sur **Enregistrer**.

### <a name="job-level-policies"></a>Stratégies au niveau du travail
Avec les stratégies au niveau du projet, vous pouvez contrôler hello AUs maximales et hello priorité maximale que des utilisateurs individuels (ou les membres de groupes de sécurité spécifiques) peuvent définir sur les tâches qu’ils ont envoyés. Cette permet de contrôler les coûts de hello induites par les utilisateurs. Il vous permet également d’effet hello que les tâches planifiées peut-être avoir sur haute priorité des tâches de production qui sont exécutent dans hello même compte Analytique lac de données.

Analytique de LAC de données a deux stratégies que vous pouvez définir au niveau du travail hello :

* **Limite de l’Australie par travail**: les utilisateurs peuvent envoyer uniquement les tâches qui ont des nombre toothis de l’Australie. Par défaut, cette limite est hello identique hello AU nombre maximal de compte de hello.
* **Priorité**: les utilisateurs peuvent envoyer uniquement les tâches qui ont une valeur toothis inférieur ou égal à priorité. Notez qu’un nombre plus élevé signifie une priorité plus faible. Par défaut, il a la valeur too1, qui est la priorité la plus élevée hello.

Chaque compte contient une stratégie par défaut. stratégie par défaut de Hello s’applique aux utilisateurs de tooall du compte de hello. Vous pouvez définir des stratégies supplémentaires pour des utilisateurs et des groupes spécifiques. 

> [!NOTE]
> Les stratégies au niveau du compte et les stratégies au niveau du travail s’appliquent simultanément.
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a>Ajouter une stratégie pour un utilisateur ou un groupe spécifique

1. Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.
2. Cliquez sur **Propriétés**.
3. Sous **limite de tâches de présentation**, cliquez sur hello **ajouter une stratégie** bouton. Ensuite, sélectionnez ou entrez hello suivant les paramètres :
    1. **Nom de la stratégie de calcul**: entrez un nom de la stratégie tooremind vous objectif hello de stratégie de hello.
    2. **Sélectionnez l’utilisateur ou le groupe**: sélectionnez hello utilisateur ou un groupe s’applique cette stratégie.
    3. **Définir hello limite de tâche de l’Australie**: définir la limite de hello AU qui s’applique toohello sélectionné utilisateur ou groupe.
    4. **Définir hello limite de priorité**: définir la limite de priorité hello qui s’applique toohello sélectionné utilisateur ou groupe.

4. Cliquez sur **OK**.

5. nouvelle stratégie de Hello est répertoriée dans hello **par défaut** stratégie de table, sous **limites de soumission de travail**. 

#### <a name="delete-or-edit-an-existing-policy"></a>Supprimer ou modifier une stratégie existante

1. Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.
2. Cliquez sur **Propriétés**.
3. Sous **limite de tâches de présentation**, rechercher hello stratégie tooedit.
4.  toosee hello **supprimer** et **modifier** options, dans la colonne de droite hello de table de hello, cliquez sur **...** .

### <a name="additional-resources-for-job-policies"></a>Ressources supplémentaires relatives aux stratégies de travail
* [Post de blog Vue d’ensemble de la stratégie](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [Post de blog Stratégies au niveau du compte](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [Post de blog Stratégies au niveau du travail](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a>Étapes suivantes

* [Présentation d’Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Prise en main Analytique lac de données à l’aide de hello portail Azure](data-lake-analytics-get-started-portal.md)
* [Gestion d’Azure Data Lake Analytics à l’aide d’Azure PowerShell](data-lake-analytics-manage-use-powershell.md)

