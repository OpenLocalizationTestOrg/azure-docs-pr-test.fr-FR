---
title: "aaaReliable sérialisation des objets de Collection dans Azure Service Fabric | Documents Microsoft"
description: "Sérialisation des objets Reliable Collections dans Azure Service Fabric"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 9d35374c-2d75-4856-b776-e59284641956
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/8/2017
ms.author: mcoskun
ms.openlocfilehash: 248defbe0ae6f65b4ac5dc7c74e80d8f1152ce94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a><span data-ttu-id="c62ce-103">Sérialisation des objets Reliable Collections dans Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c62ce-103">Reliable Collection object serialization in Azure Service Fabric</span></span>
<span data-ttu-id="c62ce-104">Collections de fiable répliquent et conserver leur toomake éléments assurer qu’ils sont durables entre l’ordinateur et les pannes de courant.</span><span class="sxs-lookup"><span data-stu-id="c62ce-104">Reliable Collections' replicate and persist their items toomake sure they are durable across machine failures and power outages.</span></span>
<span data-ttu-id="c62ce-105">Éléments tooreplicate et toopersist, tooserialize besoin de Collections fiable les.</span><span class="sxs-lookup"><span data-stu-id="c62ce-105">Both tooreplicate and toopersist items, Reliable Collections' need tooserialize them.</span></span>

<span data-ttu-id="c62ce-106">Collections fiable obtenir le sérialiseur approprié de hello pour un type donné à partir du Gestionnaire d’état fiable.</span><span class="sxs-lookup"><span data-stu-id="c62ce-106">Reliable Collections' get hello appropriate serializer for a given type from Reliable State Manager.</span></span>
<span data-ttu-id="c62ce-107">Gestionnaire d’état de Reliable contient les sérialiseurs intégrés et permet des sérialiseurs personnalisés toobe enregistré pour un type donné.</span><span class="sxs-lookup"><span data-stu-id="c62ce-107">Reliable State Manager contains built-in serializers and allows custom serializers toobe registered for a given type.</span></span>

## <a name="built-in-serializers"></a><span data-ttu-id="c62ce-108">Sérialiseurs intégrés</span><span class="sxs-lookup"><span data-stu-id="c62ce-108">Built-in Serializers</span></span>

<span data-ttu-id="c62ce-109">Reliable State Manager intègre un sérialiseur qui est utilisé pour certains types courants de manière à garantir par défaut une sérialisation efficace.</span><span class="sxs-lookup"><span data-stu-id="c62ce-109">Reliable State Manager includes built-in serializer for some common types, so that they can be serialized efficiently by default.</span></span> <span data-ttu-id="c62ce-110">Pour les autres types, gestionnaire d’état fiable revient toouse hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="c62ce-110">For other types, Reliable State Manager falls back toouse hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span></span>
<span data-ttu-id="c62ce-111">Sérialiseurs intégrés ne sont plus efficaces, car ils savent leurs types ne peuvent pas modifier et tooinclude les informations de type hello comme son nom de type n’a pas besoin.</span><span class="sxs-lookup"><span data-stu-id="c62ce-111">Built-in serializers are more efficient since they know their types cannot change and they do not need tooinclude information about hello type like its type name.</span></span>

<span data-ttu-id="c62ce-112">Reliable State Manager intègre un sérialiseur pour les types suivants :</span><span class="sxs-lookup"><span data-stu-id="c62ce-112">Reliable State Manager has built-in serializer for following types:</span></span> 
- <span data-ttu-id="c62ce-113">Guid</span><span class="sxs-lookup"><span data-stu-id="c62ce-113">Guid</span></span>
- <span data-ttu-id="c62ce-114">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="c62ce-114">bool</span></span>
- <span data-ttu-id="c62ce-115">byte</span><span class="sxs-lookup"><span data-stu-id="c62ce-115">byte</span></span>
- <span data-ttu-id="c62ce-116">sbyte</span><span class="sxs-lookup"><span data-stu-id="c62ce-116">sbyte</span></span>
- <span data-ttu-id="c62ce-117">byte[]</span><span class="sxs-lookup"><span data-stu-id="c62ce-117">byte[]</span></span>
- <span data-ttu-id="c62ce-118">char</span><span class="sxs-lookup"><span data-stu-id="c62ce-118">char</span></span>
- <span data-ttu-id="c62ce-119">string</span><span class="sxs-lookup"><span data-stu-id="c62ce-119">string</span></span>
- <span data-ttu-id="c62ce-120">décimal</span><span class="sxs-lookup"><span data-stu-id="c62ce-120">decimal</span></span>
- <span data-ttu-id="c62ce-121">double</span><span class="sxs-lookup"><span data-stu-id="c62ce-121">double</span></span>
- <span data-ttu-id="c62ce-122">float</span><span class="sxs-lookup"><span data-stu-id="c62ce-122">float</span></span>
- <span data-ttu-id="c62ce-123">int</span><span class="sxs-lookup"><span data-stu-id="c62ce-123">int</span></span>
- <span data-ttu-id="c62ce-124">uint</span><span class="sxs-lookup"><span data-stu-id="c62ce-124">uint</span></span>
- <span data-ttu-id="c62ce-125">long</span><span class="sxs-lookup"><span data-stu-id="c62ce-125">long</span></span>
- <span data-ttu-id="c62ce-126">ulong</span><span class="sxs-lookup"><span data-stu-id="c62ce-126">ulong</span></span>
- <span data-ttu-id="c62ce-127">short</span><span class="sxs-lookup"><span data-stu-id="c62ce-127">short</span></span>
- <span data-ttu-id="c62ce-128">ushort</span><span class="sxs-lookup"><span data-stu-id="c62ce-128">ushort</span></span>

