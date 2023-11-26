## Comandos iniciales de un proyecto

- `ng new app`: crear una aplicación en el directorio `app`
- `ng new app --no-standalone`: lo mismo pero también creará y usará `src/app/app.module.ts`.
- `ng generate component ruta/de/componente`: crea un componente con sus 4 ficheros asociados.


## Vocabulario

**Módulo:**
  - Son códigos dedicados a resolver un objetivo.
  - Generalmente exportan una clase
  - Toda aplicación posee al menos 1 clase de módulo.
     - que llamamos **módulo raíz**
     - que posee el nombre de `AppModule`
  - Siempre lleva una clase con un decorador `@NgModule`
  - Siempre lleva una serie de propiedades de las cuales se destacan:
     - **Declarations**: define vistas que pertenecen a este módulo.
     - **Exports**: clases que deben ser visibles para otros módulos.
     - **Imports**: clases que otros módulos exportan y que se usan en el módulo actual.
     - **Providers**: servicios globales accesibles desde cualquier parte.
     - **Bootstrap**: vista principal o componente raíz, que contiene a las demás. Esto solo lo establece el móudlo raíz.

**Componente:**
  - Son elementos que controlan una vista. 
  - Define las propiedades y métodos que usa el propio template.
  - Contiene la lógica que usa la vista.
  - Puede tener atributos de entrada con `@Input`.
  - Puede tener atributos de salida con `@Output`.
  - `Componente` = `template` + `metadatos` + `clase`

**Template:**
  - Define la vista de un *Componente* mediante un fragmento de HTML.

**Metadatos:**
  - Permiten decorar una clase y configurar así su comportamiento.
  - Extiende una función mediante otra sin tocar la original.

**Data binding:**
  - Permiten intercambiar datos entre template y clase lógica del componente.
  - Existen 4 tipos:
     - **Interpolación:** muestra el valor de una propiedad.
        - `{{ propiedad }}`
     - **Property binding:** traspaso del objeto del componente padre al hijo.
        - `[objetoHijo]="objetoPadre"`
     - **Event binding:** permite invocar un método del componente pasándole un argumento al producirse un evento.
        - `(click)="accion(parametro)"`
     - **Two-way binding:** binding bidireccional que permite combinar **event binding** y **property binding**.
        - `input [(ngModel)]="objeto"`

**Directiva:**
  - Permiten añadir comportamiento dinámico al HTML mediante una etiqueta o selector.
  - `*ngFor`, `*ngIf`, `NgSwitch`, `NgStyle`, `NgClass`, etc.

**Servicio:**
  - Clases que permiten realizar acciones concretas.
  - Están a disposición abierta de cualquier componente.
  - Típicos ejemplos de uso son:
     - Obtener datos
     - Resolver lógicas especiales
     - Realizar peticiones a un servidor

**Dependency injection:**
  - Permite suministrar funcionalidades, servicios, etc. a un componente sin que sea el propio componente el encargado de crearlos.
  - Utiliza el decorador `@Injectable()`.
  - Normalmente:
     - Proporciona servicios
     - Facilita los tests y la modularidad de código.

## Ficheros más importantes

- `src/main.ts` es el desplegador. No se suele tocar.
- `src/app/app.module.ts` es el módulo raíz de la aplicación.
- `src/app/app.components.ts` es el componente raíz del módulo raíz.
- `src/app/app.component.html` es la plantilla del componente raíz.
- `src/app/app.component.css` son los estilos asociados al componente.
- `src/styles.css` son los estilos globales de la aplicación.
- `src/index.html` es el HTML inicial de la aplicación.

## Definición de componentes

> Un componente es una clase a la que se le añade un decorador `@Component` y que permite crear nuevas etiquetas HTML.

- Los componentes se organizan en forma de árbol.
- La raíz del árbol es un componente principal.
   - Su propiedad `selector` posee el valor `app-root`
   - Gracias al `selector: "app-root"` del `@Component`, éste puede incluirse en nuestro HTML, como en `src/index.html`, que lo usa con `<app-root></app-root>`.
