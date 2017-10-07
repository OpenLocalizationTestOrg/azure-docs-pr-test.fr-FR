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
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a>Liaison de certificat SSL d’Azure App Service à l’aide de PowerShell
Version de hello de Microsoft Azure PowerShell version 1.1.0 une nouvelle applet de commande a été ajoutée qui permettrait de fournir à hello utilisateur hello capacité toobind existante ou nouvelle SSL certificats tooan une application Web existante.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

toolearn sur l’utilisation du Gestionnaire de ressources Azure en fonction toomanage des applets de commande Azure PowerShell vérification de vos applications Web [Azure Resource Manager en fonction des commandes PowerShell pour l’application Web Azure](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="uploading-and-binding-a-new-ssl-certificate"></a>Chargement et liaison d’un nouveau certificat SSL
Scénario : hello aimerait toobind un tooone de certificat SSL de ses applications web.

Connaître le nom de groupe de ressources hello qui contient l’application web hello, nom de l’application web hello, chemin d’accès de fichier de hello certificat .pfx sur l’ordinateur d’utilisateur hello, hello de mot de passe pour le certificat de hello et hello nom d’hôte personnalisé, vous pouvez utiliser hello suivant toocreate de commande PowerShell qui Liaison SSL :

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

Notez qu’avant d’ajouter une liaison SSL tooa l’application web, vous devez disposer d’un nom d’hôte (domaine personnalisé) déjà configuré. Si le nom d’hôte hello n’est pas configuré, puis vous obtiendrez une erreur « hostname » n’existe pas lors de l’exécution de New-AzureRmWebAppSSLBinding. Vous pouvez ajouter un nom d’hôte directement à partir de portail de hello ou Azure PowerShell. Hello extrait de code PowerShell suivant peut être le nom d’hôte de tooconfigure hello avant d’exécuter New-AzureRmWebAppSSLBinding.   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

Il est important de toounderstand qui hello applet de commande Set-AzureRmWebApp remplace les noms d’hôtes hello pour l’application web de hello. Par conséquent, hello ci-dessus extrait de code PowerShell est l’ajout de liste existante de toohello hello des noms d’hôte pour l’application web de hello.  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a>Chargement et liaison d’un certificat SSL existant
Scénario : hello aimerait toobind un tooone de certificat SSL précédemment téléchargé de ses applications web.

Nous pouvons obtenir hello liste de certificats déjà groupe de ressources spécifique tooa téléchargé en utilisant hello commande suivante

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

Notez que les certificats de hello sont tooa local groupe d’emplacement et de ressources spécifique, hello utilisateur besoin toore-télécharger le certificat hello si l’application web hello configuré est dans un autre emplacement et groupe de ressources autres que de hello nécessaire de certificat 

Connaître le nom de groupe de ressources hello qui contient l’application web de hello, hello du nom de l’application web, hello empreinte numérique du certificat et hello nom d’hôte personnalisé, nous pouvons utiliser hello suivant toocreate de commande PowerShell que la liaison SSL :

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a>Suppression d’une liaison SSL existante
Scénario : hello aimerait toodelete une liaison SSL existante.

Connaître le nom de groupe de ressources hello qui contient l’application web de hello, hello du nom de l’application web et hello nom d’hôte personnalisé, nous pouvons utiliser hello suivant tooremove de commande PowerShell que la liaison SSL :

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

Notez que si hello supprimé la liaison SSL a été hello dernière liaison à l’aide de ce certificat à cet emplacement, par un certificat de hello par défaut est supprimée, si le certificat de hello tookeep souhaitez que l’utilisateur de hello, il peut utiliser le certificat hello tookeep hello DeleteCertificate option

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a>Références
* [Commandes PowerShell basées sur Azure Resource Manager pour Application web Azure](app-service-web-app-azure-resource-manager-powershell.md)
* [Introduction tooApp environnement de Service](app-service-app-service-environment-intro.md)
* [Utilisation d'Azure PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md)

