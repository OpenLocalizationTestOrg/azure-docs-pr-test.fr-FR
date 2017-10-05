---
title: "Utiliser Robomongo pour Azure Cosmos DB | Microsoft Docs"
description: "Découvrez comment utiliser Robomongo avec un compte Azure Cosmos DB : API pour MongoDB"
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
ms.openlocfilehash: 8983594776a1bbe413a6d7cf2cd518f0e327648a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="0d924-104">Utiliser Robomongo avec un compte Azure Cosmos DB : API pour MongoDB</span><span class="sxs-lookup"><span data-stu-id="0d924-104">Use Robomongo with an Azure Cosmos DB: API for MongoDB account</span></span>
<span data-ttu-id="0d924-105">Pour vous connecter à un compte Azure Cosmos DB : API pour MongoDB avec Robomongo, vous devez :</span><span class="sxs-lookup"><span data-stu-id="0d924-105">To connect to an Azure Cosmos DB: API for MongoDB account using Robomongo, you must:</span></span>

* <span data-ttu-id="0d924-106">Télécharger et installer [Robomongo](https://robomongo.org/)</span><span class="sxs-lookup"><span data-stu-id="0d924-106">Download and install [Robomongo](https://robomongo.org/)</span></span>
* <span data-ttu-id="0d924-107">Disposer des informations de [chaîne de connexion](connect-mongodb-account.md) de votre compte Azure Cosmos DB : API pour MongoDB</span><span class="sxs-lookup"><span data-stu-id="0d924-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="connect-using-robomongo"></a><span data-ttu-id="0d924-108">Connexion à l’aide de Robomongo</span><span class="sxs-lookup"><span data-stu-id="0d924-108">Connect using Robomongo</span></span>
<span data-ttu-id="0d924-109">Pour ajouter votre compte Azure Cosmos DB : API pour MongoDB aux connexions Robomongo MongoDB, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="0d924-109">To add your Azure Cosmos DB: API for MongoDB account to the Robomongo MongoDB Connections, perform the following steps.</span></span>

1. <span data-ttu-id="0d924-110">Récupérez les informations de connexion de votre compte Azure Cosmos DB : API pour MongoDB à l’aide des instructions [ici](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="0d924-110">Retrieve your Azure Cosmos DB: API for MongoDB account connection information using the instructions [here](connect-mongodb-account.md).</span></span>

    ![Capture d’écran du panneau Chaîne de connexion](./media/mongodb-robomongo/connectionstringblade.png)
2. <span data-ttu-id="0d924-112">Exécutez *Robomongo.exe*</span><span class="sxs-lookup"><span data-stu-id="0d924-112">Run *Robomongo.exe*</span></span>

3. <span data-ttu-id="0d924-113">Cliquez sur le bouton de connexion sous **Fichier** pour gérer vos connexions.</span><span class="sxs-lookup"><span data-stu-id="0d924-113">Click the connection button under **File** to manage your connections.</span></span> <span data-ttu-id="0d924-114">Ensuite, cliquez sur **Créer** dans la fenêtre **Connexions MongoDB**, ce qui ouvre la fenêtre **Paramètres de connexion**.</span><span class="sxs-lookup"><span data-stu-id="0d924-114">Then, click **Create** in the **MongoDB Connections** window, which will open up the **Connection Settings** window.</span></span>

4. <span data-ttu-id="0d924-115">Dans la fenêtre **Paramètres de connexion**, choisissez un nom.</span><span class="sxs-lookup"><span data-stu-id="0d924-115">In the **Connection Settings** window, choose a name.</span></span> <span data-ttu-id="0d924-116">Ensuite, recherchez **Hôte** et **Port** dans vos informations de connexion à l’étape 1 et entrez-les dans les champs **Adresse** et **Port**, respectivement.</span><span class="sxs-lookup"><span data-stu-id="0d924-116">Then, find the **Host** and **Port** from your connection information in Step 1 and enter them into **Address** and **Port**, respectively.</span></span>

    ![Capture d’écran de gestion des connexions avec Robomongo](./media/mongodb-robomongo/manageconnections.png)
5. <span data-ttu-id="0d924-118">Dans l’onglet **Authentification**, cliquez sur **Effectuer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="0d924-118">On the **Authentication** tab, click **Perform authentication**.</span></span> <span data-ttu-id="0d924-119">Entrez ensuite votre base de données (la valeur par défaut est *Admin*), le **Nom d’utilisateur** et le **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="0d924-119">Then, enter your Database (default is *Admin*), **User Name** and **Password**.</span></span>
<span data-ttu-id="0d924-120">Le **Nom d’utilisateur** et le **Mot de passe** figurent tous deux dans vos informations de connexion à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="0d924-120">Both **User Name** and **Password** can be found in your connection information in Step 1.</span></span>

    ![Capture d’écran de l’onglet authentification de Robomongo](./media/mongodb-robomongo/authentication.png)
6. <span data-ttu-id="0d924-122">Dans l’onglet **SSL**, cochez **Utiliser le protocole SSL**, puis modifiez la **Méthode d’authentification** sur **Certificat auto-signé**.</span><span class="sxs-lookup"><span data-stu-id="0d924-122">On the **SSL** tab, check **Use SSL protocol**, then change the **Authentication Method** to **Self-signed Certificate**.</span></span>

    ![Capture d’écran de l’onglet SSL de Robomongo](./media/mongodb-robomongo/SSL.png)
7. <span data-ttu-id="0d924-124">Enfin, cliquez sur **Test** pour vérifier que vous êtes en mesure de vous connecter, puis sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="0d924-124">Finally, click **Test** to verify that you are able to connect, then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d924-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0d924-125">Next steps</span></span>
* <span data-ttu-id="0d924-126">Explorez les [exemples](mongodb-samples.md) d’Azure Cosmos DB : API pour MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0d924-126">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
