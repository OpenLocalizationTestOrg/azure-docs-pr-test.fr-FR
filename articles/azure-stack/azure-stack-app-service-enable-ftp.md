---
title: "aaaEnable FTP dans le Service d’applications sur la pile de Azure | Documents Microsoft"
description: "Étapes toocomplete tooenable FTP dans le Service d’applications sur la pile de Azure"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/6/2017
ms.author: anwestg
ms.openlocfilehash: 9c02da6362085fdd9f8d285da04efe85cf352398
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-ftp-in-app-service-on-azure-stack"></a>Activer FTP dans App Service sur Azure Stack

Une fois que vous avez correctement déployé sur Azure pile du Service d’applications si vous souhaitez que la publication tooenable FTP, afin que vos clients peuvent télécharger leurs fichiers d’application et le contenu, il existe quelques étapes supplémentaires qui doivent toobe s’est terminée.  Ces étapes seront automatisées dans les prochaines versions.

> [!NOTE]
> Ces étapes sont destinées aux administrateurs Service ou Entreprise qui souhaitent configurer un fournisseur de ressources App Service ou Azure Stack.

## <a name="enable-ftp"></a>Activer FTP

1.  Ouvrez une session en tant qu’administrateur de service hello dans le portail d’Azure pile toohello.
2.  Parcourir trop**interfaces réseau** et sélectionnez hello **FTP-NIC** sous **groupe de ressources** - **AppService LOCAL**. ![Interfaces réseau Azure Stack][1]
3.  Hello de note **adresse IP publique** Hello **FTP-NIC**. 
![Détails de l’interface réseau Azure Stack][2]
4.  Ensuite parcourir trop**virtuels** et sélectionnez hello **FTP0-VM**. ![Machines virtuelles Azure Stack][3]
5.  Ouvrez une session Bureau à distance de toohello machine virtuelle à l’aide de hello **Connect** bouton et connexion session toohello à l’aide des informations d’identification de l’administrateur hello vous définissez au cours du déploiement du Service d’applications.  
![Détails des machines virtuelles Azure Stack][4]
6.  Ouvrez **Internet Information Services (IIS) Manager** sur hello FTP machine virtuelle (VM-FTP0).
7.  Sous **Sites**, sélectionnez **Hosting FTP Site** (Site d’hébergement FTP).
8.  Ouvrez **Prise en charge du pare-feu FTP**. ![Gestionnaire des services IIS sur App Service FTP0-VM][5]
9.  Entrez hello adresse IP publique de hello FTP-NIC et cliquez sur **appliquer** ![prise en charge du pare-feu FTP IIS Manager][6]

## <a name="validate-hello-enabling-of-ftp"></a>Valider l’activation de hello du serveur FTP

1.  Ouvrez une session dans toohello portail de la pile d’Azure sous la forme d’un administrateur de service hello ou un client.
2.  Parcourir trop**des Services d’application** et sélectionnez un Web, mobiles ou application API que vous avez créé. ![Services d’application][7]
3.  Dans l’application hello détails Notez hello **nom d’hôte FTP** et **nom d’utilisateur FTP/déploiement**. ![Détails de l’application App Service][8]
> [!NOTE]
> Si vous ne voyez pas une entrée sous **nom d’utilisateur FTP/déploiement**, vous avez besoin d’informations d’identification du déploiement tooset hello à l’aide de première hello **informations d’identification de déploiement** panneau.

4.  Ouvrez l’Explorateur Windows, entrez des nom d’hôte hello FTP dans la barre ftp://ftp.appservice.azurestack.local, par exemple, d’adresses fichier hello
5.  Lorsque vous y êtes invité entrez hello **informations d’identification de déploiement** vous avez noté à l’étape 3, si la fonctionnalité de hello a été activée vous verrez une liste de répertoires de contenu de l’application de service application hello. ![Liste de fichiers FTP][9]
<!--Image references-->
[1]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-network-interfaces.png
[2]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-network-interface-details.png
[3]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-virtual-machines.png
[4]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-virtual-machines-FTP0-VM.png
[5]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-IIS-Manager.png
[6]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-IIS-Manager-FTP-Firewall-Support.png
[7]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-app-services.png
[8]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-app-service-app-detail.png
[9]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-ftp-file-listing.png
