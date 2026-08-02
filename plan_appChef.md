# Plan de la aplicación

La idea tiene bastante potencial porque no es solamente una aplicación de recetas: sería un asistente de alimentación doméstica que conecta inventario, compras, vencimientos, recetas, nutrición y planificación.

El ciclo principal sería:

Compro alimentos → registro lo que tengo → la aplicación propone qué cocinar → selecciono un menú → se descuentan ingredientes → se genera la próxima lista de compras.

## 1. Definición del producto

La aplicación debería resolver principalmente cuatro problemas:

- No saber qué cocinar.
- Perder alimentos porque vencen o se dañan.
- Terminar comprando comida rápida por falta de planificación.
- Comprar ingredientes sin saber qué hace falta realmente.

Una posible propuesta de valor sería:

> “Una aplicación que convierte los alimentos disponibles en casa en un menú semanal práctico, saludable y personalizado, reduciendo desperdicios y compras innecesarias.”

## 2. Funcionalidades de la aplicación

### A. Inventario de alimentos del hogar

Sería el núcleo del sistema.

Cada producto debería registrar:

- Nombre del alimento.
- Categoría: carnes, vegetales, lácteos, granos, condimentos, etc.
- Cantidad.
- Unidad: gramos, kilogramos, unidades, mililitros, tazas.
- Fecha de compra.
- Fecha estimada de vencimiento.
- Ubicación: refrigerador, congelador, despensa.
- Precio.
- Marca, opcional.
- Código de barras, opcional.
- Fotografía del producto, opcional.
- Estado: disponible, próximo a vencer, agotado o descartado.

La aplicación debería permitir registrar alimentos de varias maneras:

- Manualmente.
- Escaneando el código de barras.
- Fotografiando una factura.
- Repitiendo una compra anterior.
- Seleccionando productos frecuentes.

Para el MVP empezaría con registro manual y productos frecuentes. El reconocimiento de facturas y alimentos mediante IA puede añadirse posteriormente.

### B. Control de vencimientos

El sistema debería priorizar automáticamente los ingredientes que se pueden perder.

Por ejemplo:

> “Tienes pollo que debería utilizarse en los próximos dos días. Estas son tres recetas compatibles con los demás ingredientes disponibles.”

También podría presentar:

- Productos que vencen esta semana.
- Alimentos abiertos.
- Productos congelados desde hace mucho tiempo.
- Dinero aproximado en riesgo de desperdiciarse.
- Historial de productos descartados.

Este último dato puede ser motivador:

> “Este mes evitaste desperdiciar aproximadamente ₡12.500 en alimentos.”

### C. Base de datos de recetas

Cada receta debería incluir:

- Nombre.
- Descripción.
- Ingredientes y cantidades.
- Porciones.
- Tiempo de preparación.
- Tiempo de cocción.
- Dificultad.
- Utensilios requeridos.
- Pasos.
- Categoría: desayuno, almuerzo, cena o merienda.
- Tipo de cocina.
- Valores nutricionales aproximados.
- Ingredientes sustituibles.
- Condiciones alimentarias: vegetariana, sin gluten, alta en proteína, etc.
- Costo aproximado por porción.

Conviene separar dos tipos de recetas:

- Recetas verificadas, cargadas y estructuradas dentro de la plataforma.
- Recetas personales, creadas o adaptadas por el usuario.

La aplicación también debería permitir guardar modificaciones. Por ejemplo:

> “La última vez usaste menos chile dulce y agregaste queso.”

### D. Motor de compatibilidad entre inventario y recetas

Esta sería la funcionalidad diferenciadora.

Cada receta podría recibir una puntuación basada en:

- Porcentaje de ingredientes disponibles.
- Cantidad de ingredientes faltantes.
- Cercanía de vencimiento de los ingredientes.
- Tiempo disponible para cocinar.
- Preferencias del usuario.
- Objetivo nutricional.
- Historial de platos recientes.
- Nivel de dificultad.
- Presupuesto.

Ejemplo:

| Receta | Compatibilidad | Faltantes | Motivo |
|---|---:|---:|---|
| Arroz con pollo | 92% | 1 | Utiliza pollo próximo a vencer |
| Pasta con vegetales | 85% | 2 | Rápida y utiliza vegetales disponibles |
| Lentejas con huevo | 80% | 1 | Alta en proteína y bajo costo |

