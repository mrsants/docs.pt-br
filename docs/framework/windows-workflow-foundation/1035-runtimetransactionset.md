---
title: 1035 - RuntimeTransactionSet
ms.date: 03/30/2017
ms.assetid: 03b37de9-778c-4beb-b0e3-de73ece6088e
ms.openlocfilehash: 198e11dd94b0ad5cdc1e01c3611280754ca081d3
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61924846"
---
# <a name="1035---runtimetransactionset"></a>1035 - RuntimeTransactionSet
## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|1035|  
|Palavras-chave|WFRuntime|  
|Nível|Detalhado|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  
 Indica que uma atividade definiu a transação de tempo de execução.  
  
## <a name="message"></a>Mensagem  
 A transação de tempo de execução foi definida pela atividade "%1", DisplayName: "%2", InstanceId: '%3'.  Execução isolada a atividade "%4', DisplayName:"%5", InstanceId: '%6'.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|Atividade|xs:string|O nome do tipo de atividade.|  
|DisplayName|xs:string|O nome para exibição de atividade.|  
|InstanceId|xs:string|A identificação de instância de atividade.|  
|IsolatedActivity|xs:string|O nome do tipo de que a atividade isolada a transação está.|  
|IsolatedActivityDisplayName|xs:string|O nome para exibição de que a atividade isolada a transação está.|  
|IsolatedActivityInstanceId|xs:string|A identificação de instância de que a atividade isolada a transação está.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