## <a name="custom-serialization"></a><span data-ttu-id="c62ce-129">Sérialisation personnalisée</span><span class="sxs-lookup"><span data-stu-id="c62ce-129">Custom Serialization</span></span>

<span data-ttu-id="c62ce-130">Sérialiseurs personnalisés sont couramment utilisés tooincrease performances ou tooencrypt des données hello acheminement hello et sur le disque.</span><span class="sxs-lookup"><span data-stu-id="c62ce-130">Custom serializers are commonly used tooincrease performance or tooencrypt hello data over hello wire and on disk.</span></span> <span data-ttu-id="c62ce-131">Parmi les autres raisons, des sérialiseurs personnalisés sont généralement plus efficaces que le sérialiseur générique, car ils n’avez pas besoin d’informations sur le type de hello tooserialize.</span><span class="sxs-lookup"><span data-stu-id="c62ce-131">Among other reasons, custom serializers are commonly more efficient than generic serializer since they don't need tooserialize information about hello type.</span></span> 

<span data-ttu-id="c62ce-132">[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) est tooregister utilisé un sérialiseur personnalisé pour hello reçoit le type T. Cet enregistrement doit se produire dans la construction de hello de hello StatefulServiceBase tooensure que, avant le début de la récupération, toutes les Collections fiables ont accès toohello sérialiseur approprié tooread leurs données persistantes.</span><span class="sxs-lookup"><span data-stu-id="c62ce-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) is used tooregister a custom serializer for hello given type T. This registration should happen in hello construction of hello StatefulServiceBase tooensure that before recovery starts, all Reliable Collections have access toohello relevant serializer tooread their persisted data.</span></span>

```C#
public StatefulBackendService(StatefulServiceContext context)
  : base(context)
  {
    if (!this.StateManager.TryAddStateSerializer(new OrderKeySerializer()))
    {
      throw new InvalidOperationException("Failed tooset OrderKey custom serializer");
    }
  }
```

> [!NOTE]
> <span data-ttu-id="c62ce-133">Les sérialiseurs personnalisés prévalent sur les sérialiseurs intégrés.</span><span class="sxs-lookup"><span data-stu-id="c62ce-133">Custom serializers are given precedence over built-in serializers.</span></span> <span data-ttu-id="c62ce-134">Par exemple, lorsqu’un sérialiseur personnalisé pour int est inscrite, elle est entiers tooserialize utilisé au lieu de sérialiseur intégré de hello pour int.</span><span class="sxs-lookup"><span data-stu-id="c62ce-134">For example, when a custom serializer for int is registered, it is used tooserialize integers instead of hello built-in serializer for int.</span></span>

### <a name="how-tooimplement-a-custom-serializer"></a><span data-ttu-id="c62ce-135">Comment tooimplement un sérialiseur personnalisé</span><span class="sxs-lookup"><span data-stu-id="c62ce-135">How tooimplement a custom serializer</span></span>

