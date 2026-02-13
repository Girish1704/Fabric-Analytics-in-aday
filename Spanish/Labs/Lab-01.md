# Microsoft Fabric Fabric Analyst in a Day - Laboratorio 1

![](../media/Lab-01/main1.png)

# Contenido	
- Estructura del documento
- Escenario/planteamiento del problema
- Información general del informe de Power BI Desktop	
    - Tarea 1: Configurar Power BI Desktop en un entorno de laboratorio	
    - Tarea 2: Analizar el informe de Power BI Desktop	
    - Tarea 3: Revisar consultas de Power Query	
- Referencias

# Estructura del documento

El laboratorio incluye pasos que el usuario debe seguir junto con
capturas de pantalla asociadas que sirven de ayuda visual. En cada
captura de pantalla, las secciones se resaltan con cuadros de color
naranja para indicar en qué áreas debe centrarse el usuario.

>**Nota:** Algunas de las capturas de pantalla pueden estar
desactualizadas debido a las actualizaciones continuas del producto.

# Escenario/planteamiento del problema

Fabrikam, Inc. es un distribuidor mayorista de artículos novedosos. Como
mayorista, los clientes de Fabrikam son en su mayoría empresas que
revenden a particulares. Fabrikam vende a clientes minoristas en todo
Estados Unidos, incluidas tiendas especializadas, supermercados, tiendas
de informática y tiendas de atracciones turísticas. Fabrikam también
vende a otros mayoristas a través de una red de agentes que promocionan
los productos en nombre de Fabrikam. Si bien todos los clientes de
Fabrikam tienen su sede actualmente en los Estados Unidos, la compañía
tiene la intención de impulsar la expansión a otros países y regiones.

Es analista de datos en el equipo de ventas. Usted recopila, limpia e
interpreta conjuntos de datos para resolver problemas comerciales.
También reúne visualizaciones como cuadros y gráficos, escribe informes
y los presenta a los encargados de tomar decisiones de la organización.

Para extraer información valiosa de los datos, se extraen datos de
varios sistemas, se limpian y se combinan. Extrae datos de los
siguientes orígenes:

- **Datos de ventas:** estos datos provienen del sistema ERP y los datos
  se almacenan en una base de datos ADLS Gen2. Se actualiza a
  mediodía/12:00 todos los días.

- **Datos de proveedor:** estos datos provienen de diferentes
  proveedores y se almacenan en una base de datos de Snowflake. Se
  actualiza a medianoche/00:00 todos los días.

- **Datos de cliente:** estos datos provienen de Customer Insights y se
  almacenan en Dataverse. Los datos siempre están actualizados.

- **Datos de empleado:** estos datos provienen del sistema de recursos
  humanos; se almacenan como un archivo de exportación en una carpeta de
  SharePoint. Se actualiza a todas las mañanas a las 9:00.

    ![](../media/Lab-01/image4.jpeg)

Actualmente está creando un modelo semántico en Power BI Premium que
extrae los datos de los sistemas de origen anteriores para satisfacer
sus necesidades de informes y ofrecer a los usuarios finales la
capacidad de autoservicio. Use Power Query para actualizar su modelo.

**Se enfrenta a lo siguiente:**

- Debe actualizar su conjunto de datos al menos tres veces al día para
  adaptarse a los diferentes tiempos de actualización para los
  diferentes orígenes de datos.

- Sus actualizaciones tardan mucho tiempo, ya que necesita hacer una
  actualización completa cada vez para capturar cualquier actualización
  que haya ocurrido en los sistemas de origen.

- Cualquier error en cualquiera de los orígenes de datos de los que
  extrae provocará que se interrumpa la actualización del conjunto de
  datos. Muchas veces, el archivo del empleado no se carga a tiempo, lo
  que provoca que se interrumpa la actualización del conjunto de datos.

