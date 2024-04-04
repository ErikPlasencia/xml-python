# XML  MINI DOM 
Funciones que este realiza;
  - Modulo de ==Python== es el que implementa DOM
  - Te permite trabajar con fitxeros xml:
			  - Obtener datos 
			  - Añadir Datos 
Tipos de Objetos;
![[Pasted image 20240402184213.png]]
Tipos de Elementos 
  ![[Pasted image 20240402184246.png]]

Para comenzar --> importaremos un modulo;
```
from xml.dom import minidom 
```

I para poder crear algún objeto en el documento realizaremos el siguiente comando:

```
doc = minidom.pare("fitxer.xml")
```

***Resumen de  como aplicarlo;***
```
# Exemple de com llegir xml i imprimir nom de l'element arrel
from xml.dom import minidom

# parse() - Retorna un objecte tipus Document
# A doc guardo l'arbre DOM que representa el fitxer xml
doc = minidom.parse("config.xml");

# Amb Document.documentElement recuperem objecte que representa l'element arrel del document
tag_principal = doc.documentElement;

# tot el nom de tag amb namespace
print (f"TAGNAME de l'element arrel és {tag_principal.tagName}\n")

# nom sense namespace
print (f"LOCALNAME de l'element arrel és {tag_principal.localName}\n")

# com locaname però mes "generic"... a un XML hi ha elements que són tags i d'altres que no
# https://phuoc.ng/collection/this-vs-that/node-name-vs-tag-name/
print (f"NODENAME nom de l'element arrel és {tag_principal.nodeName}\n")

# RESUMINT:
#   NODENAME és el més genèric
#   TAGNAME és el nom del tag amb namespace (si el tingués)
#   LOCALNAME és el nom del tag sense namespace
```

Pequeña explicación de las funciones Python que utilizaremos en el mini-dom
```XML
import xml.dom.minidom

# Parsear el documento XML
doc = xml.dom.minidom.parse("archivo.xml")

# Acceder al elemento raíz del documento
raiz = doc.documentElement

# Obtener todos los elementos hijos de la raíz
elementos = raiz.childNodes

# Iterar sobre los elementos hijos
for elemento in elementos:
    # Realizar las operaciones necesarias con cada elemento
    print(elemento.nodeName)


```

*==(Esta ultima parte es repetitiva pero como Phyton es lo que mas me cuesta prefiero que este repetido a que aparezca pocas veces en los apuntes)==*

***Ejercicios***
---
**UF2A2**
```XML
<?xml version="1.0"?>

<example>
    <company>OpenAI</company>
    <people>
        <person id="P001">
            <name gender="male">John</name>
            <age>30</age>
            <naixement>1985-11-24</naixement>
        </person>

        <person id="P002">
            <name gender="female">Jane</name>
            <age>21</age>
            <naixement>2002-05-11</naixement>
        </person>
    </people>
</example>
```

```PHYTON
from xml.dom import minidom 

doc = minidom.parse("test-dom.xml")

# Aquest es el node arrel del document ( tipus element)
arrel = doc.documentElement

print(arrel.tagName)

llista_personas= doc.getElementsByTagName ("person")
for person in llista_personas:
    id_ = person.getAttribute("id")
    nom = person.getElementsByTagName ("name")[0]
    nom_text = nom.firstChild
    edat = person.getElementsByTagName ("age")[0].firstChild.data 
    naixement = person.getElementsByTagName ("naixement")[0].firstChild.data
    gender = nom.getAttribute("gender")
print(f"  Nom :{nom_text} ------------ Edat: {edat} ------- Naixement: {naixement}")
print(id_)
print(gender)

print(doc.toxml())

# apartado 5 

print( '''
        <h2>{id_} - {Nom_text}</h2>
               <ul>
                   <li>age - {edat}</li>
                   <li>sex - {gender}</li>
                   <li>maixement - {naixement}</li>
               </ul>
        </h2>
              ''')      
print( '''
      </body>
      </html> ''')


```


---

# PATH

XPath (XML Path Language) es un lenguaje utilizado para navegar y seleccionar elementos en un documento XML. Proporciona una sintaxis para ubicar y acceder a partes específicas de un documento XML, como elementos, atributos, y texto, utilizando expresiones de ruta.

Partes de este:

1. **Nodos**: En XPath, todo en un documento XML es considerado un nodo. Los tipos de nodos principales son:
   - Elementos
   - Atributos
   - Texto
   - Nodos de comentario
   - Nodos de procesamiento

2. **Expresiones de ruta**: Las expresiones de ruta en XPath describen un camino a través de la estructura jerárquica del documento XML para ubicar nodos específicos. Por ejemplo, `/libro/titulo` describe una ruta que selecciona el elemento `titulo` que es hijo directo del elemento `libro`.

3. **Ejes**: Los ejes en XPath definen relaciones entre los nodos. Los ejes más comunes son:
   - `child`: Selecciona todos los nodos hijos directos de un nodo dado.
   - `parent`: Selecciona el nodo padre de un nodo dado.
   - `attribute`: Selecciona todos los atributos de un nodo dado.
   - `descendant`: Selecciona todos los nodos descendientes de un nodo dado.
   - `ancestor`: Selecciona todos los nodos ancestros de un nodo dado.

4. **Predicados**: Los predicados en XPath se utilizan para filtrar los nodos seleccionados basándose en ciertas condiciones. Por ejemplo, en la expresión `/libro[1]/titulo`, el predicado `[1]` selecciona el primer elemento `libro` del documento XML.

5. **Funciones**: XPath proporciona una serie de funciones integradas que pueden utilizarse para realizar operaciones en los nodos o para obtener información específica. Algunas funciones comunes incluyen `text()`, `name()`, `contains()`, `starts-with()`, entre otras.


-  [Mas Informacion](https://www.mclibre.org/consultar/xml/lecciones/xml-xpath.html)


**Aquí un ejemplo de expresión Xpath simple:**

```
/libro[@id='1']/titulo
```

Esta expresión selecciona el elemento `titulo` que es hijo directo del elemento `libro` que tiene un atributo `id` con el valor `'1'`.

XPath es una herramienta poderosa para manipular documentos XML y es ampliamente utilizado en la selección y extracción de datos de XML en aplicaciones web, procesamiento de datos y consultas de bases de datos XML.

`CHULETA DE FUNCIONES DEL PWP.
![[Pasted image 20240301174734.png]]

**Ejercicios**
---


---
# XSLT 

El ==*XSLT*== es un lenguaje para transformar documentos XML en otros documentos XML o otros tipos de documentos como por ejemplo HTML.
Normalmente estos documentos son de entrada XML pero también existen otros tipos de formatos. También hay diferentes procesadores de ==*XSLT*== como C,C++…
Los navegadores webs mas habituales llevan un procesador XSLT incorporado.

**==XSLT==** funciona tomando un documento XML de origen y aplicando reglas de transformación definidas en un archivo XSLT para generar un nuevo documento con un formato diferente. Es como un conjunto de instrucciones que le dice al procesador cómo presentar los datos XML de una manera específica.
![[Pasted image 20240402185026.png]]

- Toda la teoria la tenemos en el modle --> [Presentación de XSLT](https://drive.google.com/file/d/1DPOCh9ivLsYqKHWN2exdTVY96LhhdoOS/view)

**Para poder visualizar el documento XSL haremos lo siguiente;**![[Pasted image 20240312184212.png]]

>[!warning]
El examen seguramente será mas fácil que la practica evaluable ya que es muy complicada.