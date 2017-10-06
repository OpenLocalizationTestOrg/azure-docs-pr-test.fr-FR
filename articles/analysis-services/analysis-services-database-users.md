---
title: "aaaManage de la base de données des rôles et les utilisateurs dans Azure Analysis Services | Documents Microsoft"
description: "Découvrez comment toomanage base de données les rôles et les utilisateurs sur un serveur Analysis Services dans Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 2ad069a6bcce11bc43347625cb32ec400d48af18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-database-roles-and-users"></a>Gérer les rôles et les utilisateurs de base de données

Au niveau de base de données de modèle hello, tous les utilisateurs doivent appartenir tooa rôle. Les rôles définissent les utilisateurs disposant d’autorisations spécifiques pour la base de données model hello. N’importe quel utilisateur ou groupe de sécurité ajouté tooa rôle doit avoir un compte dans un locataire Azure AD Bonjour même abonnement que hello serveur.

Comment définir des rôles est différent selon outil hello que vous utilisez, mais effet de hello est hello identiques.

Les autorisations des rôles incluent :
*  **Administrateur** -les utilisateurs disposent des autorisations complètes pour la base de données hello. Les rôles de base de données avec des autorisations d’administrateur sont différents des administrateurs de serveur.
*  **Processus** -les utilisateurs peuvent se connecter tooand effectuer des opérations de traitement sur la base de données hello et analyser les données de base de données de modèle.
*  **Lecture** -les utilisateurs peuvent utiliser un client application tooconnect tooand analyser les données de base de données de modèle.

