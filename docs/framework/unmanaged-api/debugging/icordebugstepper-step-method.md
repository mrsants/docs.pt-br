---
title: Método ICorDebugStepper::Step
ms.date: 03/30/2017
api_name:
- ICorDebugStepper.Step
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper::Step
helpviewer_keywords:
- Step method, ICorDebugStepper interface [.NET Framework debugging]
- ICorDebugStepper::Step method [.NET Framework debugging]
ms.assetid: 38c1940b-ada1-40ba-8295-4c0833744e1e
topic_type:
- apiref
ms.openlocfilehash: 39d2fd0163b0e61295187461d5dbdf5742450306
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379513"
---
# <a name="icordebugstepperstep-method"></a>Método ICorDebugStepper::Step
Faz com que esse ICorDebugStepper faça uma única etapa por meio de seu thread que o contém e, opcionalmente, continue a avançar por meio de funções que são chamadas dentro do thread.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Step (  
    [in] BOOL   bStepIn  
);  
```  
  
## <a name="parameters"></a>Parâmetros  
 `bStepIn`  
 no Defina como entrar `true` em uma função que é chamada dentro do thread. Defina como `false` para percorrer a função.  
  
## <a name="remarks"></a>Comentários  
 A etapa é concluída quando o Common Language Runtime executa a próxima instrução gerenciada neste quadro de stepper. Se `Step` for chamado em um stepper, que não está no código gerenciado, a etapa será concluída quando a próxima instrução de código gerenciado for executada pelo thread.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
