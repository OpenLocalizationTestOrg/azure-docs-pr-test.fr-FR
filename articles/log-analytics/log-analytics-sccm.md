---
title: aaaConnect Analytique de Configuration Manager tooLog | Documents Microsoft
description: "Cet article explique hello étapes tooconnect Configuration Manager tooLog Analytique et commencer à analyser les données."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f2298bd7-18d7-4371-b24a-7f9f15f06d66
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: banders
ms.openlocfilehash: dc50ebc46020a806d99d1a3e3d0e91fd09ad2c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-configuration-manager-toolog-analytics"></a>Se connecter à Configuration Manager tooLog Analytique
Vous pouvez vous connecter System Center Configuration Manager tooLog Analytique dans les données de collection de périphérique toosync OMS. Cela rend les données de votre hiérarchie Configuration Manager disponibles dans OMS.

## <a name="prerequisites"></a>Composants requis

Log Analytics prend en charge la branche actuelle de System Center Configuration Manager, version 1606 et supérieure.  

## <a name="configuration-overview"></a>Présentation de la configuration
Hello suit résume hello processus tooconnect Configuration Manager tooLog Analytique.  

1. Bonjour portail de gestion Azure, inscrire le Gestionnaire de Configuration en tant qu’Application Web et/ou API Web application et assurez-vous d’avoir hello client et ID de clé secrète du client de l’inscription du hello d’Azure Active Directory. Consultez [utiliser une application de portail toocreate Active Directory et de principal du service qui peut accéder aux ressources](../azure-resource-manager/resource-group-create-service-principal-portal.md) pour des informations détaillées sur la façon de procéder à cette étape.
2. Bonjour portail de gestion Azure, [fournissent à Configuration Manager (application web inscrit de hello) autorisation tooaccess OMS](#provide-configuration-manager-with-permissions-to-oms).
3. Dans le Gestionnaire de Configuration, [ajouter une connexion à l’aide de hello Assistant Ajout d’une connexion OMS](#add-an-oms-connection-to-configuration-manager).
4. Dans le Gestionnaire de Configuration, [mettre à jour les propriétés de connexion hello](#update-oms-connection-properties) si la clé secrète hello client ou le mot de passe expire jamais ou est perdue.
5. Avec les informations du portail OMS : hello, [télécharger et installer Microsoft Monitoring Agent de hello](#download-and-install-the-agent) sur ordinateur hello exécutant la connexion au service Gestionnaire de Configuration hello point de rôle de système de site. l’agent de Hello envoie tooOMS de données de Configuration Manager.
6. Dans Log Analytics, [importez les collections de Configuration Manager](#import-collections) en tant que groupes d’ordinateurs.
7. Dans Log Analytics, affichez les données de Configuration Manager en tant que [groupes d’ordinateurs](log-analytics-computer-groups.md).

Vous pouvez en savoir plus sur la connexion tooOMS Configuration Manager à [synchroniser des données à partir de toohello du Gestionnaire de Configuration de Microsoft Operations Management Suite](https://technet.microsoft.com/library/mt757374.aspx).

## <a name="provide-configuration-manager-with-permissions-toooms"></a>Fournir le Gestionnaire de Configuration avec les autorisations tooOMS
Hello procédure suivante fournit hello portail de gestion Azure avec autorisations tooaccess OMS. Plus précisément, vous devez accorder hello *rôle Collaborateur* toousers dans le groupe de ressources hello dans l’ordre tooallow hello portail de gestion Azure tooconnect tooOMS de Configuration Manager.

> [!NOTE]
> Vous devez spécifier des autorisations dans OMS pour Configuration Manager. Sinon, vous recevrez un message d’erreur lorsque vous utilisez Assistant de configuration de hello dans Configuration Manager.
>
>

1. Ouvrez hello [portail Azure](https://portal.azure.com/) et cliquez sur **Parcourir** > **Analytique des journaux (OMS)** Panneau de tooopen hello Analytique des journaux (OMS).  
2. Sur hello **Analytique des journaux (OMS)** panneau, cliquez sur **ajouter** tooopen hello **espace de travail OMS** panneau.  
   ![Panneau OMS](./media/log-analytics-sccm/sccm-azure01.png)
3. Sur hello **espace de travail OMS** panneau, fournir hello informations suivantes, puis cliquez sur **OK**.

   * **Espace de travail OMS**
   * **Abonnement**
   * **Groupe de ressources**
   * **Emplacement**
   * **Niveau tarifaire**  
     ![Panneau OMS](./media/log-analytics-sccm/sccm-azure02.png)  

     > [!NOTE]
     > exemple Hello ci-dessus crée un nouveau groupe de ressources. groupe de ressources Hello est uniquement utilisé tooprovide Configuration Manager avec l’espace de travail OMS de toohello autorisations dans cet exemple.
     >
     >
4. Cliquez sur **Parcourir** > **groupes de ressources** tooopen hello **groupes de ressources** panneau.
5. Bonjour **groupes de ressources** panneau, cliquez sur le groupe de ressources hello créé ci-dessus tooopen hello &lt;nom de groupe de ressources&gt; panneau des paramètres.  
   ![Panneau de paramètres de groupe de ressources](./media/log-analytics-sccm/sccm-azure03.png)
6. Bonjour &lt;nom de groupe de ressources&gt; Panneau de paramètres, cliquez sur hello d’accès contrôle (IAM) tooopen &lt;nom de groupe de ressources&gt; panneau utilisateurs.  
   ![Panneau d’utilisateurs de groupe de ressources](./media/log-analytics-sccm/sccm-azure04.png)  
7. Bonjour &lt;nom de groupe de ressources&gt; panneau utilisateurs, cliquez sur **ajouter** tooopen hello **ajouter un accès** panneau.
8. Bonjour **ajouter un accès** panneau, cliquez sur **sélectionner un rôle**, puis sélectionnez hello **collaborateur** rôle.  
   ![Sélectionner un rôle](./media/log-analytics-sccm/sccm-azure05.png)  
9. Cliquez sur **ajouter des utilisateurs**, sélectionnez l’utilisateur du Gestionnaire de Configuration hello, cliquez sur **sélectionnez**, puis cliquez sur **OK**.  
   ![Ajouter des utilisateurs](./media/log-analytics-sccm/sccm-azure06.png)  

## <a name="add-an-oms-connection-tooconfiguration-manager"></a>Ajouter une tooConfiguration de connexion OMS Manager
Commande tooadd une connexion à OMS, votre environnement Configuration Manager doit avoir un [point de connexion de service](https://technet.microsoft.com/library/mt627781.aspx) configuré pour le mode en ligne.

1. Bonjour **Administration** espace de travail du Gestionnaire de Configuration, sélectionnez **connecteur OMS**. Cette opération ouvre hello **Assistant Ajout de connexion OMS**. Sélectionnez **Suivant**.
2. Sur hello **général** , vérifiez que vous avez effectué hello suivant des actions et que vous obteniez des détails pour chaque élément, puis sélectionnez **suivant**.

   1. Dans hello portail de gestion Azure, vous avez enregistré le Gestionnaire de Configuration en tant qu’Application Web et/ou API Web application et que vous avez hello [ID client de l’inscription du hello](../active-directory/active-directory-integrating-applications.md).
   2. Bonjour portail de gestion Azure, vous avez créé une clé secrète d’application pour l’application inscrite hello dans Azure Active Directory.  
   3. Bonjour portail de gestion Azure, vous avez fourni hello web inscrit application avec autorisation tooaccess OMS.  
      ![Page de connexion tooOMS généraux de l’Assistant](./media/log-analytics-sccm/sccm-console-general01.png)
3. Sur hello **Azure Active Directory** écran, configurez votre tooOMS de paramètres de connexion en fournissant votre **client** , **ID Client** , et **clé secrète Client**  , puis sélectionnez **suivant**.  
   ![Page de connexion tooOMS Assistant Azure Active Directory](./media/log-analytics-sccm/sccm-wizard-tenant-filled03.png)
4. Si vous avez effectué hello toutes les autres procédures avec succès, puis hello plus d’informations sur hello **Configuration de la connexion OMS** écran s’afficheront automatiquement sur cette page. Informations pour les paramètres de connexion hello doivent apparaître pour votre **abonnement Azure** , **groupe de ressources Azure** , et **espace de travail Operations Management Suite**.  
   ![Page de connexion tooOMS Assistant connexion à OMS](./media/log-analytics-sccm/sccm-wizard-configure04.png)
5. Assistant de Hello connecte à service OMS de toohello à l’aide des informations hello que vous avez entrée. Sélectionnez les regroupements de périphériques hello que vous souhaitez toosync avec OMS, puis sur **ajouter**.  
   ![Sélectionner les regroupements](./media/log-analytics-sccm/sccm-wizard-add-collections05.png)
6. Vérifiez vos paramètres de connexion sur hello **Résumé** écran, puis sélectionnez **suivant**. Hello **progression** écran affiche l’état de la connexion hello, puis doit **Complete**.

> [!NOTE]
> Vous devez connecter le site de niveau supérieur OMS toohello dans votre hiérarchie. Si vous vous connecter à un site principal OMS tooa autonome et que vous ajoutez ensuite un environnement tooyour du site administration centrale, vous avez toodelete et recréez la connexion à OMS hello au sein de la nouvelle hiérarchie de hello.
>
>

Une fois que vous avez lié tooOMS du Gestionnaire de Configuration, vous pouvez ajouter ou supprimer des collections et afficher les propriétés de hello Hello connexion OMS.

## <a name="update-oms-connection-properties"></a>Mettre à jour les propriétés de la connexion OMS
Si une clé secrète du client ou le mot de passe expire jamais ou est perdue, vous aurez besoin des propriétés de connexion toomanually mise à jour hello OMS.

1. Dans Configuration Manager, accédez trop**Services de cloud computing** , puis sélectionnez **connecteur OMS** tooopen hello **propriétés de connexion OMS** page.
2. Dans cette page, cliquez sur hello **Azure Active Directory** onglet tooview votre **client**, **ID Client**, **expiration de clés secrète Client**. **Vérifiez** votre **Clé secrète client** pour voir si elle a expiré.

## <a name="download-and-install-hello-agent"></a>Téléchargez et installez l’agent de hello
1. Dans le portail OMS hello, [fichier de configuration de l’agent de hello téléchargement d’OMS](log-analytics-windows-agents.md#download-the-agent-setup-file-from-oms).
2. Utilisez une des hello suivant les méthodes tooinstall et configurer l’agent de hello sur hello ordinateur exécutant le rôle de système site de point de connexion de hello Configuration Manager service :
   * [Installer l’agent de hello à l’aide du programme d’installation](log-analytics-windows-agents.md#install-the-agent-using-setup)
   * [Installer l’agent de hello à l’aide de la ligne de commande hello](log-analytics-windows-agents.md#install-the-agent-using-the-command-line)
   * [Installer l’agent de hello à l’aide de DSC dans Azure Automation](log-analytics-windows-agents.md#install-the-agent-using-dsc-in-azure-automation)

## <a name="import-collections"></a>Importer des regroupements
Une fois que vous avez ajouté une tooConfiguration de connexion OMS Manager et installé l’agent de hello sur ordinateur hello connexion au service Gestionnaire de Configuration hello point rôle de système de site, hello prochaine étape consiste tooimport regroupements à partir du Gestionnaire de Configuration d’OMS en tant que groupes d’ordinateurs.

Après l’importation est activée, les informations d’appartenance au regroupement hello sont récupérées toutes les 3 heures tookeep hello appartenances à la collection actuelles. Vous pouvez choisir d’importation toodisable à tout moment.

1. Dans le portail OMS : hello, cliquez sur **paramètres**.
2. Cliquez sur hello **groupes d’ordinateurs** onglet, puis cliquez sur hello **SCCM** onglet.
3. Sélectionnez **Importer les appartenances aux regroupements Configuration Manager**, puis cliquez sur **Enregistrer**.  
   ![Groupes d’ordinateurs - Onglet SCCM](./media/log-analytics-sccm/sccm-computer-groups01.png)

## <a name="view-data-from-configuration-manager"></a>Afficher les données de Configuration Manager
Après avoir ajouté une tooConfiguration de connexion OMS Manager et installé l’agent de hello sur ordinateur hello rôle de système site de point de connexion de hello Configuration Manager service en cours d’exécution, les données à partir de l’agent de hello sont envoyées tooOMS. Dans OMS, vos regroupements de Configuration Manager apparaissent sous la forme de [groupes d’ordinateurs](log-analytics-computer-groups.md). Vous pouvez afficher les groupes hello hello **Configuration Manager** page sous **groupes d’ordinateurs** dans **paramètres**.

Après avoir hello collections sont importées, vous pouvez voir combien d’ordinateurs avec appartenances aux collections ont été détectées. Vous pouvez également voir hello collection qui ont été importés.

![Groupes d’ordinateurs - Onglet SCCM](./media/log-analytics-sccm/sccm-computer-groups02.png)

Lorsque vous cliquez sur le des deux, ouvre de recherche, affichage de toutes les soit hello importé groupes ou tous les ordinateurs qui appartiennent tooeach groupe. Dans [Recherche de journal](log-analytics-log-searches.md), vous pouvez démarrer une analyse approfondie des données Configuration Manager.

## <a name="next-steps"></a>Étapes suivantes
* Utilisez [recherche de journal](log-analytics-log-searches.md) tooview des informations détaillées sur vos données de Configuration Manager.
