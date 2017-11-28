---
title: "Présentation du modèle de licence PlayReady de Media Services"
description: "Cette rubrique donne un aperçu d’un modèle de licence PlayReady utilisé pour configurer des licences PlayReady."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: fddce5d0-1278-478f-ae05-9b985c748731
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: be19f616e36916655390cd05e738e93c08dcdf68
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="media-services-playready-license-template-overview"></a><span data-ttu-id="faa77-103">Présentation du modèle de licence PlayReady de Media Services</span><span class="sxs-lookup"><span data-stu-id="faa77-103">Media Services PlayReady license template overview</span></span>
<span data-ttu-id="faa77-104">Azure Media Services fournit à présent un service pour la distribution de licences Microsoft PlayReady.</span><span class="sxs-lookup"><span data-stu-id="faa77-104">Azure Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="faa77-105">Lorsque le lecteur de l’utilisateur final (par exemple Silverlight) tente de lire votre contenu PlayReady protégé, une demande est envoyée au service de remise de licence pour obtenir une licence.</span><span class="sxs-lookup"><span data-stu-id="faa77-105">When the end user player (for example, Silverlight) tries to play your PlayReady protected content, a request is sent to the license delivery service to obtain a license.</span></span> <span data-ttu-id="faa77-106">Si le service de licence approuve la demande, il émet la licence, qui est envoyée au client et peut être utilisée pour déchiffrer et lire le contenu spécifié.</span><span class="sxs-lookup"><span data-stu-id="faa77-106">If the license service approves the request, it issues the license which is sent to the client and can be used to decrypt and play the specified content.</span></span>

<span data-ttu-id="faa77-107">Media Services propose également des API qui vous permettent de configurer vos licences PlayReady.</span><span class="sxs-lookup"><span data-stu-id="faa77-107">Media Services also provides APIs that let you configure your PlayReady licenses.</span></span> <span data-ttu-id="faa77-108">Les licences contiennent les droits et les restrictions que vous souhaitez pour le runtime DRM PlayReady, qui s’appliquent lorsqu’un utilisateur tente de lire du contenu protégé.</span><span class="sxs-lookup"><span data-stu-id="faa77-108">Licenses contain the rights and restrictions that you want for the PlayReady DRM runtime to enforce when a user is trying to playback protected content.</span></span>
<span data-ttu-id="faa77-109">Voici quelques exemples des restrictions de licences PlayReady que vous pouvez spécifier :</span><span class="sxs-lookup"><span data-stu-id="faa77-109">Below are some examples of PlayReady license restrictions that you can specify:</span></span>

* <span data-ttu-id="faa77-110">La valeur DateTime à partir de laquelle la licence est valide.</span><span class="sxs-lookup"><span data-stu-id="faa77-110">The DateTime from which the license is valid.</span></span>
* <span data-ttu-id="faa77-111">La valeur DateTime à laquelle la licence expire.</span><span class="sxs-lookup"><span data-stu-id="faa77-111">The DateTime value when the license expires.</span></span> 
* <span data-ttu-id="faa77-112">Pour que la licence soit enregistrée dans un stockage persistant sur le client.</span><span class="sxs-lookup"><span data-stu-id="faa77-112">For the license to be saved in persistent storage on the client.</span></span> <span data-ttu-id="faa77-113">Les licences persistantes servent généralement à autoriser la lecture hors connexion du contenu.</span><span class="sxs-lookup"><span data-stu-id="faa77-113">Persistent licenses are typically used to allow offline playback of the content.</span></span>
* <span data-ttu-id="faa77-114">Le niveau de sécurité minimal qu'un lecteur doit avoir pour pouvoir lire votre contenu.</span><span class="sxs-lookup"><span data-stu-id="faa77-114">The minimum security level that a player must have to play your content.</span></span> 
* <span data-ttu-id="faa77-115">Le niveau de protection de sortie des contrôles de sortie pour du contenu audio/vidéo.</span><span class="sxs-lookup"><span data-stu-id="faa77-115">The output protection level for the output controls for audio\video content.</span></span> 
* <span data-ttu-id="faa77-116">Pour plus d'informations, consultez la section Contrôles de sortie (3.5) dans le document [Règles de conformité PlayReady](https://www.microsoft.com/playready/licensing/compliance/) .</span><span class="sxs-lookup"><span data-stu-id="faa77-116">For more information, see the Output Controls section (3.5) in the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>

