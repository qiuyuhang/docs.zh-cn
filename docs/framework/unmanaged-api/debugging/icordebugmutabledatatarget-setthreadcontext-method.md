---
title: "ICorDebugMutableDataTarget::SetThreadContext 方法"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 8c0d01d5-67e5-4522-9ccf-c8f3a78cb4fd
caps.latest.revision: "5"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 8c43ef5405ed582cc55af69d7f41887c0615965f
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="icordebugmutabledatatargetsetthreadcontext-method"></a><span data-ttu-id="4eeab-102">ICorDebugMutableDataTarget::SetThreadContext 方法</span><span class="sxs-lookup"><span data-stu-id="4eeab-102">ICorDebugMutableDataTarget::SetThreadContext Method</span></span>
<span data-ttu-id="4eeab-103">设置某个线程的上下文（寄存器值）。</span><span class="sxs-lookup"><span data-stu-id="4eeab-103">Sets the context (register values) for a thread.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="4eeab-104">语法</span><span class="sxs-lookup"><span data-stu-id="4eeab-104">Syntax</span></span>  
  
```  
HRESULT SetThreadContext(  
   [in] DWORD dwThreadID,  
   [in] ULONG32 contextSize,   [in, size_is(contextSize)] const BYTE * pContext);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="4eeab-105">参数</span><span class="sxs-lookup"><span data-stu-id="4eeab-105">Parameters</span></span>  
 `dwThreadID`  
 <span data-ttu-id="4eeab-106">[in] 由操作系统定义的线程标识符。</span><span class="sxs-lookup"><span data-stu-id="4eeab-106">[in] The operating system-defined thread identifier.</span></span>  
  
 `contextSize`  
 <span data-ttu-id="4eeab-107">[in] 要写入的 `pContext` 缓冲区的大小。</span><span class="sxs-lookup"><span data-stu-id="4eeab-107">[in] The size of the `pContext` buffer to be written.</span></span>  
  
 `pContext`  
 <span data-ttu-id="4eeab-108">[in] 指向要写入的字节的指针。</span><span class="sxs-lookup"><span data-stu-id="4eeab-108">[in] A pointer to the bytes to be written.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="4eeab-109">备注</span><span class="sxs-lookup"><span data-stu-id="4eeab-109">Remarks</span></span>  
 <span data-ttu-id="4eeab-110">`SetThreadContext` 方法将更新由操作系统定义的 `dwThreadID` 参数指定的当前线程上下文。</span><span class="sxs-lookup"><span data-stu-id="4eeab-110">The `SetThreadContext` method updates the current context for the thread specified by the operating system-defined `dwThreadID` argument.</span></span> <span data-ttu-id="4eeab-111">上下文记录的格式由通过指示的平台[icordebugdatatarget:: Getplatform](../../../../docs/framework/unmanaged-api/debugging/icordebugdatatarget-getplatform-method.md)方法。</span><span class="sxs-lookup"><span data-stu-id="4eeab-111">The format of the context record is determined by the platform indicated by the [ICorDebugDataTarget::GetPlatform](../../../../docs/framework/unmanaged-api/debugging/icordebugdatatarget-getplatform-method.md) method.</span></span> <span data-ttu-id="4eeab-112">在 Windows 上，这是[上下文](http://msdn.microsoft.com/library/windows/desktop/ms679284.aspx)结构。</span><span class="sxs-lookup"><span data-stu-id="4eeab-112">On Windows, this is a [CONTEXT](http://msdn.microsoft.com/library/windows/desktop/ms679284.aspx) structure.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="4eeab-113">要求</span><span class="sxs-lookup"><span data-stu-id="4eeab-113">Requirements</span></span>  
 <span data-ttu-id="4eeab-114">**平台：**请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="4eeab-114">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="4eeab-115">**标头：** CorDebug.idl、 CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="4eeab-115">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="4eeab-116">**库：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="4eeab-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="4eeab-117">**.NET framework 版本：**[!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="4eeab-117">**.NET Framework Versions:** [!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4eeab-118">另请参阅</span><span class="sxs-lookup"><span data-stu-id="4eeab-118">See Also</span></span>  
 [<span data-ttu-id="4eeab-119">ICorDebugMutableDataTarget 接口</span><span class="sxs-lookup"><span data-stu-id="4eeab-119">ICorDebugMutableDataTarget Interface</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugmutabledatatarget-interface.md)  
 [<span data-ttu-id="4eeab-120">调试接口</span><span class="sxs-lookup"><span data-stu-id="4eeab-120">Debugging Interfaces</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)