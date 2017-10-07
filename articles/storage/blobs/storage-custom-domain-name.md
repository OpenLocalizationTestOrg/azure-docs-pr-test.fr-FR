---
title: "aaaConfigure un nom de domaine personnalisé pour votre point de terminaison de stockage d’objets Blob Azure | Documents Microsoft"
description: "Utilisez hello toomap portail Azure de votre propre point de terminaison du stockage d’objets Blob toohello nom canonique (CNAME) dans un compte de stockage Azure."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: aaafd8c5-eacb-49dc-8c8b-3f7011ad5e92
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: marsma
ms.openlocfilehash: bfee6d28039f389ba2e2ed6b28d43894b6e15469
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-for-your-blob-storage-endpoint"></a>Configurer un nom de domaine personnalisé pour un point de terminaison de stockage Blob

Vous pouvez configurer un domaine personnalisé pour accéder à des données d’objets blob dans votre compte de stockage Azure. Hello de point de terminaison par défaut pour le stockage d’objets Blob est `<storage-account-name>.blob.core.windows.net`. Si vous mappez un domaine personnalisé et un sous-domaine comme **www.contoso.com** toohello blob point de terminaison pour votre compte de stockage, les utilisateurs peuvent accéder ensuite les données dans votre compte de stockage à l’aide de ce domaine d’objets blob.

> [!IMPORTANT]
> Stockage Azure ne prend pas encore en charge HTTPS nativement avec des domaines personnalisés. Vous ne pouvez actuellement [utilisent des objets BLOB de hello Azure CDN tooaccess avec des domaines personnalisés sur HTTPS](storage-https-custom-domain-cdn.md).
>

Hello tableau suivant présente quelques exemple d’URL pour des données blob dans un compte de stockage nommé **mystorageaccount**. domaine personnalisé de Hello inscrit pour le compte de stockage hello est **www.contoso.com**:

| Type de ressource | URL par défaut | URL du domaine personnalisé |
| --- | --- | --- |
| Compte de stockage | http://mystorageaccount.blob.core.windows.net | http://www.contoso.com |
| Blob |http://mystorageaccount.blob.core.windows.net/mycontainer/myblob | http://www.contoso.com/mycontainer/myblob |
| Conteneur racine | http://mystorageaccount.blob.core.windows.net/myblob ou http://mystorageaccount.blob.core.windows.net/$root/myblob| http://www.contoso.com/myblob ou http://www.contoso.com/$root/myblob |

## <a name="direct-vs-intermediary-domain-mapping"></a>Mappage de domaine direct ou intermédiaire

Il existe deux façons toopoint votre point de terminaison du blob de toohello de domaine personnalisé pour votre compte de stockage : directe CNAME mappage et à l’aide de hello *asverify* sous-domaine intermédiaire.

### <a name="direct-cname-mapping"></a>Mappage CNAME direct

première et la plus simple, la méthode Hello est toocreate un enregistrement de nom canonique (CNAME) qui mappe votre domaine personnalisé et votre sous-domaine directement toohello point de terminaison d’objets blob. Un enregistrement CNAME est une fonctionnalité de système (DNS) de nom de domaine qui est mappé à un domaine de destination de tooa de domaine source. Dans ce cas, domaine de source de hello est votre propre domaine personnalisé et votre sous-domaine, par exemple *www.contoso.com*. domaine de destination hello est votre point de terminaison de service Blob, par exemple  *mystorageaccount.BLOB.Core.Windows.NET*.