> [!NOTE]
> <span data-ttu-id="faa77-117">Actuellement, vous pouvez uniquement configurer le droit de lecture de la licence PlayReady (ce droit est requis).</span><span class="sxs-lookup"><span data-stu-id="faa77-117">Currently, you can only configure the PlayRight of the PlayReady license (this right is required).</span></span> <span data-ttu-id="faa77-118">Le droit de lecture permet au client de lire le contenu.</span><span class="sxs-lookup"><span data-stu-id="faa77-118">The PlayRight gives the client the ability to playback the content.</span></span> <span data-ttu-id="faa77-119">Il permet également de configurer les restrictions spécifiques à la lecture.</span><span class="sxs-lookup"><span data-stu-id="faa77-119">The PlayRight also allows configuring restrictions specific to playback.</span></span> <span data-ttu-id="faa77-120">Pour plus d'informations, consultez [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span><span class="sxs-lookup"><span data-stu-id="faa77-120">For more information, see [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span></span>
> 
> 

<span data-ttu-id="faa77-121">Pour configurer des licences PlayReady à l'aide de Media Services, vous devez configurer le modèle de licence PlayReady de Media Services.</span><span class="sxs-lookup"><span data-stu-id="faa77-121">To configure PlayReady licenses using Media Services, you must configure the Media Services PlayReady license template.</span></span> <span data-ttu-id="faa77-122">Ce modèle est défini en XML.</span><span class="sxs-lookup"><span data-stu-id="faa77-122">The template is defined in XML.</span></span>

<span data-ttu-id="faa77-123">L'exemple ci-dessous illustre le modèle le plus simple (et le plus utilisé) pour configurer une licence de diffusion en continu de base.</span><span class="sxs-lookup"><span data-stu-id="faa77-123">The following example shows the simplest (and most common) template that configures a basic streaming license.</span></span> <span data-ttu-id="faa77-124">Avec cette licence, vos clients seraient en mesure de lire votre contenu protégé par PlayReady.</span><span class="sxs-lookup"><span data-stu-id="faa77-124">With this license, your clients would be able to playback your PlayReady protected content.</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" 
                                      xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1">
      <LicenseTemplates>
        <PlayReadyLicenseTemplate>
          <ContentKey i:type="ContentEncryptionKeyFromHeader" />
          <PlayRight />
        </PlayReadyLicenseTemplate>
      </LicenseTemplates>
    </PlayReadyLicenseResponseTemplate>

<span data-ttu-id="faa77-125">Le code XML est conforme au schéma XML de modèle de licence PlayReady défini dans la section Schéma XML de modèle de licence PlayReady.</span><span class="sxs-lookup"><span data-stu-id="faa77-125">The XML conforms to the PlayReady license template XML schema defined in the PlayReady license template XML schema section.</span></span>

<span data-ttu-id="faa77-126">Media Services définit également un ensemble de classes .NET susceptibles d'être utilisées pour sérialiser et désérialiser à destination et à partir du code XML.</span><span class="sxs-lookup"><span data-stu-id="faa77-126">Media Services also defines a set of .NET classes that could be used to serialized and deserialized to and from the XML.</span></span> <span data-ttu-id="faa77-127">Pour obtenir une description des classes principales, consultez les [classes .NET de Media Services](media-services-playready-license-template-overview.md#classes)</span><span class="sxs-lookup"><span data-stu-id="faa77-127">For description of main classes, see [Media Services .NET classes](media-services-playready-license-template-overview.md#classes).</span></span> <span data-ttu-id="faa77-128">qui permettent de configurer des modèles de licence.</span><span class="sxs-lookup"><span data-stu-id="faa77-128">that are used to configure license templates.</span></span>

<span data-ttu-id="faa77-129">Pour obtenir un exemple de bout en bout utilisant les classes .NET pour configurer le modèle de licence PlayReady, consultez [Utilisation du chiffrement dynamique et du service de fourniture de licence PlayReady](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="faa77-129">For an end-to-end example that uses .NET classes to configure the PlayReady license template, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span></span>

## <span data-ttu-id="faa77-130"><a id="classes"></a>Classes .NET de Media Services permettant de configurer des modèles de licence</span><span class="sxs-lookup"><span data-stu-id="faa77-130"><a id="classes"></a>Media Services .NET classes that are used to configure license templates</span></span>
<span data-ttu-id="faa77-131">Les classes .NET principales utilisées pour configurer des modèles de licence Media Services PlayReady sont répertoriées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="faa77-131">The following are the main .NET classes are used to configure Media Services PlayReady license templates.</span></span> <span data-ttu-id="faa77-132">Ces classes correspondent aux types définis dans [Schéma XML de modèle de licence PlayReady](media-services-playready-license-template-overview.md#schema).</span><span class="sxs-lookup"><span data-stu-id="faa77-132">These classes map to the types defined in [PlayReady license template XML schema](media-services-playready-license-template-overview.md#schema).</span></span>

<span data-ttu-id="faa77-133">La classe [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) permet de sérialiser et de désérialiser à destination et à partir du code XML de modèle de licence Media Services.</span><span class="sxs-lookup"><span data-stu-id="faa77-133">The [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) class is used to serialize and deserialize to and from the Media Services license template XML.</span></span>

### <a name="playreadylicenseresponsetemplate"></a><span data-ttu-id="faa77-134">PlayReadyLicenseResponseTemplate</span><span class="sxs-lookup"><span data-stu-id="faa77-134">PlayReadyLicenseResponseTemplate</span></span>
<span data-ttu-id="faa77-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) : Cette classe représente le modèle pour la réponse retournée à l'utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="faa77-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) - This class represents the template for the response sent back to the end user.</span></span> <span data-ttu-id="faa77-136">Elle contient un champ pour une chaîne de données personnalisée entre le serveur de licences et l'application (peut être utile pour la logique d'application personnalisée), ainsi qu'une liste d'un ou plusieurs modèles de licence.</span><span class="sxs-lookup"><span data-stu-id="faa77-136">It contains a field for a custom data string between the license server and the application (may be useful for custom app logic) as well as a list of one or more license templates.</span></span>

