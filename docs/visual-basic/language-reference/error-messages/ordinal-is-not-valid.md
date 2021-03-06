---
title: O ordinal não é válido
ms.date: 07/20/2015
f1_keywords:
- vbrID452
ms.assetid: 7459562b-cd4f-4590-95e0-6126ae3589a5
ms.openlocfilehash: 64f56b2ecace0ceafb310a175ea605e6959b7256
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90871385"
---
# <a name="ordinal-is-not-valid"></a>O ordinal não é válido

Sua chamada para uma DLL (biblioteca de vínculo dinâmico) indicou usar um número em vez de um nome de procedimento, usando a `#num` sintaxe. Esse erro tem as seguintes causas possíveis:  
  
- Falha ao tentar converter a `#num` expressão em um ordinal.  
  
- O `#num` especificado não especifica nenhuma função na dll.  
  
- Uma biblioteca de tipos tem uma declaração inválida que resulta em uso interno de um número ordinal inválido.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
1. Verifique se a expressão representa um número válido ou chame o procedimento por nome.  
  
2. Certifique-se de que `#num` identifica uma função válida na dll.  
  
3. Isole a chamada de procedimento que está causando o problema comentando o código. Escreva uma `Declare` instrução para o procedimento e relate o problema ao fornecedor da biblioteca de tipos.  
  
## <a name="see-also"></a>Confira também

- [Instrução Declare](../statements/declare-statement.md)