- Se necesita mucho tiempo para hacer cambios en su modelo de datos, ya
  que Power Query tarda mucho en actualizar sus versiones preliminares,
  dado el gran tamaño de los datos y las transformaciones complejas.

- Necesita que un PC con Windows use Power BI Desktop aunque el estándar
  corporativo es Mac.

Ha oído hablar sobre Microsoft Fabric y ha decidido probar para ver si
abordaba sus desafíos.

### **Información general del informe de Power BI Desktop**

Antes de comenzar con Fabric, veamos el informe actual en Power BI
Desktop para comprender las transformaciones y el modelo.

## Tarea 1: Configurar Power BI Desktop en un entorno de laboratorio

1. Abra **FAIAD.pbix**, que se encuentra en la carpeta **Reports** en
    el **escritorio** de su entorno de laboratorio. El archivo se abrirá
    en Power BI Desktop.

    ![](../media/Lab-01/image6.png)

2. Una vez que aparezca el cuadro de diálogo "Introduzca su dirección
    de correo electrónico", copie el **Nombre de usuario** y péguelo en
    el campo **Correo electrónico** del cuadro de diálogo, y seleccione
    **Continuar**.

    - Correo electrónico/nombre de usuario: <inject key="AzureAdUserEmail"></inject>

      ![](../media/Lab-01/image7.png)

3. En la pestaña de inicio de sesión de Microsoft Azure, verá la
    pantalla de inicio de sesión. Introduzca el siguiente correo
    electrónico/nombre de usuario y luego haga clic en **Siguiente**.

    - Correo electrónico/nombre de usuario: <inject key="AzureAdUserEmail"></inject>

      ![](../media/Lab-01/image8.png)

4. Ahora introduzca el siguiente **Pase de acceso temporal** y haga
    clic en **Iniciar sesión**.

    - Pase de acceso temporal: <inject key="AzureAdUserPassword"></inject>

      ![](../media/Lab-01/image9.png)

5. Se abre el cuadro de diálogo **Sesión iniciada en todas las
    aplicaciones**. Seleccione **OK**.

    ![](../media/Lab-01/image10.png)

6. **Ya está todo listo.** Se abre un cuadro de diálogo. Seleccione
    **Listo**.

Ahora se abrirá Power BI Desktop.

## Tarea 2: Analizar el informe de Power BI Desktop

El siguiente informe analiza las ventas de Fabrikam. Los KPI se enumeran
en la parte superior izquierda de la página. Los objetos visuales
restantes resaltan Sales a lo largo del tiempo, por territorio, grupo de
productos y empresa revendedora.

![](../media/Lab-01/image11.jpeg)

>**Nota:** En esta formación, nos centraremos en la adquisición,
transformación y modelado de datos mediante las herramientas disponibles
en Fabric. No nos centraremos en el desarrollo de informes ni en la
navegación. Dediquemos un par de minutos a comprender el informe y
avancemos a los siguientes pasos.

1. Analicemos los datos por zona de ventas. Seleccione **New England en
    el objeto visual Sales Territory** (gráfico de dispersión). Vea que
    en las Ventas a lo largo del tiempo, el revendedor Tailspin Toys
    tiene más ventas en comparación con Wingtip Toys en New England. Si
    observa el gráfico de columnas de YoY% de ventas, notará que el
    crecimiento de las ventas de Wingtip Toys ha sido bajo y ha
    disminuido trimestre tras trimestre durante el año pasado. Tras
    un pequeño repunte en el tercer trimestre, volvió a bajar en el
    cuarto.

    ![](../media/Lab-01/image12.jpeg)

2. Comparemos esto con la zona de las Rocky Mountains. Seleccione
    **Rocky Mountains en el objeto visual Sales Territory** (gráfico de
    dispersión). Observe que en el gráfico de columnas YoY% de ventas,
    las ventas de Wingtip Toys aumentaron drásticamente en el cuarto
    trimestre de 2023 después de haber sido bajas durante los dos
    trimestres anteriores.

    ![](../media/Lab-01/image13.jpeg)

