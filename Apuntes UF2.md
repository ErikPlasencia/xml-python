 # XML  MINI DOM 
Funciones que este realiza;
  - Modulo de **Python** es el que implementa DOM
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

*(Esta ultima parte es repetitiva pero como Phyton es lo que mas me cuesta prefiero que este repetido a que aparezca pocas veces en los apuntes)*

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

```


1. Sobre el fitxer [botiga.xml](https://drive.google.com/file/d/1vvqo-yC0ZPLqMTkmDR5cADYz5ttivvLm/view?usp=sharing) escriu els paths per a fer les següents cerques:
    

- Llistat dels títols de totes les pel·lícules de la botiga.
    

/botiga/bluray/titol/text()

- Llistat de tots els preus de les pel·lícules de la botiga.
    

/botiga/bluray/preu/text()

- Llistat dels títols de les pel·lícules en català.
    

//titol[@idioma="ca"]/text()

- Llistat dels títols de les pel·lícules realitzades després o durant el 2008.
    

//any[text()>=2008]

- Llistat dels títols de les pel·lícules dirigides per “Balaguero, Plaza” amb idioma català.
    

//bluray[director='Balaguero, Plaza']/titol[@idioma='ca']/text()

- Llistat dels títols i preus de totes les pel·lícules.
    

//titol | // preu

- Llistat dels títols de les pel·lícules amb un preu superior a 20.
    

//bluray[preu >20]

- Llistat dels títols de les 5 primeres pel·lícules.
    

/botiga/bluray[position()<6]/titol

- Preu de la darrera pel·lícula
    

//bluray[last()]/preu/text()

- Preu de les pel·licules dirigides per "J. Cameron"
    

//bluray[director='J. Cameron']/preu/text()

Pots provar les solucions amb el [tester online](http://www.freeformatter.com/xpath-tester.html) de xpath[](http://www.freeformatter.com/xpath-tester.html)**

```

Xml sobre el que se ha realizado este ejercicio;
```XML
<?xml version="1.0" encoding="ISO-8859-1"?>
<botiga>
	<bluray>
		<titol idioma="ca">Avatar</titol>
		<director>J. Cameron</director>
		<preu>21</preu>
		<any>2009</any>
	</bluray>
	<bluray>
		<titol idioma="en">Zombieland</titol>
		<director>R. Fleischer</director>
		<preu>16</preu>
		<any>2009</any>
	</bluray>
	<bluray>
		<titol idioma="es">REC</titol>
		<director>Balaguero, Plaza</director>
		<preu>13</preu>
		<any>2007</any>
	</bluray>
	<bluray>
		<titol idioma="ca">REC2</titol>
		<director>Balaguero, Plaza</director>
		<preu>17</preu>
		<any>2009</any>
	</bluray>
	<bluray>
		<titol idioma="en">La herencia</titol>
		<director>Stephen</director>
		<preu>17</preu>
		<any>2010</any>
	</bluray>
	<bluray>
		<titol idioma="ca">Even the Rain</titol>
		<director>Thomas Edison</director>
		<preu>11</preu>
		<any>2005</any>
	</bluray>
	<bluray>
		<titol idioma="en">Black Bread</titol>
		<director>Vila</director>
		<preu>7</preu>
		<any>2010</any>
	</bluray>
</botiga>

```

---
# XSLT 

El ***XSLT*** es un lenguaje para transformar documentos XML en otros documentos XML o otros tipos de documentos como por ejemplo HTML.
Normalmente estos documentos son de entrada XML pero también existen otros tipos de formatos. También hay diferentes procesadores de ==*XSLT*== como C,C++…
Los navegadores webs mas habituales llevan un procesador XSLT incorporado.

***XSLT*** funciona tomando un documento XML de origen y aplicando reglas de transformación definidas en un archivo XSLT para generar un nuevo documento con un formato diferente. Es como un conjunto de instrucciones que le dice al procesador cómo presentar los datos XML de una manera específica.
![[Pasted image 20240402185026.png]]

