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
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="d6404-104">Utiliser Robomongo avec un compte Azure Cosmos DB : API pour MongoDB</span><span class="sxs-lookup"><span data-stu-id="d6404-104">Use Robomongo with an Azure Cosmos DB: API for MongoDB account</span></span>
<span data-ttu-id="d6404-105">tooconnect tooan base de données Azure Cosmos : API pour le compte de MongoDB à l’aide de Robomongo, vous devez :</span><span class="sxs-lookup"><span data-stu-id="d6404-105">tooconnect tooan Azure Cosmos DB: API for MongoDB account using Robomongo, you must:</span></span>

* <span data-ttu-id="d6404-106">Télécharger et installer [Robomongo](https://robomongo.org/)</span><span class="sxs-lookup"><span data-stu-id="d6404-106">Download and install [Robomongo](https://robomongo.org/)</span></span>
* <span data-ttu-id="d6404-107">Disposer des informations de [chaîne de connexion](connect-mongodb-account.md) de votre compte Azure Cosmos DB : API pour MongoDB</span><span class="sxs-lookup"><span data-stu-id="d6404-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="connect-using-robomongo"></a><span data-ttu-id="d6404-108">Connexion à l’aide de Robomongo</span><span class="sxs-lookup"><span data-stu-id="d6404-108">Connect using Robomongo</span></span>
<span data-ttu-id="d6404-109">tooadd votre base de données Azure Cosmos : API pour MongoDB compte toohello Robomongo MongoDB connexions, effectuer hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="d6404-109">tooadd your Azure Cosmos DB: API for MongoDB account toohello Robomongo MongoDB Connections, perform hello following steps.</span></span>

1. <span data-ttu-id="d6404-110">Récupérer votre base de données Azure Cosmos : API pour les informations de connexion de compte MongoDB en suivant les instructions hello [ici](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="d6404-110">Retrieve your Azure Cosmos DB: API for MongoDB account connection information using hello instructions [here](connect-mongodb-account.md).</span></span>

    ![Capture d’écran du Panneau de chaîne de connexion hello](./media/mongodb-robomongo/connectionstringblade.png)
2. <span data-ttu-id="d6404-112">Exécutez *Robomongo.exe*</span><span class="sxs-lookup"><span data-stu-id="d6404-112">Run *Robomongo.exe*</span></span>

3. <span data-ttu-id="d6404-113">Cliquez sur le bouton de connexion hello sous **fichier** toomanage vos connexions.</span><span class="sxs-lookup"><span data-stu-id="d6404-113">Click hello connection button under **File** toomanage your connections.</span></span> <span data-ttu-id="d6404-114">Ensuite, cliquez sur **créer** Bonjour **MongoDB connexions** fenêtre, ce qui permet d’ouvrir hello **paramètres de connexion** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="d6404-114">Then, click **Create** in hello **MongoDB Connections** window, which will open up hello **Connection Settings** window.</span></span>

4. <span data-ttu-id="d6404-115">Bonjour **paramètres de connexion** fenêtre, choisissez un nom.</span><span class="sxs-lookup"><span data-stu-id="d6404-115">In hello **Connection Settings** window, choose a name.</span></span> <span data-ttu-id="d6404-116">Recherchez ensuite hello **hôte** et **Port** à vos informations de connexion dans l’étape 1 et entrez-les dans **adresse** et **Port**, respectivement .</span><span class="sxs-lookup"><span data-stu-id="d6404-116">Then, find hello **Host** and **Port** from your connection information in Step 1 and enter them into **Address** and **Port**, respectively.</span></span>

    ![Capture d’écran de hello Robomongo gérer les connexions](./media/mongodb-robomongo/manageconnections.png)
5. <span data-ttu-id="d6404-118">Sur hello **authentification** , cliquez sur **effectuer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="d6404-118">On hello **Authentication** tab, click **Perform authentication**.</span></span> <span data-ttu-id="d6404-119">Entrez ensuite votre base de données (la valeur par défaut est *Admin*), le **Nom d’utilisateur** et le **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d6404-119">Then, enter your Database (default is *Admin*), **User Name** and **Password**.</span></span>
<span data-ttu-id="d6404-120">Le **Nom d’utilisateur** et le **Mot de passe** figurent tous deux dans vos informations de connexion à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="d6404-120">Both **User Name** and **Password** can be found in your connection information in Step 1.</span></span>

    ![Capture d’écran de hello onglet authentification de Robomongo](./media/mongodb-robomongo/authentication.png)
6. <span data-ttu-id="d6404-122">Sur hello **SSL** onglet, vérifiez **protocole d’utiliser SSL**, puis modifiez hello **méthode d’authentification** trop**un certificat auto-signé**.</span><span class="sxs-lookup"><span data-stu-id="d6404-122">On hello **SSL** tab, check **Use SSL protocol**, then change hello **Authentication Method** too**Self-signed Certificate**.</span></span>

    ![Capture d’écran de hello Robomongo SSL onglet](./media/mongodb-robomongo/SSL.png)
7. <span data-ttu-id="d6404-124">Enfin, cliquez sur **Test** tooverify que vous êtes en mesure de tooconnect, puis **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d6404-124">Finally, click **Test** tooverify that you are able tooconnect, then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6404-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d6404-125">Next steps</span></span>
* <span data-ttu-id="d6404-126">Explorez les [exemples](mongodb-samples.md) d’Azure Cosmos DB : API pour MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d6404-126">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
