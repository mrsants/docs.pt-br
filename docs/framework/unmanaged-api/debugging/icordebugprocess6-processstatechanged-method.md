---
title: Método ICorDebugProcess6::ProcessStateChanged
ms.date: 03/30/2017
ms.assetid: fb6d30d9-54f3-462b-8ebf-ce0440791ad5
ms.openlocfilehash: 6be216741e902b15efc3a3ece95cb4a4229960e3
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212835"
---
# <a name="icordebugprocess6processstatechanged-method"></a>Método ICorDebugProcess6::ProcessStateChanged
Notifica o [ICorDebug](icordebug-interface.md) de que o processo está em execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ProcessStateChanged(   [in] CorDebugStateChange change);  
```  
  
## <a name="parameters"></a>Parâmetros  
 `change`  
 no Um membro da enumeração [ProcessStateChanged](icordebugprocess6-processstatechanged-method.md)  
  
## <a name="remarks"></a>Comentários  
 O depurador chama esse método para notificar [ICorDebug](icordebug-interface.md) que o processo está em execução.  
  
> [!NOTE]
> Esse método está disponível somente com .NET Native.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Confira também

- [Interface ICorDebugProcess6](icordebugprocess6-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
