---
title: "aaaHow tooconfigure une application de Proxy d’Application | Documents Microsoft"
description: "Découvrez comment toocreate une configuration d’une application Proxy d’APplication en quelques étapes simples"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: c64019098fc124e4fe10b8288830bcd2b7239d3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application"></a>Comment tooconfigure une application de Proxy d’Application

Cet article vous a-t-il toounderstand tooconfigure une application de Proxy d’Application dans Azure AD tooexpose votre toohello d’applications sur site de cloud.

## <a name="recommended-documents"></a>Documents recommandés 

toolearn sur les configurations initiales hello et la création d’une application de Proxy d’Application via hello portail d’administration, suivez hello [publier des applications à l’aide du Proxy d’Application Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

Pour plus d’informations sur la configuration des connecteurs, consultez [activer le Proxy d’Application Bonjour Azure portal](active-directory-application-proxy-enable.md).

Pour plus d’informations sur le chargement des certificats et l’utilisation des domaines personnalisés, consultez [Utilisation des domaines personnalisés dans le proxy d’application Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).

## <a name="create-hello-applicationsetting-hello-urls"></a>Créer des URL de hello de paramètre d’Application hello

Si vous suivez les étapes hello Bonjour [publier des applications à l’aide du Proxy d’Application Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentation et sont une erreur de création d’application hello, consultez les détails de l’erreur hello pour plus d’informations et des suggestions pour application hello toofix. La plupart des messages d’erreur incluent la suggestion d’un correctif. les erreurs courantes tooavoid, vérifiez que :

-   Vous êtes un administrateur disposant d’autorisations toocreate une application de Proxy d’Application

-   une URL interne Hello est unique

-   URL externe de Hello est unique

-   Hello commencent URL http ou https et se terminer par un « / »

-   URL de Hello doit être un nom de domaine, et non une adresse IP

message d’erreur Hello doit afficher dans le coin supérieur droit de hello lorsque vous créez l’application hello. Vous pouvez également sélectionner les messages d’erreur hello notification icône toosee hello.

   ![Invite de notification](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a>Configurer des connecteurs/groupes de connecteurs

Si vous avez des difficultés à configurer votre application en raison de l’avertissement concernant les connecteurs hello et groupes de connecteurs, consultez les instructions sur l’activation du Proxy d’Application pour plus d’informations sur la façon des connecteurs toodownload. Si vous souhaitez toolearn plus d’informations sur les connecteurs, consultez hello [documentation de connecteurs](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).

Si vos connecteurs sont inactives, cela signifie qu’ils sont le service de hello tooreach impossible. Il s’agit souvent, car tous les ports hello requis ne sont pas ouverts. toosee une liste des ports requis, consultez la section de conditions préalables de hello Hello l’activation de la documentation de Proxy d’Application.

## <a name="upload-certificates-for-custom-domains"></a>Charger des certificats pour des domaines personnalisés

Domaines personnalisés vous permettent de domaine de hello toospecify de votre URL externes. toouse des domaines personnalisés, vous avez besoin tooupload hello certificat pour ce domaine. Pour plus d’informations sur l’utilisation des domaines et des certificats personnalisés, consultez [Utilisation des domaines personnalisés dans le proxy d’application Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains). 

Si vous rencontrez des problèmes de téléchargement de votre certificat, recherchez les messages d’erreur de hello dans portail hello pour plus d’informations sur un problème avec le certificat de hello hello. Voici les problèmes courants liés aux certificats :

-   Expiration du certificat

-   Certificat auto-signé

-   Certificat ne contient pas de clé privée de hello

affichage messages d’erreur Hello dans hello coin supérieur droit lorsque vous essaierez de certificat de hello tooupload. Vous pouvez également sélectionner les messages d’erreur hello notification icône toosee hello.

   ![Invite de notification](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a>Étapes suivantes
[Publier des applications avec le Proxy d’application Azure AD](application-proxy-publish-azure-portal.md)
