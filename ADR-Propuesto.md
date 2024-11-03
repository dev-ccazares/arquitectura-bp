# ADR: Uso de GraphQL con Backend for Frontend (BFF)

## Contexto

El sistema de banca digital requiere un método eficiente para gestionar y servir los datos desde el backend hacia múltiples plataformas en el frontend (web y móvil), cada una con sus propios requerimientos de datos y estructura. Actualmente, el sistema utiliza REST para las comunicaciones entre frontend y backend. Sin embargo, REST ha mostrado limitaciones en términos de sobrecarga de datos y flexibilidad, especialmente cuando los requerimientos de datos varían entre la SPA web y la aplicación móvil.

Además, mantener la consistencia en los datos y la experiencia de usuario entre las plataformas es crucial, al igual que optimizar la eficiencia en la transferencia de datos debido a las limitaciones de latencia y recursos de la aplicación móvil.

### Fuerzas

- **Flexibilidad de Datos**: La SPA y la aplicación móvil requieren diferentes cantidades y formatos de datos, por lo que es esencial un sistema que permita esta flexibilidad sin necesidad de realizar múltiples llamadas o manejar datos innecesarios.
- **Costos de Desarrollo**: La implementación debe ser sostenible en términos de costos de desarrollo y mantenimiento.
- **Rendimiento**: Minimizar la latencia y el tamaño de los datos transferidos es clave, particularmente para la aplicación móvil.
- **Facilidad de Escalabilidad**: La solución debe ser escalable para adaptarse a futuros requerimientos de la aplicación sin un rediseño completo.

## Decisión

Nosotros implementaremos **GraphQL** en conjunto con un **Backend for Frontend (BFF)** para manejar las necesidades de datos específicas de cada plataforma frontend (web y móvil). El BFF actuará como intermediario entre el frontend y los servicios de backend, gestionando las consultas de GraphQL para cada plataforma de manera optimizada.

## Justificación

La elección de GraphQL permite al frontend solicitar solo los datos que necesita, lo que reduce la sobrecarga de datos y mejora el rendimiento, especialmente en conexiones móviles. Al combinar GraphQL con un BFF específico para cada plataforma (SPA web y aplicación móvil), aseguramos que cada frontend tenga acceso a los datos necesarios sin recibir información irrelevante.

### Alternativas Rechazadas

1. **REST con BFF**: Aunque REST combinado con BFF hubiera reducido la sobrecarga de datos en comparación con un enfoque REST tradicional, la flexibilidad de GraphQL para definir estructuras de datos específicas se ajusta mejor a nuestras necesidades.
2. **GraphQL sin BFF**: Esta opción fue considerada, pero un enfoque de BFF dedicado permite una mejor segmentación de las responsabilidades de cada plataforma y facilita la escalabilidad de la solución.
3. **Mantener REST sin BFF**: Esta opción no permite la flexibilidad y eficiencia necesarias, y se descarta en favor de una solución más adaptativa.

## Estado

Propuesto

## Consecuencias

- **Positivas**:
  - Reducción en la sobrecarga de datos y mejora en el rendimiento, especialmente en la aplicación móvil.
  - Mayor flexibilidad en las consultas de datos, permitiendo a cada plataforma solicitar exactamente lo que necesita.
  - Facilita la escalabilidad y la introducción de nuevas plataformas en el futuro.
- **Negativas**:
  - Aumenta la complejidad de la arquitectura y el número de componentes a mantener.
  - Requiere un conocimiento adicional de GraphQL y BFF, lo que implica capacitación para el equipo de desarrollo.
  - Posible incremento inicial en los costos de desarrollo para implementar y probar la solución.
