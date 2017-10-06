---
title: "Azure Active Directory Domain Services : créer ou sélectionner un réseau virtuel | Microsoft Docs"
description: "Activer Azure Active Directory Domain Services à l’aide de hello portail Azure classic"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 13ab1608-e3d8-40de-9f7b-9b5b42199af4
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 212c741b20e846742d94f70342c4263ce8984153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a>Créer ou sélectionner un réseau virtuel pour Azure Active Directory Domain Services
## <a name="before-you-begin"></a>Avant de commencer
Consultez trop[considérations relatives à la mise en réseau pour les Services de domaine Active Directory Azure](active-directory-ds-networking.md).

## <a name="task-2-create-an-azure-virtual-network"></a>Tâche 2 : créer un réseau virtuel Azure
tâche de configuration suivante Hello est toocreate un réseau virtuel Azure et un sous-réseau qu’il contient. Vous activez Azure Active Directory Domain Services dans ce sous-réseau de votre réseau virtuel. Si vous avez un réseau virtuel existant que vous préférez toouse, vous pouvez ignorer cette étape.

> [!NOTE]
> Assurez-vous que ce réseau virtuel Azure que vous créez ou choisissez toouse avec Azure Active Directory Domain Services appartient tooan région Azure qui est pris en charge par les Services de domaine Active Directory Azure hello. tooascertain hello régions Azure dans lequel les Services de domaine Active Directory de Azure est disponible, consultez [des services Azure par région](https://azure.microsoft.com/regions/#services/).
>
>Notez le nom hello de hello tooensure de réseau virtuel que vous sélectionnez réseau virtuel à droite de hello lorsque vous activez Azure Active Directory Domain Services dans une étape de configuration suivantes.


toocreate un réseau virtuel Azure dans lequel vous souhaitez tooenable Azure Active Directory Domain Services, suivez les instructions de configuration :

1. Accédez toohello [portail Azure classic](https://manage.windowsazure.com).
2. Dans le volet gauche de hello, sélectionnez **réseaux**.

    ![Nœud Réseaux](./media/active-directory-domain-services-getting-started/networks-node.png)  
    Hello **réseaux virtuels** fenêtre s’ouvre.
3. Dans le volet des tâches hello bas hello de fenêtre hello, cliquez sur **nouveau**.

    ![Fenêtre Réseaux virtuels](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. Cliquez sur **Services réseau**, puis sélectionnez **Réseau virtuel**.

    ![Réseau virtuel : création rapide](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. toocreate un réseau virtuel, cliquez sur **création rapide**.

6. Spécifiez un **nom** pour votre machine virtuelle, réseau et de prendre en compte la manière hello suivante :
    * Vous pouvez choisir tooconfigure **l’espace d’adressage** ou **nombre d’ordinateurs virtuels Maximum** pour ce réseau.
    * Vous pouvez laisser hello **serveur DNS** définition en tant que **aucun** pour l’instant. Vous pouvez mettre à jour le paramètre de hello après avoir activé Azure des Services de domaine Active Directory.
7. Bonjour **emplacement** liste déroulante, sélectionnez une région Azure prise en charge.  
    tooascertain hello régions Azure dans lequel les Services de domaine Active Directory de Azure est disponible, consultez [des services Azure par région](https://azure.microsoft.com/regions/#services/).
8. toocreate votre réseau virtuel, cliquez sur **créer un réseau virtuel**.

    ![Créer un réseau virtuel pour Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. Une fois que vous avez créé un réseau virtuel, sélectionnez le nom hello du réseau virtuel de hello, puis cliquez sur hello **configurer** onglet.

    ![Créer un sous-réseau](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. Sous **espaces d’adressage de réseau virtuel**, cliquez sur **ajouter un sous-réseau**, puis spécifiez un sous-réseau nommé hello **AaddsSubnet**.

    ![Créer un sous-réseau pour Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. toocreate hello sous-réseau, cliquez sur **enregistrer**.


## <a name="next-step"></a>Étape suivante
[Tâche 3 : Activer Azure Active Directory Domain Services](active-directory-ds-getting-started-enableaadds.md)
