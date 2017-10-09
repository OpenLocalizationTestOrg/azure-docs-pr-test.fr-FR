---
title: "aaaWhat est Azure RemoteApp ? | Microsoft Docs"
description: "Découvrez comment tooshare aux applications et ressources tooany appareil via Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: d7a8a311-e70a-4463-ac85-c7f62c500921
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e13909f3a5698f58c7e4348f3ce53f43560f9b1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-remoteapp"></a>Présentation d'Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Azure RemoteApp offre une fonctionnalité de hello du programme de RemoteApp de Microsoft locale hello, soutenu par les Services Bureau à distance, tooAzure. Azure RemoteApp vous permet de fournir des tooapplications un accès sécurisé à distance à partir de nombreux appareils utilisateur. Azure RemoteApp héberge essentiellement des sessions Terminal Server non persistant dans le cloud de hello et que vous obtenez toouse les et les partager avec vos utilisateurs.

Azure RemoteApp vous permet de partager des applications et des ressources avec des utilisateurs sur presque n’importe quel appareil. Nous héberger vos applications dans le cloud de hello, ce qui signifie que nous nous occupons du matériel de hello et les demandes des utilisateurs toomeet de mise à l’échelle. Tout ce que vous avez toodo est de télécharger des applications hello souhaité tooshare, puis obtenir votre toouse les utilisateurs de ces applications. [Les utilisateurs obtiennent tookeep leurs propres appareils](remoteapp-clients.md), tandis que vous gérez tous les éléments via hello portail Azure. Vous avez même option hello d’à l’aide de vos informations d’identification d’entreprise, ce qui vous permet de garantir la sécurité des données et applications hello.

Lisez la suite pour plus d'informations sur Azure RemoteApp, ou, si vous êtes déjà convaincu, [essayez-le maintenant](https://azure.microsoft.com/services/remoteapp/).

Vous avez des questions sur Azure RemoteApp ? Consultez notre [FAQ](remoteapp-faq.md).

Azure RemoteApp fait partie de hello [Microsoft Virtual Desktop Infrastructure](http://www.microsoft.com/server-cloud/products/virtual-desktop-infrastructure/explore.aspx).

**Nouveau !** Vous souhaitez toolearn plus d’informations sur Azure RemoteApp ? Ou prêt toovalidate Azure RemoteApp à grande échelle ? Joindre notre hebdomadaire [demander aux experts de hello webinaire](https://azureinfo.microsoft.com/AzureRemoteAppAskTheExperts-Registration-Page.html?ls=Website).

## <a name="azure-remoteapp-collections"></a>Collections Azure RemoteApp
Il existe deux types de [collections Azure RemoteApp](remoteapp-collections.md):

* A **cloud collection** est hébergé dans et stocke les données de programmes dans le cloud de hello. Les utilisateurs peuvent accéder aux applications en se connectant avec leur compte Microsoft ou leurs informations d'identification d'entreprise, synchronisées ou fédérées avec Azure Active Directory.
  
    Choisissez une collection cloud lorsque application hello souhaité tooshare ne nécessite pas une ressource de tooany de connexion réseau privé de votre société (par exemple, via un périphérique VPN). Si l’application hello utilise des ressources sur hello Internet, OneDrive ou Azure, une collection cloud fonctionne pour vous. Il est également toocreate plus rapide de hello.
* A **collection hybride** est hébergé dans et stocke les données dans hello cloud Azure, mais également permet aux utilisateurs accéder aux données et ressources stockées sur votre réseau local. Les utilisateurs peuvent accéder aux applications en se connectant avec leurs informations d'identification d'entreprise, synchronisées ou fédérées avec Azure Active Directory.
  
    Choisissez une collection hybride si vous avez besoin d’un tooresources de connexion sur le réseau privé de votre société. Par exemple, si hello application a besoin d’accéder à tooone suivants de hello :
  
  * Serveurs de fichiers situés sur votre intranet
  * Quicken
  * Bases de données derrière un pare-feu
    
    Cela est généralement plus utile pour les grandes entreprises avec un grand nombre de ressources sur leurs réseaux privés qui ne peut pas être déplacé toohello cloud.

options différentes, y compris les réseaux Hello différents regroupements, donc déterminer [quelle collection](remoteapp-collections.md) vous convient le mieux. 

### <a name="updating-your-collection"></a>Mise à jour de votre collection
Une des hello principales différences entre les collections hybride et cloud hello est la gestion des mises à jour logicielles. Avec une collection de cloud qui utilise hello image pré-installée Office 365 ProPlus ou Office 2013, il est inutile tooworry sur toutes les mises à jour. service de Hello gère elle-même et déploie les mises à jour sur une base continue, tooboth applications et système d’exploitation de hello.

Pour les collections hybride, ainsi que des collections de cloud qui utilisent une image de modèle personnalisé, vous êtes responsable de la gestion d’applications et image de hello. Pour les images jointes à un domaine, vous pouvez contrôler les mises à jour à l'aide de certains outils comme Windows Update, les stratégies de groupe ou encore System Center.

Une fois que vous mettez à jour votre image de modèle personnalisé, vous téléchargez hello nouvelle image toohello cloud Azure et ensuite mettre à jour de la nouvelle image hello collection toouse hello. (Cela à partir de hello Azure RemoteApp **Quick Start** page ou de bienvenue du tableau de bord.)

Consultez la section [Mise à jour de votre collection](remoteapp-update.md) pour plus d'informations.

## <a name="supported-remoteapp-clients"></a>Clients RemoteApp pris en charge
Azure RemoteApp est pris en charge sur les applications clientes hello RemoteApp pour Windows et Windows RT, ainsi que des applications de bureau à distance Microsoft hello pour Mac, iOS et Android. Vos utilisateurs peuvent utiliser ces applications sur leur mobile ou de calcul appareils tooaccess hello nouveaux programmes Azure RemoteApp.

Consultez [l’accès à vos applications dans Azure RemoteApp](remoteapp-clients.md) pour plus d’informations sur les clients de hello.

## <a name="next-steps"></a>Étapes suivantes
OK Faites un essai. Ces articles vous aident à prendre en main Azure RemoteApp :

* [Quel type de collection avez-vous besoin pour Azure RemoteApp ?](remoteapp-collections.md)
* [Création d’une image Azure RemoteApp](remoteapp-imageoptions.md)
* [Comment toocreate une collection de cloud d’Azure RemoteApp](remoteapp-create-cloud-deployment.md)
* [Comment toocreate une collection hybride d’Azure RemoteApp](remoteapp-create-hybrid-deployment.md)
* [Fonctionnement des licences dans Azure RemoteApp](remoteapp-licensing.md)
* [Meilleures pratiques pour l'utilisation d'Azure RemoteApp](remoteapp-bestpractices.md)
* [FAQ Azure RemoteApp](remoteapp-faq.md)

### <a name="help-us-help-you"></a>Vos commentaires nous aideront à mieux vous servir
Saviez-vous que toorating d’ajout de cet article et de faire des commentaires vers le bas, vous pouvez effectuer modifications toohello article ? Il manque des informations ? Des informations sont erronées ? Certains passages ne sont pas clairs ? Faites défiler et cliquez sur **modifier sur GitHub** ou **modifier** toomake modifications - ces proviendront toous pour révision et, une fois que nous se déconnecter sur ces derniers, vous verrez alors vos modifications et des améliorations ici.

