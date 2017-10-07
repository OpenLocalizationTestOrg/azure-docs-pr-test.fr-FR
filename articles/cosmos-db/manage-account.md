---
title: "aaaManage un compte de base de données Azure Cosmos via hello portail Azure | Documents Microsoft"
description: "Découvrez comment toomanage votre base de données Azure Cosmos compte via hello portail Azure. Rechercher un guide sur l’utilisation de tooview du portail Azure hello, copier, supprimer et l’accès des comptes."
keywords: Portail Azure, documentdb, azure, Microsoft azure
services: cosmos-db
documentationcenter: 
author: kirillg
manager: jhubbard
editor: cgronlun
ms.assetid: 00fc172f-f86c-44ca-8336-11998dcab45c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kirillg
ms.openlocfilehash: 77ad953cf558a519674be08ad913a12202f69496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-an-azure-cosmos-db-account"></a>Comment toomanage un compte de base de données Azure Cosmos
Découvrez comment la cohérence tooset, travailler avec les clés et supprimer un compte de base de données Azure Cosmos Bonjour portail Azure.

## <a id="consistency"></a>Gérer les paramètres de cohérence Azure Cosmos DB
En sélectionnant le niveau de cohérence droite hello dépend de la sémantique de hello de votre application. Vous devez vous familiariser avec les niveaux de cohérence disponible hello dans la base de données Azure Cosmos en lisant [à l’aide de la cohérence des niveaux de disponibilité de toomaximize et les performances dans la base de données Azure Cosmos][consistency]. Azure Cosmos DB fournit les garanties de cohérence, de disponibilité et de performance, à tous les niveaux de cohérence disponibles pour votre compte de base de données. Configuration de votre compte de base de données avec un niveau de cohérence de fort requiert que vos données sont confiné tooa une seule région Azure et non globalement disponible. On hello d’autre part, hello des niveaux de cohérence souple - obsolescence limitée, de session ou d’activer éventuelle vous tooassociate n’importe quel nombre de régions Azure avec votre compte de base de données. Hello suivant étapes simples vous montre comment tooselect hello le niveau de cohérence par défaut pour votre compte de base de données. 