<span data-ttu-id="faa77-137">Il s'agit de la classe « de niveau supérieur » dans la hiérarchie des modèles.</span><span class="sxs-lookup"><span data-stu-id="faa77-137">This is the “top level” class in the template hierarchy.</span></span> <span data-ttu-id="faa77-138">Cela signifie que le modèle de réponse inclut une liste de modèles de licence et que les modèles de licence incluent (directement ou indirectement) toutes les autres classes qui composent les données de modèle à sérialiser.</span><span class="sxs-lookup"><span data-stu-id="faa77-138">Meaning that the response template includes a list of license templates and the license templates include (directly or indirectly) all of the other classes that make up the template data to be serialized.</span></span>

### <a name="playreadylicensetemplate"></a><span data-ttu-id="faa77-139">PlayReadyLicenseTemplate</span><span class="sxs-lookup"><span data-stu-id="faa77-139">PlayReadyLicenseTemplate</span></span>
<span data-ttu-id="faa77-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) : Cette classe représente un modèle de licence permettant de créer les licences PlayReady à retourner aux utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="faa77-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) - The class represents a license template for creating PlayReady licenses to be returned to the end users.</span></span> <span data-ttu-id="faa77-141">Elle contient les données relatives à la clé de contenu figurant dans la licence et à tous les droits ou restrictions qui doivent être appliqués par le runtime de gestion des droits numériques (DRM) PlayReady quand la clé de contenu est utilisée.</span><span class="sxs-lookup"><span data-stu-id="faa77-141">It contains the data on the content key in the license and any rights or restrictions to be enforced by the PlayReady DRM runtime when using the content key.</span></span>

### <span data-ttu-id="faa77-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span><span class="sxs-lookup"><span data-stu-id="faa77-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span></span>
<span data-ttu-id="faa77-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) : Cette classe représente le droit de lecture d'une licence PlayReady.</span><span class="sxs-lookup"><span data-stu-id="faa77-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) - This class represents the PlayRight of a PlayReady license.</span></span> <span data-ttu-id="faa77-144">Elle accorde à l'utilisateur la capacité de lire le contenu faisant l'objet de restrictions de niveau zéro ou supérieur, configurées dans la licence et sur le droit de lecture lui-même (pour la stratégie spécifique de lecture).</span><span class="sxs-lookup"><span data-stu-id="faa77-144">It grants the user the ability to playback the content subject to the zero or more restrictions configured in the license and on the PlayRight itself (for playback specific policy).</span></span> <span data-ttu-id="faa77-145">Une grande partie de la stratégie relative au droit de lecture se rapporte aux restrictions de sortie qui contrôlent les types de sortie utilisables pour la lecture du contenu, ainsi qu'aux restrictions qui doivent être mises en place quand une sortie donnée est utilisée.</span><span class="sxs-lookup"><span data-stu-id="faa77-145">Much of the policy on the PlayRight has to do with output restrictions which control the types of outputs that the content can be played over and any restrictions that must be put in place when using a given output.</span></span> <span data-ttu-id="faa77-146">Par exemple, si la restriction DigitalVideoOnlyContentRestriction est activée, le runtime DRM autorise uniquement l'affichage de la vidéo via des sorties numériques (les sorties vidéo analogiques ne sont pas autorisées à transmettre le contenu).</span><span class="sxs-lookup"><span data-stu-id="faa77-146">For example, if the DigitalVideoOnlyContentRestriction is enabled, then the DRM runtime will only allow the video to be displayed over digital outputs (analog video outputs won’t be allowed to pass the content).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="faa77-147">Ces types de restrictions peuvent être très puissants mais ils peuvent également affecter l'expérience des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="faa77-147">These types of restrictions can be very powerful but can also affect the consumer experience.</span></span> <span data-ttu-id="faa77-148">Si les protections de sortie sont configurées de manière trop restrictive, le contenu risque de ne pas pouvoir être lu sur certains clients.</span><span class="sxs-lookup"><span data-stu-id="faa77-148">If the output protections are configured too restrictive, the content might be unplayable on some clients.</span></span> <span data-ttu-id="faa77-149">Pour plus d’informations, consultez le document [Règles de conformité PlayReady](https://www.microsoft.com/playready/licensing/compliance/) .</span><span class="sxs-lookup"><span data-stu-id="faa77-149">For more information, see the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>
> 
> 

