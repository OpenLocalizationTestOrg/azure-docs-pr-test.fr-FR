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
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a>Sérialisation des objets Reliable Collections dans Azure Service Fabric
Collections de fiable répliquent et conserver leur toomake éléments assurer qu’ils sont durables entre l’ordinateur et les pannes de courant.
Éléments tooreplicate et toopersist, tooserialize besoin de Collections fiable les.

Collections fiable obtenir le sérialiseur approprié de hello pour un type donné à partir du Gestionnaire d’état fiable.
Gestionnaire d’état de Reliable contient les sérialiseurs intégrés et permet des sérialiseurs personnalisés toobe enregistré pour un type donné.

## <a name="built-in-serializers"></a>Sérialiseurs intégrés

Reliable State Manager intègre un sérialiseur qui est utilisé pour certains types courants de manière à garantir par défaut une sérialisation efficace. Pour les autres types, gestionnaire d’état fiable revient toouse hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).
Sérialiseurs intégrés ne sont plus efficaces, car ils savent leurs types ne peuvent pas modifier et tooinclude les informations de type hello comme son nom de type n’a pas besoin.

Reliable State Manager intègre un sérialiseur pour les types suivants : 
- Guid
- valeur booléenne
- byte
- sbyte
- byte[]
- char
- string
- décimal
- double
- float
- int
- uint
- long
- ulong
- short
- ushort

## <a name="custom-serialization"></a>Sérialisation personnalisée

Sérialiseurs personnalisés sont couramment utilisés tooincrease performances ou tooencrypt des données hello acheminement hello et sur le disque. Parmi les autres raisons, des sérialiseurs personnalisés sont généralement plus efficaces que le sérialiseur générique, car ils n’avez pas besoin d’informations sur le type de hello tooserialize. 

[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) est tooregister utilisé un sérialiseur personnalisé pour hello reçoit le type T. Cet enregistrement doit se produire dans la construction de hello de hello StatefulServiceBase tooensure que, avant le début de la récupération, toutes les Collections fiables ont accès toohello sérialiseur approprié tooread leurs données persistantes.

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
> Les sérialiseurs personnalisés prévalent sur les sérialiseurs intégrés. Par exemple, lorsqu’un sérialiseur personnalisé pour int est inscrite, elle est entiers tooserialize utilisé au lieu de sérialiseur intégré de hello pour int.

### <a name="how-tooimplement-a-custom-serializer"></a>Comment tooimplement un sérialiseur personnalisé

Un sérialiseur personnalisé doit tooimplement hello [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.

> [!NOTE]
> IStateSerializer<T> inclut une surcharge d’écriture et de lecture qui prend une valeur de base T supplémentaire. Cette API s’applique à la sérialisation différentielle. La fonctionnalité de sérialisation différentielle n’est pas exposée pour le moment. Par conséquent, ces deux surcharges ne sont pas appelées tant que la sérialisation différentielle n’est pas exposée et activée.

Voici un exemple de type personnalisé appelé OrderKey qui contient quatre propriétés

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

Voici un exemple d’implémentation de IStateSerializer<OrderKey>.
Notez que les surcharges de lecture et d’écriture qui prennent la valeur de base (baseValue) appellent leur surcharge respective pour assurer la compatibilité en aval.

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

## <a name="upgradability"></a>Mise à niveau
Dans un [application mise à niveau propagée](service-fabric-application-upgrade.md), mise à niveau hello est appliqué tooa sous-ensemble de nœuds, un seul domaine de mise à niveau à la fois. Pendant ce processus, certains domaines de mise à niveau sera sur une version plus récente de hello de votre application, et certains domaines de mise à niveau sera hello ancienne version de votre application. Lors du déploiement hello, hello nouvelle version de votre application doit être en mesure de tooread hello ancienne version de vos données et hello ancienne version de votre application doit être en mesure de tooread hello nouvelle version de vos données. Si le format de données hello n’est pas mise à niveau vers l’avant et vers l’arrière compatible, hello peuvent échouer ou pire, de données peut être perdue ou corrompue.

Si vous utilisez le sérialiseur intégré, vous n’avez pas tooworry sur la compatibilité.
Toutefois, si vous utilisez un sérialiseur personnalisé ou un hello DataContractSerializer, les données de salutation ont toobe vers l’arrière à l’infini et transfère compatibles.
En d’autres termes, chaque version du sérialiseur doit tooserialize en mesure de toobe et désérialiser sur n’importe quelle version du type de hello.

Les utilisateurs de contrat de données doivent suivre les règles de contrôle de version bien défini de hello pour ajout, suppression et modification des champs. Contrat de données est également prise en charge de traitement avec des champs inconnus, se connecter à un processus de sérialisation et désérialisation hello et de gestion d’héritage de classe. Pour plus d'informations, consultez la page [Utilisation du contrat de données](https://msdn.microsoft.com/library/ms733127.aspx).

Les utilisateurs de sérialiseur personnalisé doivent respecter les instructions de toohello du sérialiseur hello qu’ils utilisent toomake qu’il est en arrière et compatible avec.
Une méthode courante de prendre en charge toutes les versions consiste à ajouter les informations de taille au début de hello et ajoutez uniquement des propriétés facultatives.
De cette manière, chaque version peut lire autant pouvoir et passer sur la partie restante de hello du flux de hello.

## <a name="next-steps"></a>Étapes suivantes
  * [Sérialisation et mise à niveau](service-fabric-application-upgrade-data-serialization.md)
  * [Référence du développeur pour les Collections fiables](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * [mise à niveau de votre application à l’aide de Visual Studio](service-fabric-application-upgrade-tutorial.md) vous guide à travers une mise à niveau de l’application à l’aide de Visual Studio.
  * [mise à niveau de votre application à l’aide de PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) vous guide à travers une mise à niveau de l’application à l’aide de PowerShell.
  * Contrôlez les mises à niveau de votre application à l'aide des [Paramètres de mise à niveau](service-fabric-application-upgrade-parameters.md).
  * Découvrez comment toouse des fonctionnalités avancées lors de la mise à niveau de votre application en vous reportant trop[rubriques avancées](service-fabric-application-upgrade-advanced.md).
  * Résoudre les problèmes courants dans les mises à niveau de l’application en faisant référence à des étapes de toohello de [résolution des problèmes de mises à niveau Application](service-fabric-application-upgrade-troubleshooting.md).
