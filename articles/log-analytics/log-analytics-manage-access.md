---
title: aaaManage espaces de travail Analytique des journaux Azure et hello du portail OMS | Documents Microsoft
description: "Vous pouvez gérer les espaces de travail Analytique des journaux Azure et hello portail OMS à l’aide de diverses tâches d’administration sur les utilisateurs, les comptes, les espaces de travail et les comptes Azure."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: d0e5162d-584b-428c-8e8b-4dcaa746e783
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/06/2017
ms.author: magoedte
ms.openlocfilehash: 570e6c1f13ad28f120ecd65052d00c4ca986ac98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-workspaces"></a>Gestion des espaces de travail

tooLog d’accès toomanage Analytique, vous effectuer diverses tooworkspaces associés de tâches d’administration. Cet article fournit des conseils et des procédures toomanage espaces de travail meilleure pratique. Un espace de travail est essentiellement un conteneur qui inclut des informations de compte et les informations de configuration simple pour le compte de hello. Vous ou autres membres de votre organisation peuvent utiliser plusieurs espaces de travail toomanage différents jeux de données qui sont recueillies à partir de tous les ou de parties de votre infrastructure informatique.

toocreate un espace de travail, vous devez :

1. J’ai un abonnement Azure.
2. Choisissez un nom d’espace de travail.
3. Associer l’espace de travail hello avec votre abonnement.
4. Choisissez un emplacement géographique.

## <a name="determine-hello-number-of-workspaces-you-need"></a>Déterminer le nombre hello d’espaces de travail que vous avez besoin
Un espace de travail est une ressource Azure et un conteneur dans lequel les données sont collectées, agrégées, analysées et présentées dans hello portail Azure.

Vous pouvez avoir plusieurs espaces de travail par abonnement Azure et vous pouvez avoir accès toomore à un espace de travail. Réduction hello nombre d’espaces de travail vous permet de tooquery et mettre en corrélation hello la plupart des données, car il n’est pas possible de tooquery entre plusieurs espaces de travail. Cette section décrit quand il peut être utile toocreate plus d’un espace de travail.

Aujourd'hui, un espace de travail fournit :

* un emplacement géographique pour le stockage des données ;
* des données granulaires pour la facturation ;
* l’isolation des données.
* Étendue de la configuration

Hello précédant les caractéristiques, vous pouvez avoir besoin toocreate plusieurs espaces de travail si :

* Vous travaillez pour une entreprise globale et vous avez besoin de stocker vos données dans des régions spécifiques pour des raisons de conformité ou de souveraineté des données.
* À l’aide de Azure et vous souhaitez que le transfert de données sortantes tooavoid frais en demandant à un espace de travail hello même région que hello ressources Azure qu’il gère.
* Vous souhaitez départements de toodifferent tooallocate frais ou des groupes professionnels en fonction de leur utilisation. Lorsque vous créez un espace de travail pour chaque service ou le groupe Professionnel, votre instruction de facture et de l’utilisation Azure présente des frais hello pour chaque espace de travail séparément.
* Vous êtes un fournisseur de service administré et que vous devez données analytique de tookeep hello du journal pour chaque client que vous gérez isolé des autres données de client.
* Vous gérez plusieurs clients et que vous souhaitez que chaque client / service / entreprise de groupe toosee leurs propres données, mais pas les données hello pour d’autres.

Lorsque vous utilisez des données de toocollect agents, vous pouvez [configurer chaque tooone tooreport de l’agent ou de plusieurs espaces de travail](log-analytics-windows-agents.md).

Si vous utilisez System Center Operations Manager, chaque groupe d’administration Operations Manager ne peut être connecté qu’à un seul espace de travail. Vous pouvez installer hello Microsoft Monitoring Agent sur des ordinateurs gérés par Operations Manager et tooboth de rapport hello l’agent Operations Manager et un autre espace de travail Analytique de journal.

### <a name="workspace-information"></a>Informations sur l’espace de travail

Vous pouvez afficher des détails sur votre espace de travail Bonjour portail Azure. Vous pouvez également afficher les détails dans le portail OMS est hello.

#### <a name="view-workspace-information-in-hello-azure-portal"></a>Afficher les informations d’espace de travail Bonjour portail Azure