- Toda la teoria la tenemos en el modle --> [Presentación de XSLT](https://drive.google.com/file/d/1DPOCh9ivLsYqKHWN2exdTVY96LhhdoOS/view)

**Para poder visualizar el documento XSL haremos lo siguiente;**![[Pasted image 20240312184212.png]]

>[!warning]
El examen seguramente será mas fácil que la practica evaluable ya que es muy complicada.

**Ejercicios**
---
XML sobre el cual realizaremos el ejercicio;
```XML
<?xml version="1.0" encoding="ISO-8859-1"?>
<?xml-stylesheet type="text/xsl" href="botiga.xsl"?>
<botiga>
	<bluray>
		<titol idioma="ca">Avatar</titol>
		<director>J. Cameron</director>
		<preu>21</preu>
		<any>2009</any>
	</bluray>
	<bluray>
		<titol idioma="en">Zombieland</titol>
		<director>R. Fleischer</director>
		<preu>16</preu>
		<any>2009</any>
	</bluray>
	<bluray>
		<titol idioma="es">REC</titol>
		<director>Balaguero, Plaza</director>
		<preu>13</preu>
		<any>2007</any>
	</bluray>
	<bluray>
		<titol idioma="ca">REC2</titol>
		<director>Balaguero, Plaza</director>
		<preu>17</preu>
		<any>2009</any>
	</bluray>
	<bluray>
		<titol idioma="en">La herencia</titol>
		<director>Stephen</director>
		<preu>17</preu>
		<any>2010</any>
	</bluray>
	<bluray>
		<titol idioma="ca">Even the Rain</titol>
		<director>Thomas Edison</director>
		<preu>11</preu>
		<any>2005</any>
	</bluray>
	<bluray>
		<titol idioma="en">Black Bread</titol>
		<director>Vila</director>
		<preu>7</preu>
		<any>2010</any>
	</bluray>
</botiga>


```

XSLT:
```XSLT
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
<xsl:template match="/">
  <html>
    <head>
        <script src="https://kit.fontawesome.com/3e4c1a6931.js" crossorigin="anonymous"></script> 
    </head>
  <body>
    <h2>Exercici de la botiga</h2>
    <table border="1">
      <tr>
        <th>Titol</th>
        <th>Director</th>
        <th>Preu</th>
        <th>Any</th>
        <th>Idioma</th>
      </tr>
      <xsl:for-each select="botiga/bluray">
      <tr>
        <td><xsl:value-of select="titol" /></td>
        <td><xsl:value-of select="director" /></td>
        <td>
            <xsl:choose>
                <xsl:when test="preu &gt; 15">
                    <i class="fa-solid fa-money-bills"></i>
                </xsl:when>
                <xsl:otherwise>
                    <i class="fa-solid fa-money-bill"></i>
                </xsl:otherwise>
            </xsl:choose>
        </td>
        <td><xsl:value-of select="any" /></td>
        <td>
            <img width="20px" height="20px">
                <xsl:attribute name="src"><xsl:value-of select="titol/@idioma" />.jpg</xsl:attribute>
            </img>
        </td>
      </tr>
      </xsl:for-each>
    </table>
  </body>
  </html>
</xsl:template>
</xsl:stylesheet>

```
# Practica Evaluable 

XML:
```XML
<?xml version="1.0" encoding="UTF-8"?>
<?xml-stylesheet type="text/xsl" href="horari.xsl"?>
<horari header="https://i.ibb.co/ykHW3gB/school.jpg">
    <colors>
        <!-- Pista: genera classes CSS que es diguin M01, M02
        <color codi="M01">#ff9999</color>
        <color codi="M02">#99ff99</color>
        <color codi="M03">#9999ff</color>
        <color codi="M04">#ffff99</color>
        <color codi="M08">#cc99ff</color>
        <color codi="M09">#ff99ff</color>
        <color codi="M10">#ffcc99</color>
        <color codi="M11">#99ffff</color>
    </colors>
    <links nom="Enllaços directes">
        <!-- Pista: els hauràs d'ordenar pq a la imatge es ve
        <link>
            <nom>Moodle</nom>
            <url>https://moodle.insjoaquimmir.cat/</url>
        </link>
        <link>
            <nom>Institut Joaquim Mir</nom>
            <url>https://agora.xtec.cat/iesjoaquimmir/</url>
        </link>
         <link>
            <nom>Departament d'Educació</nom>
            <url>https://educacio.gencat.cat/ca/inici</url>
        </link>
        <link>
            <nom>IsardVDI</nom>
            <url>https://pilotfp.gencat.isardvdi.com/login/jo
        </link>
        <link>
            <nom>IEduca</nom>
            <url>https://joaquimmir.ieduca.com</url>
        </link>
    </links>
    <setmana>
        <!-- L'horari el pots fer amb <table> o fent servir f
        <dia nom="Dilluns">
            <modul>
                <codi>M01</codi>
                <nom>Sistemes Operatius</nom>
            </modul>
            <modul>
                <codi>M02</codi>
                <nom>Bases de Dades</nom>
            </modul>
            <modul>
                <codi>M03</codi>
                <nom>Programació</nom>
            </modul>
            <modul>
                <codi>M04</codi>
                <nom>Marques</nom>
            </modul>
            <modul>
                <codi>M09</codi>
                <nom>Implantació</nom>
            </modul>
            <modul>
                <codi>M11</codi>
                <nom>EIE</nom>
            </modul>
        </dia>
        <dia nom="Dimarts">
            <modul>
                <codi>M01</codi>
                <nom>Sistemes Operatius</nom>
            </modul>
            <modul>
                <codi>M10</codi>
                <nom>FOL</nom>
            </modul>
            <modul>
                <codi>M08</codi>
                <nom>Desplegament</nom>
            </modul>
            <modul>
                <codi>M03</codi>
                <nom>Programació</nom>
            </modul>
            <modul>
                <codi>M11</codi>
                <nom>EIE</nom>
            </modul>
            <modul>
                <codi>M09</codi>
                <nom>Implantació</nom>
            </modul>
        </dia>
        <dia nom="Dimecres">
            <modul>
                <codi>M02</codi>
                <nom>Bases de Dades</nom>
            </modul>
            <modul>
                <codi>M10</codi>
                <nom>FOL</nom>
            </modul>
            <modul>
                <codi>M08</codi>
                <nom>Desplegament</nom>
            </modul>
            <modul>
                <codi>M04</codi>
                <nom>Marques</nom>
            </modul>
            <modul>
                <codi>M09</codi>
                <nom>Implantació</nom>
            </modul>
            <modul>
                <codi>M11</codi>
                <nom>EIE</nom>
            </modul>
        </dia>
        <dia nom="Dijous">
            <modul>
                <codi>M01</codi>
                <nom>Sistemes Operatius</nom>
            </modul>
            <modul>
                <codi>M02</codi>
                <nom>Bases de Dades</nom>
            </modul>
            <modul>
                <codi>M03</codi>
                <nom>Programació</nom>
            </modul>
            <modul>
                <codi>M10</codi>
                <nom>FOL</nom>
            </modul>
            <modul>
                <codi>M04</codi>
                <nom>Marques</nom>
            </modul>
            <modul>
                <codi>M11</codi>
                <nom>EIE</nom>
            </modul>
        </dia>
        <dia nom="Divendres">
            <modul>
                <codi>M01</codi>
                <nom>Sistemes Operatius</nom>
            </modul>
            <modul>
                <codi>M02</codi>
                <nom>Bases de Dades</nom>
            </modul>
            <modul>
                <codi>M10</codi>
                <nom>FOL</nom>
            </modul>
            <modul>
                <codi>M08</codi>
                <nom>Desplegament</nom>
            </modul>
            <modul>
                <codi>M04</codi>
                <nom>Marques</nom>
            </modul>
            <modul>
                <codi>M09</codi>
                <nom>Implantació</nom>
            </modul>
        </dia>
    </setmana>
</horari>

```

XSL:
```
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
    <xsl:output method="html" indent="yes"/>
    <xsl:template match="/horari">
        <head>
            <style type="text/css">
                <xsl:for-each select="colors/color">
                    .<xsl:value-of select="@codi"/>{background-color: <xsl:value-of select="."/>; padding: 15px; margin: 2px;}
                </xsl:for-each>
                body{
                    background-color: rgb(197, 193, 193);
                    text-align: center;
                }
                table{
                    width: 100%;
                    text-align: center;
                    border-collapse: collapse;
                }
                th{
                    background-color: rgb(150, 144, 144);
                }
                li{
                    list-style-type: none;
                    padding: 6px;
                }
                a{
                    color: rgb(0,0,0);
                }
                img{
                    width: 100%;
                    height: 130px;
                }
            </style>
        </head>
        <html>
            <body>
                <img src="{@header}"/>
                <table>
                    <tr>
                        <xsl:for-each select="setmana/dia">
                            <th>
                                <xsl:value-of select="@nom"/>
                            </th>
                        </xsl:for-each>
                    </tr>
                    <tr>
                        <xsl:for-each select="setmana/dia">
                            <td>
                                <xsl:for-each select="modul">
                                    <p class="{codi}">
                                        <xsl:value-of select="codi"/>&#160;<xsl:value-of select="nom"/>
                                    </p>
                                </xsl:for-each>
                            </td>
                        </xsl:for-each>
                    </tr>
                </table>
                <ul>
                    <h1><xsl:value-of select="links/@nom"/></h1>
                    <xsl:for-each select="links/link">
                        <xsl:sort select="nom"/>
                        <li>
                            <a href="{url}">
                                <xsl:value-of select="nom"/>
                            </a>
                        </li>
                    </xsl:for-each>
                </ul>
            </body>
        </html>
    </xsl:template>
</xsl:stylesheet>
```
# Resultado Practica Evaluable;
(https://github.com/ErikPlasencia/xml-python/blob/9874014d8526c26aaed57e90fb61e0d7e5ce5264/RESULTADO%20EVALUABLE.png)