- Los componentes se conforman por 3 partes:
   - **Anotaciones**: Son metadatos que agregamos a nuestro código. Permiten definir ciertas propiedades del componente, como son:
      - `selector`: nombre a utilizar como tag en el HTML.
      - `template`: plantilla a usar para el componente. Usa un String como plantilla.
      - `templateUrl`: lo mismo, pero lo define mediante URL externa.
      - `style`: definición de estilos para plantilla.
      - `styleUrl`: array con distintos archivos de estilos que pueden usarse en el componente.
      - `host`: permite encapsular ciertas partes del componente.
      - `directive`: array con las directivas que pueden usarse en el componente.
      - `input`: variables que recogen información del padre.
      - `output`: variables que pasan información al padre.
   - **Vista:** contiene la plantilla que usaremos para elaborar la pantalla asociada al componente. Puede definirse en un fichero auxiliar o directamente como String.
   - **Controlador:** clase que contendrá la lógica del componente: definiciones, funciones, etc.

Los componentes suelen llevar asociados 4 ficheros:

- `app.component.html`: contiene el código HTML o de marcas de la vista.
- `app.component.css`: contiene el código CSS o de estilos de la vista.
- `app.component.ts`: contiene el código JS o del controlador.
- `app.component.spec.ts`: archivo para tests unitarios.