3. Seleccione **Rocky Mountains en el objeto visual Sales Territory**
    para eliminar el filtro.

4. Desde el objeto visual Gráfico de dispersión en la parte inferior
    central de la pantalla (Pedidos de venta por Sales), seleccione el
    valor atípico en la parte superior derecha (4.º cuadrante). Observe
    que el porcentaje de margen es del 52 %, que está por encima del
    promedio del 50 %. Además, el porcentaje de ventas interanuales ha
    subido los dos últimos trimestres de 2023.

    ![](../media/Lab-01/image14.jpeg)

5. Seleccione el Reseller atípico en el objeto visual del gráfico de
    dispersión para **eliminar el filtro**.

6. Obtengamos los detalles del producto por grupo de productos y
    revendedor. En el objeto visual del gráfico de barras de Sales por
    Product Group y Reseller Company, **haga clic en la barra de
    Packaging Materials de Tailspin Toys** y, en el cuadro de diálogo,
    seleccione **Obtener detalles -> Product Detail**.

    ![](../media/Lab-01/image15.png)

7. Se le dirigirá a la página que proporciona los detalles del
    producto. Tenga en cuenta que también hay algunos pedidos futuros.

8. Una vez que haya terminado de revisar esta página, seleccione
    **Ctrl+flecha hacia atrás** en la parte superior izquierda de la
    página para volver al informe de ventas.

    ![](../media/Lab-01/image16.png)

9. Analice el informe a su gusto. Una vez listo, veamos la vista del
    modelo. En el panel
    de la izquierda, seleccione el **icono Vista del modelo**.

    ![](../media/Lab-01/image17.png)

10. Observe que hay dos tablas de hechos, Sales y PO.

    a. La granularidad de Sales de ventas se organiza por Date,
    Reseller, Product y People. Date, Reseller, Product y People se
    conectan con Sales.

    b. La granularidad de los datos de PO se organiza por Date, Product
    y People. Date, Product y People se conectan con PO.

    c. Disponemos de datos de Supplier por Product. Supplier se conecta
    con Product.

    d. Contamos con datos de ubicación de Reseller por Geo. Geo se
    conecta con Reseller.

    e. Disponemos de información de Customer por Reseller. Customer se
    conecta con Reseller.

## Tarea 3: Revisar consultas de Power Query

1. Echemos un vistazo a Power Query para entender los orígenes de
    datos. En la cinta de opciones, seleccione **Inicio -> Transformar
    datos**.

    ![](../media/Lab-01/image18.png)

2. Se abre la ventana de Power Query. En la cinta de opciones,
    seleccione **Inicio -> Configuración del origen de datos**. Se abre
    el cuadro de diálogo Configuración de origen de datos. A medida que
    se desplaza por la lista, verá que hay cuatro orígenes de datos,
    como se menciona en el planteamiento del problema:

    - Snowflake

    - SharePoint

    - ADLS Gen2

    - Dataverse

3. Seleccione **Cerrar** para cerrar el cuadro de diálogo Configuración
    de origen de datos.

    ![](../media/Lab-01/image19.png)

4. En el panel Consultas de la izquierda, observe que las consultas
    están agrupadas por origen deṣdatos.

5. Vea que la carpeta **DataverseData** tiene datos de Customer
    disponibles en cuatro consultas diferentes: BabyBoomer, GenX, GenY y
    GenZ. Estas cuatro consultas se adjuntan para crear la consulta
    Customer.

6. Haga clic en la consulta Customer en la ventana Consultas. Al
    seleccionar esta consulta, tendrá que volver a escribir sus
    credenciales de Dataverse. Haga clic en **Editar credenciales**.

    ![](../media/Lab-01/image20.png)

7. Haga clic en **iniciar sesión** para iniciar sesión en la cuenta.

    ![](../media/Lab-01/image21.png)