La aplicación no debería limitarse a decir “puedes preparar esto”. También debería explicar el motivo:

> “Te recomiendo esta receta porque ya tienes 8 de sus 9 ingredientes, utiliza dos productos próximos a vencer y toma 25 minutos.”

### E. Generador de menú semanal

El usuario debería indicar:

- Cuántas personas comen.
- Cuáles días necesita planificar.
- Qué tiempos de comida necesita.
- Tiempo disponible para cocinar.
- Presupuesto semanal.
- Objetivo: comer más saludable, gastar menos, usar inventario o aumentar proteína.
- Días en los que probablemente comerá fuera.
- Si acepta repetir alimentos o aprovechar sobras.

El menú debería considerar la reutilización inteligente de preparaciones.

Ejemplo:

- Lunes: pollo al horno.
- Martes: tacos con el pollo restante.
- Miércoles: ensalada con vegetales abiertos.
- Jueves: arroz salteado con sobrantes.
- Viernes: receta rápida o flexible.

Esto es mejor que generar siete recetas independientes, porque cocinar diariamente desde cero puede ser poco realista.

### F. Lista automática de compras

Después de seleccionar el menú, la aplicación calcularía:

Ingredientes requeridos − inventario disponible = lista de compras.

La lista debería agruparse por:

- Frutas y vegetales.
- Carnes.
- Refrigerados.
- Despensa.
- Limpieza u otros, si posteriormente se amplía.

También debería:

- Unificar cantidades de varias recetas.
- Convertir unidades.
- Evitar comprar productos que ya existen.
- Mostrar qué receta utiliza cada producto.
- Permitir marcar productos comprados.
- Ingresar automáticamente lo comprado al inventario.
- Mostrar un costo estimado.
- Identificar compras opcionales.

Ejemplo:

> Necesitas 500 g de pollo. Tienes 200 g. Agregar a la lista: 300 g.

### G. Nutrición y calorías

Puede utilizarse una fuente nutricional estructurada, como FoodData Central del USDA, que dispone de una API para integrar información de alimentos y nutrientes en aplicaciones. FoodData Central

La aplicación podría calcular aproximadamente:

- Calorías.
- Proteína.
- Carbohidratos.
- Grasas.
- Fibra.
- Sodio.
- Azúcares.
- Distribución por comida y por día.

Sin embargo, deben mostrarse como estimaciones, porque cambian según la marca, cantidad real, método de cocción y tamaño de las porciones.

En una primera versión no intentaría convertir la aplicación en un sistema clínico. Presentaría información como:

> “Estimación nutricional basada en los ingredientes y porciones registrados. No sustituye asesoría profesional.”

### H. Experiencia culinaria y motivación

Esta parte puede marcar una diferencia importante frente a una aplicación tradicional de inventario.

Podría incluir:

- Racha de días cocinando.
- Meta semanal: cocinar tres o cuatro veces.
- Nivel culinario.
- Nuevas técnicas aprendidas.
- Recetas favoritas.
- Desafíos semanales.
- Historial visual de platos.
- Indicador de ahorro.
- Indicador de alimentos rescatados.
- Logros no infantiles, pero sí motivadores.

Ejemplos:

- “Esta semana cocinaste cuatro veces.”
- “Utilizaste todos los vegetales antes de vencer.”
- “Preparaste tu primera salsa casera.”
- “Gastaste aproximadamente un 25% menos que comprando fuera.”

También puede existir un modo guiado de cocina:

- Preparar ingredientes.
- Mostrar un paso por pantalla.
- Temporizadores integrados.
- Lectura en voz alta.
- Alertas para empezar el siguiente paso.
- Sustituciones cuando falta algo.

### I. Perfil y personalización

El usuario debería configurar:

- Cantidad de personas en el hogar.
- Preferencias alimentarias.
- Alergias.
- Ingredientes que no consume.
- Nivel de cocina.
- Electrodomésticos disponibles.
- Objetivo nutricional.
- Presupuesto.
- Tiempo habitual disponible.
- Tamaño preferido de las porciones.
- Días habituales de compra.
- Supermercados frecuentes.

