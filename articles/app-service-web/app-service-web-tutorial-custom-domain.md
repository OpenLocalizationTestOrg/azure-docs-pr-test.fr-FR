---
title: "aaaMap un DNS personnalisé existant nom tooAzure Web Apps | Documents Microsoft"
description: "Découvrez comment tooadd un domaine DNS personnalisé existant nom d’application web de tooa (domaine personnel), serveur principal d’application mobile ou application API dans Azure App Service."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2c4eea3c56c758ca11355554321ffa52dd2c6b9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="map-an-existing-custom-dns-name-tooazure-web-apps"></a>Mapper une tooAzure de nom DNS personnalisé existant Web Apps

[Azure Web Apps](app-service-web-overview.md) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques. Ce didacticiel vous montre comment toomap un DNS personnalisé existant nom tooAzure Web Apps.

![Application tooAzure de navigation du portail](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

Ce didacticiel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Mapper un sous-domaine (par exemple, `www.contoso.com`) à l’aide d’un enregistrement CNAME
> * Mapper un domaine racine (par exemple, `contoso.com`) à l’aide d’un enregistrement A
> * Mapper un domaine générique (par exemple, `*.contoso.com`) à l’aide d’un enregistrement CNAME
> * Automatiser le mappage de domaine à l’aide de scripts

Vous pouvez utiliser un **enregistrement CNAME** ou **un enregistrement** toomap DNS personnalisé nom tooApp Service. 

> [!NOTE]
> Nous vous recommandons d’utiliser un enregistrement CNAME pour tous les noms DNS personnalisés, à l’exception d’un domaine racine (par exemple, `contoso.com`).

toomigrate un site actif et son tooApp de nom de domaine DNS Service, consultez [migrer une tooAzure de nom DNS du Service d’applications active](app-service-custom-domain-name-migrate.md).

## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel :

* [Créez une application App Service](/azure/app-service/), ou utilisez une application créée pour un autre didacticiel.
* Acheter un nom de domaine et assurez-vous que vous disposez du Registre de l’accès toohello DNS de votre fournisseur de domaine (par exemple, GoDaddy).

  Par exemple, les entrées DNS tooadd pour `contoso.com` et `www.contoso.com`, vous devez être en mesure de tooconfigure paramètres de DNS hello pour hello `contoso.com` domaine racine.

  > [!NOTE]
  > Si vous n’avez un domaine existant nom, envisagez de [achat d’un domaine à l’aide de hello Azure portal](custom-dns-web-site-buydomains-web-app.md). 

## <a name="prepare-hello-app"></a>Préparer l’application hello

toomap une personnalisé DNS nom tooa l’application web, l’application web hello [plan App Service](https://azure.microsoft.com/pricing/details/app-service/) doit être un niveau payant (**Shared**, **base**, **Standard**, ou  **Premium**). Dans cette étape, vous vérifiez que ce Service d’applications app est Bonjour hello pris en charge le niveau de tarification.

### <a name="sign-in-tooazure"></a>Connectez-vous à tooAzure

Ouvrez hello [portail Azure](https://portal.azure.com) et connectez-vous avec votre compte Azure.

### <a name="navigate-toohello-app-in-hello-azure-portal"></a>Accédez application toohello Bonjour portail Azure

Dans le menu de gauche hello, sélectionnez **des Services d’application**, puis sélectionnez le nom hello de l’application hello.

![Application tooAzure de navigation du portail](./media/app-service-web-tutorial-custom-domain/select-app.png)

Page de gestion hello Hello application de Service de l’application s’affiche.  

<a name="checkpricing"></a>

### <a name="check-hello-pricing-tier"></a>Vérifier le niveau tarifaire de hello

Bonjour barre de navigation de page de l’application hello gauche, faites défiler toohello **paramètres** section et sélectionnez **montée en puissance (plan App Service)**.

![Menu Monter en puissance](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

niveau actuel de l’application Hello est mis en surbrillance d’une bordure bleue. Vérifiez que cette application hello n’est pas hello de toomake **libre** couche. DNS personnalisé n’est pas pris en charge dans hello **libre** couche. 

![Vérification du niveau de tarification](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

Si hello plan App Service n’est pas **libre**, fermez hello **choisir votre niveau tarifaire** page et ignorer trop[mapper un enregistrement CNAME](#cname).

<a name="scaleup"></a>

### <a name="scale-up-hello-app-service-plan"></a>Montée en puissance hello plan App Service

Sélectionnez un des niveaux de hello occupé (**Shared**, **base**, **Standard**, ou **Premium**). 

Cliquez sur **Sélectionner**.

![Vérification du niveau de tarification](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

Lorsque vous voyez hello suivant la notification, l’opération de mise à l’échelle de hello est terminée.

![Confirmation d’opération de mise à l’échelle](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a>Mapper un enregistrement CNAME

Dans l’exemple de didacticiel hello, vous ajoutez un enregistrement CNAME pour hello `www` sous-domaine (par exemple, `www.contoso.com`).

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a>Créer l’enregistrement CNAME de hello

Ajouter un toomap enregistrement CNAME nom d’hôte par défaut de l’application de toohello un sous-domaine (`<app_name>.azurewebsites.net`).

Pourquoi `www.contoso.com` exemple de domaine, ajoutez un enregistrement CNAME qui mappe le nom hello `www` trop`<app_name>.azurewebsites.net`.

Après avoir ajouté hello CNAME, page d’enregistrements DNS hello ressemble hello l’exemple suivant :

![Application tooAzure de navigation du portail](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-hello-cname-record-mapping-in-azure"></a>Activer le mappage d’enregistrement CNAME hello dans Azure

Bonjour gauche de navigation de page de l’application hello Bonjour portail Azure, sélectionnez **les domaines personnalisés**. 

![Menu Domaines personnalisés](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Bonjour **les domaines personnalisés** page de l’application hello, ajoutez hello complet nom DNS personnalisé (`www.contoso.com`) toohello liste.

Sélectionnez hello  **+**  icône suivant trop**ajouter le nom d’hôte**.

![Ajouter un nom d’hôte](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Nom de domaine complet de hello type que vous avez ajouté un enregistrement CNAME pour, tel que `www.contoso.com`. 

Sélectionnez **Valider**.

Hello **ajouter le nom d’hôte** bouton est activé. 

Assurez-vous que **type d’enregistrement de nom d’hôte** est défini trop**CNAME (www.example.com ou tout sous-domaine)**.

Sélectionnez **Ajouter un nom d’hôte**.

![Ajouter une application de toohello nom DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

Il peut prendre un certain temps pour hello nouveau nom d’hôte toobe est répercutée dans l’application hello **les domaines personnalisés** page. Essayez d’actualiser les données de salutation navigateur tooupdate hello.

![Enregistrement CNAME ajouté](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

Si vous manqué une étape ou que vous faites une faute de frappe quelque part précédemment, vous voyez une erreur de vérification bas hello de page de hello.

![Erreur de vérification](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a>Mapper un enregistrement A

Dans l’exemple de didacticiel hello, vous ajoutez un enregistrement A pour le domaine racine de hello (par exemple, `contoso.com`). 

<a name="info"></a>

### <a name="copy-hello-apps-ip-address"></a>Copiez l’adresse IP de l’application hello

toomap un un enregistrement, vous devez adresse IP externe de l’application hello. Vous pouvez trouver cette adresse IP de l’application hello **les domaines personnalisés** page Bonjour portail Azure.

Bonjour gauche de navigation de page de l’application hello Bonjour portail Azure, sélectionnez **les domaines personnalisés**. 

![Menu Domaines personnalisés](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Bonjour **les domaines personnalisés** page, copiez l’adresse IP de l’application hello.

![Application tooAzure de navigation du portail](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-a-record"></a>Créer l’enregistrement A de hello

requiert l’application Service toomap un un enregistrement tooan application, **deux** enregistrements DNS :

- Un **A** enregistrer l’adresse IP de l’application toomap toohello.
- A **TXT** enregistrer le nom d’hôte par défaut de l’application toomap toohello `<app_name>.azurewebsites.net`. Service d’applications utilise cet enregistrement uniquement au moment de la configuration, tooverify que vous possédez le domaine personnalisé de hello. Une fois votre domaine personnalisé validé et configuré dans App Service, vous pourrez supprimer cet enregistrement TXT. 

Pourquoi `contoso.com` exemple de domaine, créer des enregistrements A et TXT hello selon toohello tableau suivant (`@` généralement représente hello domaine racine). 

| Type d’enregistrement | Host | Valeur |
| - | - | - |
| A | `@` | Adresse IP à partir de [adresse IP de l’application hello de copie](#info) |
| TXT | `@` | `<app_name>.azurewebsites.net` |

Lorsque les enregistrements de hello sont ajoutés, hello page d’enregistrements DNS se présente comme hello l’exemple suivant :

![Page Enregistrements DNS](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-hello-a-record-mapping-in-hello-app"></a>Activer hello un mappage d’enregistrements dans l’application hello

Dans l’application hello **les domaines personnalisés** Bonjour portail Azure, ajoutez hello complet nom DNS personnalisé (par exemple, `contoso.com`) toohello liste.

Sélectionnez hello  **+**  icône suivant trop**ajouter le nom d’hôte**.

![Ajouter un nom d’hôte](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

Nom de domaine complet de hello type que vous avez configuré comme enregistrement hello A, `contoso.com`.

Sélectionnez **Valider**.

Hello **ajouter le nom d’hôte** bouton est activé. 

Assurez-vous que **type d’enregistrement de nom d’hôte** est défini trop**un enregistrement (example.com)**.

Sélectionnez **Ajouter un nom d’hôte**.

![Ajouter une application de toohello nom DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

Il peut prendre un certain temps pour hello nouveau nom d’hôte toobe est répercutée dans l’application hello **les domaines personnalisés** page. Essayez d’actualiser les données de salutation navigateur tooupdate hello.

![Enregistrement A ajouté](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

Si vous manqué une étape ou que vous faites une faute de frappe quelque part précédemment, vous voyez une erreur de vérification bas hello de page de hello.

![Erreur de vérification](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a>Mapper un domaine générique

Dans l’exemple de didacticiel hello, vous mappez un [nom DNS de caractère générique](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (par exemple, `*.contoso.com`) toohello application de Service de l’application en ajoutant un enregistrement CNAME. 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a>Créer l’enregistrement CNAME de hello

Ajouter un toomap enregistrement CNAME nom d’hôte par défaut de nom de caractère générique d’une application de toohello (`<app_name>.azurewebsites.net`).

Pourquoi `*.contoso.com` exemple de domaine, hello enregistrement CNAME mappera les nom hello `*` trop`<app_name>.azurewebsites.net`.

Lorsque hello CNAME est ajouté, hello page d’enregistrements DNS se présente comme hello l’exemple suivant :

![Application tooAzure de navigation du portail](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-hello-cname-record-mapping-in-hello-app"></a>Activer le mappage d’enregistrement CNAME hello dans l’application hello

Vous pouvez maintenant ajouter un sous-domaine qui correspond au nom toohello application de hello génériques (par exemple, `sub1.contoso.com` et `sub2.contoso.com` correspond à `*.contoso.com`). 

Bonjour gauche de navigation de page de l’application hello Bonjour portail Azure, sélectionnez **les domaines personnalisés**. 

![Menu Domaines personnalisés](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Sélectionnez hello  **+**  icône suivant trop**ajouter le nom d’hôte**.

![Ajouter un nom d’hôte](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Tapez un nom de domaine complet qui correspond au domaine de hello générique (par exemple, `sub1.contoso.com`), puis sélectionnez **Validate**.

Hello **ajouter le nom d’hôte** bouton est activé. 

Assurez-vous que **type d’enregistrement de nom d’hôte** est défini trop**enregistrement CNAME (www.example.com ou tout sous-domaine)**.

Sélectionnez **Ajouter un nom d’hôte**.

![Ajouter une application de toohello nom DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

Il peut prendre un certain temps pour hello nouveau nom d’hôte toobe est répercutée dans l’application hello **les domaines personnalisés** page. Essayez d’actualiser les données de salutation navigateur tooupdate hello.

Sélectionnez hello  **+**  icône tooadd à nouveau un autre nom d’hôte qui correspond au domaine de caractère générique hello. Par exemple, ajoutez `sub2.contoso.com`.

![Enregistrement CNAME ajouté](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a>Test dans le navigateur

Rechercher les noms DNS toohello que vous avez configuré précédemment (par exemple, `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, et `sub2.contoso.com`).

![Application tooAzure de navigation du portail](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a>Automatiser des tâches à l’aide de scripts

Vous pouvez automatiser la gestion des domaines personnalisés avec des scripts, à l’aide de hello [CLI d’Azure](/cli/azure/install-azure-cli) ou [Azure PowerShell](/powershell/azure/overview). 

### <a name="azure-cli"></a>Interface de ligne de commande Azure 

Hello commande suivante ajoute un tooan de nom DNS personnalisé configuré application de Service d’applications. 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

Pour plus d’informations, consultez [mapper une domaine personnalisé l’application web tooa](scripts/app-service-cli-configure-custom-domain.md). 

### <a name="azure-powershell"></a>Azure PowerShell 

Hello commande suivante ajoute un tooan de nom DNS personnalisé configuré application de Service d’applications. 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

Pour plus d’informations, consultez [affecter une application web de tooa domaine personnalisé](scripts/app-service-powershell-configure-custom-domain.md).

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris à :

> [!div class="checklist"]
> * Mapper un sous-domaine à l’aide d’un enregistrement CNAME
> * Mapper un domaine racine à l’aide d’un enregistrement A
> * Mapper un domaine générique à l’aide d’un enregistrement CNAME
> * Automatiser le mappage de domaine à l’aide de scripts

Avancer toolearn de didacticiel suivant toohello comment toobind une SSL personnalisée certificat tooa l’application web.

> [!div class="nextstepaction"]
> [Lier un tooAzure de certificat SSL personnalisé existant Web Apps](app-service-web-tutorial-custom-ssl.md)
