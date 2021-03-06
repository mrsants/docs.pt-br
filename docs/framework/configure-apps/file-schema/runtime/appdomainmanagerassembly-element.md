---
title: Elemento <appDomainManagerAssembly>
ms.date: 03/30/2017
helpviewer_keywords:
- <appDomainManagerAssembly> element
- appDomainManagerAssembly element
ms.assetid: c7c56e39-a700-44f5-b94e-411bfce339d9
ms.openlocfilehash: 1716b11106775bed2c0d6ccb62e8d5b032b6e8be
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91176130"
---
# <a name="appdomainmanagerassembly-element"></a>Elemento \<appDomainManagerAssembly>

Especifica o assembly que fornece o gerenciador do domínio do aplicativo para o domínio do aplicativo padrão no processo.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<appDomainManagerAssembly>**  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<appDomainManagerAssembly
   value="assembly display name" />  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`value`|Atributo obrigatório. Especifica o nome de exibição do assembly que fornece o Gerenciador de domínio do aplicativo para o domínio de aplicativo padrão no processo.|  
  
### <a name="child-elements"></a>Elementos filho  

 Nenhum.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|`configuration`|O elemento raiz em cada arquivo de configuração usado pelos aplicativos do Common Language Runtime e .NET Framework.|  
|`runtime`|Contém informações sobre associação do assembly e coleta de lixo.|  
  
## <a name="remarks"></a>Comentários  

 Para especificar o tipo de Gerenciador de domínio do aplicativo, você deve especificar esse elemento e o [\<appDomainManagerType>](appdomainmanagertype-element.md) elemento. Se um desses elementos não for especificado, o outro será ignorado.  
  
 Quando o domínio de aplicativo padrão for carregado, <xref:System.TypeLoadException> será gerado se o assembly especificado não existir ou se o assembly não contiver o tipo especificado pelo [\<appDomainManagerType>](appdomainmanagertype-element.md) elemento; e o processo não for iniciado. Se o assembly for encontrado, mas as informações de versão não corresponderem, um <xref:System.IO.FileLoadException> será lançado.  
  
 Quando você especifica o tipo de Gerenciador de domínio do aplicativo para o domínio de aplicativo padrão, outros domínios de aplicativo criados a partir do domínio de aplicativo padrão herdam o tipo de Gerenciador de domínio do aplicativo. Use as <xref:System.AppDomainSetup.AppDomainManagerType%2A?displayProperty=nameWithType> <xref:System.AppDomainSetup.AppDomainManagerAssembly%2A?displayProperty=nameWithType> Propriedades e para especificar um tipo de Gerenciador de domínio de aplicativo diferente para um novo domínio de aplicativo.  
  
 A especificação do tipo de Gerenciador de domínio do aplicativo exige que o aplicativo tenha confiança total. (Por exemplo, um aplicativo em execução na área de trabalho tem confiança total.) Se o aplicativo não tiver confiança total, um <xref:System.TypeLoadException> será lançado.  
  
 Para o formato do nome de exibição do assembly, consulte a <xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType> propriedade.  
  
 Este elemento de configuração está disponível apenas no .NET Framework 4 e posterior.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra como especificar que o Gerenciador de domínio do aplicativo para o domínio de aplicativo padrão de um processo é o `MyMgr` tipo no `AdMgrExample` assembly.  
  
```xml  
<configuration>  
   <runtime>  
      <appDomainManagerType value="MyMgr" />  
      <appDomainManagerAssembly
         value="AdMgrExample, Version=1.0.0.0, Culture=neutral, PublicKeyToken=6856bccf150f00b3" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>Confira também

- <xref:System.AppDomainSetup.AppDomainManagerType%2A?displayProperty=nameWithType>
- <xref:System.AppDomainSetup.AppDomainManagerAssembly%2A?displayProperty=nameWithType>
- [\<appDomainManagerType> Elementos](appdomainmanagertype-element.md)
- [Esquema de configurações do runtime](index.md)
- [Esquema do arquivo de configuração](../index.md)
- [Método SetAppDomainManagerType](../../../unmanaged-api/hosting/iclrcontrol-setappdomainmanagertype-method.md)
