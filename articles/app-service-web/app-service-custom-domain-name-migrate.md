---
title: "aaaMigrate un DNS active nom tooAzure du Service d’applications | Documents Microsoft"
description: "Découvrez comment toomigrate un nom de domaine DNS personnalisé qui est déjà affecté tooa live tooAzure de site du Service d’applications sans interruption de service."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 10da5b8a-1823-41a3-a2ff-a0717c2b5c2d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: cephalin
ms.openlocfilehash: fbc4cc30dcb87efb2e867cb65c5404b667661e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-active-dns-name-tooazure-app-service"></a>Migrer un active tooAzure de nom DNS du Service d’applications

Cet article explique comment toomigrate un DNS active Nom trop[Azure App Service](../app-service/app-service-value-prop-what-is.md) sans interruption de service.

Lorsque vous migrez un site actif et son tooApp de nom de domaine DNS Service, ce nom DNS sert déjà le trafic dynamique. Vous pouvez éviter des temps d’arrêt dans la résolution DNS pendant la migration de hello en hello active DNS nom tooyour application de Service d’applications de liaison de manière préemptive.

Si vous n’êtes pas inquiet de temps d’arrêt dans la résolution DNS, consultez [mapper un tooAzure de nom DNS personnalisé existant Web Apps](app-service-web-tutorial-custom-domain.md).

## <a name="prerequisites"></a>Composants requis

toocomplete ce procédure :

- [Vérifiez que votre application App Service n’est pas au niveau Gratuit](app-service-web-tutorial-custom-domain.md#checkpricing).

## <a name="bind-hello-domain-name-preemptively"></a>Lier le nom de domaine hello manière préemptive

Lorsque vous liez un domaine personnalisé de manière préemptive, vous effectuez les deux suivantes hello avant d’apporter des modifications à vos enregistrements DNS :

- Vérifier la propriété du domaine
- Activer le nom de domaine hello pour votre application

Lorsque vous migrez enfin votre nom DNS personnalisé à partir de hello ancien site toohello application de Service de l’application, il n’y aura aucun temps d’arrêt dans la résolution DNS.

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a>Créer un enregistrement de vérification de domaine

la propriété du domaine tooverify, ajouter un TXT enregistrer. Hello enregistrement TXT est mappé à partir de _awverify.&lt; sous-domaine >_ too_&lt;appname >. azurewebsites.net_. 

Hello enregistrement TXT que vous avez besoin dépend hello enregistrement DNS que vous souhaitez toomigrate. Pour obtenir des exemples, consultez hello tableau suivant (`@` généralement représente hello domaine racine) :  

| Exemple d’enregistrement DNS | Hôte TXT | Valeur TXT |
| - | - | - |
| @ (racine) | _awverify_ | _&lt;nomapplication&gt;.azurewebsites.net_ |
| www (sous-domaine) | _awverify.www_ | _&lt;nomapplication&gt;.azurewebsites.net_ |
| \* (caractère générique) | _awverify.\*_ | _&lt;nomapplication&gt;.azurewebsites.net_ |

Dans votre page d’enregistrements DNS, notez le type d’enregistrement de hello nom DNS que vous souhaitez toomigrate hello. App Service prend en charge les mappages d’enregistrements CNAME et A.

### <a name="enable-hello-domain-for-your-app"></a>Activer le domaine hello pour votre application

Bonjour [portail Azure](https://portal.azure.com)hello du volet de navigation gauche de la page de l’application hello, dans Sélectionnez **les domaines personnalisés**. 

![Menu Domaines personnalisés](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Bonjour **les domaines personnalisés** page, sélectionnez hello  **+**  icône suivant trop**ajouter le nom d’hôte**.

![Ajouter un nom d’hôte](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Nom de domaine complet de hello type que vous avez ajouté enregistrement TXT de hello, tel que `www.contoso.com`. Pour un domaine de caractère générique (comme \*. contoso.com), vous pouvez utiliser n’importe quel nom DNS qui correspond au domaine de caractère générique hello. 

Sélectionnez **Valider**.

Hello **ajouter le nom d’hôte** bouton est activé. 

Assurez-vous que **type d’enregistrement de nom d’hôte** a la valeur toohello type d’enregistrement DNS vous souhaitez toomigrate.

Sélectionnez **Ajouter un nom d’hôte**.

![Ajouter une application de toohello nom DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

Il peut prendre un certain temps pour hello nouveau nom d’hôte toobe est répercutée dans l’application hello **les domaines personnalisés** page. Essayez d’actualiser les données de salutation navigateur tooupdate hello.

![Enregistrement CNAME ajouté](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

Votre nom DNS personnalisé est à présent activé dans votre application Azure. 

## <a name="remap-hello-active-dns-name"></a>Remapper les nom DNS active hello

Hello chose uniquement les toodo gauche est le remappage votre tooApp de toopoint enregistrement DNS Service actif. Droit à présent, il continue de pointer tooyour ancien site.

<a name="info"></a>

### <a name="copy-hello-apps-ip-address-a-record-only"></a>Copiez l’adresse IP de l’application hello (enregistrement uniquement)

Si vous remappez un enregistrement CNAME, ignorez cette section. 

tooremap un un enregistrement, vous avez besoin d’adresse IP externe de l’application de Service de l’application hello, qui est affichée dans hello **les domaines personnalisés** page.

Fermer hello **ajouter le nom d’hôte** page en sélectionnant **X** dans le coin supérieur droit de hello. 

Bonjour **les domaines personnalisés** page, copiez l’adresse IP de l’application hello.

![Application tooAzure de navigation du portail](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-hello-dns-record"></a>Mettre à jour un enregistrement DNS hello

Dans la page d’enregistrements hello DNS de votre fournisseur de domaine, sélectionnez tooremap enregistrement DNS de hello.

Pourquoi `contoso.com` racine d’exemple de domaine, de remapper l’enregistrement A ou CNAME de hello comme exemples hello Bonjour tableau suivant : 

| Exemple de nom de domaine complet | Type d’enregistrement | Host | Valeur |
| - | - | - | - |
| contoso.com (racine) | A | `@` | Adresse IP à partir de [adresse IP de l’application hello de copie](#info) |
| www.contoso.com (sous-domaine) | CNAME | `www` | _&lt;nomapplication&gt;.azurewebsites.net_ |
| \*.contoso.com (caractère générique) | CNAME | _\*_ | _&lt;nomapplication&gt;.azurewebsites.net_ |

Enregistrez vos paramètres.

Requêtes DNS doivent commencer à résoudre les tooyour application de Service de l’application immédiatement après que la propagation DNS se produit.

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment toobind une SSL personnalisée certificat tooApp Service.

> [!div class="nextstepaction"]
> [Lier un tooAzure de certificat SSL personnalisé existant Web Apps](app-service-web-tutorial-custom-ssl.md)