<span data-ttu-id="faa77-150">Pour obtenir un exemple des niveaux de protection que Silverlight prend charge, consultez [Protections de sortie prises en charge par Silverlight](http://go.microsoft.com/fwlink/?LinkId=617318).</span><span class="sxs-lookup"><span data-stu-id="faa77-150">For an example of what protection levels Silverlight supports, see: [Silverlight support for output protections](http://go.microsoft.com/fwlink/?LinkId=617318).</span></span>

## <span data-ttu-id="faa77-151"><a id="schema"></a>Schéma XML de modèle de licence PlayReady</span><span class="sxs-lookup"><span data-stu-id="faa77-151"><a id="schema"></a>PlayReady license template XML schema</span></span>
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:ser="http://schemas.microsoft.com/2003/10/Serialization/" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:import namespace="http://schemas.microsoft.com/2003/10/Serialization/" />
      <xs:complexType name="AgcAndColorStripeRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction" />
      <xs:simpleType name="ContentType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Unspecified" />
          <xs:enumeration value="UltravioletDownload" />
          <xs:enumeration value="UltravioletStreaming" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="ContentType" nillable="true" type="tns:ContentType" />
      <xs:complexType name="ExplicitAnalogTelevisionRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="BestEffort" type="xs:boolean" />
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ExplicitAnalogTelevisionRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction" />
      <xs:complexType name="PlayReadyContentKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="PlayReadyContentKey" nillable="true" type="tns:PlayReadyContentKey" />
      <xs:complexType name="ContentEncryptionKeyFromHeader">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence />
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromHeader" nillable="true" type="tns:ContentEncryptionKeyFromHeader" />
      <xs:complexType name="ContentEncryptionKeyFromKeyIdentifier">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence>
              <xs:element minOccurs="0" name="KeyIdentifier" type="ser:guid" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromKeyIdentifier" nillable="true" type="tns:ContentEncryptionKeyFromKeyIdentifier" />
      <xs:complexType name="PlayReadyLicenseResponseTemplate">
        <xs:sequence>
          <xs:element name="LicenseTemplates" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
          <xs:element minOccurs="0" name="ResponseCustomData" nillable="true" type="xs:string">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseResponseTemplate" nillable="true" type="tns:PlayReadyLicenseResponseTemplate" />
      <xs:complexType name="ArrayOfPlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfPlayReadyLicenseTemplate" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
      <xs:complexType name="PlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AllowTestDevices" type="xs:boolean" />
          <xs:element minOccurs="0" name="BeginDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element name="ContentKey" nillable="true" type="tns:PlayReadyContentKey" />
          <xs:element minOccurs="0" name="ContentType" type="tns:ContentType">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExpirationDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="GracePeriod" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="LicenseType" type="tns:PlayReadyLicenseType" />
          <xs:element minOccurs="0" name="PlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
      <xs:simpleType name="PlayReadyLicenseType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Nonpersistent" />
          <xs:enumeration value="Persistent" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="PlayReadyLicenseType" nillable="true" type="tns:PlayReadyLicenseType" />
      <xs:complexType name="PlayReadyPlayRight">
        <xs:sequence>
          <xs:element minOccurs="0" name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AllowPassingVideoContentToUnknownOutput" type="tns:UnknownOutputPassingOption">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AnalogVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="DigitalVideoOnlyContentRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExplicitAnalogTelevisionOutputRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="FirstPlayExpiration" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComponentVideoRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComputerMonitorRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyPlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
      <xs:simpleType name="UnknownOutputPassingOption">
        <xs:restriction base="xs:string">
          <xs:enumeration value="NotAllowed" />
          <xs:enumeration value="Allowed" />
          <xs:enumeration value="AllowedWithVideoConstriction" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="UnknownOutputPassingOption" nillable="true" type="tns:UnknownOutputPassingOption" />
      <xs:complexType name="ScmsRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction" />
    </xs:schema>



## <a name="media-services-learning-paths"></a><span data-ttu-id="faa77-152">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="faa77-152">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="faa77-153">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="faa77-153">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