<span data-ttu-id="c62ce-136">Un sérialiseur personnalisé doit tooimplement hello [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span><span class="sxs-lookup"><span data-stu-id="c62ce-136">A custom serializer needs tooimplement hello [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span></span>

> [!NOTE]
> <span data-ttu-id="c62ce-137">IStateSerializer<T> inclut une surcharge d’écriture et de lecture qui prend une valeur de base T supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="c62ce-137">IStateSerializer<T> includes an overload for Write and Read that takes in an additional T called base value.</span></span> <span data-ttu-id="c62ce-138">Cette API s’applique à la sérialisation différentielle.</span><span class="sxs-lookup"><span data-stu-id="c62ce-138">This API is for differential serialization.</span></span> <span data-ttu-id="c62ce-139">La fonctionnalité de sérialisation différentielle n’est pas exposée pour le moment.</span><span class="sxs-lookup"><span data-stu-id="c62ce-139">Currently differential serialization feature is not exposed.</span></span> <span data-ttu-id="c62ce-140">Par conséquent, ces deux surcharges ne sont pas appelées tant que la sérialisation différentielle n’est pas exposée et activée.</span><span class="sxs-lookup"><span data-stu-id="c62ce-140">Hence, these two overloads are not called until differential serialization is exposed and enabled.</span></span>

<span data-ttu-id="c62ce-141">Voici un exemple de type personnalisé appelé OrderKey qui contient quatre propriétés</span><span class="sxs-lookup"><span data-stu-id="c62ce-141">Following is an example custom type called OrderKey that contains four properties</span></span>

```C#
public class OrderKey : IComparable<OrderKey>, IEquatable<OrderKey>
{
    public byte Warehouse { get; set; }

    public short District { get; set; }

    public int Customer { get; set; }

    public long Order { get; set; }

    #region Object Overrides for GetHashCode, CompareTo and Equals
    #endregion
}
```

<span data-ttu-id="c62ce-142">Voici un exemple d’implémentation de IStateSerializer<OrderKey>.</span><span class="sxs-lookup"><span data-stu-id="c62ce-142">Following is an example implementation of IStateSerializer<OrderKey>.</span></span>
<span data-ttu-id="c62ce-143">Notez que les surcharges de lecture et d’écriture qui prennent la valeur de base (baseValue) appellent leur surcharge respective pour assurer la compatibilité en aval.</span><span class="sxs-lookup"><span data-stu-id="c62ce-143">Note that Read and Write overloads that take in baseValue, call their respective overload for forwards compatibility.</span></span>

```C#
public class OrderKeySerializer : IStateSerializer<OrderKey>
{
  OrderKey IStateSerializer<OrderKey>.Read(BinaryReader reader)
  {
      var value = new OrderKey();
      value.Warehouse = reader.ReadByte();
      value.District = reader.ReadInt16();
      value.Customer = reader.ReadInt32();
      value.Order = reader.ReadInt64();

      return value;
  }

  void IStateSerializer<OrderKey>.Write(OrderKey value, BinaryWriter writer)
  {
      writer.Write(value.Warehouse);
      writer.Write(value.District);
      writer.Write(value.Customer);
      writer.Write(value.Order);
  }
  
  // Read overload for differential de-serialization
  OrderKey IStateSerializer<OrderKey>.Read(OrderKey baseValue, BinaryReader reader)
  {
      return ((IStateSerializer<OrderKey>)this).Read(reader);
  }

  // Write overload for differential serialization
  void IStateSerializer<OrderKey>.Write(OrderKey baseValue, OrderKey newValue, BinaryWriter writer)
  {
      ((IStateSerializer<OrderKey>)this).Write(newValue, writer);
  }
}
```

## <a name="upgradability"></a><span data-ttu-id="c62ce-144">Mise à niveau</span><span class="sxs-lookup"><span data-stu-id="c62ce-144">Upgradability</span></span>
<span data-ttu-id="c62ce-145">Dans un [application mise à niveau propagée](service-fabric-application-upgrade.md), mise à niveau hello est appliqué tooa sous-ensemble de nœuds, un seul domaine de mise à niveau à la fois.</span><span class="sxs-lookup"><span data-stu-id="c62ce-145">In a [rolling application upgrade](service-fabric-application-upgrade.md), hello upgrade is applied tooa subset of nodes, one upgrade domain at a time.</span></span> <span data-ttu-id="c62ce-146">Pendant ce processus, certains domaines de mise à niveau sera sur une version plus récente de hello de votre application, et certains domaines de mise à niveau sera hello ancienne version de votre application.</span><span class="sxs-lookup"><span data-stu-id="c62ce-146">During this process, some upgrade domains will be on hello newer version of your application, and some upgrade domains will be on hello older version of your application.</span></span> <span data-ttu-id="c62ce-147">Lors du déploiement hello, hello nouvelle version de votre application doit être en mesure de tooread hello ancienne version de vos données et hello ancienne version de votre application doit être en mesure de tooread hello nouvelle version de vos données.</span><span class="sxs-lookup"><span data-stu-id="c62ce-147">During hello rollout, hello new version of your application must be able tooread hello old version of your data, and hello old version of your application must be able tooread hello new version of your data.</span></span> <span data-ttu-id="c62ce-148">Si le format de données hello n’est pas mise à niveau vers l’avant et vers l’arrière compatible, hello peuvent échouer ou pire, de données peut être perdue ou corrompue.</span><span class="sxs-lookup"><span data-stu-id="c62ce-148">If hello data format is not forward and backward compatible, hello upgrade may fail, or worse, data may be lost or corrupted.</span></span>

<span data-ttu-id="c62ce-149">Si vous utilisez le sérialiseur intégré, vous n’avez pas tooworry sur la compatibilité.</span><span class="sxs-lookup"><span data-stu-id="c62ce-149">If you are using  built-in serializer, you do not have tooworry about compatibility.</span></span>
<span data-ttu-id="c62ce-150">Toutefois, si vous utilisez un sérialiseur personnalisé ou un hello DataContractSerializer, les données de salutation ont toobe vers l’arrière à l’infini et transfère compatibles.</span><span class="sxs-lookup"><span data-stu-id="c62ce-150">However, if you are using a custom serializer or hello DataContractSerializer, hello data have toobe infinitely backwards and forwards compatible.</span></span>
<span data-ttu-id="c62ce-151">En d’autres termes, chaque version du sérialiseur doit tooserialize en mesure de toobe et désérialiser sur n’importe quelle version du type de hello.</span><span class="sxs-lookup"><span data-stu-id="c62ce-151">In other words, each version of serializer needs toobe able tooserialize and de-serialize any version of hello type.</span></span>

<span data-ttu-id="c62ce-152">Les utilisateurs de contrat de données doivent suivre les règles de contrôle de version bien défini de hello pour ajout, suppression et modification des champs.</span><span class="sxs-lookup"><span data-stu-id="c62ce-152">Data Contract users should follow hello well-defined versioning rules for adding, removing, and changing fields.</span></span> <span data-ttu-id="c62ce-153">Contrat de données est également prise en charge de traitement avec des champs inconnus, se connecter à un processus de sérialisation et désérialisation hello et de gestion d’héritage de classe.</span><span class="sxs-lookup"><span data-stu-id="c62ce-153">Data Contract also has support for dealing with unknown fields, hooking into hello serialization and deserialization process, and dealing with class inheritance.</span></span> <span data-ttu-id="c62ce-154">Pour plus d'informations, consultez la page [Utilisation du contrat de données](https://msdn.microsoft.com/library/ms733127.aspx).</span><span class="sxs-lookup"><span data-stu-id="c62ce-154">For more information, see [Using Data Contract](https://msdn.microsoft.com/library/ms733127.aspx).</span></span>

<span data-ttu-id="c62ce-155">Les utilisateurs de sérialiseur personnalisé doivent respecter les instructions de toohello du sérialiseur hello qu’ils utilisent toomake qu’il est en arrière et compatible avec.</span><span class="sxs-lookup"><span data-stu-id="c62ce-155">Custom serializer users should adhere toohello guidelines of hello serializer they are using toomake sure it is backwards and forwards compatible.</span></span>
<span data-ttu-id="c62ce-156">Une méthode courante de prendre en charge toutes les versions consiste à ajouter les informations de taille au début de hello et ajoutez uniquement des propriétés facultatives.</span><span class="sxs-lookup"><span data-stu-id="c62ce-156">Common way of supporting all versions is adding size information at hello beginning and only adding optional properties.</span></span>
<span data-ttu-id="c62ce-157">De cette manière, chaque version peut lire autant pouvoir et passer sur la partie restante de hello du flux de hello.</span><span class="sxs-lookup"><span data-stu-id="c62ce-157">This way each version can read as much it can and jump over hello remaining part of hello stream.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c62ce-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c62ce-158">Next steps</span></span>
  * [<span data-ttu-id="c62ce-159">Sérialisation et mise à niveau</span><span class="sxs-lookup"><span data-stu-id="c62ce-159">Serialization and upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="c62ce-160">Référence du développeur pour les Collections fiables</span><span class="sxs-lookup"><span data-stu-id="c62ce-160">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * <span data-ttu-id="c62ce-161">[mise à niveau de votre application à l’aide de Visual Studio](service-fabric-application-upgrade-tutorial.md) vous guide à travers une mise à niveau de l’application à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c62ce-161">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>
  * <span data-ttu-id="c62ce-162">[mise à niveau de votre application à l’aide de PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) vous guide à travers une mise à niveau de l’application à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c62ce-162">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>
  * <span data-ttu-id="c62ce-163">Contrôlez les mises à niveau de votre application à l'aide des [Paramètres de mise à niveau](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="c62ce-163">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>
  * <span data-ttu-id="c62ce-164">Découvrez comment toouse des fonctionnalités avancées lors de la mise à niveau de votre application en vous reportant trop[rubriques avancées](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="c62ce-164">Learn how toouse advanced functionality while upgrading your application by referring too[Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
  * <span data-ttu-id="c62ce-165">Résoudre les problèmes courants dans les mises à niveau de l’application en faisant référence à des étapes de toohello de [résolution des problèmes de mises à niveau Application](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="c62ce-165">Fix common problems in application upgrades by referring toohello steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