8. Puede escribir las credenciales para el origen de datos de Dataverse
    si escribe el **nombre de usuario** y la contraseña. Las
    credenciales se proporcionan a **continuación**. Cuando termine,
    seleccione **Conectar**.

    - Correo electrónico/nombre de usuario: <inject key="AzureAdUserEmail"></inject>

    - Contraseña: <inject key="AzureAdUserPassword"></inject>

9. Haga clic en la consulta **ADLS Base Folder** en la ventana
    Consultas. Al seleccionar esta consulta, tendrá que volver a
    escribir las credenciales. Haga clic en **Editar credenciales**.

    ![](../media/Lab-01/image22.png)

10. Para el origen de datos ADLS, elija la opción **Firma de acceso
    compartido** **(SAS)** e introduzca el **token de SAS** que se
    proporciona a continuación. Después, seleccione **Conectar**.

    - **Token de SAS:** se encuentra en la pestaña Entorno.<inject key="Sas token"></inject>

      ![](../media/Lab-01/image23.png)

11. Observe que la carpeta **ADLSData** tiene varias dimensiones: Geo,
    Product, Reseller y Date. También tiene datos de Sales.

    - **Dimensión Geo** se crea mediante la combinación de datos de la
      consulta de Cities, Countries y States.

    - **Dimensión de Product** se crea mediante la combinación de datos
      de la consulta Product Groups y Product Item Group.

    - **Dimensión de Reseller** se filtra mediante la consulta
      BuyingGroup.

    - **Datos de Sales** se crea mediante la combinación de
      InvoiceLineItems con la consulta Invoice.

12. Para el origen de datos de Snowflake, seleccione la consulta
    **SupplierCategories** en la ventana Consultas. Al seleccionar esta
    consulta, se le pedirá que escriba las credenciales. Haga clic en
    **Editar credenciales**.

    ![](../media/Lab-01/image24.png)

13. Introduzca el **nombre de usuario de Snowflake** y la **contraseña
    de Snowflake** que se proporcionan a continuación. Use estas
    credenciales para conectar todas las tablas de Snowflake con
    Snowflake y luego seleccione **Conectar**.

    - **Nombre de usuario de Snowflake:** <inject key="SnowFlake Username" enableCopy="false" />

    - **Contraseña de Snowflake:** <inject key="SnowFlake Password" enableCopy="false" />

    >**Nota:** Si tiene algún problema para conectarse a Snowflake con las
    credenciales anteriores, utilice las credenciales de copia de seguridad
    que se proporcionan a continuación.*

    - **Nombre de usuario de Snowflake:** SNOWFLAKE_BACKUP

    - **Contraseña de Snowflake:** 8UpfRpExVDXv2AC1

14. Observe que la carpeta **SnowflakeData** tiene la dimensión Supplier
    y los datos de PO (pedido/gasto).

    - **Dimensión de Supplier** se crea mediante la combinación de la
      consulta de Suppliers con la consulta SupplierCategories.

    - **Datos de PO** se crea mediante la combinación de PO con la
      consulta PO Line Items.

15. Para el origen de datos de SharePoint, seleccione la consulta
    **People** en la ventana Consultas. Al seleccionar esta consulta, se
    le pedirá que escriba las credenciales. Haga clic en **Editar
    credenciales**.

    ![](../media/Lab-01/image25.png)

16. Seleccione la opción **Cuenta de Microsoft** y, a continuación, haga
    clic en **Iniciar sesión**. Introduzca el nombre de usuario y la
    contraseña que se proporcionan a continuación
    y luego seleccione **Conectar**.

    - **Correo electrónico/nombre de usuario:** <inject key="AzureAdUserEmail"></inject>

    - **Contraseña:** <inject key="AzureAdUserPassword"></inject>

      ![](../media/Lab-01/image26.png)

