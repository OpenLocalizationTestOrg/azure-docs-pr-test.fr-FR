---
title: "Certificats aaaSSL liaison à l’aide de PowerShell"
description: "Découvrez comment toobind SSL certificats tooyour l’application web à l’aide de PowerShell."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 8ce32508-e982-48d3-b878-0e526afda537
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: 82f0e7c796da99ab50f69f3638ef64d55a94fc8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a><span data-ttu-id="8a22e-103">Liaison de certificat SSL d’Azure App Service à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a22e-103">Azure App Service SSL Certificate Binding using PowerShell</span></span>
<span data-ttu-id="8a22e-104">Version de hello de Microsoft Azure PowerShell version 1.1.0 une nouvelle applet de commande a été ajoutée qui permettrait de fournir à hello utilisateur hello capacité toobind existante ou nouvelle SSL certificats tooan une application Web existante.</span><span class="sxs-lookup"><span data-stu-id="8a22e-104">With hello release of Microsoft Azure PowerShell version 1.1.0 a new cmdlet has been added that would give hello user hello ability toobind existing or new SSL certificates tooan existing Web App.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="8a22e-105">toolearn sur l’utilisation du Gestionnaire de ressources Azure en fonction toomanage des applets de commande Azure PowerShell vérification de vos applications Web [Azure Resource Manager en fonction des commandes PowerShell pour l’application Web Azure](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="8a22e-105">toolearn about using Azure Resource Manager based Azure PowerShell cmdlets toomanage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="uploading-and-binding-a-new-ssl-certificate"></a><span data-ttu-id="8a22e-106">Chargement et liaison d’un nouveau certificat SSL</span><span class="sxs-lookup"><span data-stu-id="8a22e-106">Uploading and Binding a new SSL certificate</span></span>
<span data-ttu-id="8a22e-107">Scénario : hello aimerait toobind un tooone de certificat SSL de ses applications web.</span><span class="sxs-lookup"><span data-stu-id="8a22e-107">Scenario: hello user would like toobind an SSL certificate tooone of his web apps.</span></span>

<span data-ttu-id="8a22e-108">Connaître le nom de groupe de ressources hello qui contient l’application web hello, nom de l’application web hello, chemin d’accès de fichier de hello certificat .pfx sur l’ordinateur d’utilisateur hello, hello de mot de passe pour le certificat de hello et hello nom d’hôte personnalisé, vous pouvez utiliser hello suivant toocreate de commande PowerShell qui Liaison SSL :</span><span class="sxs-lookup"><span data-stu-id="8a22e-108">Knowing hello resource group name that contains hello web app, hello web app name, hello certificate .pfx file path on hello user machine, hello password for hello certificate, and hello custom hostname, we can use hello following PowerShell command toocreate that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

<span data-ttu-id="8a22e-109">Notez qu’avant d’ajouter une liaison SSL tooa l’application web, vous devez disposer d’un nom d’hôte (domaine personnalisé) déjà configuré.</span><span class="sxs-lookup"><span data-stu-id="8a22e-109">Note that before adding a SSL binding tooa web app, you must have a host name (custom domain) already configured.</span></span> <span data-ttu-id="8a22e-110">Si le nom d’hôte hello n’est pas configuré, puis vous obtiendrez une erreur « hostname » n’existe pas lors de l’exécution de New-AzureRmWebAppSSLBinding.</span><span class="sxs-lookup"><span data-stu-id="8a22e-110">If hello host name is not configured , then you will get an error 'hostname' does not exist while running  New-AzureRmWebAppSSLBinding.</span></span> <span data-ttu-id="8a22e-111">Vous pouvez ajouter un nom d’hôte directement à partir de portail de hello ou Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a22e-111">You can add a hostname directly from hello portal or using Azure PowerShell.</span></span> <span data-ttu-id="8a22e-112">Hello extrait de code PowerShell suivant peut être le nom d’hôte de tooconfigure hello avant d’exécuter New-AzureRmWebAppSSLBinding.</span><span class="sxs-lookup"><span data-stu-id="8a22e-112">hello following PowerShell snippet can be tooconfigure hello hostname before running New-AzureRmWebAppSSLBinding.</span></span>   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

<span data-ttu-id="8a22e-113">Il est important de toounderstand qui hello applet de commande Set-AzureRmWebApp remplace les noms d’hôtes hello pour l’application web de hello.</span><span class="sxs-lookup"><span data-stu-id="8a22e-113">It is important toounderstand that hello Set-AzureRmWebApp cmdlet overwrites hello hostnames for hello web app.</span></span> <span data-ttu-id="8a22e-114">Par conséquent, hello ci-dessus extrait de code PowerShell est l’ajout de liste existante de toohello hello des noms d’hôte pour l’application web de hello.</span><span class="sxs-lookup"><span data-stu-id="8a22e-114">Hence hello above PowerShell snippet is appending toohello existing list of hello host names for hello web app.</span></span>  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a><span data-ttu-id="8a22e-115">Chargement et liaison d’un certificat SSL existant</span><span class="sxs-lookup"><span data-stu-id="8a22e-115">Uploading and Binding an existing SSL certificate</span></span>
<span data-ttu-id="8a22e-116">Scénario : hello aimerait toobind un tooone de certificat SSL précédemment téléchargé de ses applications web.</span><span class="sxs-lookup"><span data-stu-id="8a22e-116">Scenario: hello user would like toobind a previously uploaded SSL certificate tooone of his web apps.</span></span>

<span data-ttu-id="8a22e-117">Nous pouvons obtenir hello liste de certificats déjà groupe de ressources spécifique tooa téléchargé en utilisant hello commande suivante</span><span class="sxs-lookup"><span data-stu-id="8a22e-117">We can get hello list of certificates already uploaded tooa specific resource group by using hello following command</span></span>

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

<span data-ttu-id="8a22e-118">Notez que les certificats de hello sont tooa local groupe d’emplacement et de ressources spécifique, hello utilisateur besoin toore-télécharger le certificat hello si l’application web hello configuré est dans un autre emplacement et groupe de ressources autres que de hello nécessaire de certificat</span><span class="sxs-lookup"><span data-stu-id="8a22e-118">Note that hello certificates are local tooa specific location and resource group, hello user need toore-upload hello certificate if hello configured web app is in a different location and resource group other that that of hello needed certificate</span></span> 

<span data-ttu-id="8a22e-119">Connaître le nom de groupe de ressources hello qui contient l’application web de hello, hello du nom de l’application web, hello empreinte numérique du certificat et hello nom d’hôte personnalisé, nous pouvons utiliser hello suivant toocreate de commande PowerShell que la liaison SSL :</span><span class="sxs-lookup"><span data-stu-id="8a22e-119">Knowing hello resource group name that contains hello web app, hello web app name, hello certificate thumbprint, and hello custom hostname, we can use hello following PowerShell command toocreate that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a><span data-ttu-id="8a22e-120">Suppression d’une liaison SSL existante</span><span class="sxs-lookup"><span data-stu-id="8a22e-120">Deleting an existing SSL binding</span></span>
<span data-ttu-id="8a22e-121">Scénario : hello aimerait toodelete une liaison SSL existante.</span><span class="sxs-lookup"><span data-stu-id="8a22e-121">Scenario: hello user would like toodelete an existing SSL binding.</span></span>

<span data-ttu-id="8a22e-122">Connaître le nom de groupe de ressources hello qui contient l’application web de hello, hello du nom de l’application web et hello nom d’hôte personnalisé, nous pouvons utiliser hello suivant tooremove de commande PowerShell que la liaison SSL :</span><span class="sxs-lookup"><span data-stu-id="8a22e-122">Knowing hello resource group name that contains hello web app, hello web app name, and hello custom hostname, we can use hello following PowerShell command tooremove that SSL binding:</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

<span data-ttu-id="8a22e-123">Notez que si hello supprimé la liaison SSL a été hello dernière liaison à l’aide de ce certificat à cet emplacement, par un certificat de hello par défaut est supprimée, si le certificat de hello tookeep souhaitez que l’utilisateur de hello, il peut utiliser le certificat hello tookeep hello DeleteCertificate option</span><span class="sxs-lookup"><span data-stu-id="8a22e-123">Note that if hello removed SSL binding was hello last binding using that certificate in that location, by default hello certificate will be deleted, if hello user want tookeep hello certificate he can use hello DeleteCertificate option tookeep hello certificate</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a><span data-ttu-id="8a22e-124">Références</span><span class="sxs-lookup"><span data-stu-id="8a22e-124">References</span></span>
* [<span data-ttu-id="8a22e-125">Commandes PowerShell basées sur Azure Resource Manager pour Application web Azure</span><span class="sxs-lookup"><span data-stu-id="8a22e-125">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="8a22e-126">Introduction tooApp environnement de Service</span><span class="sxs-lookup"><span data-stu-id="8a22e-126">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="8a22e-127">Utilisation d'Azure PowerShell avec Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8a22e-127">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