### <a name="toospecify-hello-default-consistency-for-an-azure-cosmos-db-account"></a>toospecify hello par défaut la cohérence pour un compte de base de données Azure Cosmos
1. Bonjour [portail Azure](https://portal.azure.com/), accéder à votre compte de base de données Azure Cosmos.
2. Dans le panneau de compte hello, cliquez sur **par défaut de la cohérence**.
3. Bonjour **cohérence par défaut** panneau, niveau de cohérence hello sélectionnez Nouveau, cliquez sur **enregistrer**.
    ![Cohérence par défaut Session][5]

## <a id="keys"></a>Affichage, copie et régénération des clés d’accès
Lorsque vous créez un compte de base de données Azure Cosmos, service de hello génère deux clés d’accès maître qui peuvent être utilisés pour l’authentification lors de l’accès hello compte de base de données Azure Cosmos. En fournissant deux clés d’accès, base de données Azure Cosmos vous permet de clés de hello tooregenerate avec aucune tooyour d’interruption du compte de base de données Azure Cosmos. 

Bonjour [portail Azure](https://portal.azure.com/), hello d’accès **clés** panneau à partir du menu ressources hello hello **compte de base de données Azure Cosmos** panneau tooview, copier et régénérer hello touches d’accès sont tooaccess utilisé votre compte de base de données Azure Cosmos.

![Capture d’écran du portail Azure, panneau Clés](./media/manage-account/keys.png)

> [!NOTE]
> Hello **clés** panneau inclut également principal et de chaînes de connexion secondaire qui peuvent être utilisé tooconnect tooyour compte du hello [outil de Migration de données](import-data.md).
> 
> 

Des clés en lecture seule sont également disponibles sur ce panneau. Les lectures et les demandes sont des opérations en lecture seule, contrairement aux opérations de création, de suppression et de remplacement.

### <a name="copy-an-access-key-in-hello-azure-portal"></a>Copier une clé d’accès Bonjour portail Azure
Sur hello **clés** panneau, cliquez sur hello **copie** toohello bouton à droite de la clé de hello que vous souhaitez toocopy.

![Afficher et copier une clé d’accès Bonjour Azure Portal, panneau de clés](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a>Régénération de clés d'accès
Vous devez modifier le compte de base de données Azure Cosmos tooyour hello accès clés périodiquement toohelp renforcer vos connexions. Deux clés d’accès sont affectés tooenable connexions toomaintain vous toohello compte de base de données Azure Cosmos à l’aide d’une clé d’accès pendant la régénération de hello autre clé d’accès.

> [!WARNING]
> Régénérer vos clés d’accès affecte toutes les applications qui dépendent de la clé actuelle de hello. Tous les clients qui utilisent le compte de base de données Azure Cosmos hello accès tooaccess clé hello doivent être la nouvelle clé de hello toouse mis à jour.
> 
> 

Si vous avez des applications ou services de cloud computing à l’aide du compte de base de données Azure Cosmos de hello, vous perdrez les connexions hello si vous régénérez des clés, sauf si vous régénérez vos clés. Hello étapes suivantes décrivent les processus hello de transfert de vos clés.

1. Mettre à jour la clé d’accès hello dans votre clé d’accès secondaire application code tooreference hello Hello compte de base de données Azure Cosmos.
2. Régénérer la clé d’accès primaire hello pour votre compte de base de données Azure Cosmos. Bonjour [Azure Portal](https://portal.azure.com/), accéder à votre compte de base de données Azure Cosmos.
3. Bonjour **compte de base de données Azure Cosmos** panneau, cliquez sur **clés**.
4. Sur hello **clés** panneau, cliquez sur hello régénérer, puis cliquez sur **Ok** tooconfirm que vous souhaitez toogenerate une nouvelle clé.
    ![Régénération des clés d’accès](./media/manage-account/regenerate-keys.png)
5. Une fois que vous avez vérifié de cette nouvelle clé de hello est disponible pour une utilisation (environ 5 minutes après la régénération), mettre à jour la clé d’accès hello dans votre application code tooreference hello nouvelle clé primaire.
6. Régénérer la clé d’accès secondaire hello.
   
    ![Régénération de clés d'accès](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> Il peut prendre plusieurs minutes avant d’une clé qui vient d’être générée peut être tooaccess utilisé votre compte de base de données Azure Cosmos.
> 
> 

## <a name="get-hello--connection-string"></a>Obtenir la chaîne de connexion hello
tooretrieve votre connexion de chaîne, hello suivant : 

1. Bonjour [portail Azure](https://portal.azure.com), accéder à votre compte de base de données Azure Cosmos.
2. Dans le menu de ressource hello, cliquez sur **clés**.
3. Cliquez sur hello **copie** toohello suivant du bouton **chaîne de connexion principal** ou **chaîne de connexion secondaire** boîte. 

Si vous utilisez une chaîne de connexion hello Bonjour [outil de Migration de base de données Azure Cosmos DB](import-data.md), ajouter hello de base de données nom toohello end hello de chaîne de connexion. `AccountEndpoint=< >;AccountKey=< >;Database=< >`.

## <a id="delete"></a> Supprimer un compte Azure Cosmos DB
tooremove une base de données Azure Cosmos compte hello portail Azure que vous n’utilisez plus, nom du compte hello avec le bouton droit, puis cliquez sur **supprimer le compte**.

![Procédure toodelete une base de données Azure Cosmos compte dans hello portail Azure](./media/manage-account/deleteaccount.png)

1. Bonjour [portail Azure](https://portal.azure.com/), accéder au compte de base de données Azure Cosmos hello toodelete vous le souhaitez.
2. Sur hello **compte de base de données Azure Cosmos** panneau, cliquez sur le compte de hello, puis cliquez sur **supprimer un compte**. 
3. Sur le panneau de confirmation qui en résulte hello, tapez tooconfirm de nom du compte de base de données Azure Cosmos hello toodelete hello compte.
4. Cliquez sur hello **supprimer** bouton.

![Procédure toodelete une base de données Azure Cosmos compte dans hello portail Azure](./media/manage-account/delete-account-confirm.png)

## <a id="next"></a>Étapes suivantes
Découvrez comment trop[prise en main votre compte de base de données Azure Cosmos](http://go.microsoft.com/fwlink/p/?LinkId=402364).

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
