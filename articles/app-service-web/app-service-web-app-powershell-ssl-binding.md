---
title: "Liaison de certificats SSL à l’aide de PowerShell"
description: "Découvrez comment lier des certificats SSL à votre application web à l’aide de PowerShell."
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
ms.openlocfilehash: a1fcc618fb0c68778e39cc227368a60b008f9401
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a><span data-ttu-id="ce0fd-103">Liaison de certificat SSL d’Azure App Service à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="ce0fd-103">Azure App Service SSL Certificate Binding using PowerShell</span></span>
<span data-ttu-id="ce0fd-104">Avec la publication de Microsoft Azure PowerShell version 1.1.0, une nouvelle applet de commande a été ajoutée. Elle permet à l’utilisateur de lier des certificats SSL nouveaux ou existants à une application web existante.</span><span class="sxs-lookup"><span data-stu-id="ce0fd-104">With the release of Microsoft Azure PowerShell version 1.1.0 a new cmdlet has been added that would give the user the ability to bind existing or new SSL certificates to an existing Web App.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="ce0fd-105">Pour savoir comment utiliser les applets de commande Azure PowerShell basées sur Azure Resource Manager pour gérer vos applications web, consultez [Commandes PowerShell basées sur Azure Resource Manager pour Application web Azure](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="ce0fd-105">To learn about using Azure Resource Manager based Azure PowerShell cmdlets to manage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="uploading-and-binding-a-new-ssl-certificate"></a><span data-ttu-id="ce0fd-106">Chargement et liaison d’un nouveau certificat SSL</span><span class="sxs-lookup"><span data-stu-id="ce0fd-106">Uploading and Binding a new SSL certificate</span></span>
<span data-ttu-id="ce0fd-107">Scénario : l’utilisateur souhaite lier un certificat SSL à l’une de ses applications web.</span><span class="sxs-lookup"><span data-stu-id="ce0fd-107">Scenario: The user would like to bind an SSL certificate to one of his web apps.</span></span>

<span data-ttu-id="ce0fd-108">Si nous connaissons le nom du groupe de ressources qui contient l’application web, le nom de l’application web, le chemin d’accès du fichier .pfx du certificat sur l’ordinateur de l’utilisateur, le mot de passe pour le certificat et le nom d’hôte personnalisé, nous pouvons utiliser la commande PowerShell suivante pour créer cette liaison SSL :</span><span class="sxs-lookup"><span data-stu-id="ce0fd-108">Knowing the resource group name that contains the web app, the web app name, the certificate .pfx file path on the user machine, the password for the certificate, and the custom hostname, we can use the following PowerShell command to create that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

<span data-ttu-id="ce0fd-109">Notez qu’avant d’ajouter une liaison SSL à une application web, vous devez déjà avoir configuré un nom d’hôte (domaine personnalisé).</span><span class="sxs-lookup"><span data-stu-id="ce0fd-109">Note that before adding a SSL binding to a web app, you must have a host name (custom domain) already configured.</span></span> <span data-ttu-id="ce0fd-110">Si le nom d’hôte n’est pas configuré, vous recevrez un message d’erreur indiquant que « hostname » n’existe pas lors de l’exécution de New-AzureRmWebAppSSLBinding.</span><span class="sxs-lookup"><span data-stu-id="ce0fd-110">If the host name is not configured , then you will get an error 'hostname' does not exist while running  New-AzureRmWebAppSSLBinding.</span></span> <span data-ttu-id="ce0fd-111">Vous pouvez ajouter un nom d’hôte directement depuis le portail ou à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ce0fd-111">You can add a hostname directly from the portal or using Azure PowerShell.</span></span> <span data-ttu-id="ce0fd-112">L’extrait de code PowerShell suivant peut vous permettre de configurer le nom d’hôte avant d’exécuter New-AzureRmWebAppSSLBinding.</span><span class="sxs-lookup"><span data-stu-id="ce0fd-112">The following PowerShell snippet can be to configure the hostname before running New-AzureRmWebAppSSLBinding.</span></span>   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

<span data-ttu-id="ce0fd-113">Il est important de comprendre que l’applet de commande Set-AzureRmWebApp remplace les noms d’hôte de l’application web.</span><span class="sxs-lookup"><span data-stu-id="ce0fd-113">It is important to understand that the Set-AzureRmWebApp cmdlet overwrites the hostnames for the web app.</span></span> <span data-ttu-id="ce0fd-114">Par conséquent, l’extrait de code PowerShell ci-dessus vient s’ajouter à la liste existante des noms d’hôte de l’application web.</span><span class="sxs-lookup"><span data-stu-id="ce0fd-114">Hence the above PowerShell snippet is appending to the existing list of the host names for the web app.</span></span>  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a><span data-ttu-id="ce0fd-115">Chargement et liaison d’un certificat SSL existant</span><span class="sxs-lookup"><span data-stu-id="ce0fd-115">Uploading and Binding an existing SSL certificate</span></span>
<span data-ttu-id="ce0fd-116">Scénario : l’utilisateur souhaite lier un certificat SSL préalablement chargé à l’une de ses applications web.</span><span class="sxs-lookup"><span data-stu-id="ce0fd-116">Scenario: The user would like to bind a previously uploaded SSL certificate to one of his web apps.</span></span>

<span data-ttu-id="ce0fd-117">Nous pouvons obtenir la liste des certificats déjà chargés vers un groupe de ressources spécifique en utilisant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ce0fd-117">We can get the list of certificates already uploaded to a specific resource group by using the following command</span></span>

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

<span data-ttu-id="ce0fd-118">Comme les certificats sont locaux dans un emplacement spécifique et un groupe de ressources, notez que l’utilisateur doit recharger le certificat si l’application web configurée se trouve à un emplacement différent et dans un groupe de ressources autre que celui du certificat nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ce0fd-118">Note that the certificates are local to a specific location and resource group, the user need to re-upload the certificate if the configured web app is in a different location and resource group other that that of the needed certificate</span></span> 

<span data-ttu-id="ce0fd-119">Si nous connaissons le nom du groupe de ressources qui contient l’application web, le nom de l’application web, l’empreinte de certificat et le nom d’hôte personnalisé, nous pouvons utiliser la commande PowerShell suivante pour créer cette liaison SSL :</span><span class="sxs-lookup"><span data-stu-id="ce0fd-119">Knowing the resource group name that contains the web app, the web app name, the certificate thumbprint, and the custom hostname, we can use the following PowerShell command to create that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a><span data-ttu-id="ce0fd-120">Suppression d’une liaison SSL existante</span><span class="sxs-lookup"><span data-stu-id="ce0fd-120">Deleting an existing SSL binding</span></span>
<span data-ttu-id="ce0fd-121">Scénario : l’utilisateur souhaite supprimer une liaison SSL existante.</span><span class="sxs-lookup"><span data-stu-id="ce0fd-121">Scenario: The user would like to delete an existing SSL binding.</span></span>

<span data-ttu-id="ce0fd-122">Si nous connaissons le nom du groupe de ressources qui contient l’application web, le nom de l’application web et le nom d’hôte personnalisé, nous pouvons utiliser la commande PowerShell suivante pour supprimer cette liaison SSL :</span><span class="sxs-lookup"><span data-stu-id="ce0fd-122">Knowing the resource group name that contains the web app, the web app name, and the custom hostname, we can use the following PowerShell command to remove that SSL binding:</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

<span data-ttu-id="ce0fd-123">Notez que si la liaison SSL supprimée était la dernière liaison utilisant ce certificat à cet emplacement, le certificat est supprimé par défaut. Si l’utilisateur souhaite le conserver, il peut utiliser l’option DeleteCertificate.</span><span class="sxs-lookup"><span data-stu-id="ce0fd-123">Note that if the removed SSL binding was the last binding using that certificate in that location, by default the certificate will be deleted, if the user want to keep the certificate he can use the DeleteCertificate option to keep the certificate</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a><span data-ttu-id="ce0fd-124">Références</span><span class="sxs-lookup"><span data-stu-id="ce0fd-124">References</span></span>
* [<span data-ttu-id="ce0fd-125">Commandes PowerShell basées sur Azure Resource Manager pour Application web Azure</span><span class="sxs-lookup"><span data-stu-id="ce0fd-125">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="ce0fd-126">Présentation de l'environnement App Service</span><span class="sxs-lookup"><span data-stu-id="ce0fd-126">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="ce0fd-127">Utilisation d’Azure PowerShell avec Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ce0fd-127">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

