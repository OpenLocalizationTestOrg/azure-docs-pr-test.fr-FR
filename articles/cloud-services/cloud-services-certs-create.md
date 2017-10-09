---
title: certificats de gestion et de Services aaaCloud | Documents Microsoft
description: "Découvrez comment toocreate et l’utilisation des certificats avec Microsoft Azure"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: fc70d00d-899b-4771-855f-44574dc4bfc6
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 69cb5467ece58a91dae06b4120954aeb2826bde1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="certificates-overview-for-azure-cloud-services"></a>Vue d’ensemble des certificats pour Azure Cloud Services
Les certificats sont utilisés dans Azure pour les services cloud ([certificats de service](#what-are-service-certificates)) et pour l’authentification avec l’API de gestion hello ([certificats de gestion](#what-are-management-certificates) lorsque l’utilisation hello portail Azure classic et non Hello non classique portail Azure). Cette rubrique donne une vue d’ensemble des deux types de certificat, comment trop[créer](#create) et [déployer](#deploy) les tooAzure.

Les certificats utilisés dans Azure sont des certificats x.509 v3 et peuvent être signés par un autre certificat approuvé ou être auto-signés. Un certificat auto-signé est signé par son propre créateur et n’est donc pas approuvé par défaut. La plupart des navigateurs peuvent ignorer ce problème. Les certificats auto-signés ne doivent être utilisés que par vous au moment où vous développez et testez vos services cloud. 

Les certificats utilisés par Azure peuvent contenir une clé privée ou publique. Les certificats ont une empreinte numérique qui fournit un moyen tooidentify leur de façon non ambiguë. Cette empreinte numérique est utilisée dans hello Azure [fichier de configuration](cloud-services-configure-ssl-certificate.md) tooidentify lequel un service cloud du certificat doit utiliser. 

## <a name="what-are-service-certificates"></a>Que sont les certificats de service ?
Certificats de service sont des services toocloud attaché et activer tooand de sécuriser la communication à partir du service de hello. Par exemple, si vous avez déployé un rôle web, vous pouvez toosupply un certificat qui peut authentifier un point de terminaison HTTPS exposé. Certificats de service, définis dans votre définition de service, sont toohello automatiquement déployé l’ordinateur virtuel qui exécute une instance de votre rôle. 

Vous pouvez télécharger classique de tooAzure de certificats de service portail à l’aide de hello classique Azure portail ou à l’aide du modèle de déploiement classique hello. Les certificats de service sont associés à un service cloud spécifique. Ils sont attribués déploiement tooa dans le fichier de définition de service hello.

Les certificats de service peuvent être gérés séparément de vos services et par différentes personnes. Par exemple, un développeur peut télécharger un package de service qui fait référence de certificat tooa qu’un responsable informatique a téléchargé précédemment tooAzure. Un responsable informatique peut gérer et renouveler le certificat (modification de configuration de hello du service de hello) sans avoir besoin de tooupload un nouveau package de service. Il est possible de mettre à jour sans un nouveau package de service, car le nom logique de hello, nom du magasin et l’emplacement du certificat de hello est dans un fichier de définition de service hello et lors de l’empreinte numérique du certificat hello est spécifié dans le fichier de configuration de service hello. certificat de hello tooupdate, il est uniquement nécessaire tooupload un nouveau certificat et l’empreinte numérique hello de modification de valeur dans le fichier de configuration de service hello.

>[!Note]
>Hello [FAQ sur les Services de Cloud](cloud-services-faq.md) article comporte des informations utiles sur les certificats.

## <a name="what-are-management-certificates"></a>Que sont les certificats de gestion ?
Certificats de gestion permettent de tooauthenticate avec le modèle de déploiement classique hello. Plusieurs des programmes et des outils (tels que Visual Studio ou hello Azure SDK) utilisent ces tooautomate configuration des certificats et le déploiement des services Azure différents. Ils ne sont pas vraiment connexes toocloud services. 

> [!WARNING]
> Soyez prudent ! Ces types de certificats autorisent tout le monde qui s’authentifie avec les abonnements de hello toomanage auxquels ils sont associés. 
> 
> 

### <a name="limitations"></a>Limites
Le nombre de certificats de gestion est limité à 100 par abonnement. Il existe également une limite de 100 certificats de gestion pour l’ensemble des abonnements figurant sous un identificateur d’utilisateur d’administrateur de service spécifique. Si hello ID d’utilisateur pour l’administrateur de compte hello a déjà été utilisé tooadd 100 les certificats de gestion et il est nécessaire pour les certificats de plus, vous pouvez ajouter un coadministrateur tooadd hello autres certificats. 

Avant d’ajouter plus de 100 certificats, regardez si vous pouvez réutiliser un certificat existant. L’utilisation de coadministrateurs ajoute des processus de gestion de certificat tooyour complexité éventuellement inutile.

<a name="create"></a>
## <a name="create-a-new-self-signed-certificate"></a>Création d’un certificat auto-signé
Vous pouvez utiliser n’importe quel un certificat auto-signé du outil disponible toocreate tant qu’ils respectent les paramètres toothese :

* Certificat X.509.
* Contient une clé privée.
* Créé pour l’échange de clés (fichier .pfx).
* Nom du sujet doit correspondre au service de cloud hello domaine utilisé tooaccess hello.

    > Impossible d’acquérir un certificat SSL pour hello cloudapp.net (ou liées à Azure) domaine ; nom du sujet du certificat Hello doit correspondre à hello domaine personnalisé nom utilisé tooaccess votre application. Par exemple, **contoso.net**, mais pas **contoso.cloudapp.net**.

* Chiffrement à 2 048 bits au minimum.
* **Certificat de service uniquement**: certificat côté Client doit résider dans hello *personnel* magasin de certificats.

Il existe deux moyens faciles toocreate un certificat sur Windows, avec hello `makecert.exe` utilitaire ou IIS.

### <a name="makecertexe"></a>Makecert.exe
Cet utilitaire a été déconseillé et n’est plus documenté ici. Pour plus d’informations, consultez [cet article MSDN](https://msdn.microsoft.com/library/windows/desktop/aa386968).

### <a name="powershell"></a>PowerShell
```powershell
$cert = New-SelfSignedCertificate -DnsName yourdomain.cloudapp.net -CertStoreLocation "cert:\LocalMachine\My"
$password = ConvertTo-SecureString -String "your-password" -Force -AsPlainText
Export-PfxCertificate -Cert $cert -FilePath ".\my-cert-file.pfx" -Password $password
```

> [!NOTE]
> Si vous souhaitez que le certificat de hello toouse avec une adresse IP au lieu d’un domaine, utiliser l’adresse IP de hello dans le paramètre de DnsName - hello.


Si vous le souhaitez toouse [certificat avec le portail de gestion hello](../azure-api-management-certs.md), exportez-le tooa **.cer** fichier :

```powershell
Export-Certificate -Type CERT -Cert $cert -FilePath .\my-cert-file.cer
```

### <a name="internet-information-services-iis"></a>Internet Information Services (IIS)
Il existe de nombreuses pages sur hello internet qui couvrent la toodo avec IIS. [ici](https://www.sslshopper.com/article-how-to-create-a-self-signed-certificate-in-iis-7.html) une procédure détaillée particulièrement claire. 

### <a name="java"></a>Java
Vous pouvez utiliser Java trop[créer un certificat](../app-service-web/java-create-azure-website-using-java-sdk.md#create-a-certificate).

### <a name="linux"></a>Linux
[Cela](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article décrit l’utilisation des certificats toocreate avec SSH.

## <a name="next-steps"></a>Étapes suivantes
[Télécharger votre toohello de certificat de service portail Azure classic](cloud-services-configure-ssl-certificate.md) (ou hello [portail Azure](cloud-services-configure-ssl-certificate-portal.md)).

Télécharger un [certificat de l’API de gestion](../azure-api-management-certs.md) toohello portail Azure classic. Hello portail Azure n’utilise pas de certificats de gestion pour l’authentification.

