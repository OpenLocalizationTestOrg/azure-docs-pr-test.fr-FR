---
titre : aaa « leçon du didacticiel Azure Analysis Services 13 : déployer | Description de Microsoft Docs » : décrit comment le didacticiel de hello toodeploy project tooAzure Analysis Services.
Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».

MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 17/07/2017 ms.author : owend
---
# <a name="lesson-13-deploy"></a>Leçon 13 : Déployer

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Dans cette leçon, vous configurez les propriétés de déploiement ; spécification d’un ordinateur Azure Analysis Services server toodeploy tooand un nom pour le modèle de hello. Vous déployez ensuite hello modèle toothat instance. Une fois votre modèle est déployé, les utilisateurs peuvent se connecter à tooit à l’aide d’une application cliente de création de rapports. toolearn, voir [déployer tooAzure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).  
  
Estimé temps toocomplete cette leçon : **5 minutes**  
  
## <a name="prerequisites"></a>Composants requis  
Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu. Avant d’effectuer les tâches de hello dans cette leçon, vous devez avoir terminé les leçon précédente hello : [leçon 12 : analyser dans Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).  

> [!IMPORTANT]  
> Vous devez avoir [des autorisations d’administrateur](../analysis-services-server-admins.md) on hello distant Analysis Services server dans l’ordre toodeploy tooit.  

> [!IMPORTANT]  
> Si vous avez installé la base de données exemple hello AdventureWorksDW2014 sur un ordinateur local SQL Server, et que vous déployez votre serveur Azure Analysis Services de tooan de modèle, un [passerelle de données locale](../analysis-services-gateway.md) est requis.
  
## <a name="deploy-hello-model"></a>Déployer le modèle de hello  
  
#### <a name="tooconfigure-deployment-properties"></a>propriétés de déploiement tooconfigure  

  
1.  Dans **l’Explorateur de solutions**, avec le bouton hello **AW Internet Sales** de projet, puis cliquez sur **propriétés**.  
  
2.  Bonjour **Pages de propriétés de AW Internet Sales** boîte de dialogue **serveur de déploiement**, Bonjour **Server** propriété, entrez le serveur complet de hello.  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  Bonjour **base de données** , tapez **Internet Sales Adventure Works**.  
  
4.  Bonjour **Nom_modèle** , tapez **Adventure Works Internet Sales Model**.  
  
5.  Passez en revue vos sélections, puis cliquez sur **OK**.  
  
#### <a name="toodeploy-hello-adventure-works-internet-sales"></a>toodeploy hello Adventure Works Internet Sales
  
1.  Dans **l’Explorateur de solutions**, avec le bouton hello **AW Internet Sales** projet > **Build**.  

2.  Avec le bouton hello **AW Internet Sales** projet > **déployer**.

    Lorsque vous déployez tooAzure Analysis Services, vous pouvez être invité à tooenter votre compte. Entrez votre compte professionnel et votre mot de passe, par exemple nancy@adventureworks.com. Ce compte doit être dans les administrateurs sur le serveur de hello.
  
    boîte de dialogue déployer Hello apparaît et affiche l’état du déploiement des métadonnées de hello hello et chaque table incluse dans le modèle de hello.  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. Si le déploiement se termine sans erreurs, cliquez sur **Fermer**.  
  
## <a name="conclusion"></a>Conclusion  
Félicitations ! Vous venez de terminer la création et le déploiement de votre premier modèle tabulaire Analysis Services. Ce didacticiel a permis de vous guider dans la réalisation des tâches courantes de hello lors de la création d’un modèle tabulaire. Maintenant que votre modèle Internet Sales Adventure Works est déployé, vous pouvez utiliser le modèle de SQL Server Management Studio toomanage hello ; créer des scripts de processus et d’un plan de sauvegarde. Les utilisateurs peuvent également connectez-vous de modèle toohello à l’aide d’une application cliente de création de rapports tels que Microsoft Excel ou Power BI.  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a>Et ensuite ?
[Connect with Power BI Desktop (Se connecter avec Power BI Desktop)](../analysis-services-connect-pbi.md)   
[Leçon supplémentaire – Sécurité dynamique](../tutorials/aas-supplemental-lesson-dynamic-security.md)   
[Leçon supplémentaire – Lignes de détails](../tutorials/aas-supplemental-lesson-detail-rows.md)   
[Leçon supplémentaire – Hiérarchies déséquilibrées](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
