---
title: "modèles d’aaaDeploy avec ligne de commande hello dans la pile de Azure | Documents Microsoft"
description: "Découvrez comment toouse hello inter-plateformes interface de ligne de commande (CLI) toodeploy modèles tooAzure pile."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 9584177f-4af3-4834-864d-930b09ae0995
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 6fa6b19ac94d3f020008d04ff07f1ce489aa3418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-templates-in-azure-stack-using-hello-command-line"></a><span data-ttu-id="e583c-103">Déployer des modèles dans la pile d’Azure à l’aide de la ligne de commande hello</span><span class="sxs-lookup"><span data-stu-id="e583c-103">Deploy templates in Azure Stack using hello command line</span></span>
<span data-ttu-id="e583c-104">Utilisez Azure Resource Manager modèles toohello Kit de développement de pile Azure hello ligne de commande toodeploy.</span><span class="sxs-lookup"><span data-stu-id="e583c-104">Use hello command line toodeploy Azure Resource Manager templates toohello Azure Stack Development Kit.</span></span> <span data-ttu-id="e583c-105">Les modèles de gestionnaire de ressources Azure déploiement et approvisionnement des toutes les ressources hello pour votre application dans une opération unique et coordonnée.</span><span class="sxs-lookup"><span data-stu-id="e583c-105">Azure Resource Manager templates deploy and provision all hello resources for your application in a single, coordinated operation.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e583c-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="e583c-106">Before you begin</span></span>
 - <span data-ttu-id="e583c-107">[Installer et connecter](azure-stack-connect-cli.md) tooAzure pile avec CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="e583c-107">[Install and connect](azure-stack-connect-cli.md) tooAzure Stack with Azure CLI</span></span>
 - <span data-ttu-id="e583c-108">Télécharger les fichiers de hello *azuredeploy.json* et *azuredeploy.parameters.json* de hello [créer l’exemple de modèle compte de stockage](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="e583c-108">Download hello files *azuredeploy.json* and *azuredeploy.parameters.json* from hello [create storage account example template](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-create-storage-account).</span></span>
 
## <a name="deploy-template"></a><span data-ttu-id="e583c-109">Déployer un modèle</span><span class="sxs-lookup"><span data-stu-id="e583c-109">Deploy template</span></span>
<span data-ttu-id="e583c-110">Accédez dossier toohello où ces fichiers ont été téléchargés et exécutez hello suivant le modèle de commande toodeploy hello :</span><span class="sxs-lookup"><span data-stu-id="e583c-110">Navigate toohello folder where these files were downloaded and run hello following command toodeploy hello template:</span></span>

    azure group create "cliRG" "local" –f azuredeploy.json –d "testDeploy" –e azuredeploy.parameters.json

<span data-ttu-id="e583c-111">Cette commande déploie le groupe de ressources hello modèle toohello **cliRG** dans l’emplacement par défaut de hello Azure pile preuve de concept.</span><span class="sxs-lookup"><span data-stu-id="e583c-111">This command deploys hello template toohello resource group **cliRG** in hello Azure Stack POC’s default location.</span></span>

## <a name="validate-template-deployment"></a><span data-ttu-id="e583c-112">Valider le déploiement du modèle</span><span class="sxs-lookup"><span data-stu-id="e583c-112">Validate template deployment</span></span>
<span data-ttu-id="e583c-113">commandes de ce compte de stockage et le groupe de ressources, hello utilisation suivant toosee :</span><span class="sxs-lookup"><span data-stu-id="e583c-113">toosee this resource group and storage account, use hello following commands:</span></span>

    azure group list

    azure storage account list

## <a name="next-steps"></a><span data-ttu-id="e583c-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e583c-114">Next steps</span></span>
[<span data-ttu-id="e583c-115">Gérer les autorisations utilisateur</span><span class="sxs-lookup"><span data-stu-id="e583c-115">Manage user permissions</span></span>](azure-stack-manage-permissions.md)

