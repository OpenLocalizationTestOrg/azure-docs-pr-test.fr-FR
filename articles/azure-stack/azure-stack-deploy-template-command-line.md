---
title: "Déployer des modèles en ligne de commande dans Azure Stack | Microsoft Docs"
description: "Découvrez comment utiliser l’interface de ligne de commande (CLI) multiplateforme pour déployer des modèles sur Azure Stack."
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
ms.openlocfilehash: cd1b61899ead7b4e86a81125841c1b37d019280b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-templates-in-azure-stack-using-the-command-line"></a><span data-ttu-id="a2755-103">Déployer des modèles dans Azure Stack à l’aide de la ligne de commande</span><span class="sxs-lookup"><span data-stu-id="a2755-103">Deploy templates in Azure Stack using the command line</span></span>
<span data-ttu-id="a2755-104">Utilisez la ligne de commande pour déployer des modèles Azure Resource Manager dans le kit de développement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a2755-104">Use the command line to deploy Azure Resource Manager templates to the Azure Stack Development Kit.</span></span> <span data-ttu-id="a2755-105">Les modèles Azure Resource Manager déploient et approvisionnent toutes les ressources de l’application en une seule opération coordonnée.</span><span class="sxs-lookup"><span data-stu-id="a2755-105">Azure Resource Manager templates deploy and provision all the resources for your application in a single, coordinated operation.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a2755-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="a2755-106">Before you begin</span></span>
 - <span data-ttu-id="a2755-107">[Procédez à l’installation et à la connexion](azure-stack-connect-cli.md) à Azure Stack avec Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a2755-107">[Install and connect](azure-stack-connect-cli.md) to Azure Stack with Azure CLI</span></span>
 - <span data-ttu-id="a2755-108">Télécharger les fichiers *azuredeploy.json* et *azuredeploy.parameters.json* à partir du [modèle Créer un exemple de compte de stockage](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="a2755-108">Download the files *azuredeploy.json* and *azuredeploy.parameters.json* from the [create storage account example template](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-create-storage-account).</span></span>
 
## <a name="deploy-template"></a><span data-ttu-id="a2755-109">Déployer un modèle</span><span class="sxs-lookup"><span data-stu-id="a2755-109">Deploy template</span></span>
<span data-ttu-id="a2755-110">Accédez au dossier dans lequel ces fichiers ont été téléchargés et exécutez la commande suivante pour déployer le modèle :</span><span class="sxs-lookup"><span data-stu-id="a2755-110">Navigate to the folder where these files were downloaded and run the following command to deploy the template:</span></span>

    azure group create "cliRG" "local" –f azuredeploy.json –d "testDeploy" –e azuredeploy.parameters.json

<span data-ttu-id="a2755-111">Cette commande déploie le modèle dans le groupe de ressources **cliRG** à l’emplacement par défaut d’Azure Stack POC.</span><span class="sxs-lookup"><span data-stu-id="a2755-111">This command deploys the template to the resource group **cliRG** in the Azure Stack POC’s default location.</span></span>

## <a name="validate-template-deployment"></a><span data-ttu-id="a2755-112">Valider le déploiement du modèle</span><span class="sxs-lookup"><span data-stu-id="a2755-112">Validate template deployment</span></span>
<span data-ttu-id="a2755-113">Pour voir ce groupe de ressources et le compte de stockage associé, utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="a2755-113">To see this resource group and storage account, use the following commands:</span></span>

    azure group list

    azure storage account list

## <a name="next-steps"></a><span data-ttu-id="a2755-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a2755-114">Next steps</span></span>
[<span data-ttu-id="a2755-115">Gérer les autorisations utilisateur</span><span class="sxs-lookup"><span data-stu-id="a2755-115">Manage user permissions</span></span>](azure-stack-manage-permissions.md)

