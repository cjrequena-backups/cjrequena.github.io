---
layout: post
title: "Arquitectura Orientada a Microservicios"
date: 2016-09-20 06:39:00 +6390
categories: micro-services
lang: es
ref: micro-services-architecture
---

La arquitectura orientada a microservicios, es un método particular de
desarrollar sistemas de software que ha crecido en popularidad en los últimos años.

En esencia, la arquitectura orientada a microservicios es un método de
desarrollo de aplicaciones de software como un conjunto de servicios pequeños,
independientes, desplegables, y modulares en el que cada servicio se ejecuta
en un proceso único y se comunica a través de un mecanismo bien definido, de peso
ligero para servir a un objetivo de negocio. Estos servicios están construidos
sobre las capas de negocio y con independencia de despliegue y totalmente
automatizados.

La forma en la cual los microservicios se comunican entre sí depende de
los requisitos de cada aplicación, sin embargo muchos desarrolladores
utilizan HTTP /REST con JSON o Protobuf. En la mayoría de los casos,
REST (Representational State Transfer) el cual es un método de integración útil
debido a su baja complejidad.

Hay un mínimo de gestión centralizada de estos servicios, que pueden estar
escritos en lenguajes de programación diferentes y que pueden utilizan
diferentes tecnologías de almacenamiento de datos.

La arquitectura orientada a microservicios pone cada elemento de funcionalidad
en un servicio separado y los escala mediante la distribución de estos servicios
a través de servidores, según sea necesario replicar.

### Aplicaciones monoliticas.

Para explicar los microservicios es útil compararlos con una aplicación monolítica
construida como una sola unidad.

Las aplicaciones empresariales se construyen a menudo en tres partes principales:

 -  Una interfaz de usuario del lado del cliente (que consiste en páginas HTML y
 JavaScript que se ejecutan en un navegador en el ordenador del usuario)
 -  Una base de datos (que consta de muchas tablas en una base de datos común y
 por lo general relacional).
 -  Una aplicación del lado del servidor.

La aplicacón del lado del servidor se encargará de las peticiones HTTP,
ejecutará la logica de negocio, recuperará y actualizará datos de la base
de datos, recuperará y rellenará formularios de las vistas HTML que se envian
desde el navegador. Esta aplicación es monolitica (Un único ejecutable logico)
Cualquier cambio en el sistema implica la creación y despliegue de una nueva
version de la aplicación del lado del servidor.

Las aplicaciones monolíticas pueden tener éxito, pero cada vez más personas
se sienten frustradas con ellas, especialmente a medida que más aplicaciones
se están desplegando a la nube.

Un cambio realizado en una pequeña parte de la aplicación, requiere que todo el
sistema deba ser reconstruido y desplegado. Con el tiempo, a menudo es difícil
mantener una buena estructura modular, por lo que es más difícil mantener
los cambios que deberían afectar a un solo módulo dentro de la aplicación.

El escalamiento requiere el despliegue de toda la aplicación en lugar de solo
las partes que requieren un mayor recurso.

Estas frustraciones han llevado a seguir una arquitectura orientada a microservicios,
construyendo un conjunto de servicios. Así como el hecho de que los servicios sean
escalables y posean independencia en el despliegue, puedan ser escritos en distintos
lenguajes de programación y a su vez administrados por distintos equipos.

Desarrollar aplicaciones usando una arquitectura orientada a micro servicios
puede ofrecer un numero significativo de beneficios.

### Agilidad y productividad en el desarrollo

El tamaño y la complejidad de un Microservicio es muy pequeña en comparación
con una gran aplicación monolítica. Un Microservicio también tiene un contexto
limitado y está desacoplado de otros servicios. Además, la descomposición
de lo que solía ser una aplicación monolítica en una colección de
pequeños procesos / funciones reduce drásticamente la complejidad del código
y mejora la productividad de programación.

También hace que sea más fácil escalar el desarrollo con múltiples equipos donde
cada equipo posee una parte independiente de la aplicación que puede funcionar
como un servicio en si mismo. La única pieza clave que necesitan saber es cómo
interactuar con otros servicios.

El riesgo innerte a introducir nuevos cambios se reduce, lo cual permite que la tasa
de cambio aumente desembocando en una mayor agilidad y tiempos de respuestas más rápido.

### Flexibilidad en los despliegues

Debido a que están débilmente acoplados a otros servicios, los microservicios están
versionados de forma independiente y con independencia de despliegue lo que reduce
en gran medida el riesgo de fallos que son inherentes a las aplicaciones grandes y monolíticas.

Por otra parte, el bajo acoplamiento a otros servicios reduce la dependencia de los
desarrolladores de otros equipos y les proporciona la agilidad necesaria para liberar
y poner a prueba nuevas características, prácticamente a la carta, como los nuevos requisitos
y casos de uso que vienen en parte del cliente.

La arquitectura orientada a microservicios también permite flexibilidad en la implementación
en términos de opciones de hardware para los servicios individuales. Algunos servicios pueden
ser altamente informatizados, mientras que otros pueden requerir un uso intensivo de procesamiento o
de memoria.

En lugar de implementar una aplicación entera en un tipo de hardware de computación de alto rendimiento,
los microservicios se pueden implementar en diferentes servidores de configuración de hardware para
maximizar la potencia de cálculo. Esto da lugar a adoptar una plataforma en la nube para minimixar
el coste, maximixar el rendimiento y la capacidad de escalar a demanda sin afectar a los sistemas en absoluto.

### Escalabilidad

La arquitectura orientada a microservicios permite la independencia de escalabilidad,
por lo que sólo los servicios que necesitan escalar lo hacen de manera independiente de
los otros microservicios, en lugar de escalar toda la aplicación, lo que puede ahorrar
una gran cantidad de recursos informáticos. Por ejemplo, si hay más tráfico a un servicio
de búsqueda en comparación con un servicio de autenticación, sólo escalas el servicio de búsqueda.

Debido a su tamaño, flexibilidad de implementación y el contexto limitado,
los microservicios son más fáciles de escalar y más rápido de crear que una instancia
de aplicaciones grandes y monolíticas.

### Identificar y corregir los problemas más rápidamente

La descomposición y el despliegue de las aplicaciones en servicios más pequeños reduce
el tiempo para identificar y corregir fallos. Además, permite el aislamiento de fallos
(por ejemplo: pérdidas de memoria).

### Independencia en la pila de tecnologias

Al estar débilmente acoplados, los microservicios también eliminan muchas limitaciones
en la pila de tecnología, lo que permite a los desarrolladores ser capaces de elegir
el lenguaje de programación en el que sientan más cómodos. Esto hace que sea fácil reemplazar un
servicio cuando existan mejores tecnologías disponibles. Por ejemplo, uno microservicio podría
ser escrito en Java, mientras que otro se podría escribir en node.js.

A medida que evolucionan mejores patrones en cada pila, el código puede ser fácilmente rediseñado y redistribuido.

### Referencias

* [Martin Fowler] - Microservices, a definition of this new architectural term
* [smartbear] - What is Microservices Architecture?
* [jumpintothecloud] - 5 Benefits of Migrating to a Microservice Architecture

[Martin Fowler]: http://martinfowler.com/articles/microservices.html
[SMARTBEAR]: https://smartbear.com/learn/api-design/what-are-microservices/
[jumpintothecloud]: http://jumpintothecloud.net/5-benefits-of-migrating-to-a-microservice-architecture/