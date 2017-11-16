---
title: "Actualización de proyectos a la versión actual de Azure Tools | Microsoft Docs"
description: "Aprenda a actualizar proyectos de Azure en Visual Studio a la versión actual de Azure Tools"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1d64070a-078d-468a-87f4-e6715de6475f
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.translationtype: Human Translation
ms.sourcegitcommit: 219dcbfdca145bedb570eb9ef747ee00cc0342eb
ms.openlocfilehash: e346640f6cbf7969bf373b84d8a20a24a74f654e
ms.contentlocale: es-es
ms.lasthandoff: 11/17/2016

---
# <a name="how-to-upgrade-projects-to-the-current-version-of-the-azure-tools-for-visual-studio"></a>Actualización de proyectos a la versión actual de Azure Tools para Visual Studio
## <a name="overview"></a>Información general
Después de instalar la versión actual de Azure Tools (o una versión anterior que sea posterior a la 1.6), todos los proyectos que se crearon con una versión de Azure Tools anterior a la 1.6 (noviembre de 2011) se actualizarán automáticamente en cuanto se abran. Si creó proyectos con la versión de 1.6 (noviembre de 2011) de las herramientas y sigue teniendo esa versión instalada, puede abrir dichos proyectos en la versión anterior y decidir más tarde si desea actualizarlos.

## <a name="how-your-project-changes-when-you-upgrade-it"></a>Cómo cambia un proyecto al actualizarlo
Si un proyecto se actualiza automáticamente o se especifica que se desea actualizarlo, el proyecto se modifica para funcionar con las versiones actuales de determinados ensamblados y también se modifican algunas propiedades como se describe en esta sección. Si el proyecto requiere otros cambios para ser compatible con la versión más reciente de las herramientas, será preciso realizarlos manualmente.

* El archivo web.config para roles web y el archivo app.config para roles de trabajo se actualizan para hacer referencia a la versión más reciente de Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitoirTraceListener.dll.
* Los ensamblados Microsoft.WindowsAzure.StorageClient.dll, Microsoft.WindowsAzure.Diagnostics.dll y Microsoft.WindowsAzure.ServiceRuntime.dll se actualizan a las nuevas versiones.
* Los perfiles de publicación que se almacenaron en el archivo de proyecto de Azure (.ccproj) se mueven a un archivo independiente, con la extensión .azurePubXml, en el subdirectorio **Publish** .
* Algunas de las propiedades del perfil de publicación se actualizan para admitir características nuevas y modificadas. **AllowUpgrade** se reemplaza por **DeploymentReplacementMethod**, ya que los servicios en la nube implementados se pueden actualizar de forma simultánea o incremental.
* La propiedad **UseIISExpressByDefault** se agrega y se establece en false para que el servidor web que se usa para la depuración no cambie automáticamente de Internet Information Services (IIS) a IIS Express. IIS Express es el servidor web predeterminado para los proyectos que se crean con las versiones más recientes de las herramientas.
* Si el Servicio de caché de Azure se hospeda en uno o varios de los roles del proyecto, algunas propiedades de la configuración del servicio (archivo .cscfg) y la definición del servicio (archivo .csdef) se cambian cuando se actualiza un proyecto. Si el proyecto usa el paquete de NuGet Servicio de caché de Azure, el proyecto se actualiza a la versión más reciente del paquete. Debe abrir el archivo web.config y comprobar que la configuración del cliente se mantuvo correctamente durante el proceso de actualización. Si agregó las referencias a los ensamblados de cliente del Servicio de caché de Azure sin usar el paquete de NuGet, dichos ensamblados no se actualizarán, por lo que debe actualizar manualmente las referencias a las nuevas versiones.

> [!IMPORTANT]
> En el caso de los proyectos de F#, debe actualizar manualmente las referencias a los ensamblados de Azure para que hagan referencia a las versiones más recientes de dichos ensamblados.
> 
> 

### <a name="how-to-upgrade-an-azure-project-to-the-current-release"></a>Actualización de un proyecto de Azure a la versión actual
1. Instale la versión actual de Azure Tools en la instalación de Visual Studio que desea usar para el proyecto actualizado y, a continuación, abra el proyecto que desea actualizar. Si el proyecto se creó con una versión de Azure Tools anterior a la 1.6 (noviembre de 2011), el proyecto se actualiza automáticamente a la versión actual. Si el proyecto se creó con la versión de noviembre de 2011 y esa versión todavía está instalada, el proyecto se abre en dicha versión.
2. En el Explorador de soluciones, abra el menú contextual del nodo del proyecto, elija **Propiedades**, y, a continuación, elija la pestaña **Aplicación** del cuadro de diálogo que aparece.
   
    La pestaña **Aplicación** muestra la versión de las herramientas asociada con el proyecto. Si aparece la versión actual de Azure Tools, significa que el proyecto ya se actualizó. Si ha instalado una versión de las herramientas más reciente que la que se muestra en la pestaña, aparece un botón **Actualizar** .
3. Elija el botón **Actualizar** para actualizar un proyecto a la versión actual de las herramientas.
4. Compile el proyecto y, a continuación, solucione los errores que produzcan los cambios en la API. Para obtener información acerca de cómo modificar el código de la nueva versión, consulte la documentación de la API específica.


