---
title: aaaSet des PowerShell toocreate une machine virtuelle pour hello Marketplace | Documents Microsoft
description: "Instructions pour configurer Azure PowerShell et l’utiliser comme un processus facultatif toodeploy d’images de machine virtuelle toocreate, de flux et vendent sur, hello Azure Marketplace"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e19d6cda-76df-4e42-be84-c9fe47a636db
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/04/2016
ms.author: hascipio
ms.openlocfilehash: cd2ebad7472248b8f921706e1a8c82d41f33b9cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-powershell-toocreate-an-offer-for-hello-azure-marketplace"></a>Configurer Azure PowerShell toocreate offre hello Azure Marketplace
Pour plus d’informations sur la façon de tooset de PowerShell dans Azure, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview). Une approche simple est la méthode certificat toouse hello, qui télécharge et importe un certificat nécessaire pour l’authentification. tooobtain hello nécessaire de certificat, utilisez hello **Get-AzurePublishSettingsFile** applet de commande. Enregistrer le fichier de hello lorsque vous êtes invité. certificat de hello tooimport dans une session PowerShell, utilisez hello **Import-AzurePublishSettingsFile** applet de commande.

tooconfigure et magasin hello commune Microsoft Azure paramètres d’abonnement pour la session de PowerShell hello, utiliser hello **Set-AzureSubscription** et **Select-AzureSubscription** applets de commande :

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

commande premier Hello associe un compte de stockage par défaut abonnement hello (nécessaire pour certaines opérations de configuration de machine virtuelle).  Hello effectue ensuite les abonnement hello hello celui en cours (reconnu par les autres applets de commande).

## <a name="see-also"></a>Voir aussi
* [Mise en route : comment toopublish une toohello offre Azure Marketplace](marketplace-publishing-getting-started.md)
* [Création d’une image de machine virtuelle pour hello Marketplace](marketplace-publishing-vm-image-creation.md)

