---
title: Restringir el acceso a los tipos de máquina
shortTitle: Acceso de los tipos de máquina
intro: Puedes configurar restricciones en los tipos de máquina que los usuarios pueden elegir cuando crean codespaces en tu organizción.
product: '{% data reusables.gated-features.codespaces %}'
permissions: 'To manage access to machine types for the repositories in an organization, you must be an organization owner.'
versions:
  fpt: '*'
  ghec: '*'
type: how_to
topics:
  - Codespaces
---

## Resumen

Habitualmente, cuando creas un codespace, se te ofrece una selección de especificaciones para la máquina que lo ejecutará. Puedes elegir el tipo de máquina que se acople mejor a tus necesidades. Para obtener más información, consulta la sección "[Crear un codespace](/codespaces/developing-in-codespaces/creating-a-codespace#creating-a-codespace)". Si pagas por utilizar {% data variables.product.prodname_github_codespaces %}, entonces tu elección de tipo de máquina afectará cuánto se te factura. Para obtener más información sobre los precios, consulta la sección "[Acerca de la facturación para los codespaces](/billing/managing-billing-for-github-codespaces/about-billing-for-codespaces)".

Como propietario de organización, podrías querer configurar restricciones en los tipos de máquina que están disponibles. Por ejemplo, si el trabajo en tu organización no requiere de una potencia de cómputo o espacio de almacenamiento significativos, puedes eliminar las máquinas con muchos recursos de la lista de opciones que las personas pueden elegir. Esto se hace definiendo una o más políticas en los ajustes de {% data variables.product.prodname_codespaces %} de tu organización.

### Comportamiento cuando configuras una restricción de tipo de máquina

Si hay codespaces existentes que ya no se ajusten a una política que definiste, estos seguirán operando hasta que venzan. Cuando el usuario intente reanudar el codespace, se le mostrará un mensaje que indica que el tipo de máquina que se seleccionó actualmente ya no está permitido en esta organización y se indicará elegir un tipo de máquina como alternativa.

Si eliminas tipos de máquina con especificaciones más altas, los cuales requiera la configuración de {% data variables.product.prodname_codespaces %} para un repositorio individual de tu organización, entonces no se podrá crear un codespace en dicho repositorio. Cuando alguien intenta crear un codespace, verán un mensaje que les dice que no hay tipos de máquina válidos disponibles que cumplan con los requisitos de la configuración de {% data variables.product.prodname_codespaces %} del repositorio.

{% note %}

**Nota**: Cualquiera que pueda editar el archivo de configuración `devcontainer.json` en un repositorio puede ajustar una especificación mínima para las máquinas, la cual puede utilizarse para los codespaces de dicho repositorio. Para obtener más información, consulta la sección "[Configurar una especificación mínima para las máquinas de los codespaces](/codespaces/setting-up-your-project-for-codespaces/setting-a-minimum-specification-for-codespace-machines)".

{% endnote %}

Si el configurar una política para los tipos de máquina previene que las personas utilicen {% data variables.product.prodname_codespaces %} para un repositorio en particular, hay dos opciones para hacerlo:

* Puedes ajustar tus políticas para que eliminen específicamente las restricciones del repositorio afectado.
* Cualquiera que tenga un codespace al cuál ya no puedan acceder debido a la política nueva puede exportar su codespace a una rama. Esta rama contendrá todos los cambios de su codespace. Pueden abrir un codespace nuevo en esta rama con un tipo de máquina compatible o trabajar en ella localmente. Para obtener más información, consulta la sección "[Exportar cambios a una rama](/codespaces/troubleshooting/exporting-changes-to-a-branch)".

### Configurar políticas específicas para los repositorios y a lo largo de la organización

Cuando creas una política, eliges si esta aplica a todos los repositorios de tu organización o solo a algunos específicos. Si configuras una política a lo largo de la organización, entonces cualquier política que configures para los repositorios individuales debe de caer dentro de las restricciones que se configuraron a nivel organizacional. El agregar políticas hace que la elección de máquinas sea más restrictiva, no menos.

Por ejemplo, podrías crear una política en toda la organización, la cual restrinja los tipos de máquina a aquellos de 2 o 4 núcleos. Entonces podrás configurar una política para el repositorio "A" que lo restrinja a máquinas de 2 núcleos. El configurar una política para un repositorio "A", la cual lo restrinja a máquinas de 2, 4 u 8 núcleos, daría como resultado una elección de solo máquinas de 2 y 4 núcleos, ya que la política organizacional previene el acceso a máquinas de 8 núcleos.

Si agregas una política a nivel organizacional, deberías configurarla en la elección de tipos de máquina más grande que deberá estar disponible para cualquier repositorio de tu organización. Entonces podrás agregar las políticas específicas para los repositorios y así restringir aún más la elección.

## Agregar una política para limitar los tipos de máquina disponibles

{% data reusables.profile.access_org %}
{% data reusables.profile.org_settings %}
1. En la sección de "Código, planeación y automatización" de la barra lateral, selecciona **{% octicon "codespaces" aria-label="The codespaces icon" %} {% data variables.product.prodname_codespaces %}** y luego haz clic en **Política**.
2. En la página de "Políticas de los codespaces", haz clic en **Crear política**.
3. Ingresa un nombre para tu política nueva.
4. Haz clic en **Agregar restricción** y elige **Tipos de máquina**.

   ![Agrega una restricción para los tipos de máquina](/assets/images/help/codespaces/add-constraint-dropdown.png)

5. Haz clic en {% octicon "pencil" aria-label="The edit icon" %} para editar la restricción y luego borra la selección de cualquier tipo de máquina que no quieras que estén disponibles.

   ![Editar la restricción de tipo de máquina](/assets/images/help/codespaces/edit-machine-constraint.png)

6. En el área de "Cambiar destino de la política", haz clic en el botón desplegable.
7. Elige y asea **Todos los repositorios** o **Repositorios seleccionados** para determinar a cuáles aplicará esta política.
8. Si eliges **Repositorios seleccionados**:
   1. Da clic en {% octicon "gear" aria-label="The settings icon" %}.

      ![Editar los ajustes para la política](/assets/images/help/codespaces/policy-edit.png)

   2. Selecciona los repositorios a los cuales quieres que aplique esta política.
   3. En la parte inferior de la lista de repositorios, haz clic en **Seleccionar repositorios**.

      ![Selecciona los repositorios para esta política](/assets/images/help/codespaces/policy-select-repos.png)

9. Haz clic en **Save ** (guardar).

## Editar una política

1. Muestra la página de "Políticas del Codespace". Para obtener más información, consulta la sección "[Agregar una política para limitar los tipos de máquina disponibles](#adding-a-policy-to-limit-the-available-machine-types)".
1. Haz clic en el nombre de la política que quieres editar.
1. Haz los cambios requeridos y luego haz clic en **Guardar**.

## Borrar una política

1. Muestra la página de "Políticas del Codespace". Para obtener más información, consulta la sección "[Agregar una política para limitar los tipos de máquina disponibles](#adding-a-policy-to-limit-the-available-machine-types)".
1. Haz clic en el botón de borrar a la derecha de la política que quieras borrar.

   ![El botón de borrar para una política](/assets/images/help/codespaces/policy-delete.png)

## Leer más

- "[Administrar los límites de gastos de los Codespaces](/billing/managing-billing-for-github-codespaces/managing-spending-limits-for-codespaces)"
