---
title: "Função GetVersionFromProcess"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: GetVersionFromProcess
api_location:
- mscoree.dll
- mscoreei.dll
api_type: DLLExport
f1_keywords: GetVersionFromProcess
helpviewer_keywords: GetVersionFromProcess function [.NET Framework hosting]
ms.assetid: a9f7f824-64a1-408d-8607-91c7f19d21fe
topic_type: apiref
caps.latest.revision: "20"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: db5054ab9b71eb93005fc0315acba82d807487ec
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="getversionfromprocess-function"></a>Função GetVersionFromProcess
Obtém o número de versão do common language runtime (CLR) que está associado com o identificador de processo especificado.  
  
 Essa função foi preterida no [!INCLUDE[net_v40_long](../../../../includes/net-v40-long-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetVersionFromProcess (  
    [in]  HANDLE  hProcess,   
    [out] LPWSTR  pVersion,   
    [in]  DWORD   cchBuffer,   
    [out] DWORD  *dwLength  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `hProcess`  
 [in] Um identificador para um processo.  
  
 `pVersion`  
 [out] Um buffer que contém a cadeia de caracteres de número de versão após a conclusão bem-sucedida do método.  
  
 `cchBuffer`  
 [in] O comprimento do buffer de versão.  
  
 `pdwLength`  
 [out] Um ponteiro para o comprimento da cadeia de número de versão.  
  
## <a name="return-value"></a>Valor de retorno  
 Esse método retorna códigos de erro do modelo de objeto de componente (COM) padrão, conforme definido no Winerror. H, além dos valores a seguir.  
  
|Código de retorno|Descrição|  
|-----------------|-----------------|  
|S_OK|O método foi concluído com êxito.|  
|E_INVALIDARG|`pVersion`é nulo e `cchBuffer` não for null, ou vice-versa.<br /><br /> -ou-<br /><br /> `hProcess`não é um identificador válido para um processo.<br /><br /> -ou-<br /><br /> O CLR não está carregado.|  
|ERROR_INSUFFICIENT_BUFFER|`cchBuffer`é nula ou menor que o comprimento da cadeia de caracteres de versão.|  
|E_NOTIMPL|Este método não está disponível no sistema operacional Microsoft Windows 95, Microsoft Windows 98 ou Microsoft Windows Millennium Edition.|  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** consulte [requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE.h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **Versões do .NET framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Função GetRequestedRuntimeInfo](../../../../docs/framework/unmanaged-api/hosting/getrequestedruntimeinfo-function.md)  
 [Função GetRequestedRuntimeVersion](../../../../docs/framework/unmanaged-api/hosting/getrequestedruntimeversion-function.md)  
 [Funções de hospedagem CLR preteridas](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