1. Si vous n’avez pas déjà fait, connectez-vous à toohello [portail Azure](https://portal.azure.com) à l’aide de votre abonnement Azure.
2. Sur hello **Hub** menu, cliquez sur **davantage de services** et, dans la liste hello des ressources, tapez **Analytique de journal**. Comme vous commencez à taper, hello filtres de la liste en fonction de votre entrée. Cliquez sur **Log Analytics**.  
    ![Hub Azure](./media/log-analytics-manage-access/hub.png)  
3. Dans le panneau des abonnements hello Analytique de journal, sélectionnez un espace de travail.
4. panneau espace de travail de Hello affiche des détails sur l’espace de travail hello et des liens vers des informations supplémentaires.  
    ![détails sur l’espace de travail](./media/log-analytics-manage-access/workspace-details.png)  


## <a name="manage-accounts-and-users"></a>Gérer les comptes et les utilisateurs
Chaque espace de travail peut avoir plusieurs comptes sont associés, et chaque compte (compte Microsoft ou compte professionnel) peut avoir des espaces de travail access toomultiple.

Par défaut, le compte de Microsoft hello ou organisation qui crée l’espace de travail hello devient hello administrateur de l’espace de travail hello.

Il existe deux modèles d’autorisation qui contrôlent l’espace de travail access tooa Analytique de journal :

1. Rôles d’utilisateur Log Analytics hérités
2. [Accès en fonction du rôle Azure](../active-directory/role-based-access-control-configure.md)

Hello tableau suivant résume les accès hello qui peuvent être définies à l’aide de chaque modèle d’autorisation :

|                          | Portail Log Analytics | Portail Azure | API (y compris PowerShell) |
|--------------------------|----------------------|--------------|----------------------------|
| Rôles d’utilisateur Log Analytics | Oui                  | Non           | Non                         |
| Accès en fonction du rôle Azure  | Oui                  | Oui          | Oui                        |

> [!NOTE]
> Analytique de journal est le déplacement toouse en fonction du rôle d’accès Azure en tant que modèle d’autorisations hello, en remplaçant les rôles d’utilisateur hello Analytique de journal.
>
>

Hello hérités rôles d’utilisateur Analytique de journal uniquement contrôlent tooactivities accès effectuées dans hello [portal d’Analytique de journal](https://mms.microsoft.com).

Hello suit également les activités nécessite des autorisations Azure :

| Action                                                          | Autorisations Azure nécessaires | Remarques |
|-----------------------------------------------------------------|--------------------------|-------|
| Ajout et suppression de solutions de gestion                        | `Microsoft.Resources/deployments/*` <br> `Microsoft.OperationalInsights/*` <br> `Microsoft.OperationsManagement/*` <br> `Microsoft.Automation/*` <br> `Microsoft.Resources/deployments/*/write` | |
| La modification hello niveau tarifaire                                       | `Microsoft.OperationalInsights/workspaces/*/write` | |
| Affichage des données dans hello *sauvegarde* et *Site Recovery* vignettes de la solution | Administrateur/coadministrateur | Déployer les ressources de l’accès à l’aide du modèle de déploiement classique de hello |
| Création d’un espace de travail dans hello portail Azure                        | `Microsoft.Resources/deployments/*` <br> `Microsoft.OperationalInsights/workspaces/*` ||


### <a name="managing-access-toolog-analytics-using-azure-permissions"></a>La gestion des accès tooLog Analytique à l’aide d’autorisations Azure
toogrant toohello Analytique de journal espace de travail access à l’aide d’autorisations Azure, suivez les étapes de hello dans [utiliser les ressources de rôle affectations toomanage accès tooyour abonnement Azure](../active-directory/role-based-access-control-configure.md).

Azure intègre deux rôles utilisateur pour Log Analytics :
- Lecteur Log Analytics
- Contributeur Log Analytics

Membres de hello *lecteur de journal Analytique* rôle peut :
- Visualisation et recherche de toutes les données d’analyse 
- Afficher les paramètres d’analyse, y compris l’affichage configuration hello des diagnostics Azure sur toutes les ressources Azure.

| Type    | Autorisation | Description |
| ------- | ---------- | ----------- |
| Action | `*/read`   | Capacité tooview toutes les ressources et la configuration de la ressource. Inclut la visualisation des éléments suivants : <br> État d’extension de machine virtuelle <br> Configuration des diagnostics Azure sur les ressources <br> Totalité des paramètres et propriétés de l’ensemble des ressources |
| Action | `Microsoft.OperationalInsights/workspaces/analytics/query/action` | Requêtes tooperform v2 de recherche de journal de capacité |
| Action | `Microsoft.OperationalInsights/workspaces/search/action` | Requêtes tooperform v1 de recherche de journal de capacité |
| Action | `Microsoft.Support/*` | Cas de prise en charge de tooopen de capacité |
|Non-action | `Microsoft.OperationalInsights/workspaces/sharedKeys/read` | Empêche la lecture d’un espace de travail toouse requis clé hello données API et tooinstall agents de collecte |


Membres de hello *collaborateur Analytique de journal* rôle peut :
- Lecture de toutes les données d’analyse 
- Création et configuration des comptes Automation
- Ajout et suppression de solutions de gestion
- Lecture des clés de compte de stockage 
- Configuration de la collecte de journaux à partir du stockage Azure
- Modification des paramètres d’analyse pour les ressources Azure, notamment :
  - Ajout de hello VM extension tooVMs
  - Configuration des diagnostics Azure sur toutes les ressources Azure

> [!NOTE] 
> Vous pouvez utiliser la possibilité de hello tooadd un machine virtuelle extension tooa machine virtuelle toogain un contrôle total sur un ordinateur virtuel.

| Autorisation | Description |
| ---------- | ----------- |
| `*/read`     | Capacité tooview toutes les ressources et la configuration de la ressource. Inclut la visualisation des éléments suivants : <br> État d’extension de machine virtuelle <br> Configuration des diagnostics Azure sur les ressources <br> Totalité des paramètres et propriétés de l’ensemble des ressources |
| `Microsoft.Automation/automationAccounts/*` | Capacité toocreate et configurer des comptes Azure Automation, y compris l’ajout et modification des procédures opérationnelles |
| `Microsoft.ClassicCompute/virtualMachines/extensions/*` <br> `Microsoft.Compute/virtualMachines/extensions/*` | Ajouter, mettre à jour et supprimer des extensions de machine virtuelle, y compris les extensions de Microsoft Monitoring Agent hello et hello Agent OMS pour Linux extension |
| `Microsoft.ClassicStorage/storageAccounts/listKeys/action` <br> `Microsoft.Storage/storageAccounts/listKeys/action` | Clé de compte de stockage hello de vue. Requis des journaux de tooread tooconfigure Analytique de journal à partir des comptes de stockage Azure |
| `Microsoft.Insights/alertRules/*` | Ajout, mise à jour et suppression de règles d’alerte |
| `Microsoft.Insights/diagnosticSettings/*` | Ajout, mise à jour et suppression de paramètres de diagnostic sur les ressources Azure |
| `Microsoft.OperationalInsights/*` | Ajout, mise à jour et suppression de configuration pour les espaces de travail Log Analytics |
| `Microsoft.OperationsManagement/*` | Ajout et suppression de solutions de gestion |
| `Microsoft.Resources/deployments/*` | Création et suppression de déploiements ; opération requise pour l’ajout et la suppression de solutions, d’espaces de travail et de comptes Automation |
| `Microsoft.Resources/subscriptions/resourcegroups/deployments/*` | Création et suppression de déploiements ; opération requise pour l’ajout et la suppression de solutions, d’espaces de travail et de comptes Automation |

tooadd et supprimer les utilisateurs tooa rôle d’utilisateur, il est nécessaire toohave `Microsoft.Authorization/*/Delete` et `Microsoft.Authorization/*/Write` autorisation.

Utilisez ces rôles toogive les utilisateurs d’accès à différentes portées :
- Abonnement - espaces de travail Access tooall dans l’abonnement de hello
- Groupe de ressources - espace de travail Access tooall dans le groupe de ressources hello
- Ressource : hello de tooonly d’accès spécifié espace de travail

Utilisez [des rôles personnalisés](../active-directory/role-based-access-control-custom-roles.md) toocreate les rôles avec des autorisations spécifiques hello si nécessaires.

### <a name="azure-user-roles-and-log-analytics-portal-user-roles"></a>Rôles utilisateur Azure et rôles utilisateur du portail Log Analytics
Si vous avez au moins Azure en lecture sur l’espace de travail Analytique de journal hello, que vous pouvez ouvrir le portail Analytique de journal de hello en cliquant sur hello **portail OMS** lorsque vous affichez l’espace de travail hello Analytique des journaux de tâches.

Lorsque vous ouvrez le portail d’Analytique de journal hello, vous basculez de rôles d’utilisateur toousing hello hérités Analytique de journal. Si vous n’avez pas d’une attribution de rôle dans le portail d’Analytique de journal hello, hello service [vérifications hello Azure autorisations sur l’espace de travail hello](https://docs.microsoft.com/rest/api/authorization/permissions#Permissions_ListForResource).
Votre attribution de rôle dans le portail d’Analytique de journal hello est déterminée en utilisant comme suit :

| Conditions                                                   | Rôle d’utilisateur Log Analytics affecté | Remarques |
|--------------------------------------------------------------|----------------------------------|-------|
| Votre compte appartient le rôle d’utilisateur tooa hérité Analytique de journal     | Hello spécifié le rôle d’utilisateur Analytique de journal | |
| Votre compte n’appartient pas le rôle d’utilisateur tooa hérité Analytique de journal <br> Espace de travail Azure complet d’autorisations toohello (`*` autorisation <sup>1</sup>) | Administrateur ||
| Votre compte n’appartient pas le rôle d’utilisateur tooa hérité Analytique de journal <br> Espace de travail Azure complet d’autorisations toohello (`*` autorisation <sup>1</sup>) <br> *non-actions* de `Microsoft.Authorization/*/Delete` et `Microsoft.Authorization/*/Write` | Collaborateur ||
| Votre compte n’appartient pas le rôle d’utilisateur tooa hérité Analytique de journal <br> Autorisation d’accès en lecture Azure | Lecture seule ||
| Votre compte n’appartient pas le rôle d’utilisateur tooa hérité Analytique de journal <br> Les autorisations Azure ne sont pas comprises | Lecture seule ||
| Pour les abonnements gérés par le fournisseur de solutions Cloud (CSP) <br> compte de Hello de que vous êtes connecté à l’aide est hello Azure Active Directory lié toohello espace de travail | Administrateur | En général, les clients hello d’un fournisseur de services cryptographiques |
| Pour les abonnements gérés par le fournisseur de solutions Cloud (CSP) <br> compte de Hello de que vous êtes connecté à l’aide n’est pas hello Azure Active Directory lié toohello espace de travail | Collaborateur | En général, hello CSP |

<sup>1</sup> reportez-vous trop[autorisations Azure](../active-directory/role-based-access-control-custom-roles.md) pour plus d’informations sur les définitions de rôles. Lors de l’évaluation des rôles, une action de `*` n’est pas équivalent trop`Microsoft.OperationalInsights/workspaces/*`.

Tookeep de certains points à l’esprit hello portail Azure :

* Lorsque vous vous connectez à l’aide de http://mms.microsoft.com portail OMS est toohello, vous voyez hello **sélectionner un espace de travail** liste. Cette liste contient uniquement des espaces de travail dans lesquels vous avez un rôle d’utilisateur Log Analytics. toowith Azure d’accéder aux espaces de travail hello toosee vous avez des abonnements, vous devez toospecify un locataire dans le cadre de l’URL de hello. Par exemple : `mms.microsoft.com/?tenant=contoso.com`. Identificateur du locataire Hello est souvent cette dernière partie hello d’adresse de messagerie que vous utilisez toosign dans.
* Si vous souhaitez toonavigate directement toousing Azure d’accéder au portail tooa dont vous disposez des autorisations, vous devez ressource de hello toospecify dans le cadre de l’URL de hello. Il est possible de tooget cette URL à l’aide de PowerShell.

  Par exemple, `(Get-AzureRmOperationalInsightsWorkspace).PortalUrl`.

  URL de Hello ressemble à :`https://eus.mms.microsoft.com/?tenant=contoso.com&resource=%2fsubscriptions%2faaa5159e-dcf6-890a-a702-2d2fee51c102%2fresourcegroups%2fdb-resgroup%2fproviders%2fmicrosoft.operationalinsights%2fworkspaces%2fmydemo12`

### <a name="managing-users-in-hello-oms-portal"></a>Gestion des utilisateurs dans le portail OMS de hello
Gestion des utilisateurs et groupe sur hello **gérer les utilisateurs** onglet sous hello **comptes** onglet dans la page des paramètres hello.   

![gérer des utilisateurs](./media/log-analytics-manage-access/setup-workspace-manage-users.png)


#### <a name="add-a-user-tooan-existing-workspace"></a>Ajouter un espace de travail utilisateur tooan existant
Utilisez hello suivant les étapes tooadd un espace de travail tooa utilisateur ou un groupe.

1. Dans le portail OMS hello, cliquez sur hello **paramètres** vignette.
2. Cliquez sur hello **comptes** onglet, puis cliquez sur hello **gérer les utilisateurs** onglet.
3. Bonjour **gérer les utilisateurs** , choisissez tooadd de type hello compte : **compte professionnel**, **Account Microsoft**, **le Support technique de Microsoft**.

   * Si vous choisissez Microsoft Account, tapez l’adresse de messagerie de hello d’utilisateur hello associé hello Account Microsoft.
   * Si vous choisissez compte professionnel, entrez une partie de l’utilisateur de hello / nom d’alias du groupe de messagerie électronique et d’une liste de mise en correspondance les utilisateurs et groupes apparaît dans une zone de liste déroulante. Sélectionnez un utilisateur ou un groupe.
   * Utilisez toogive de Support technique de Microsoft un ingénieur du Support technique de Microsoft ou autres toohelp d’espace de travail de Microsoft employés un accès temporaire tooyour résolution des problèmes.

     > [!NOTE]
     > Pour de meilleures performances de hello, limiter le nombre de hello de groupes Active Directory associés à un seul toothree de compte OMS : un pour les administrateurs, une pour les contributeurs et un pour les utilisateurs en lecture seule. À l’aide de plusieurs groupes peut affecter les performances de hello d’Analytique de journal.
     >
     >
4. Choisissez type hello d’utilisateur ou le groupe tooadd : **administrateur**, **collaborateur**, ou **ReadOnly utilisateur**.  
5. Cliquez sur **Add**.

   Si vous ajoutez un compte Microsoft, un espace de travail invitation toojoin hello est envoyé par courrier électronique toohello que vous avez fourni. Une fois hello suivi les instructions de hello hello invitation toojoin OMS, hello peut accéder à espace de travail hello.
   Si vous ajoutez un compte professionnel, hello peut accéder à Analytique de journal immédiatement.  

#### <a name="edit-an-existing-user-type"></a>Modification d’un type d’utilisateur existant
Vous pouvez modifier le rôle de compte hello pour un utilisateur associé à votre compte OMS. Vous avez hello rôle options suivantes :

* *Administrateur*: peut gérer les utilisateurs, afficher et agir sur toutes les alertes, ainsi qu’ajouter et supprimer des serveurs.
* *Collaborateur*: peut afficher toutes les alertes et agir sur celles-ci, ainsi qu’ajouter et supprimer des serveurs.
* *Utilisateur en lecture seule* : les utilisateurs marqués comme étant en lecture seule ne peuvent pas :

  1. Ajouter ou supprimer des solutions. Galerie de solutions Hello est masquée.
  2. Ajouter/modifier/supprimer des mosaïques sur **Mon tableau de bord**.
  3. Hello de vue **paramètres** pages. pages de Hello sont masqués.
  4. Dans Affichage de la recherche hello, Power BI configuration, recherches enregistrées, alertes et les tâches sont masquées.

#### <a name="tooedit-an-account"></a>tooedit un compte
1. Dans le portail OMS hello, cliquez sur hello **paramètres** vignette.
2. Cliquez sur hello **comptes** onglet, puis cliquez sur hello **gérer les utilisateurs** onglet.
3. Sélectionnez rôle hello pour utilisateur hello que vous souhaitez toochange.
4. Dans la boîte de dialogue de confirmation hello, cliquez sur **Oui**.

### <a name="remove-a-user-from-a-workspace"></a>Supprimer un utilisateur d’un espace de travail
Utilisez hello suivant les étapes tooremove un utilisateur à partir d’un espace de travail. Utilisateur de hello suppression ne ferme pas l’espace de travail hello. Au lieu de cela, elle supprime association hello entre cet utilisateur et l’espace de travail hello. Si un utilisateur est associé à plusieurs espaces de travail, cet utilisateur peut toujours se connecter tooOMS et afficher leurs autres espaces de travail.

1. Dans le portail OMS hello, cliquez sur hello **paramètres** vignette.
2. Cliquez sur hello **comptes** onglet, puis cliquez sur hello **gérer les utilisateurs** onglet.
3. Cliquez sur **supprimer** suivant toohello nom d’utilisateur que vous tooremove.
4. Dans la boîte de dialogue de confirmation hello, cliquez sur **Oui**.

### <a name="add-a-group-tooan-existing-workspace"></a>Ajouter un espace de travail groupe tooan existant
1. Bonjour précédant la section « tooadd un espace de travail utilisateur tooan existant », suivez les étapes 1 à 4.
2. Sous **Choisir un utilisateur/groupe**, sélectionnez **Groupe**.  
   ![Ajouter un espace de travail groupe tooan existant](./media/log-analytics-manage-access/add-group.png)
3. Entrez hello nom complet ou adresse de messagerie pour le groupe de hello vous aimeriez tooadd.
4. Sélectionnez le groupe de hello dans les résultats de la liste hello, puis cliquez **ajouter**.

## <a name="link-an-existing-workspace-tooan-azure-subscription"></a>Lier un tooan d’espace de travail existant abonnement Azure
Tous les espaces de travail créés après le 26 septembre 2016 doivent être lié tooan abonnement Azure au moment de la création. Espaces de travail créés avant cette date doivent être l’espace de travail lié tooa lors de la connexion. Lorsque vous créez un espace de travail hello de hello portail Azure, ou lorsque vous liez votre espace de travail de tooan abonnement Azure, Azure Active Directory est lié en tant que votre compte professionnel.

### <a name="toolink-a-workspace-tooan-azure-subscription-in-hello-oms-portal"></a>toolink un abonnement Azure dans le portail OMS est hello de tooan espace de travail

- Lorsque vous vous connectez au portail OMS de hello, vous êtes invité à tooselect un abonnement Azure. Sélectionnez hello abonnement que vous souhaitez toolink tooyour espace de travail, puis sur **lien**.  
    ![lier un abonnement Azure](./media/log-analytics-manage-access/required-link.png)

    > [!IMPORTANT]
    > toolink un espace de travail, votre compte Azure doit déjà avoir accès espace de travail de toohello toolink voulue.  En d’autres termes, le compte hello vous utilisez tooaccess hello portail Azure doit être **hello même** en tant que compte hello vous utiliser l’espace de travail tooaccess hello. Dans le cas contraire, consultez [ajouter un espace de travail utilisateur tooan existant](#add-a-user-to-an-existing-workspace).

### <a name="toolink-a-workspace-tooan-azure-subscription-in-hello-azure-portal"></a>toolink un abonnement Azure Bonjour Azure portal de tooan espace de travail
1. L’authentification à hello [portail Azure](http://portal.azure.com).
2. Recherchez **Log Analytics** et sélectionnez-le.
3. Vous voyez la liste des espaces de travail existants. Cliquez sur **Add**.  
   ![liste des espaces de travail](./media/log-analytics-manage-access/manage-access-link-azure01.png)
4. Sous **Espace de travail OMS**, cliquez sur **Ou liez**.  
   ![lier un élément existant](./media/log-analytics-manage-access/manage-access-link-azure02.png)
5. Cliquez sur **Configurer les paramètres requis**.  
   ![configure required settings](./media/log-analytics-manage-access/manage-access-link-azure03.png)
6. Vous voyez la liste hello d’espaces de travail qui ne sont pas encore liés tooyour compte Azure. Sélectionnez un espace de travail.  
   ![sélectionner des espaces de travail](./media/log-analytics-manage-access/manage-access-link-azure04.png)
7. Si nécessaire, vous pouvez modifier les valeurs pour hello éléments suivants :
   * Abonnement
   * Groupe de ressources
   * Emplacement
   * Niveau tarifaire   
     ![modifier des valeurs](./media/log-analytics-manage-access/manage-access-link-azure05.png)
8. Cliquez sur **OK**. espace de travail Hello est désormais lié tooyour compte Azure.

> [!NOTE]
> Si vous ne voyez pas l’espace de travail hello toolink voulue, puis votre abonnement Azure n’a pas d’espace de travail toohello access que vous avez créé à l’aide du portail OMS hello.  compte de toothis toogrant accès à partir du portail OMS hello, consultez [ajouter un espace de travail utilisateur tooan existant](#add-a-user-to-an-existing-workspace).
>
>

## <a name="upgrade-a-workspace-tooa-paid-plan"></a>Mise à niveau d’un tooa d’espace de travail payé plan
Il existe trois types de plan pour les espaces de travail OMS : **Gratuit**, **Autonome** et **OMS**.  Si vous êtes sur hello *libre* planifier, il existe une limite de 500 Mo de données par jour envoyé tooLog Analytique.  Si vous dépassez cette quantité, vous devez toochange votre tooavoid de plan tooa payé espace de travail ne collecte ne pas de données au-delà de cette limite. Vous pouvez convertir votre type de plan à tout moment.  Pour en savoir plus sur la tarification d’OMS, consultez la rubrique relative aux [détails de tarification](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-pricing).

### <a name="using-entitlements-from-an-oms-subscription"></a>Utilisation de droits dans le cadre d’un abonnement OMS
droits hello toouse provenant d’achat OMS E1, OMS E2 OMS ou au module complémentaire OMS pour System Center, choisissez hello *OMS* plan d’Analytique des journaux OMS.

Lorsque vous achetez un abonnement OMS, les droits de hello sont ajoutés tooyour accord entreprise. N’importe quel abonnement Azure qui est créé sous ce contrat peut utiliser les droits hello. Tous les espaces de travail sur ces abonnements utilisent des droits d’OMS hello.

tooensure que l’utilisation d’un espace de travail est appliqué tooyour les droits de hello abonnement OMS, vous devez :

1. Créer votre espace de travail dans un abonnement Azure qui fait partie de hello contrat entreprise qui comprend hello OMS abonnement
2. Sélectionnez hello *OMS* plan pour l’espace de travail hello

> [!NOTE]
> Si votre espace de travail a été créé avant le 26 septembre 2016 et votre Analytique de journal plan de tarification est *Premium*, cet espace de travail utilise des droits à partir de hello au module complémentaire OMS pour System Center. Vous pouvez également utiliser vos droits en modifiant toohello *OMS* niveau tarifaire.
>
>

droits d’abonnement Hello OMS ne sont pas visibles dans hello Azure ou le portail OMS. Vous pouvez voir les droits d’accès et l’utilisation dans hello Enterprise Portal.  

Si vous devez toochange hello abonnement Azure lié à votre espace de travail, vous pouvez utiliser hello Azure PowerShell [Move-AzureRmResource](https://msdn.microsoft.com/library/mt652516.aspx) applet de commande.

### <a name="using-azure-commitment-from-an-enterprise-agreement"></a>Utilisation de l’engagement Azure d’un Contrat Entreprise
Si vous n’avez pas d’abonnement OMS, vous payez séparément pour chaque composant OMS et l’utilisation de hello apparaît sur votre facture Azure.

Si vous avez Azure engagement sur hello entreprise d’inscription toowhich vos abonnements Azure sont liées, l’utilisation de l’Analytique des journaux est automatiquement débit contre hello restant validation monétaire.

Si vous avez besoin de toochange hello abonnement Azure qui hello d’espace de travail est lié, vous pouvez utiliser des hello Azure PowerShell [Move-AzureRmResource](https://msdn.microsoft.com/library/mt652516.aspx) applet de commande.  

### <a name="change-a-workspace-tooa-paid-pricing-tier-in-hello-azure-portal"></a>Modifier un tooa d’espace de travail payé niveau tarifaire Bonjour portail Azure
1. L’authentification à hello [portail Azure](http://portal.azure.com).
2. Recherchez **Log Analytics** et sélectionnez-le.
3. Vous voyez la liste des espaces de travail existants. Sélectionnez un espace de travail.  
4. Dans le panneau espace de travail de hello, sous **général**, cliquez sur **niveau tarifaire**.  
5. Sous **Niveau tarifaire**, sélectionnez un niveau tarifaire, puis cliquez sur **Sélectionner**.  
    ![select plan](./media/log-analytics-manage-access/manage-access-change-plan03.png)
6. Lorsque vous actualisez l’affichage dans hello portail Azure, vous voyez **niveau tarifaire** mis à jour pour le niveau de hello que vous avez sélectionné.  
    ![plan mis à jour](./media/log-analytics-manage-access/manage-access-change-plan04.png)

> [!NOTE]
> Si votre espace de travail est lié tooan compte Automation, avant que vous pouvez sélectionner hello *autonome (par Go)* tarification vous devez supprimer les **Automation & Control** solutions et dissocier hello Automation compte. Dans le panneau espace de travail de hello, sous **général**, cliquez sur **Solutions** toosee et supprimer des solutions. toounlink hello compte Automation, cliquez sur le nom hello Hello compte Automation sur hello **niveau tarifaire** panneau.
>
>

### <a name="change-a-workspace-tooa-paid-pricing-tier-in-hello-oms-portal"></a>Modifier un tooa d’espace de travail payé un niveau de tarification dans portail OMS : hello

toochange hello niveau tarifaire à l’aide du portail OMS hello, vous devez avoir un abonnement Azure.

1. Dans le portail OMS hello, cliquez sur hello **paramètres** vignette.
2. Cliquez sur hello **comptes** onglet, puis cliquez sur hello **abonnement Azure et le Plan de données** onglet.
3. Cliquez sur hello tarification souhaité toouse.
4. Cliquez sur **Enregistrer**.  
   ![forfaits d’abonnement et de données](./media/log-analytics-manage-access/subscription-tab.png)

Votre nouveau plan de données s’affiche dans hello ruban portail OMS haut de hello de votre page web.

![Ruban OMS](./media/log-analytics-manage-access/data-plan-changed.png)


## <a name="change-how-long-log-analytics-stores-data"></a>Modifier la durée de stockage des données par Log Analytics

Sur le niveau de tarification gratuit de hello, Analytique de journal rend disponible hello sept jours de données.
Sur le niveau de tarification Standard hello, Analytique de journal rend disponible hello 30 derniers jours de données.
Sur le niveau de tarification Premium hello, Analytique de journal rend disponible hello cours des 365 derniers jours de données.
Hello autonome et OMS, les niveaux de tarification par défaut, Analytique de journal rend disponible hello 31 derniers jours de données.

Lorsque vous utilisez hello autonome et niveaux de tarification d’OMS, vous pouvez conserver les années too2 de données (730 jours). Données stockées plus longtemps que la valeur par défaut de hello de 31 jours entraîne des frais de rétention de données. Pour plus d’informations sur la tarification, reportez-vous aux [frais de dépassement](https://azure.microsoft.com/pricing/details/log-analytics/).

longueur de hello toochange de rétention des données :

1. L’authentification à hello [portail Azure](http://portal.azure.com).
2. Recherchez **Log Analytics** et sélectionnez-le.
3. Vous voyez la liste des espaces de travail existants. Sélectionnez un espace de travail.  
4. Dans le panneau espace de travail de hello sous **général**, cliquez sur **rétention**.  
5. Utilisez hello curseur tooincrease ou diminuer le nombre de hello de jours de rétention, puis cliquez **enregistrer**.  
    ![modifier la durée de rétention](./media/log-analytics-manage-access/manage-access-change-retention01.png)

## <a name="change-an-azure-active-directory-organization-for-a-workspace"></a>Modifier une organisation Azure Active Directory pour un espace de travail

Vous pouvez modifier l’organisation Azure Active Directory d’un espace de travail. Modification hello organisation Azure Active Directory vous permet de tooadd utilisateurs et groupes à partir de cet espace de travail toohello active.

### <a name="toochange-hello-azure-active-directory-organization-for-a-workspace"></a>toochange hello organisation Azure Active Directory pour un espace de travail

1. Dans la page Paramètres hello du portail OMS hello, cliquez sur **comptes** puis cliquez sur hello **gérer les utilisateurs** onglet.  
2. Passez en revue les hello plus d’informations sur les comptes de société, puis cliquez sur **modification organisation**.  
    ![modifier l’organisation](./media/log-analytics-manage-access/manage-access-add-adorg01.png)
3. Entrez les informations d’identité hello pour l’administrateur de hello de votre domaine Azure Active Directory. Ensuite, vous voyez un accusé de réception indiquant que votre espace de travail est le domaine d’Azure Active Directory tooyour lié.  
    ![confirmation d’espace de travail lié](./media/log-analytics-manage-access/manage-access-add-adorg02.png)


## <a name="delete-a-log-analytics-workspace"></a>Supprimer un espace de travail Log Analytics
Lorsque vous supprimez un espace de travail Analytique de journal, toutes les données liées tooyour espace de travail est supprimé à partir de hello service OMS dans les 30 jours.

Si vous êtes administrateur et que plusieurs utilisateurs sont associés avec l’espace de travail hello, association hello entre les utilisateurs et l’espace de travail hello est rompue. Si les utilisateurs de hello sont associés à des autres espaces de travail, ils peuvent continuer à utiliser OMS avec ces autres espaces de travail. Toutefois, si elles ne sont pas associés à des espaces de travail, ils doivent toocreate un toouse de l’espace de travail OMS.

### <a name="toodelete-a-workspace"></a>toodelete un espace de travail
1. L’authentification à hello [portail Azure](http://portal.azure.com).
2. Recherchez **Log Analytics** et sélectionnez-le.
3. Vous voyez la liste des espaces de travail existants. Sélectionnez l’espace de travail hello que vous souhaitez toodelete.
4. Dans le panneau espace de travail de hello, cliquez sur **supprimer**.  
    ![delete](./media/log-analytics-manage-access/delete-workspace01.png)
5. Dans la boîte de dialogue de confirmation de hello delete espace de travail, cliquez sur **Oui**.

## <a name="next-steps"></a>Étapes suivantes
* Consultez [tooLog d’ordinateurs Windows de se connecter Analytique](log-analytics-windows-agents.md) tooadd agents et collecter des données.
* [Ajouter des solutions d’Analytique de journal à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md) tooadd fonctionnalité et collecter les données.
* [Configurer les paramètres de pare-feu et de proxy dans le journal Analytique](log-analytics-proxy-firewall.md) si votre organisation utilise un serveur proxy ou un pare-feu afin que les agents de communiquer avec hello service d’Analytique de journal.
