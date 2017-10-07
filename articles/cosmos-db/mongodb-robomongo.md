---
title: "aaaUse Robomongo pour la base de données Azure Cosmos | Documents Microsoft"
description: "Découvrez comment toouse Robomongo avec une base de données Azure Cosmos : API pour MongoDB compte"
keywords: robomongo
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 3018243e904015426dc69a69b26fb53421e1fe4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a>Utiliser Robomongo avec un compte Azure Cosmos DB : API pour MongoDB
tooconnect tooan base de données Azure Cosmos : API pour le compte de MongoDB à l’aide de Robomongo, vous devez :

* Télécharger et installer [Robomongo](https://robomongo.org/)
* Disposer des informations de [chaîne de connexion](connect-mongodb-account.md) de votre compte Azure Cosmos DB : API pour MongoDB

## <a name="connect-using-robomongo"></a>Connexion à l’aide de Robomongo
tooadd votre base de données Azure Cosmos : API pour MongoDB compte toohello Robomongo MongoDB connexions, effectuer hello comme suit.

1. Récupérer votre base de données Azure Cosmos : API pour les informations de connexion de compte MongoDB en suivant les instructions hello [ici](connect-mongodb-account.md).

    ![Capture d’écran du Panneau de chaîne de connexion hello](./media/mongodb-robomongo/connectionstringblade.png)
2. Exécutez *Robomongo.exe*

3. Cliquez sur le bouton de connexion hello sous **fichier** toomanage vos connexions. Ensuite, cliquez sur **créer** Bonjour **MongoDB connexions** fenêtre, ce qui permet d’ouvrir hello **paramètres de connexion** fenêtre.

4. Bonjour **paramètres de connexion** fenêtre, choisissez un nom. Recherchez ensuite hello **hôte** et **Port** à vos informations de connexion dans l’étape 1 et entrez-les dans **adresse** et **Port**, respectivement .

    ![Capture d’écran de hello Robomongo gérer les connexions](./media/mongodb-robomongo/manageconnections.png)
5. Sur hello **authentification** , cliquez sur **effectuer l’authentification**. Entrez ensuite votre base de données (la valeur par défaut est *Admin*), le **Nom d’utilisateur** et le **Mot de passe**.
Le **Nom d’utilisateur** et le **Mot de passe** figurent tous deux dans vos informations de connexion à l’étape 1.

    ![Capture d’écran de hello onglet authentification de Robomongo](./media/mongodb-robomongo/authentication.png)
6. Sur hello **SSL** onglet, vérifiez **protocole d’utiliser SSL**, puis modifiez hello **méthode d’authentification** trop**un certificat auto-signé**.

    ![Capture d’écran de hello Robomongo SSL onglet](./media/mongodb-robomongo/SSL.png)
7. Enfin, cliquez sur **Test** tooverify que vous êtes en mesure de tooconnect, puis **enregistrer**.

## <a name="next-steps"></a>Étapes suivantes
* Explorez les [exemples](mongodb-samples.md) d’Azure Cosmos DB : API pour MongoDB.
