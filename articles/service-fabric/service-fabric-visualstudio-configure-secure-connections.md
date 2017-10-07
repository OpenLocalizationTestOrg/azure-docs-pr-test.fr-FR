---
title: "aaaConfigure sécuriser les connexions de cluster Azure Service Fabric | Documents Microsoft"
description: "Découvrez comment toouse Visual Studio tooconfigure sécuriser les connexions qui sont pris en charge par cluster de Azure Service Fabric hello."
services: service-fabric
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: tglee
ms.assetid: 80501867-dd7a-4648-8bd6-d4f26b68402d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/04/2017
ms.author: cawa
ms.openlocfilehash: ed3e5043264cf026f74e24ca09b40ccc70086cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-connections-tooa-service-fabric-cluster-from-visual-studio"></a>Configurer des connexions sécurisées tooa Service Fabric cluster à partir de Visual Studio
Découvrez comment toouse Visual Studio toosecurely accéder à un cluster Azure Service Fabric avec les stratégies de contrôle d’accès configurées.

## <a name="cluster-connection-types"></a>Types de connexion au cluster
Deux types de connexions sont pris en charge par cluster de Azure Service Fabric hello : **non sécurisées** connexions et **x509 basée sur certificat** des connexions sécurisées. (Pour les clusters Service Fabric hébergés localement, les authentifications **Windows** et **dSTS** sont également prises en charge.) Vous avez le type de connexion de cluster tooconfigure hello lors de la création de cluster de hello. Lorsqu’il est créé, type de connexion hello ne peut pas être modifié.

outils de Visual Studio Service Fabric Hello prend en charge tous les types d’authentification pour la connexion de cluster tooa pour la publication. Consultez [configuration d’un cluster Service Fabric à partir de hello portail Azure](service-fabric-cluster-creation-via-portal.md) pour obtenir des instructions sur la façon de tooset configuration d’un cluster Service Fabric sécurisé.

## <a name="configure-cluster-connections-in-publish-profiles"></a>Configurer des connexions au cluster dans les profils de publication
Si vous publiez un projet de Service Fabric à partir de Visual Studio, utilisez hello **publier une Application de Service Fabric** toochoose de boîte de dialogue un cluster Azure Service Fabric. Sous **Point de terminaison de connexion**, sélectionnez un cluster existant sous votre abonnement.

![Hello ** boîte de dialogue Publier Service Fabric Application ** est tooconfigure utilisé une connexion de Service Fabric.][publishdialog]

Hello **publier une Application de Service Fabric** boîte de dialogue valide automatiquement la connexion de cluster hello. Si vous y êtes invité, connectez-vous tooyour compte Azure. Si la validation réussit, cela signifie que votre système hello correct de certificats installés tooconnect toohello cluster en toute sécurité, ou de votre cluster est non sécurisé. Échecs de validation peuvent être dû à des problèmes réseau ou en l’absence de votre cluster de sécurisé de tooa tooconnect système est correctement configuré.

![Hello ** publier Service Fabric Application ** boîte de dialogue valide existant, correctement configuré connexion du cluster Service Fabric.][selectsfcluster]

### <a name="tooconnect-tooa-secure-cluster"></a>cluster sécurisée de tooconnect tooa
1. Assurez-vous que vous pouvez accéder à un des certificats de client hello hello approbations de cluster de destination. certificat de Hello est habituellement partagé sous un fichier d’échange d’informations personnelles (.pfx). Consultez [configuration d’un cluster Service Fabric à partir de hello portail Azure](service-fabric-cluster-creation-via-portal.md) permettant à accéder à tooconfigure hello server toogrant tooa client.
2. Installez le certificat de confiance hello. toodo, double-cliquez sur le fichier .pfx de hello, ou utiliser des certificats de hello PowerShell script Import-PfxCertificate tooimport hello. Installer le certificat de hello trop**Cert : \LocalMachine\My**. Il est OK tooaccept tous les paramètres par défaut lors de l’importation du certificat de hello.
3. Choisissez hello **publier...**  menu contextuel de hello Hello de hello projet tooopen **publier l’Application Azure** boîte de dialogue et le cluster cible de hello puis sélectionnez. outil de Hello résout les connexion hello automatiquement et enregistre les paramètres Bonjour publier une connexion sécurisée hello profil.
4. Facultatif : Vous pouvez modifier hello publier profil toospecify une connexion sécurisée de cluster.
   
   Étant donné que vous modifiez manuellement les informations de certificat du fichier toospecify hello hello XML du profil de publication, être le nom du magasin de certificat que toonote hello, stocker l’emplacement et l’empreinte numérique du certificat. Vous devez tooprovide ces valeurs pour la banque de certificats hello nom et emplacement du magasin. Consultez [Comment : récupérer hello empreinte d’un certificat](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx) pour plus d’informations.
   
   Vous pouvez utiliser hello *ClusterConnectionParameters* paramètres toospecify hello PowerShell paramètres toouse lors de la connexion de cluster du Service Fabric toohello. Les paramètres valides sont ceux qui sont acceptées par l’applet de commande Connect-ServiceFabricCluster hello. Consultez la rubrique [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx) pour obtenir la liste des paramètres disponibles.
   
   Si vous publiez tooa de cluster distant, vous devez les paramètres appropriés de toospecify hello pour ce cluster spécifique. Hello Voici un exemple de cluster de non sécurisé tooa connexion :
   
   `<ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000" />`
   
   Voici un exemple de connexion tooan x509 basée sur certificat sécurisé cluster :
   
   ```xml
   <ClusterConnectionParameters
   ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000"
   X509Credential="true"
   ServerCertThumbprint="0123456789012345678901234567890123456789"
   FindType="FindByThumbprint"
   FindValue="9876543210987654321098765432109876543210"
   StoreLocation="CurrentUser"
   StoreName="My" />
   ```
5. Modifier tous les autres paramètres nécessaires, tels que les paramètres de mise à niveau et emplacement du fichier de paramètres d’Application, puis publier votre application à partir de hello **publier une Application de Service Fabric** boîte de dialogue dans Visual Studio.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’accès aux clusters Service Fabric, consultez [Visualisation de votre cluster à l’aide de l’outil Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).

<!--Image references-->
[publishdialog]:./media/service-fabric-visualstudio-configure-secure-connections/publishdialog.png
[selectsfcluster]:./media/service-fabric-visualstudio-configure-secure-connections/selectsfcluster.png
