---
title: ICorProfilerCallback4 接口
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback4
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback4
helpviewer_keywords:
- ICorProfilerCallback4 interface [.NET Framework profiling]
ms.assetid: 665f3cfc-cd6f-4880-906c-ea65ad384783
topic_type:
- apiref
ms.openlocfilehash: 1b85c48859ac29738347d112dd0466a76bfdfd2c
ms.sourcegitcommit: b11efd71c3d5ce3d9449c8d4345481b9f21392c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2020
ms.locfileid: "76865332"
---
# <a name="icorprofilercallback4-interface"></a>ICorProfilerCallback4 接口
提供公共语言运行时（CLR）用于将信息传递给探查器的回调方法。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[GetReJITParameters 方法](icorprofilercallback4-getrejitparameters-method.md)|允许代码探查器为新的重新编译的方法体设置备用代码生成标志。|  
|[MovedReferences2 方法](icorprofilercallback4-movedreferences2-method.md)|作为压缩垃圾回收的结果，报告堆中对象的新布局。|  
|[ReJITCompilationFinished 方法](icorprofilercallback4-rejitcompilationfinished-method.md)|通知探查器，实时（JIT）编译器已完成函数的重新编译。|  
|[ReJITCompilationStarted 方法](icorprofilercallback4-rejitcompilationstarted-method.md)|通知探查器实时（JIT）编译器已开始重新编译某个函数。|  
|[ReJITError 方法](icorprofilercallback4-rejiterror-method.md)|报告处理重新编译请求时遇到的错误。|  
|[SurvivingReferences2 方法](icorprofilercallback4-survivingreferences2-method.md)|将堆中对象的布局报告为非压缩垃圾回收的结果。|  
  
## <a name="remarks"></a>备注  
  
## <a name="requirements"></a>需求  
 **平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **头文件：** CorProf.idl、CorProf.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>另请参阅

- [ICorProfilerCallback2 接口](icorprofilercallback2-interface.md)
- [Profiling 接口](profiling-interfaces.md)
- [ICorProfilerInfo 接口](icorprofilerinfo-interface.md)