Más adelante podría soportarse un hogar compartido, donde varias personas actualicen el mismo inventario y lista de compras.

## 3. Alcance recomendado para el MVP

No desarrollaría todo desde el inicio. La primera versión debería demostrar que el ciclo central realmente funciona.

### MVP 1: validación personal

- Registro e inicio de sesión.
- Inventario manual.
- Registro de cantidades y vencimientos.
- Base inicial de recetas.
- Comparación receta–inventario.
- Recomendaciones según ingredientes disponibles.
- Menú semanal básico.
- Lista automática de compras.
- Marcar una receta como preparada.
- Descontar ingredientes utilizados.

La nutrición podría comenzar con valores aproximados cargados en las recetas, sin integrar todavía todos los productos comerciales.

### Segunda etapa

- Código de barras.
- Información nutricional por API.
- Perfiles alimentarios.
- Inventario compartido.
- Notificaciones de vencimiento.
- Costos y presupuesto.
- Registro rápido de compras.
- Fotografías de platos.
- Sustituciones inteligentes.
- Reconocimiento de facturas.

### Tercera etapa

- Generación y adaptación de recetas con IA.
- Asistente conversacional.
- Integración con supermercados.
- Comparación de precios.
- Planes nutricionales avanzados.
- Recomendaciones según actividad física.
- Integración con Apple Health o Google Health Connect.
- Plataforma para nutricionistas o creadores de recetas.

## 4. Web, móvil o ambas

Mi recomendación sería pensarla como una aplicación principalmente móvil, porque el usuario necesita interactuar con ella:

- En el supermercado.
- Frente al refrigerador.
- Mientras cocina.
- Al escanear productos.
- Al revisar la lista de compras.

No obstante, una versión web es útil para:

- Administrar recetas.
- Analizar gastos.
- Configurar el hogar.
- Revisar estadísticas.
- Cargar información de manera masiva.

### Recomendación

Desarrollar una base compartida para:

- Android.
- iOS.
- Web.

Expo con React Native y TypeScript permite construir desde un mismo proyecto aplicaciones para Android, iOS y web. Expo Documentation

Esto no significa que todas las pantallas deban ser idénticas. La interfaz móvil puede enfocarse en el uso diario, mientras que la web puede presentar una administración más amplia.

## 5. Stack tecnológico recomendado

### Frontend

#### Recomendación principal

- React Native
- Expo
- TypeScript
- Expo Router
- Biblioteca de componentes propia o una librería compatible con React Native.
- TanStack Query para sincronización y caché.
- Zustand para estados locales sencillos.

Razones:

- Un solo ecosistema para móvil y web.
- Buena experiencia para escáner, cámara y notificaciones.
- TypeScript en frontend y funciones del backend.
- Menor costo inicial que mantener tres aplicaciones completamente separadas.

Expo se presenta precisamente como una forma de construir una aplicación universal para Android, iOS y web desde un proyecto JavaScript/TypeScript. Expo Documentation

### Backend y base de datos

#### Recomendación inicial: Supabase

- PostgreSQL.
- Autenticación.
- API automática.
- Almacenamiento de imágenes.
- Seguridad mediante Row Level Security.
- Funciones de servidor.
- Tareas programadas.
- Eventos en tiempo real.

Supabase proporciona una base PostgreSQL y servicios integrados de autenticación, almacenamiento, APIs y funciones de servidor, lo que reduce bastante la infraestructura necesaria durante un MVP. Supabase

Las Edge Functions pueden utilizarse para integraciones, webhooks y lógica que no debería ejecutarse directamente en el dispositivo. Supabase

#### Alternativa para mayor control

Cuando el producto crezca:

- Backend con FastAPI o NestJS.
- PostgreSQL administrado.
- Redis.
- Almacenamiento S3 compatible.
- Workers para procesos asíncronos.
- Docker.
- AWS, Azure, Google Cloud o una plataforma más sencilla.

Pero para comenzar, esa infraestructura agregaría trabajo operativo sin validar todavía el producto.

### Arquitectura propuesta

```text
Aplicación móvil / web
        │
        ├── Autenticación
        │
        ├── Inventario
        │
        ├── Recetas
        │
        ├── Menú semanal
        │
        └── Lista de compras
        │
        ▼
Supabase
        ├── PostgreSQL
        ├── Auth
        ├── Storage
        ├── Row Level Security
        └── Edge Functions
                │
                ├── API nutricional
                ├── Servicio de IA
                ├── Notificaciones
                └── Pagos
```

