---
title: "AAA « activer HTTPS sur un domaine personnalisé CDN Azure | Documents Microsoft »"
description: "Découvrez comment tooenable HTTPS sur votre point de terminaison CDN Azure avec un domaine personnalisé."
services: cdn
documentationcenter: 
author: camsoper
manager: erikre
editor: 
ms.assetid: 10337468-7015-4598-9586-0b66591d939b
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: casoper
ms.openlocfilehash: 93746222616c9ed7977ec3b22c38ac1d43b118f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a>Activer HTTPS sur un domaine personnalisé Azure CDN

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Prise en charge HTTPS pour les domaines personnalisés CDN Azure vous permet de toodeliver de contenu sécurisée via SSL à l’aide de votre propre sécurité hello de domaine nom tooimprove de données en cours de transit. tooenable de flux de travail de bout en bout Hello HTTPS pour votre domaine personnalisé est simplifié via l’activation en un clic, la gestion des certificats terminée et toutes les données avec sans coût supplémentaire.

Il s’agit de confidentialité de hello tooensure critiques et l’intégrité des données de toutes les données sensibles applications web en cours de transit. À l’aide de hello le protocole HTTPS garantit que vos données sensibles sont chiffrées lorsqu’elles sont envoyées sur hello internet. Il assure la confiance et l’authentification, mais protège également vos applications web contre les attaques. Actuellement, Azure CDN prend en charge HTTPS sur un point de terminaison CDN. Ainsi, si vous créez un point de terminaison CDN à partir d’Azure CDN (par exemple, https://contoso.azureedge.net), HTTPS est activé par défaut. Désormais, avec HTTPS sur votre domaine personnalisé, vous pouvez également activer la fourniture sécurisée pour un domaine personnalisé (par exemple, https://www.contoso.com). 

Certains des attributs de clé hello de fonctionnalité HTTPS sont :

- Aucun coût supplémentaire : l’acquisition ou le renouvellement de certificat n’entraîne aucun coût supplémentaire, tout comme le trafic HTTPS. Vous payez uniquement pour les sorties Go à partir de hello CDN.

- L’activation du simple : cliquez sur un l'approvisionnement est disponible à partir de hello [portail Azure](https://portal.azure.com). Vous pouvez également utiliser l’API REST ou autre fonctionnalité de hello tooenable developer tools.

- Gestion complète de certificats : l’approvisionnement et la gestion de tous les certificats sont assurés pour vous. Les certificats sont automatiquement configurés et renouvellement tooexpiration préalable. Cette opération supprime complètement risques hello d’interruption de service à la suite d’une expiration du certificat.

>[!NOTE] 
>Tooenabling préalable support HTTPS, vous devez avoir déjà établi un [domaine Azure CDN personnalisé](./cdn-map-content-to-custom-domain.md).

## <a name="step-1-enabling-hello-feature"></a>Étape 1 : Activer la fonctionnalité de hello 

1. Bonjour [portail Azure](https://portal.azure.com), recherchez le profil CDN tooyour Verizon standard ou premium.

2. Dans hello de points de terminaison, cliquez sur le point de terminaison hello contenant votre domaine personnalisé.

3. Cliquez sur le domaine personnalisé de hello pour lequel vous souhaitez tooenable HTTPS.

    ![Panneau Point de terminaison](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. Cliquez sur **sur** tooenable HTTPS, puis enregistrez les modifications hello.

    ![Boîte de dialogue HTTPS personnalisé](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a>Étape 2 : Validation du domaine

>[!IMPORTANT] 
>Vous devez effectuer la validation de domaine avant que le protocole HTTPS soit activé sur votre domaine personnalisé. Vous avez 6 jours tooapprove hello domaine. La demande sera annulée si aucune approbation n’intervient dans ce délai.  

Après l’activation de HTTPS sur votre domaine personnalisé, notre fournisseur du certificat HTTPS DigiCert validera la propriété de votre domaine en contactant un abonné de hello pour votre domaine, en fonction des informations d’abonné WHOIS, par courrier électronique (par défaut) ou par téléphone. DigiCert envoie également toohello de courrier électronique de vérification hello adresses suivantes. Si les informations sur l’inscrit whois sont privées, vérifiez que vous pouvez effectuer directement l’approbation à partir de ces adresses.

>admin@<votre-nom-de-domaine.com> administrator@<votre-nom-de-domaine.com>  
>webmaster@<votre-nom-de-domaine.com>  
>hostmaster@<votre-nom-de-domaine.com>  
>postmaster@<votre-nom-de-domaine.com>


Lors de la réception de courrier électronique de hello, vous avez deux options de vérification :

1. Vous pouvez approuver toutes les futures commandes placées via hello même compte pour hello même domaine racine, par exemple, consoto.com. Cette approche est recommandée si vous envisagez de domaines personnalisés supplémentaires de tooadd Bonjour future pour hello même domaine racine.
 
2. Vous pouvez simplement l’approuver nom d’hôte spécifique hello utilisée dans cette demande. L’approbation supplémentaire sera nécessaire pour les demandes suivantes.

    Exemple d’e-mail :
    
    ![Boîte de dialogue HTTPS personnalisé](./media/cdn-custom-ssl/domain-validation-email-example.png)

Après l’approbation, DigiCert ajouterez votre certificat de SAN de toohello de nom de domaine personnalisé. certificat de Hello est valide pendant un an et sera automatiquement renouvelé avant qu’il a expiré.

## <a name="step-3-wait-for-hello-propagation-then-start-using-your-feature"></a>Étape 3 : Attendez que la propagation hello puis démarrer à l’aide de la fonction

Après la validation de nom de domaine hello il occupera too6-8 heures pour la fonctionnalité hello domaine personnalisé HTTPS toobe active. Une fois hello est terminée, l’état « HTTPS personnalisé » hello Bonjour portail Azure est défini trop « activé ». Le protocole HTTPS avec votre domaine personnalisé est maintenant prêt à l’emploi.

## <a name="frequently-asked-questions"></a>Forum Aux Questions

1. *Qui est le fournisseur de certificats hello et le type de certificat est utilisé ?*

    Nous utilisons le certificat SAN (Subject Alternative Names) fourni par DigiCert. Un certificat SAN peut sécuriser plusieurs noms de domaine qualifiés complets avec un certificat.

2. *Puis-je utiliser mon certificat dédié ?*
    
    Pas actuellement, mais son on hello feuille de route.

3. *Que se passe-t-il si je ne plus recevoir par courrier électronique de vérification de domaine hello de DigiCert ?*

    Contactez Microsoft si vous ne recevez pas l’e-mail dans les 24 heures.

4. *Un certificat SAN est-il moins sécurisé qu’un certificat dédié ?*
    
    Un certificat SAN suit hello mêmes normes de chiffrement et de sécurité comme un certificat dédié. Tous les certificats SSL émis utilisent la norme SHA-256 pour une sécurité améliorée du serveur.

5. *Puis-je utiliser le protocole HTTPS de domaine personnalisé avec Azure CDN Akamai ?*

    Actuellement, cette fonctionnalité est uniquement disponible avec Azure CDN Verizon. Nous travaillons sur la prise en charge de cette fonctionnalité avec le CDN Azure à partir d’Akamai dans les mois à venir hello.


## <a name="next-steps"></a>Étapes suivantes

- Découvrez comment tooset d’un [domaine personnalisé sur votre point de terminaison CDN Azure](./cdn-map-content-to-custom-domain.md)


