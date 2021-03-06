---
title: <serviceTokenResolver>
ms.date: 03/30/2017
ms.assetid: 6e9001e1-e064-4f47-84b2-46225c177746
author: BrucePerlerMS
ms.openlocfilehash: 3ea9684245bd1c1c3b9ce171a045fff49d0ba592
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91156908"
---
# \<serviceTokenResolver>

Registra o resolvedor de token de serviço que é usado pelos manipuladores na coleção de manipuladores de token. O resolvedor de token de serviço é usado para resolver o token de criptografia em mensagens e tokens de entrada.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel>**](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<identityConfiguration>**](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<securityTokenHandlers>**](securitytokenhandlers.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<securityTokenHandlerConfiguration>**](securitytokenhandlerconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<serviceTokenResolver>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <serviceTokenResolver type=xs:string>  
        </serviceTokenResolver>  
      </securityTokenHandlerConfiguration>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|type|Especifica o tipo do resolvedor de token de serviço. O <xref:System.IdentityModel.Selectors.SecurityTokenResolver> tipo ou um tipo que deriva da <xref:System.IdentityModel.Selectors.SecurityTokenResolver> classe. Para obter mais informações sobre como especificar o `type` atributo, consulte [referências de tipo personalizado]. Necessário.|  
  
### <a name="child-elements"></a>Elementos filho  

 Nenhum  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<securityTokenHandlerConfiguration>](securitytokenhandlerconfiguration.md)|Fornece a configuração para uma coleção de manipuladores de token de segurança.|  
  
## <a name="remarks"></a>Comentários  

 O resolvedor de token de serviço pode ser usado para resolver o token de criptografia em mensagens e tokens de entrada. Ele é usado para recuperar a chave que deve ser usada para descriptografar tokens de entrada. Você deve especificar o `type` atributo. O tipo especificado pode ser <xref:System.IdentityModel.Selectors.SecurityTokenResolver> ou um tipo personalizado que deriva da <xref:System.IdentityModel.Selectors.SecurityTokenResolver> classe.  
  
 Alguns manipuladores de token permitem que você especifique as configurações do resolvedor de token de serviço na configuração. As configurações em manipuladores de token individuais substituem aquelas especificadas na coleção do manipulador de token de segurança.  
  
> [!NOTE]
> A especificação do `<serviceTokenResolver>` elemento como um elemento filho do [\<identityConfiguration>](identityconfiguration.md) elemento foi preterida, mas ainda tem suporte para compatibilidade com versões anteriores. As configurações no `<securityTokenHandlerConfiguration>` elemento substituem aquelas no `<identityConfiguration>` elemento.  
  
## <a name="example"></a>Exemplo  
  
```xml  
<serviceTokenResolver type="MyNamespace.CustomTokenResolver, MyAssembly" />  
```