## 6. Modelo inicial de base de datos

Una estructura preliminar podría contener:

```text
users
households
household_members

food_items
food_categories
inventory_items
inventory_movements
purchase_records
purchase_items

recipes
recipe_steps
recipe_ingredients
recipe_categories
recipe_tags

meal_plans
meal_plan_days
meal_plan_items

shopping_lists
shopping_list_items

nutrition_foods
nutrition_values

user_preferences
dietary_restrictions
allergens

cooking_history
food_waste_records
notifications
subscriptions
```

Un concepto importante es no guardar únicamente la cantidad actual. Conviene mantener movimientos de inventario:

- Compra.
- Consumo.
- Ajuste.
- Descarte.
- Vencimiento.
- Donación.

Así se puede saber por qué cambió una cantidad y generar estadísticas confiables.

## 7. Motor de recetas: reglas primero, IA después

No empezaría dejando que una inteligencia artificial decida completamente el menú.

Primero construiría un motor determinístico:

```text
Puntuación =
  ingredientes disponibles
+ prioridad por vencimiento
+ coincidencia con preferencias
+ coincidencia nutricional
+ tiempo disponible
- ingredientes faltantes
- repetición reciente
- costo adicional
```

Luego la IA puede ayudar a:

- Explicar la recomendación.
- Proponer sustituciones.
- Cambiar cantidades.
- Simplificar pasos.
- Adaptar una receta.
- Generar una presentación más natural.
- Crear variantes con los ingredientes disponibles.

De esta forma, la base del sistema sigue siendo auditable. La IA mejora la experiencia, pero no controla datos críticos como inventario, cantidades o restricciones alimentarias.

## 8. Funcionamiento sin conexión

Para una aplicación de supermercado y cocina, cierto nivel de funcionamiento sin conexión sería valioso.

El teléfono debería conservar localmente:

- Lista de compras activa.
- Menú de la semana.
- Recetas seleccionadas.
- Inventario reciente.
- Cambios pendientes de sincronizar.

Podría utilizarse SQLite local en el dispositivo y sincronizar con PostgreSQL cuando regrese la conexión. Para el primer MVP podría utilizarse un caché más sencillo, pero conviene diseñar el modelo pensando en sincronización futura.

## 9. Notificaciones

Notificaciones útiles:

- “El pollo vence mañana.”
- “Tienes tres ingredientes que conviene utilizar esta semana.”
- “Tu menú todavía no está planificado.”
- “Hoy corresponde descongelar la carne de la receta del martes.”
- “Te falta comprar leche y tomate.”
- “No has actualizado el inventario después de tu compra.”

Deben ser configurables para no convertirse en una molestia.

## 10. Pagos y modelo de negocio

Inicialmente no incluiría pagos hasta confirmar que la aplicación genera uso recurrente.

### Modelo freemium posible

#### Gratuito

- Un hogar.
- Inventario básico.
- Cantidad limitada de recetas guardadas.
- Menú semanal.
- Lista de compras.
- Alertas básicas.

#### Premium

- Hogar compartido.
- Nutrición avanzada.
- Historial completo.
- Escaneo de facturas.
- Generación de recetas con IA.
- Presupuestos.
- Estadísticas de ahorro.
- Planificación automática.
- Integraciones externas.
- Sincronización avanzada.

### Forma de cobro

- Suscripción mensual.
- Suscripción anual con descuento.
- Eventualmente un plan familiar.

Stripe ofrece herramientas para cobros únicos, pagos móviles y suscripciones. Documentación de Stripe

Sin embargo, para funciones digitales vendidas dentro de una aplicación móvil también se deben revisar las políticas vigentes de Apple y Google antes de lanzar. Por eso aislaría la lógica de suscripciones en el backend y no la mezclaría con el funcionamiento principal de recetas o inventario.

## 11. Infraestructura por etapas

### Etapa de desarrollo

- Expo.
- Supabase.
- Repositorio GitHub.
- Entornos de desarrollo y producción separados.
- Expo Application Services para compilaciones.
- Servicio externo de errores y telemetría.
- API nutricional.
- Sin pagos inicialmente.