17. Observe que la carpeta **SharepointData** tiene la dimensión People.

    ![](../media/Lab-01/image27.png)

    Ahora sabemos a qué nos enfrentamos. En los siguientes laboratorios,
    crearemos una consulta de Power Query similar mediante el flujo de datos
    Gen2 y haremos modelos mediante un Lakehouse.

# Referencias

Fabric Analyst in a Day (FAIAD) le presenta algunas funciones clave
disponibles en Microsoft Fabric. En el menú del servicio, la sección
Ayuda (?) tiene vínculos a algunos recursos excelentes.

![](../media/Lab-01/image28.png)

Estos son algunos recursos más que podrán ayudarle a seguir avanzando
con Microsoft Fabric.

- Vea la publicación del blog para leer el [anuncio de disponibilidad
  general de Microsoft Fabric
  completo](https://aka.ms/Fabric-Hero-Blog-Ignite23).

- Explore Fabric a través de la [Visita
  guiada](https://aka.ms/Fabric-GuidedTour)

- Regístrese en la [prueba gratuita de Microsoft
  Fabric](https://aka.ms/try-fabric)

- Visite el [sitio web de Microsoft
  Fabric](https://aka.ms/microsoft-fabric)

- Adquiera nuevas capacidades mediante la exploración de los [módulos de
  aprendizaje de Fabric](https://aka.ms/learn-fabric)

- Explore la [documentación técnica de
  Fabric](https://aka.ms/fabric-docs)

- Lea el libro [electrónico gratuito sobre cómo empezar a usar
  Fabric](https://aka.ms/fabric-get-started-ebook)

- Únase a la [comunidad de Fabric](https://aka.ms/fabric-community) para
  publicar sus preguntas, compartir sus comentarios y aprender de otros

Obtenga más información en los blogs de anuncios de la experiencia
Fabric:

- [Experiencia de Data Factory en el blog de
  Fabric](https://aka.ms/Fabric-Data-Factory-Blog)

- [Experiencia de Synapse Data Engineering en el blog de
  Fabric](https://aka.ms/Fabric-DE-Blog)

- [Experiencia de Synapse Data Science en el blog de
  Fabric](https://aka.ms/Fabric-DS-Blog)

- [Experiencia de Synapse Data Warehousing en el blog de
  Fabric](https://aka.ms/Fabric-DW-Blog)

- [Experiencia de Synapse Real-Time Analytics en el blog de
  Fabric](https://aka.ms/Fabric-RTA-Blog)

- [Blog de anuncios de Power BI](https://aka.ms/Fabric-PBI-Blog)

- [Experiencia de Data Activator en el blog de
  Fabric](https://aka.ms/Fabric-DA-Blog) 

- [Administración y gobernanza en el blog de
  Fabric](https://aka.ms/Fabric-Admin-Gov-Blog)

- [OneLake en el blog de Fabric](https://aka.ms/Fabric-OneLake-Blog)

- [Blog de integración de Dataverse y Microsoft
  Fabric](https://aka.ms/Dataverse-Fabric-Blog)

© 2026 Microsoft Corporation. Todos los derechos reservados.

Al participar en esta demostración o laboratorio práctico, acepta las
siguientes condiciones:

Microsoft Corporation pone a su disposición la tecnología o
funcionalidad descrita en esta demostración/laboratorio práctico con
el fin de obtener comentarios por su parte y de facilitarle una
experiencia de aprendizaje. Esta demostración/laboratorio práctico
solo se puede usar para evaluar las características de tal tecnología
o funcionalidad y para proporcionar comentarios a Microsoft. No se
puede usar para ningún otro propósito. Ninguna parte de esta
demostración/laboratorio práctico se puede modificar, copiar,
distribuir, transmitir, mostrar, realizar, reproducir, publicar,
licenciar, transferir ni vender, ni tampoco crear trabajos derivados
de ella.

LA COPIA O REPRODUCCIÓN DE ESTA DEMOSTRACIÓN/LABORATORIO PRÁCTICO (O
PARTE DE ELLA) EN CUALQUIER OTRO SERVIDOR O UBICACIÓN PARA SU
REPRODUCCIÓN O DISTRIBUCIÓN POSTERIOR QUEDA EXPRESAMENTE PROHIBIDA.

ESTA DEMOSTRACIÓN/LABORATORIO PRÁCTICO PROPORCIONA CIERTAS FUNCIONES
Y CARACTERÍSTICAS DE PRODUCTOS O TECNOLOGÍAS DE SOFTWARE (INCLUIDOS
POSIBLES NUEVOS CONCEPTOS Y CARACTERÍSTICAS) EN UN ENTORNO SIMULADO
SIN INSTALACIÓN O CONFIGURACIÓN COMPLEJA PARA EL PROPÓSITO ARRIBA
DESCRITO. LA TECNOLOGÍA/CONCEPTOS DESCRITOS EN ESTA
DEMOSTRACIÓN/LABORATORIO PRÁCTICO NO REPRESENTAN LA FUNCIONALIDAD
COMPLETA DE LAS CARACTERÍSTICAS Y, EN ESTE SENTIDO, ES POSIBLE QUE NO
FUNCIONEN DEL MODO EN QUE LO HARÁN EN UNA VERSIÓN FINAL. ASIMISMO,
PUEDE QUE NO SE PUBLIQUE UNA VERSIÓN FINAL DE TALES CARACTERÍSTICAS O
CONCEPTOS. DE IGUAL MODO, SU EXPERIENCIA CON EL USO DE ESTAS
CARACTERÍSTICAS Y FUNCIONALIDADES EN UN ENTORNO FÍSICO PUEDE SER
DIFERENTE.

**COMENTARIOS.** Si envía comentarios a Microsoft sobre las
características, funcionalidades o conceptos de tecnología descritos
en esta demostración/laboratorio práctico, acepta otorgar a Microsoft,
sin cargo alguno, el derecho a usar, compartir y comercializar sus
comentarios de cualquier modo y para cualquier fin. También concederá
a terceros, sin cargo alguno, los derechos de patente necesarios para
que sus productos, tecnologías y servicios usen o interactúen con
cualquier parte específica de un software o servicio de Microsoft que
incluya los comentarios. No enviará comentarios que estén sujetos a
una licencia que obligue a Microsoft a conceder su software o
documentación bajo licencia a terceras partes porque incluyamos sus
comentarios en ellos. Estos derechos seguirán vigentes después del
vencimiento de este acuerdo.

MICROSOFT CORPORATION RENUNCIA POR LA PRESENTE A TODAS LAS GARANTÍAS Y
CONDICIONES RELATIVAS A LA DEMOSTRACIÓN/LABORATORIO PRÁCTICO, INCLUIDA
CUALQUIER GARANTÍA Y CONDICIÓN DE COMERCIABILIDAD (YA SEA EXPRESA,
IMPLÍCITA O ESTATUTARIA), DE IDONEIDAD PARA UN FIN DETERMINADO, DE
TITULARIDAD Y DE AUSENCIA DE INFRACCIÓN. MICROSOFT NO DECLARA NI
GARANTIZA LA EXACTITUD DE LOS RESULTADOS, EL RESULTADO DERIVADO DE LA
REALIZACIÓN DE LA DEMOSTRACIÓN/LABORATORIO PRÁCTICO NI LA IDONEIDAD DE
LA INFORMACIÓN CONTENIDA EN ELLA CON NINGÚN PROPÓSITO.

**DECLINACIÓN DE RESPONSABILIDADES**

Esta demostración/laboratorio práctico contiene solo una parte de las
nuevas características y mejoras realizadas en Microsoft Power BI.
Puede que algunas de las características cambien en versiones futuras
del producto. En esta demostración/laboratorio práctico, conocerá
algunas de estas nuevas características, pero no todas.