Lorsque vous créez un projet de modèle tabulaire, vous créez des rôles et ajoutez des rôles de toothose des utilisateurs ou des groupes à l’aide du Gestionnaire de rôles dans SSDT. Lorsque tooa déployé server, vous utilisez SSMS, [applets de commande PowerShell Analysis Services](https://msdn.microsoft.com/library/hh758425.aspx), ou [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) tooadd ou supprimer des rôles et des membres de l’utilisateur.

## <a name="tooadd-or-manage-roles-and-users-in-ssdt"></a>tooadd ou gérer des rôles et des utilisateurs dans SSDT  
  
1.  Dans SSDT > **Tabular Model Explorer**, cliquez avec le bouton droit sur **Rôles**.  
  
2.  Dans le **Gestionnaire de rôles**, cliquez sur **Nouveau**.  
  
3.  Tapez un nom pour le rôle de hello.  
  
     Par défaut, nom hello de rôle par défaut de hello est numéroté de façon incrémentielle pour chaque nouveau rôle. Il est recommandé de que taper un nom qui identifie clairement le type de membre hello, par exemple, directeurs financiers ou responsables des ressources humaines.  
  
4.  Sélectionnez une des hello les autorisations suivantes :  
  
    |Autorisation|Description|  
    |----------------|-----------------|  
    |**Aucun**|Les membres ne peuvent pas de modifier le schéma de modèle hello et ne peut pas interroger les données.|  
    |**Lire**|Les membres peuvent interroger des données (selon les filtres de lignes), mais Impossible de modifier le schéma de modèle hello.|  
    |**Lecture et traitement**|Les membres peuvent interroger des données (selon les filtres au niveau des lignes) et l’exécution des opérations traiter et traiter tout, mais Impossible de modifier le schéma de modèle hello.|  
    |**Processus**|Les membres peuvent exécuter des processus et traiter toutes les opérations. Impossible de modifier le schéma de modèle hello et ne peut pas interroger les données.|  
    |**Administrateur**|Les membres peuvent modifier le schéma de modèle hello et interroger toutes les données.|   
  
5.  Dans le cas des rôles de hello création a lu ou autorisation en lecture et de processus, vous pouvez ajouter des filtres de lignes à l’aide d’une formule DAX. Cliquez sur hello **les filtres de lignes** onglet, sélectionnez une table, puis cliquez sur hello **filtre DAX** champ, puis tapez une formule DAX.
  
6.  Cliquez sur **Membres** > **Ajouter externe**.  
  
8.  Dans **Ajouter un membre externe**, entrez les utilisateurs ou groupes dans votre Azure AD client par adresse e-mail. Une fois que vous avez cliqué sur OK et fermé le Gestionnaire de rôles, les rôles et les membres du rôle s’affichent dans l’Explorateur de modèles tabulaires. 
 
     ![Rôles et les utilisateurs dans l’Explorateur de modèles tabulaires](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. Déployer tooyour Azure Analysis Services serveur.


## <a name="tooadd-or-manage-roles-and-users-in-ssms"></a>tooadd ou gérer des rôles et des utilisateurs dans SSMS
tooa de rôles et les utilisateurs tooadd déployé la base de données model, vous devez être connecté toohello serveur en tant qu’un administrateur de serveur ou est déjà dans un rôle de base de données avec des autorisations d’administrateur.

1. Dans Object Exporer, cliquez avec le bouton droit sur **Rôles** > **Nouveau rôle**.

2. Dans **Créer un rôle**, entrez un nom de rôle et une description.

3. Sélectionnez une autorisation.
   |Autorisation|Description|  
   |----------------|-----------------|  
   |**Contrôle total (administrateur)**|Les membres peuvent modifier le schéma de modèle hello, traiter et interroger toutes les données.| 
   |**Base de données de processus**|Les membres peuvent exécuter des processus et traiter toutes les opérations. Impossible de modifier le schéma de modèle hello et ne peut pas interroger les données.|  
   |**Lire**|Les membres peuvent interroger des données (selon les filtres de lignes), mais Impossible de modifier le schéma de modèle hello.|  
  
4. Cliquez sur **Appartenance**, puis entrez un utilisateur ou un groupe dans votre client Azure AD par adresse e-mail.

     ![Ajouter un utilisateur](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. Si le rôle que vous créez hello possède une autorisation de lecture, vous pouvez ajouter des filtres de lignes à l’aide d’une formule DAX. Cliquez sur **les filtres de lignes**, sélectionnez une table, puis tapez une formule DAX dans hello **filtre DAX** champ. 

## <a name="tooadd-roles-and-users-by-using-a-tmsl-script"></a>tooadd rôles et les utilisateurs à l’aide d’un script TMSL
Vous pouvez exécuter un script TMSL dans la fenêtre XMLA hello dans SSMS, ou à l’aide de PowerShell. Hello d’utilisation [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) commande et hello [rôles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) objet.

**Exemple de script TMSL**

Dans cet exemple, un utilisateur externe B2B et un groupe sont ajoutés rôle d’analyste toohello avec les autorisations de lecture pour la base de données SalesBI hello. Les deux hello utilisateur externe et de groupe doit être dans le même client Azure AD.

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users tooquery hello model",
      "modelPermission": "read",
      "members": [
        {
          "memberName": "user1@contoso.com",
          "identityProvider": "AzureAD"
        },
        {
          "memberName": "group1@adventureworks.com",
          "identityProvider": "AzureAD"
        }
      ]
    }
  }
}
```

## <a name="tooadd-roles-and-users-by-using-powershell"></a>tooadd rôles et les utilisateurs à l’aide de PowerShell
Hello [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module fournit spécifiques à une tâche de base de données Gestion des applets de commande et hello à usage général Invoke-ASCmd applet de commande qui accepte une requête d’écriture de scripts langage TMSL (Tabular Model) ou un script. Hello suivant d’applets de commande est utilisé pour la gestion des utilisateurs et des rôles de base de données.
  
|Applet de commande|Description|
|------------|-----------------| 
|[Add-RoleMember](https://msdn.microsoft.com/library/hh510167.aspx)|Ajouter un rôle de base de données de membre tooa.| 
|[Remove-RoleMember](https://msdn.microsoft.com/library/hh510173.aspx)|Supprime un membre d’un rôle de base de données.|   
|[Invoke-ASCmd](https://msdn.microsoft.com/library/hh479579.aspx)|Exécute un script TMSL.|

## <a name="row-filters"></a>Filtres de lignes  
Les filtres de lignes définissent les lignes d’une table qui peuvent être interrogées par les membres d’un rôle donné. Les filtres de lignes sont définis pour chaque table dans un modèle à l’aide de formules DAX.  
  
Les filtres de lignes peuvent être définis uniquement pour les rôles avec des autorisations de Lecture et de Lecture et processus. Par défaut, si un filtre de lignes n’est pas défini pour une table particulière, les membres peuvent interroger toutes les lignes de la table de hello, sauf si le filtrage croisé s’applique à partir d’une autre table.
  
 Les filtres de lignes nécessitent une formule DAX, qui doit prendre la valeur TRUE/FALSE, les lignes de hello toodefine qui peuvent être interrogées par les membres de ce rôle particulier de tooa. Les lignes non incluses dans hello formule DAX ne peut pas être interrogés. Par exemple, hello table Customers avec hello suivant l’expression de filtres de lignes, *= clients [pays] = « France »*, les membres du rôle Sales de hello peuvent visualiser uniquement les clients Bonjour USA.  
  
Les filtres de lignes s’appliquent toohello spécifié lignes et les lignes associées. Lorsqu’une table possède plusieurs relations, filtres appliquent la sécurité pour la relation de hello est active. Les filtres de lignes sont croisés avec d’autres filtres de lignes définis pour les tables associées, par exemple :  
  
|Table|Expression DAX|  
|-----------|--------------------|  
|Région|=Region[Country]=”USA”|  
|ProductCategory|=ProductCategory[Name]=”Bicycles”|  
|Transactions|=Transactions[Year]=2016|  
  
 effet net de Hello est membres peuvent interroger les lignes de données où client de hello réside aux États-Unis de hello, catégorie de produit hello correspond à des bicyclettes et l’année hello est 2016. Les utilisateurs ne peuvent pas interroger les transactions en dehors des États-Unis de hello, qui ne sont pas bicyclettes ou transactions pas de 2016, sauf si elles sont membres d’un autre rôle qui accorde ces autorisations.
  
 Vous pouvez utiliser le filtre de hello, *= False()*, les lignes tooall toodeny accès pour une table entière.

## <a name="next-steps"></a>Étapes suivantes
  [Gérer les administrateurs de serveur](analysis-services-server-admins.md)   
  [Gérer Azure Analysis Services avec PowerShell](analysis-services-powershell.md)  
  [Langage TMSL (Tabular Model Scripting Language)](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

