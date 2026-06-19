# Tokenización
A modo introductorio, antes abordar todo lo referente a los *tokens*, es interesante comentar cual es la artquitectura de un sistema LLM (large language model) moderno.

Ajeno al sistema está el usuario que realiza una consulta a la aplicación. El **orquestador** gestiona la lógica y el contexto, mientras que el **RAG** (*retrieval augmented generation*) busca la información relevante en fuentes externas. La información está almacenada en vectores llamados **Vector stores**, los cuales contienen documentos y *embeddings*. Estos son un medio para representar objetos como texto, imágenes y audio como puntos en un espacio vectorial contínuo, donde las ubicaciones de esos puntos en el espacio son semánticamente significativas para los algoritmos de *machine learning* (ML). Por último, el **LLM** procesa el contexto y genera la respuesta a la petición del usuario. Como apoyo a todo esto están los agentes, APIs y otras herramientas que ejecutan acciones concretas.

<img width="1117" height="728" alt="Captura de pantalla 2026-06-16 185206" src="https://github.com/user-attachments/assets/dd656e2a-a842-48fc-8aa2-eacb5f55b654" />

La superfície de ataque la componen distintos métodos:
**Prompt injection**: Manipulación de instrucciones para alterar el comportamiento del modelo.
**RAG manipulation**: Manipulación de las fuentes para obtener información no autorizada.
**Data extraction**: Extracción de datos sensibles del modelo, documentos o conversaciones.
**Tool abuse**: Uso indebido de herramientas, APIs o agentes para ejecutar acciones no deseadas.

<img width="1116" height="660" alt="Captura de pantalla 2026-06-16 185239" src="https://github.com/user-attachments/assets/aed83102-515a-4c35-981f-8b05baec45ca" />

Después de esta breve introducción, profundicemos en los **Tokens**. Los modelos de lenguaje no procesan texto como lo hacemos los humanos; lo convierten en unidades denominadas *tokens*, aproximadamente 3/4 partes de palabra. Comprender este proceso es fundamental para entender múltiples técnicas de ataque, como son las siguientes.

Token smuggling: Se utilizan espacios, tabulaciones, letras mayúsculas... todo para ocultar instrucciones maliciosas y evadir filtros basados en patrones.

Homoglyph smuggling: se utilizan caracteres de otros alfabetos visualmente parecidos al latino para evadir filtros de texto y ocultar instrucciones.

Context window exhaustion: se basa en que los modelos sólo pueden procesar una cantidad máxima de tokens en una conversación. Si se introduce muchísimo contenido, las partes más antiguas del contexto pueden dejar de estar disponibles para el modelo. La hipotesis del atacante es:

  1. El sistema tiene instrucciones de seguridad.
  2. Esas instrucciones ocupan tokens.
  3. Yo envío una enorme cantidad de texto.
  4. El sistema elimina las instrucciones antiguas.
  5. El modelo ya no ve las reglas.


<img width="1116" height="660" alt="Captura de pantalla 2026-06-16 185302" src="https://github.com/user-attachments/assets/6dd01390-2970-4b43-ac1a-21d6f4aac9ef" />
