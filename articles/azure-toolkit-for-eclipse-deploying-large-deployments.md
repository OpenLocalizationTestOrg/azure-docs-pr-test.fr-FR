---
title: "aaaDeploying déploiements à grande échelle"
description: "Découvrez comment toodeploy déploiements à grande échelle à l’aide de hello boîte à outils Azure pour Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6b1d2a7a5e49c78154fc856a221e64ca8dcfbe9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-large-deployments"></a><span data-ttu-id="cf79f-103">Réalisation de déploiements volumineux</span><span class="sxs-lookup"><span data-stu-id="cf79f-103">Deploying Large Deployments</span></span>
<span data-ttu-id="cf79f-104">Si votre déploiement est trop grande toobe contenu dans le dossier approot de hello par défaut, vous pouvez utiliser une ressource de stockage local en tant que dossier racine de déploiement hello pour votre JDK et serveur d’applications.</span><span class="sxs-lookup"><span data-stu-id="cf79f-104">If your deployment is too large toobe contained in hello default approot folder, you can use a local storage resource as hello deployment root folder for your JDK and application server.</span></span>

## <a name="toouse-a-local-storage-resource-as-hello-deployment-root-folder-for-large-deployments"></a><span data-ttu-id="cf79f-105">toouse une ressource de stockage local en tant que dossier racine de déploiement hello pour les déploiements à grandes échelle</span><span class="sxs-lookup"><span data-stu-id="cf79f-105">toouse a local storage resource as hello deployment root folder for large deployments</span></span>
1. <span data-ttu-id="cf79f-106">Créez une ressource de stockage local.</span><span class="sxs-lookup"><span data-stu-id="cf79f-106">Create a new local storage resource.</span></span> <span data-ttu-id="cf79f-107">nom Hello de ressource de hello n’a pas d’importance.</span><span class="sxs-lookup"><span data-stu-id="cf79f-107">hello name of hello resource does not matter.</span></span> <span data-ttu-id="cf79f-108">Ressources de stockage sont définies au niveau du rôle hello.</span><span class="sxs-lookup"><span data-stu-id="cf79f-108">Storage resources are defined at hello role level.</span></span> <span data-ttu-id="cf79f-109">Hello plus rapide moyen tooaccess hello stockage local configuration boîte de dialogue, à partir de laquelle vous pouvez créer une ressource de stockage local, est à l’aide de hello comme suit : rôle de hello avec le bouton droit dans hello **Explorateur de projets** vue (développez votre Nœud de projet Azure si vous ne voyez pas le rôle de hello), cliquez sur **Azure**, puis cliquez sur **stockage Local**.</span><span class="sxs-lookup"><span data-stu-id="cf79f-109">hello quickest way tooaccess hello local storage configuration dialog, from which you could create a new local storage resource, is by using hello following steps: Right-click hello role in hello **Project Explorer** view (expand your Azure project node if you don't see hello role), click **Azure**, and then click **Local Storage**.</span></span> <span data-ttu-id="cf79f-110">Au sein de hello **stockage Local** boîte de dialogue, cliquez sur **ajouter** toocreate une ressource de stockage local.</span><span class="sxs-lookup"><span data-stu-id="cf79f-110">Within hello **Local Storage** dialog, click **Add** toocreate a new local storage resource.</span></span>

2. <span data-ttu-id="cf79f-111">Ensemble hello souhaité taille tooat au moins 2 048 Mo (quoi que ce soit inférieure peut entraîner hello mêmes problèmes de taille de fichier que vous pouvez rencontrer dans approot de hello).</span><span class="sxs-lookup"><span data-stu-id="cf79f-111">Set hello desired size tooat least 2048 MB (anything less may cause hello same file size problems as you would encounter in hello approot).</span></span>

3. <span data-ttu-id="cf79f-112">Vérifiez que **nettoyer le contenu de hello lorsque l’instance de rôle hello est recyclé** est vérifiée ; cela empêchera la logique de démarrage du déploiement hello d’entrer en conflit avec les fichiers existants dans la ressource de hello lorsque hello rôle instance est recyclée.</span><span class="sxs-lookup"><span data-stu-id="cf79f-112">Ensure that **Clean hello contents when hello role instance is recycled** is checked; this will help prevent hello deployment's startup logic from running into conflicts with pre-existing files in hello resource when hello role instance is recycled.</span></span>

4. <span data-ttu-id="cf79f-113">Vérifiez que hello **stockage variable environnement hello le chemin d’accès du répertoire de la ressource après le déploiement** a la valeur chaîne de toohello **DEPLOYROOT**.</span><span class="sxs-lookup"><span data-stu-id="cf79f-113">Ensure that hello **Environment variable storing hello resource's directory path after deployment** value is set toohello string **DEPLOYROOT**.</span></span> <span data-ttu-id="cf79f-114">Votre boîte de dialogue de ressource de stockage local recherche similaire toohello suivant.</span><span class="sxs-lookup"><span data-stu-id="cf79f-114">Your local storage resource dialog will look similar toohello following.</span></span>

   ![][ic667943]

<span data-ttu-id="cf79f-115">Vous pouvez également, si vous utilisez **DEPLOYROOT** comme hello *nom* de votre ressource locale et que vous ne modifiez pas le nom de variable de généré automatiquement l’environnement hello (qui sera défini trop **DEPLOYROOT_PATH** dans ce cas), qui doit s’exécuter pour votre application.</span><span class="sxs-lookup"><span data-stu-id="cf79f-115">Alternatively, if you use **DEPLOYROOT** as hello *name* of your local resource and you do not change hello automatically-generated environment variable name (which will be set too**DEPLOYROOT_PATH** in that case), that would work for your application as well.</span></span>

<span data-ttu-id="cf79f-116">Vous trouverez des informations supplémentaires sur la création d’une ressource de stockage local dans [Propriétés de stockage local][Local storage properties].</span><span class="sxs-lookup"><span data-stu-id="cf79f-116">Additional information about creating a local storage resource can be found at [Local storage properties][Local storage properties].</span></span>

## <a name="see-also"></a><span data-ttu-id="cf79f-117">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="cf79f-117">See Also</span></span>
<span data-ttu-id="cf79f-118">[Kit de ressources Azure pour Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="cf79f-118">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="cf79f-119">[Création d’une application Hello World pour Azure dans Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="cf79f-119">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="cf79f-120">[Lors de l’installation hello boîte à outils Azure pour Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="cf79f-120">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="cf79f-121">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="cf79f-121">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