méthode directe Hello est couvert dans [inscrire un domaine personnalisé](#register-a-custom-domain).

### <a name="intermediary-mapping-with-asverify"></a>Mappage intermédiaire avec *asverify*

méthode deuxième Hello utilise également des enregistrements CNAME, mais tout d’abord emploie un sous-domaine spécial reconnu par les interruptions de service Azure tooavoid : **asverify**.

processus Hello de mappage de votre point de terminaison du blob tooa domaine personnalisé peut provoquer une courte période de temps d’arrêt pour le domaine de hello pendant que vous l’enregistrez dans hello [portail Azure](https://portal.azure.com). Si votre domaine personnalisé d’est actuellement prise en charge une application avec un contrat de niveau de service (SLA) nécessitant des temps d’interruption nul, vous pouvez ensuite utiliser hello Azure *asverify* sous-domaine en guise d’étape d’inscription intermédiaire. Cette étape intermédiaire garantit que les utilisateurs sont en mesure de tooaccess votre domaine pendant que le mappage DNS de hello a lieu.

méthode intermédiaire Hello est couvert dans [inscrire un domaine personnalisé à l’aide de hello *asverify* sous-domaine](#register-a-custom-domain-using-the-asverify-subdomain).

## <a name="register-a-custom-domain"></a>Inscrire un domaine personnalisé
Si vous n’avez aucun problème sur le domaine hello tooyour brièvement indisponible utilisateurs, ou si votre domaine personnalisé n’est pas actuellement héberge une application, utilisez ce tooregister procédure votre domaine personnalisé.

Si votre domaine personnalisé prend actuellement en charge une application qui ne peut pas avoir de tout temps d’arrêt, suivez la procédure hello [inscrire un domaine personnalisé à l’aide de hello *asverify* sous-domaine](#register-a-custom-domain-using-the-asverify-subdomain).

tooconfigure un nom de domaine personnalisé, vous devez créer un enregistrement CNAME dans DNS. Hello enregistrement CNAME spécifie un alias pour un nom de domaine. Dans ce cas, il est mappé adresse hello de votre domaine personnalisé toohello Blob stockage point de terminaison pour votre compte de stockage.

En règle générale, vous pouvez gérer les paramètres DNS de votre domaine sur le site web du Registre de celui-ci. Chaque bureau d’enregistrement a une méthode similaire, mais légèrement différente de la spécification d’un enregistrement CNAME, mais le concept de hello est hello identiques. Certains packages de l’inscription de domaine de base n’offrent pas configuration DNS, il vous faudra probablement tooupgrade votre package d’inscription de domaine avant de créer l’enregistrement CNAME de hello.

1. Accédez de compte de stockage tooyour Bonjour [portail Azure](https://portal.azure.com).
1. Sous **SERVICE BLOB** dans le panneau de menu hello, sélectionnez **un domaine personnalisé** tooopen hello *un domaine personnalisé* panneau.
1. Ouvrez une session sur le site Web de tooyour de domaines et atteindre la page toohello de gestion DNS. Vous pourrez trouver ces informations dans une section telle que **Domain Name**, **DNS** ou **Name Server Management**.
1. Rechercher la section de hello pour la gestion des enregistrements CNAME. Vous pouvez posséder de page de paramètres avancés de tooan toogo et recherchez les mots hello **CNAME**, **Alias**, ou **sous-domaines**.
1. Créez un enregistrement CNAME et indiquez un alias de sous-domaine tel que **www** ou **photos**. Puis indiquez un nom d’hôte, qui est votre point de terminaison Blob service au format de hello **mystorageaccount.blob.core.windows.net** (où *mystorageaccount* est le nom de hello de votre compte de stockage). toouse de nom d’hôte Hello s’affiche dans l’élément #1 Hello *un domaine personnalisé* panneau Bonjour [portail Azure](https://portal.azure.com).
1. Dans la zone de texte hello hello *un domaine personnalisé* panneau Bonjour [portail Azure](https://portal.azure.com), entrez le nom hello de votre domaine personnalisé, y compris le sous-domaine de hello. Par exemple, si votre domaine est **contoso.com** et votre alias de sous-domaine est **www**, entrez **www.contoso.com**. Si votre sous-domaine est **photos**, entrez **photos.contoso.com**. hello sous-domaine est *requis*.
1. Sélectionnez **enregistrer** sur hello *un domaine personnalisé* panneau tooregister votre domaine personnalisé. Si l’inscription de hello est réussie, vous voyez une notification de portail que votre compte de stockage a été correctement mis à jour.

Une fois que votre nouvel enregistrement CNAME a propagé via DNS, vos utilisateurs peuvent afficher les données blob à l’aide de votre domaine personnalisé, afin qu’ils ont les autorisations appropriées hello.

## <a name="register-a-custom-domain-using-hello-asverify-subdomain"></a>Inscrire un domaine personnalisé à l’aide de hello *asverify* sous-domaine
Utilisez cette procédure tooregister votre domaine personnalisé si votre domaine personnalisé d’est actuellement prise en charge une application avec un contrat SLA qui requiert qu’il n’y ait aucune interruption de service. En créant un enregistrement CNAME qui pointe de `asverify.<subdomain>.<customdomain>` trop`asverify.<storageaccount>.blob.core.windows.net`, inscrivez-vous votre domaine avec Azure. Vous pouvez ensuite créer un deuxième CNAME qui pointe de `<subdomain>.<customdomain>` trop`<storageaccount>.blob.core.windows.net`, à quel point domaine personnalisé de trafic tooyour sera le point de terminaison suggérés tooyour blob.

Hello **asverify** sous-domaine est un sous-domaine spécial reconnu par Azure. En ajoutant le préfixe `asverify` tooyour de sous-domaine propre, vous autorisez Azure toorecognize votre domaine personnalisé sans modifier l’enregistrement DNS de hello pour le domaine de hello. Lorsque vous modifiez un enregistrement DNS de hello pour le domaine de hello, il s’agit de point de terminaison toohello mappé blob sans interruption.

1. Accédez de compte de stockage tooyour Bonjour [portail Azure](https://portal.azure.com).
1. Sous **SERVICE BLOB** dans le panneau de menu hello, sélectionnez **un domaine personnalisé** tooopen hello *un domaine personnalisé* panneau.
1. Ouvrez une session sur le site Web du fournisseur tooyour DNS et atteindre la page toohello de gestion DNS. Vous pourrez trouver ces informations dans une section telle que **Domain Name**, **DNS** ou **Name Server Management**.
1. Rechercher la section de hello pour la gestion des enregistrements CNAME. Vous pouvez posséder de page de paramètres avancés de tooan toogo et recherchez les mots hello **CNAME**, **Alias**, ou **sous-domaines**.
1. Créez un enregistrement CNAME et fournir un alias de sous-domaine qui inclut hello *asverify* sous-domaine. Par exemple, **asverify.www** ou **asverify.photos**. Puis indiquez un nom d’hôte, qui est votre point de terminaison Blob service au format de hello **asverify.mystorageaccount.blob.core.windows.net** (où **mystorageaccount** est le nom de hello de votre compte de stockage). toouse de nom d’hôte Hello s’affiche dans l’élément #2 Hello *un domaine personnalisé* panneau Bonjour [portail Azure](https://portal.azure.com).
1. Dans la zone de texte hello hello *un domaine personnalisé* panneau Bonjour [portail Azure](https://portal.azure.com), entrez le nom hello de votre domaine personnalisé, y compris le sous-domaine de hello. N’incluez pas *asverify*. Par exemple, si votre domaine est **contoso.com** et votre alias de sous-domaine est **www**, entrez **www.contoso.com**. Si votre sous-domaine est **photos**, entrez **photos.contoso.com**. sous-domaine de hello est requis.
1. Sélectionnez hello **utiliser la validation CNAME indirecte** case à cocher.
1. Sélectionnez **enregistrer** sur hello *un domaine personnalisé* panneau tooregister votre domaine personnalisé. Si l’inscription de hello est réussie, vous verrez une notification indiquant que votre compte de stockage a été correctement mis à jour du portail. À ce stade, votre domaine personnalisé a été vérifié par Azure, mais le trafic tooyour domaine n’est pas encore acheminé compte de stockage tooyour.
1. Retourner le site Web du fournisseur tooyour DNS et créer un autre enregistrement CNAME qui mappe votre point de terminaison du service d’objet Blob tooyour sous-domaine. Par exemple, spécifiez le sous-domaine hello en tant que **www** ou **photos** (sans hello *asverify*), et hello nom d’hôte en tant que  **mystorageaccount.BLOB.Core.Windows.NET** (où **mystorageaccount** est le nom de hello de votre compte de stockage). Cette étape, hello l’inscription de votre domaine personnalisé est terminée.
1. Enfin, vous pouvez supprimer l’enregistrement CNAME de hello vous avez créé le conteneur hello **asverify** sous-domaine, tel qu’il était nécessaire uniquement comme une étape intermédiaire.

Une fois que votre nouvel enregistrement CNAME a propagé via DNS, vos utilisateurs peuvent afficher les données blob à l’aide de votre domaine personnalisé, afin qu’ils ont les autorisations appropriées hello.

## <a name="test-your-custom-domain"></a>Tester votre domaine personnalisé

tooconfirm que votre domaine personnalisé est mappé en effet le point de terminaison de service tooyour Blob, créer un objet blob dans un conteneur public au sein de votre compte de stockage. Puis, dans un navigateur web, utilisez un URI hello suivant l’objet blob de format tooaccess hello :

`http://<subdomain.customdomain>/<mycontainer>/<myblob>`

Par exemple, vous pouvez utiliser hello suivant URI tooaccess un formulaire web Bonjour **myforms** conteneur Bonjour **photos.contoso.com** sous-domaine personnalisé :

`http://photos.contoso.com/myforms/applicationform.htm`

## <a name="deregister-a-custom-domain"></a>Annuler l’inscription d’un domaine personnalisé

tooderegister un domaine personnalisé pour votre point de terminaison de stockage Blob, utilisez une des hello procédures suivantes.

### <a name="azure-portal"></a>Portail Azure

Effectuez les opérations suivantes de hello dans le paramètre de domaine personnalisé hello hello tooremove portail Azure :

1. Accédez de compte de stockage tooyour Bonjour [portail Azure](https://portal.azure.com).
1. Sous **SERVICE BLOB** dans le panneau de menu hello, sélectionnez **un domaine personnalisé** tooopen hello *un domaine personnalisé* panneau.
1. Contenu hello clair hello de zone de texte contenant le nom de votre domaine personnalisé.
1. Sélectionnez hello **enregistrer** bouton.

Lorsque le domaine personnalisé de hello a été supprimé avec succès, vous verrez une notification indiquant que votre compte de stockage a été correctement mis à jour du portail.

### <a name="azure-cli-20"></a>Azure CLI 2.0

Hello d’utilisation [mise à jour de compte de stockage az](https://docs.microsoft.com/cli/azure/storage/account#update) CLI de commandes et spécifiez une chaîne vide (`""`) pour hello `--custom-domain` argument valeur tooremove une inscription de domaine personnalisé.

* Format de commande :

  ```azurecli
  az storage account update \
      --name <storage-account-name> \
      --resource-group <resource-group-name> \
      --custom-domain ""
  ```

* Exemple de commande :

  ```azurecli
  az storage account update \
      --name mystorageaccount \
      --resource-group myresourcegroup \
      --custom-domain ""
  ```

### <a name="powershell"></a>PowerShell

Hello d’utilisation [Set-AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) applet de commande PowerShell et spécifiez une chaîne vide (`""`) pour hello `-CustomDomainName` argument valeur tooremove une inscription de domaine personnalisé.

* Format de commande :

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "<resource-group-name>" `
      -AccountName "<storage-account-name>" `
      -CustomDomainName ""
  ```

* Exemple de commande :

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "myresourcegroup" `
      -AccountName "mystorageaccount" `
      -CustomDomainName ""
  ```

## <a name="next-steps"></a>Étapes suivantes
* [Mapper un point de terminaison du réseau de distribution contenu (CDN) Azure tooan domaine personnalisé](../../cdn/cdn-map-content-to-custom-domain.md)
* [Avec des objets BLOB de hello Azure CDN tooaccess avec des domaines personnalisés via HTTPS](storage-https-custom-domain-cdn.md)
