---
title: "vue d’ensemble de la stratégie aaaSSL pour la passerelle d’Application Azure | Documents Microsoft"
description: "En savoir plus sur la passerelle d’Application Azure vous permet de stratégie SSL de tooconfigure"
services: application gateway
documentationcenter: na
author: amsriva
manager: 
editor: 
tags: azure resource manager
ms.service: application gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure services
ms.date: 08/03/2017
ms.author: amsriva
ms.openlocfilehash: 80dbc437da3dba8a558c518ecdbb5927a11a2ed9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-ssl-policy-overview"></a>Vue d’ensemble de la stratégie SSL Application Gateway

Passerelle d’application vous permet de gestion des certificats SSL toocentralize et réduire les frais de chiffrement et le déchiffrement à partir d’une batterie de serveurs principaux. Cette SSL centralisée gère également vous permet de toospecify une SSL centrale stratégie adaptée aux exigences de sécurité de l’organisation tooyour. Cela vous aide à répondre aux exigences de conformité ainsi qu’aux instructions de sécurité et pratiques recommandées.

Stratégie SSL inclut un contrôle de version du protocole SSL, ainsi que les suites de chiffrement et ordre de hello chiffrements sont utilisés lors d’une négociation SSL. Dans cette Application Gateway offre de stratégie SSL de deux mécanismes tooallow clients toocontrol, prédéfini ou une stratégie personnalisée.

## <a name="predefined-ssl-policy"></a>Stratégie SSL prédéfinie

Application Gateway comporte trois stratégies de sécurité prédéfinies. Vous pouvez configurer votre passerelle avec un de ces stratégies tooget hello niveau de sécurité approprié. les noms de stratégie Hello sont annotées par année de hello et mois dans lequel ils ont été configurés. Chaque stratégie offre différentes versions de protocole SSL et de suites de chiffrement. Il est recommandé de toouse hello plus récent SSL stratégies tooensure hello meilleure sécurité SSL. Passerelle d’application aujourd'hui permet toochoose les utilisateurs à partir d’une des suivantes de hello prédéfinie.

### <a name="appgwsslpolicy20150501"></a>AppGwSslPolicy20150501

|Propriété  |Valeur  |
|---|---|
|Nom     | AppGwSslPolicy20150501        |
|MinProtocolVersion     | TLSv1_0        |
|Default| True (si aucune stratégie prédéfinie n’est spécifiée) |
|CipherSuites     |TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_DHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_DHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_DHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_DHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_RSA_WITH_AES_256_GCM_SHA384<br>TLS_RSA_WITH_AES_128_GCM_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA256<br>TLS_RSA_WITH_AES_128_CBC_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA<br>TLS_DHE_DSS_WITH_AES_256_CBC_SHA256<br>TLS_DHE_DSS_WITH_AES_128_CBC_SHA256<br>TLS_DHE_DSS_WITH_AES_256_CBC_SHA<br>TLS_DHE_DSS_WITH_AES_128_CBC_SHA<br>TLS_RSA_WITH_3DES_EDE_CBC_SHA<br>TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA |
  
  ### <a name="appgwsslpolicy20170401"></a>AppGwSslPolicy20170401
  
|Propriété  |Valeur  |
|   ---      |  ---       |
|Nom     | AppGwSslPolicy20170401        |
|MinProtocolVersion     | TLSv1_0        |
|Default| False |
|CipherSuites     |TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_256_GCM_SHA384<br>TLS_RSA_WITH_AES_128_GCM_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA256<br>TLS_RSA_WITH_AES_128_CBC_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_128_CBC_SHA |
  
### <a name="appgwsslpolicy20170401s"></a>AppGwSslPolicy20170401S

|Propriété  |Valeur  |
|---|---|
|Nom     | AppGwSslPolicy20170401        |
|MinProtocolVersion     | TLSv1_2        |
|Default| False |
|CipherSuites     |TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 <br>    TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 <br>    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA <br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA <br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_256_GCM_SHA384<br>TLS_RSA_WITH_AES_128_GCM_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA256<br>TLS_RSA_WITH_AES_128_CBC_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_128_CBC_SHA<br> |

## <a name="custom-ssl-policy"></a>Stratégie SSL personnalisée

Si une stratégie SSL prédéfinie doit toobe configuré pour vos besoins, vous avez doit définir votre propre stratégie SSL personnalisé. Dans ce cas, vous contrôlez totalement hello minimale SSL protocol version toosupport ainsi prise en charge des suites de chiffrement et de leur ordre de priorité.
 
Versions du protocole SSL :

* Les protocoles SSL 2.0 et 3.0 sont désactivés par défaut pour toutes les passerelles Application Gateway. Ces versions de protocole ne sont pas configurables.
* Personnalisé donne SSL de stratégie définition vous option tooselect l’un de hello suivant des trois protocoles en tant que version de protocole SSL minimale hello pour votre passerelle TLSv1_0, TLSv1_1, TLSv1_2.
* Si aucune stratégie SSL n’est définie, les trois protocoles (TLSv1_0, TLSv1_1, TLSv1_2) sont activés.

Suite de chiffrement :

Passerelle d’application prend en charge hello suivant des suites de chiffrement à partir de laquelle votre stratégie personnalisée peut être choisie. Hello classement hello des suites de chiffrement détermine les ordre de priorité hello pendant la négociation SSL.

Suites de chiffrement disponibles :

- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_256_GCM_SHA384
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_3DES_EDE_CBC_SHA
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

## <a name="next-steps"></a>Étapes suivantes

[Configure SSL policy on an application gateway](application-gateway-configure-ssl-policy-powershell.md) (Configurer la stratégie SSL sur une passerelle d’application)
