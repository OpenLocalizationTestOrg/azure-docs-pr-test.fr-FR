---
title: aaaManage Azure Analysis Services | Documents Microsoft
description: "Découvrez comment toomanage un Analysis Services server dans Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: b03bc440801a68162039e28cdb4f863da374014e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-analysis-services"></a>Gérer Analysis Services
Une fois que vous avez créé un serveur Analysis Services dans Azure, il est peut-être certaines des tâches d’administration et de gestion vous devez tooperform immédiatement ou plus tard bas hello route. Par exemple, exécutez le traitement des données d’actualisation toohello, contrôler qui peut accéder aux modèles de hello sur votre serveur, ou surveiller l’intégrité de votre serveur. Certaines tâches de gestion ne peuvent être effectuées que dans le portail Azure, d’autres dans SQL Server Management Studio (SSMS), et certaines tâches encore peuvent être effectuées dans les deux.

## <a name="azure-portal"></a>Portail Azure
[Portail Azure](http://portal.azure.com/) est où vous pouvez créer et supprimer des serveurs, surveillance des ressources serveur, modifier la taille et gérer les utilisateurs ayant des serveurs d’accès tooyour.  Si vous rencontrez des problèmes, vous pouvez également envoyer une demande de support.

![Obtenir le nom du serveur dans Azure](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a>SQL Server Management Studio
La connexion serveur tooyour dans Azure est identique à la connexion tooa instance de serveur dans votre organisation. À partir de SSMS, vous pouvez effectuer un grand nombre de hello même tâches telles que les données de processus ou créer un script de traitement, gérer les rôles et utiliser PowerShell.
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a>Téléchargement et installation de SSMS
tooget tous hello dernières fonctionnalités et expérience plus lissé de hello lors de la connexion du serveur de Azure Analysis Services tooyour, veillez à ce que vous utilisez la version la plus récente de SSMS hello. 

[Téléchargez SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).


### <a name="tooconnect-with-ssms"></a>tooconnect avec SSMS
 Lors de l’utilisation de SSMS, avant la connexion tooyour messages hello du serveur première fois, vérifiez que votre nom d’utilisateur est inclus dans le groupe d’administrateurs de Services d’analyse hello. toolearn, voir [les administrateurs de serveur](#server-administrators) plus loin dans cet article.

1. Avant de vous connectez, vous devez le nom du serveur tooget hello. Dans **portail Azure** > serveur > **vue d’ensemble** > **nom du serveur**, copier le nom de serveur hello.
   
    ![Obtenir le nom du serveur dans Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. Dans SSMS > **Explorateur d’objets**, cliquez sur **Se connecter** > **Analysis Services**.
3. Bonjour **connecter tooServer** boîte de dialogue, coller dans le nom du serveur hello, puis en **authentification**, choisissez une des hello les types d’authentification suivants :
   
    **L’authentification Windows** toouse vos informations d’identification Windows domaine\nom d’utilisateur et mot de passe.

    **Authentification du mot de passe Active Directory** toouse un compte professionnel. Par exemple, lors d’une connexion à partir d’un ordinateur non joint à un domaine.

    **L’authentification Active Directory universel** toouse [non interactif ou multi-Factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md). 
   
    ![Se connecter dans SSMS](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a>Administrateurs de serveur et utilisateurs de base de données
Dans Azure Analysis Services, il existe deux types d’utilisateur : les administrateurs de serveur et les utilisateurs de base de données. Les deux types d’utilisateur doivent exister dans Azure Active Directory et être spécifiés par adresse de messagerie d’organisation ou UPN. toolearn, voir [d’authentification et les autorisations utilisateur](analysis-services-manage-users.md).


## <a name="troubleshooting-connection-problems"></a>Résolution des problèmes de connexion
Lors de la connexion à l’aide de SSMS, si vous rencontrez des problèmes, vous devrez peut-être le cache de connexion tooclear hello. Rien n’est toodisc mis en cache. processus de connexion tooclear hello cache, fermez et redémarrez hello. 

## <a name="next-steps"></a>Étapes suivantes
Si vous n’avez pas déjà déployé un nouveau serveur de tooyour modèle tabulaire, est judicieux. toolearn, voir [déployer tooAzure Analysis Services](analysis-services-deploy.md).

Si vous avez déployé un serveur tooyour de modèle, vous êtes tooit tooconnect prêt à l’aide d’un client ou un navigateur. toolearn, voir [obtenir des données à partir d’Azure Analysis Services](analysis-services-connect.md).

