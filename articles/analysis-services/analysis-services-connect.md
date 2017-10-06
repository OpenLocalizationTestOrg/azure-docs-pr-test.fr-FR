---
title: aaaConnect tooAzure Analysis Services | Documents Microsoft
description: "Découvrez comment tooconnect tooand obtenir des données à partir d’un serveur Analysis Services dans Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: b37f70a0-9166-4173-932d-935d769539d1
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 5df94492feb48034f156b72e83e1009683988fc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-analysis-services-server"></a>Connecter tooan Azure Analysis Services serveur

Cet article décrit le serveur tooa se connectant à l’aide de la modélisation des données et des applications de gestion telles que SQL Server Management Studio (SSMS) ou SQL Server Data Tools (SSDT). La connexion est également possible avec des applications de création de rapports client telles que Microsoft Excel, Power BI Desktop ou des applications personnalisées. Connexions tooAzure Analysis Services utilisent HTTPS.

## <a name="client-libraries"></a>Bibliothèques clientes
[Obtenir les bibliothèques clientes plus récentes hello](analysis-services-data-providers.md)

Tous les serveur tooa de connexions, quel que soit le type, nécessitent des mises à jour AMO, ADOMD.NET et OLEDB bibliothèques tooconnect tooand interface client avec un serveur Analysis Services. Pour SSMS, SSDT, Excel 2016 et Power BI, les bibliothèques clientes plus récentes hello sont installés ou mis à jour avec les versions mensuelles. Toutefois, dans certains cas, il est possible qu'une application ne peut pas avoir plus récentes hello. Par exemple, lorsque le délai de stratégies mises à jour ou des mises à jour Office 365 sont sur hello différé canal.

## <a name="server-name"></a>Nom du serveur

Lorsque vous créez un serveur Analysis Services dans Azure, vous spécifiez une région de hello et de nom unique où le serveur de hello est toobe créé. Lorsque vous spécifiez le nom du serveur hello dans une connexion, le schéma d’affectation de noms du serveur hello est :

```
<protocol>://<region>/<servername>
```
 Où protocol est chaîne **asazure**, région est hello Uri où le serveur de hello a été créé (par exemple, westus.asazure.windows.net) et nom de hello de votre serveur unique au sein de la région de hello servername.

### <a name="get-hello-server-name"></a>Obtenir le nom du serveur hello
Dans **portail Azure** > serveur > **vue d’ensemble** > **nom du serveur**, copier le nom de serveur entier hello. Si autres utilisateurs de votre organisation connectez trop toothis serveur, vous pouvez partager ce nom de serveur avec eux. Lorsque vous spécifiez un nom de serveur, le chemin d’accès complet de hello doit être utilisé.

![Obtenir le nom du serveur dans Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a>Chaîne de connexion

Lors de la connexion tooAzure Analysis Services à l’aide de hello modèle d’objet tabulaire, hello utilisation suivant les formats de chaîne de connexion :

###### <a name="integrated-azure-active-directory-authentication"></a>Authentification Azure Active Directory intégrée
L’authentification intégrée, récupère hello cache d’informations d’identification Azure Active Directory s’il est disponible. Le cas contraire, la fenêtre de connexion Azure hello est affichée.

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a>Authentification Active Directory Azure avec le nom d’utilisateur et le mot de passe

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a>Authentification Windows (sécurité intégrée)
Utiliser compte de Windows hello processus en cours hello en cours d’exécution.

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a>Connexion à l’aide d’un fichier .odc
Avec les versions antérieures d’Excel, les utilisateurs peuvent se connecter serveur des Services d’analyse Azure tooan à l’aide d’un fichier Office Data Connection (.odc). toolearn, voir [créer un fichier Office Data Connection (.odc)](analysis-services-odc.md).


## <a name="next-steps"></a>Étapes suivantes
[Connexion avec Excel](analysis-services-connect-excel.md)    
[Connexion avec Power BI](analysis-services-connect-pbi.md)   
[Gérer votre serveur](analysis-services-manage.md)   