El código típico de todo componente es así:

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'compo-root',
  templateUrl: './compo.component.html',
  styleUrl: './compo.component.scss'
})
export class AppComponent {
  title = 'compo';
}
```

## Definición de metadatos


- Decorador: `@Input`
- Módulo: `Input`
- `bindingPropertyName: string`

----

- Decorador: `@Output`
- Módulo: `Output`
- `bindingPropertyName: string`

----

- Decorador: `@Attribute`
- Módulo: `Attribute`
- `attributeName: string`

----

- Decorador: `@Hostlistener args: string[]`
- Módulo: `HostListener`
- `eventName: string`

----

- Decorador: `@HostBinding`
- Módulo: `HostBinding`
- `hostPropertyName: string`

----

- Decorador: `@Component`
- Módulo: `Component`
- `animations: any[]`
- `changeDetection: ChangeDetectionStrategy`
- `encapsulation: ViewEncapsulation`
- `entryComponents: Array<Type<any>|any[]>`
- `interpolation: [string, string]`
- `moduleId: string`
- `styles: string[]`
- `styleUrls: string[]`
- `template: string`
- `templateUrl: string`
- `viewProviders: Provider[]`

----

- Decorador: `@Directive`
- Módulo: `Directive`
- `exportAs: string`
- `host: {[key: string]: string}`
- `inputs: string[]`
- `outputs: string[]`
- `providers: Provider[]`
- `queries: {[key: string]: any}`
- `selector: string`

----

- Decorador: `@Host`
- Módulo: `Host`
- ...

----

- Decorador: `@Inject`
- Módulo: `Inject`
- `token: any`

----

- Decorador: `@Injectable`
- Módulo: `Injectable`
- ...

----

- Decorador: `@NgModule`
- Módulo: `NgModule`
- `bootstrap: Array<Type<any>|any[]>`
- `declarations: Array<Type<any>|any[]>`
- `entryComponents: Array<Type<any>|any[]>`
- `exports: Array<Type<any>|any[]>`
- `id: string`
- `imports: Array<Type<any>|ModuleWithProviders|any[]>`
- `providers: Provider[]`
- `schemas:Array<SchemaMetadata|any[]>`

----

- Decorador: `@Optional`
- Módulo: `Optional`
- `...`

----

- Decorador: `@Pipe name: string`
- Módulo: `Pipe`
- `pure: boolean`

----

- Decorador: `@Self`
- Módulo: `Self`
- ...

----

- Decorador: `@SkipSelf`
- Módulo: `SkipSelf`
- ...

Los metadatos más importantes son:

- **Animations:** lista de animaciones del componente.
- **Bootstrap:** dene los componentes que deberían tenerse en cuenta en el
arranque cuando este módulo es Bootstrap.
- **ChangeDetection:** estrategia de detección de cambios utilizada por el
componente.
- **Declarations:** lista de directivas/pipes pertenecientes al módulo.
- **Encapsulation:** estrategia de encapsulación de estilo usada por el
componente.
- **EntryComponents:** lista de componentes que deben compilarse cuando
se dene este módulo.
- **ExportAs:** nombre usado para exportar la instancia del componente en
una plantilla.
- **Exports:** lista de directivas, pipes y módulos que pueden usarse en otros
componentes que tengan importado el módulo en curso.
- **Host:** mapa de propiedad de clase para enlaces de elementos de host para
eventos, propiedades y atributos.
- **Id:** usado para identicar módulos en getModuleFactory.
- **Imports:** lista de módulos cuyas directivas/pipes exportadas pueden
utilizarse en el módulo.
- **Inputs:** lista de nombres de propiedades de clase para enlazar datos como
entradas de componentes.
- **Interpolation:** marcadores de interpolación personalizados utilizados en
la plantilla del componente.
- **ModuleID:** ID del módulo ES/CommonJS del archivo donde se dene el
componente.
- **Outputs:** lista de nombres de propiedades de clase que exponen eventos de
salida a los que otros pueden suscribirse.
- **PreserveWhitespaces:** permite mantener o eliminar espacios en blanco.
- **Providers:** dene el conjunto de objetos inyectables disponibles en el
módulo para este componente y sus hijos.
- **Queries:** consultas que pueden inyectarse en el componente.
- **Schemas:** usado para declarar elementos y propiedades que no son
componentes ni directivas Angular.
- **Selector:** tag con el que se identica el componente en una plantilla.
- **Styles:** estilos “en línea” que hay que aplicar a la vista del componente.
- **StyleUrls:** lista de URL con hojas de estilo que pueden aplicarse a la vista
del componente.
- **Template:** plantilla “en línea” aplicada a la vista del componente.
- **TemplateUrl:** URL que apunta al archivo que contiene la vista del componente.
- **ViewProviders:** lista de proveedores disponibles para el componente e hijos.

## Elementos creables con Angular CLI

> Importante: siempre que pueda utilice ng generate para crear elementos ya que, además de crearlos con una plantilla, se insertan las referencias de forma automática, lo que facilita mucho el trabajo.

- **Component**
- `ng g c`
- `ng g component nomComponente`
- Es el principal elemento mediante el cual construimos los elementos y la lógica de la página.

----

- **Directive**
- `ng g d`
- `ng g directive nomDirectiva`
- Permite añadir comportamiento dinámico a HTML (estructurales y de atributos).

----

- **Pipe**
- `ng g p`
- `ng g pipe nomPipe`
- Genera una salida transformando un dato obtenido desde la entrada.

----

- **Service**
- `ng g s`
- `ng g service nomServicio`
- Son clases complementarias a los componentes que permiten realizar cierta lógica o acciones como puede ser proporcionar datos a los componentes o realizar peticiones al servidor, etc.

----

- **Class**
- `ng g cl`
- `ng g class nomClase`
- Añade una clase a la aplicación.

----

- **Guard**
- `ng g guard nomGuard`
- Añade funciones que permiten controlar o activar ciertas rutas.

----

- **Interface**
- `ng g interface nominterface`
- Añade interfaces a la aplicación (contratos que otras clases han de cumplir para utilizarlos).

----

- **Enum**
- `ng g e`
- `ng g enum nomEnum`
- Genera una enumeración.

----

- **Module**
- `ng g m`
- `ng module nomModulo`
- Elemento que permite agrupar componentes, servicios, directivas, etc., para crear una aplicación.