### Etapa de lanzamiento

- Aplicación Android.
- Aplicación web.
- iOS cuando el flujo esté validado.
- Base de datos con backups.
- Monitoreo de errores.
- Política de privacidad.
- Eliminación y exportación de cuenta.
- Gestión de consentimiento.
- Términos de uso.
- Sistema de suscripciones.

### Etapa de crecimiento

- API backend independiente.
- Caché y workers.
- Motor de recomendaciones separado.
- Almacenamiento optimizado.
- Búsqueda especializada de recetas.
- Analítica de producto.
- Procesamiento de imágenes y facturas.
- Infraestructura regional si el volumen lo justifica.

## 12. Costos que habría que contemplar

Aunque muchos servicios tienen planes iniciales gratuitos, eventualmente existirán costos por:

- Base de datos y almacenamiento.
- Compilación y distribución móvil.
- Cuenta de desarrollador de Apple.
- Cuenta de Google Play.
- Correos transaccionales.
- Notificaciones.
- Servicio de IA.
- Procesamiento de imágenes.
- API de códigos de barras o alimentos.
- Monitoreo de errores.
- Pasarela de pagos.
- Dominio.
- Soporte y mantenimiento.
- Contenido inicial de recetas.

El mayor costo probablemente no será la infraestructura durante el MVP, sino:

- Desarrollo.
- Diseño de experiencia.
- Normalización de recetas.
- Conversión de unidades.
- Calidad de los datos nutricionales.
- Precisión del inventario.

## 13. Riesgos principales

### Registro demasiado trabajoso

Si registrar cada producto toma mucho tiempo, el usuario abandonará la aplicación.

Solución:

- Productos recientes.
- Compras frecuentes.
- Registro en pocos toques.
- Escaneo.
- Copiar compra anterior.
- Ajustes aproximados.

### Inventario desactualizado

El sistema puede recomendar algo que ya no existe.

Solución:

- Confirmación rápida antes de generar el menú.
- Preguntar “¿Todavía tienes estos productos?”.
- Descontar automáticamente después de cocinar.
- Permitir marcar cantidades como aproximadas.

### Recetas demasiado complejas

Una receta técnicamente compatible puede no ser práctica.

Solución:

- Considerar tiempo, dificultad, utensilios y nivel culinario.
- Tener un modo “necesito cocinar algo en 15 minutos”.
- Tener recetas de emergencia con pocos ingredientes.

### Datos nutricionales imprecisos

Solución:

- Mostrar estimaciones.
- Registrar porciones.
- Permitir productos específicos.
- Distinguir entre ingrediente genérico y producto comercial.

### Generación de IA poco confiable

Solución:

- No permitir que la IA modifique directamente inventarios.
- Validar unidades y cantidades.
- Marcar recetas generadas.
- Utilizar reglas para alérgenos y restricciones.
- Mantener recetas verificadas.

## 14. Recomendación concreta de inicio

Yo la construiría así:

**Producto:**

Asistente doméstico de inventario, recetas y planificación.

**Plataformas:**

Android + web inicialmente.

iOS posteriormente o desde el mismo proyecto cuando sea necesario.

**Frontend:**

React Native + Expo + TypeScript.

**Backend:**

Supabase.

**Base de datos:**

PostgreSQL.

**Primera fuente nutricional:**

FoodData Central.

**IA:**

Solo para explicaciones, sustituciones y adaptación de recetas.

**Pagos:**

No en el primer prototipo.

Stripe o gestión equivalente cuando exista validación comercial.

**MVP:**

Inventario + recetas + compatibilidad + menú semanal
+ lista de compras + descuento de ingredientes.

La pantalla principal ideal no sería un inventario lleno de tablas. Sería algo orientado a la decisión inmediata:

> ¿Qué puedes cocinar hoy?
>
> Tienes 6 recetas recomendadas.
>
> 2 utilizan productos próximos a vencer.
>
> Tiempo disponible: 30 minutos.
>
> Objetivo de hoy: comida alta en proteína.

Ese enfoque mantiene la aplicación conectada directamente con el problema que quieres resolver: evitar terminar comprando comida rápida porque no sabes qué preparar.
