---
title: "aaaEnable connexion Bureau à distance pour un rôle dans les Services de cloud computing Azure | Documents Microsoft"
description: "Tooconfigure votre azure cloud service connexions Bureau à distance tooallow d’application"
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: 73ea1d64-1529-4d72-b58e-f6c10499e6bb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: mmccrory
ms.openlocfilehash: 55d7043df571c2e88b04aa9ef01dc8ae1d6784f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a>Activer une connexion Bureau à distance pour un rôle dans Azure Cloud Services
> [!div class="op_single_selector"]
> * [Portail Azure](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Portail Azure Classic](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

Bureau à distance vous permet de bureau de hello tooaccess d’un rôle en cours d’exécution dans Azure. Vous pouvez utiliser un tootroubleshoot de connexion Bureau à distance et diagnostiquer les problèmes avec votre application pendant son exécution.

Vous pouvez activer une connexion Bureau à distance dans votre rôle pendant le développement en incluant les modules de bureau à distance hello dans votre définition de service, ou vous pouvez choisir tooenable Bureau à distance via hello Extension Bureau à distance. Hello approche par défaut est toouse hello Bureau à distance extension que vous pouvez activer le Bureau à distance même après que l’application hello est déployée sans tooredeploy votre application.

## <a name="configure-remote-desktop-from-hello-azure-portal"></a>Configurer le Bureau à distance à partir de hello portail Azure
Hello portail Azure utilise approche d’Extension Bureau à distance hello même après que l’application hello est déployée, vous pouvez activer Bureau à distance. Hello **Bureau à distance** panneau pour votre service cloud vous permet de tooenable Bureau à distance, modifier le compte d’administrateur local hello utilisé tooconnect toohello virtuels, les certificats hello utilisés dans l’authentification et définir hello date d’expiration.

1. Cliquez sur **Services de cloud computing**, cliquez sur nom hello du service de cloud hello, puis cliquez sur **Bureau à distance**.

    ![Bureau à distance des Services Cloud](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. Choisissez si vous souhaitez tooenable Bureau à distance pour un rôle individuel ou pour tous les rôles, puis modifiez trop de valeur du sélecteur de hello hello**activé**.

3. Renseignez les champs hello requis pour le nom d’utilisateur, mot de passe, d’expiration et certificat.

    ![Bureau à distance des Services Cloud](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > toutes les instances de rôle sont redémarrées lorsque vous activez pour la première fois le Bureau à distance et cliquez sur OK (coche). tooprevent un redémarrage, le mot de passe hello hello certificat tooencrypt utilisé doit être installé sur le rôle de hello. tooprevent un redémarrage, [télécharger un certificat pour le service cloud hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) , puis revenez toothis la boîte de dialogue.
   >
   >
3. Dans **rôles**, sélectionnez rôle hello souhaité tooupdate **tous les** pour tous les rôles.

4. Lorsque les mises à jour de la configuration sont terminées, cliquez sur **Enregistrer**. Il prendra un certain temps avant que vos instances de rôle sont des connexions de tooreceive prêt.

## <a name="remote-into-role-instances"></a>À distance dans les instances de rôle
Une fois que Bureau à distance est activé sur les rôles de hello, vous pouvez établir une connexion directement à partir de hello portail Azure :

1. Cliquez sur **Instances** tooopen hello **Instances** panneau.
2. Sélectionnez une instance de rôle pour laquelle la fonctionnalité Bureau à distance est configurée.
3. Cliquez sur **Connect** toodownload un RDP de fichiers pour une instance de rôle hello.

    ![Bureau à distance des Services Cloud](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. Cliquez sur **ouvrir** , puis **Connect** toostart hello connexion Bureau à distance.

>[!NOTE]
> Si votre service cloud se trouve derrière un groupe de sécurité réseau, vous devrez peut-être toocreate les règles qui autorisent le trafic sur les ports **3389** et **20000**.  Bureau à distance utilise le port **3389**.  Les instances de Service cloud sont à charge équilibrée, donc vous ne pouvez pas contrôler directement le tooconnect d’instance pour.  Hello *RemoteForwarder* et *RemoteAccess* agents gérer le trafic RDP et hello client toosend un cookie RDP et de spécifier un tooconnect instance individuelle pour.  Hello *RemoteForwarder* et *RemoteAccess* agents nécessitent ce port **20000*** être ouvert, ce qui peut être bloqué si vous disposez d’un groupe de sécurité réseau.

## <a name="additional-resources"></a>Ressources supplémentaires

[Comment tooConfigure Services de cloud computing](cloud-services-how-to-configure.md)
[Cloud FAQ - des services Bureau à distance](cloud-services-faq.md)
