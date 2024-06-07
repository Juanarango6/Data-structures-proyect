# Data-structures-proyect
Data structures proyect

required application: Aplicación requerida por lo que es importante intalar antes de ejecutar
  -windows_10_cmake_Release_graphviz-install-11.0.0-win64.exe
  
adjancency_Matrix: Archivo de texto que el profe nos suminsitro para el ejercicio con lo grafos
  -matriz_de_adyacencias_30x30.txt
  
src: Codigo c++ del proyeto 
  -Main.cpp
  
images: Donde se almacenarán las imagenes generados de los arboles binarios

Data structures proyect.dev  // proyecto para abrir con aplicación c++

Data structures proyect.exe // Permite ejecutar el software sin tener instalado copilador C++

******************************************************************************************

// PARTE DE LOS MENUS

int main() {
    int opcion;
    do {
        cout << ROJO_T"\nMenu Principal\n" << endl;
        cout << BLANCO_T"1. Presentar ABB Autobalanceados" << endl;
        cout << "2. Presentar Grafos" << endl;
        cout << "3. Salir" << endl;
        cout << "Seleccione una opcion: ";
        cin >> opcion;
           system("cls");


- `int main() {`: Define el inicio de la función `main`, que es el punto de entrada de cualquier programa en C++. Todo programa debe tener una función `main`.

- `int opcion;`: Declara una variable llamada `opcion` de tipo entero. Esta variable se utilizará para almacenar la elección del usuario en el menú.

- `do {`: Inicia un bucle `do-while`. Este tipo de bucle ejecutará el bloque de código dentro de sus llaves `{}` al menos una vez antes de evaluar la condición especificada después de los corchetes `<<`. En este caso, el bucle seguirá ejecutándose mientras la condición sea verdadera.

- `cout << ROJO_T"\nMenu Principal\n" << endl;`: Imprime el título "Menu Principal" en la consola, precedido por un color rojo definido por `ROJO_T`. `endl` se utiliza para insertar un salto de línea y limpiar el flujo de salida.

- Las siguientes líneas `cout <<... << endl;` muestran las opciones disponibles en el menú principal al usuario. Cada opción corresponde a una acción diferente que el usuario puede elegir.

- `cout << "Seleccione una opcion: ";`: Solicita al usuario que ingrese una opción seleccionando uno de los números presentados anteriormente.

- `cin >> opcion;`: Lee la elección del usuario ingresada en la consola y la almacena en la variable `opcion`.

- `system("cls");`: Ejecuta el comando `cls` en Windows o `clear` en sistemas Unix/Linux para limpiar la pantalla de la consola antes de volver a mostrar el menú. Esto da una mejor experiencia de usuario al evitar que el contenido antiguo del menú se muestre junto con el nuevo.

 *****
 switch (opcion) {
            case 1: {
                // Submenú para Árboles
                TreeNode* root = NULL;
                char subopcion;
                do {
                    cout << ROJO_T"\nSubmenu para Arboles Binarios de Busqueda Autobalanceados\n";
                    cout << BLANCO_T"a. Ingrese la lista de nodos y el recorrido para construir el arbol\n";
                    cout << "b. Mostrar de forma visual el arbol inicial (indica si el arbol es AVL o no)\n";
                    cout << "c. Convertir en AVL el arbol inicial y mostrar la visualizacion del arbol\n";
                    cout << "d. Convertir en arbol Rojo y Negro el arbol inicial y mostrar la visualizacion del arbol\n";
                    cout << "e. Volver al menu principal\n";
                    cout << "Seleccione una opcion: ";
                    cin >> subopcion;

					system("cls");


 Este fragmento de código es una declaración `switch` para manejar diferentes opciones de menú basadas en la elección del usuario. Aquí te explico cada parte:

- `switch (opcion) {`: Inicia una declaración `switch` que evalúa el valor de la variable `opcion`. Dependiendo del valor de `opcion`, se ejecutará un bloque de código correspondiente a un `case` específico.

- `case 1: {`: Si `opcion` tiene el valor `1`, se ejecuta el bloque de código dentro de este `case`. Este bloque es particularmente interesante porque contiene un submenú para trabajar con árboles binarios de búsqueda autobalanceados.

- Dentro del `case 1:`:

  - Se declara un puntero a un nodo de árbol llamado `root` y se inicializa a `NULL`. Este puntero será utilizado para manipular un árbol binario de búsqueda autobalanceado.

  - Se introduce un bucle `do-while` que presenta un submenú al usuario con varias opciones para trabajar con el árbol:

    - `a.` Permite al usuario ingresar una lista de nodos y un recorrido para construir el árbol.
    - `b.` Muestra de forma visual el árbol inicial, indicando si el árbol es un Árbol de Búsqueda Avanzado (AVL) o no.
    - `c.` Convierte el árbol inicial en un AVL y muestra la visualización del árbol.
    - `d.` Convierte el árbol inicial en un árbol Rojo y Negro y muestra la visualización del árbol.
    - `e.` Regresa al menú principal.

  - Después de mostrar el submenú, el programa solicita al usuario que seleccione una opción (`cin >> subopcion;`). 

  - Finalmente, `system("cls");` limpia la pantalla de la consola, preparándola para mostrar el resultado de la elección del usuario sin dejar el submenú visible.

Este diseño permite al usuario interactuar con un árbol binario de búsqueda autobalanceado de manera flexible, ofreciendo opciones para construir el árbol, visualizarlo, convertirlo entre diferentes tipos de árboles autobalanceados, y regresar al menú principal.

*****
  switch (subopcion) {
                        case 'a': {
                            int n, val;
                            cout << "Ingrese el numero de nodos: ";
                            cin >> n;
                            cout << "Ingrese los valores de los nodos: ";
                            for (int i = 0; i < n; ++i) {
                                cin >> val;
                                root = insertBST(root, val);
                            }
                            break;



- `switch (subopcion) {`: Inicia una declaración `switch` que evalúa el valor de la variable `subopcion`. Dependiendo del valor de `subopcion`, se ejecutará un bloque de código correspondiente a un `case` específico.

- `case 'a': {`: Si `subopcion` tiene el valor `'a'`, se ejecuta el bloque de código dentro de este `case`. Este bloque está diseñado para permitir al usuario construir un árbol binario de búsqueda autobalanceado.

Dentro del `case 'a':`:

- Se declaran dos variables enteras, `n` y `val`. `n` se utilizará para almacenar el número de nodos que el usuario desea agregar al árbol, y `val` se utilizará para almacenar temporalmente los valores de los nodos.

- `cout << "Ingrese el numero de nodos: ";`: Solicita al usuario que ingrese el número total de nodos que desea agregar al árbol.

- `cin >> n;`: Lee el número de nodos ingresado por el usuario y lo almacena en la variable `n`.

- `cout << "Ingrese los valores de los nodos: ";`: Indica al usuario que debe ingresar los valores de los nodos.

- `for (int i = 0; i < n; ++i) {`: Inicia un bucle `for` que iterará `n` veces, donde `n` es el número de nodos que el usuario desea agregar.

  - `cin >> val;`: Dentro del bucle, lee el valor del nodo actual ingresado por el usuario y lo almacena en la variable `val`.

  - `root = insertBST(root, val);`: Llama a la función `insertBST`, pasando la raíz actual del árbol (`root`) y el valor del nodo (`val`) para insertar el nuevo nodo en el árbol. La función `insertBST` modificará la raíz del árbol según sea necesario para mantener el árbol balanceado.

- `break;`: Termina el `case 'a'` y sale del bloque `switch`. Esto significa que después de completar la construcción del árbol, el programa no ejecutará más código dentro del `switch` a menos que el usuario vuelva a seleccionar la opción `'a'` o alguna otra opción válida.

****

case 'b': {
                            cout << "Arbol inicial (nivel por nivel):\n";
                            printTree(root);
                            printBSTTreeDot(root, "images/bst_tree.dot");
                            cout << "El arbol " << (isAVL(root) ? "es" : "no es") << " un AVL.\n";
                            cout << "Archivo DOT para el arbol inicial generado como 'bst_tree.dot'.\n";
                            system("dot -Tpng images/bst_tree.dot -o images/bst_tree.png");
                            cout << "Imagen del arbol inicial generada como 'images/bst_tree.png'.\n";
                            break;

- `case 'b': {`: Si `subopcion` tiene el valor `'b'`, se ejecuta el bloque de código dentro de este `case`. Este bloque está diseñado para permitir al usuario visualizar el árbol binario de búsqueda autobalanceado inicial.

Dentro del `case 'b':`:

- `cout << "Arbol inicial (nivel por nivel):\n";`: Imprime un mensaje en la consola indicando que se mostrará el árbol inicial nivel por nivel.

- `printTree(root);`: Llama a la función `printTree`, pasando la raíz del árbol (`root`). Esta función imprime el árbol en la consola, mostrándolo nivel por nivel.

- `printBSTTreeDot(root, "images/bst_tree.dot");`: Llama a la función `printBSTTreeDot`, pasando la raíz del árbol (`root`) y el nombre del archivo DOT donde se guardará la descripción del árbol. Esta función genera un archivo DOT que describe el árbol binario de búsqueda.

- `cout << "El arbol " << (isAVL(root)? "es" : "no es") << " un AVL.\n";`: Verifica si el árbol es un Árbol de Búsqueda Avanzado (AVL) utilizando la función `isAVL`, pasando la raíz del árbol (`root`). Imprime en la consola si el árbol es AVL o no.

- `cout << "Archivo DOT para el arbol inicial generado como 'bst_tree.dot'.\n";`: Informa al usuario que se ha generado un archivo DOT para el árbol inicial.

- `system("dot -Tpng images/bst_tree.dot -o images/bst_tree.png");`: Utiliza el comando `system` para invocar el programa `dot` de Graphviz, que convierte el archivo DOT en una imagen PNG. La imagen resultante se guarda en el directorio 'images', con el nombre 'bst_tree.png'.

- `cout << "Imagen del arbol inicial generada como 'images/bst_tree.png'.\n";`: Informa al usuario que se ha generado una imagen PNG del árbol inicial.

- `break;`: Termina el `case 'b'` y sale del bloque `switch`. Esto significa que después de completar la visualización y generación de la imagen del árbol, el programa no ejecutará más código dentro del `switch` a menos que el usuario vuelva a seleccionar la opción `'b'` o alguna otra opción válida.

*****

case 'c': {
                            TreeNode* avlRoot = convertToAVL(root);
                            cout << "Arbol convertido a AVL (nivel por nivel):\n";
                            printTree(avlRoot);
                            printAVLTreeDot(avlRoot, "images/avl_tree.dot");
                            cout << "Archivo DOT para AVL generado como 'images/avl_tree.dot'.\n";
                            system("dot -Tpng images/avl_tree.dot -o images/avl_tree.png");
                            cout << "Imagen del arbol AVL generada como 'images/avl_tree.png'.\n";
                            break;


- `case 'c': {`: Si `subopcion` tiene el valor `'c'`, se ejecuta el bloque de código dentro de este `case`. Este bloque está diseñado para permitir al usuario convertir el árbol binario de búsqueda autobalanceado inicial a un Árbol de Búsqueda Avanzado (AVL).

Dentro del `case 'c':`:

- `TreeNode* avlRoot = convertToAVL(root);`: Llama a la función `convertToAVL`, pasando la raíz del árbol original (`root`). Esta función intenta convertir el árbol dado a un Árbol de Búsqueda Avanzado (AVL) y devuelve la raíz del árbol AVL resultante. La nueva raíz se almacena en la variable `avlRoot`.

- `cout << "Arbol convertido a AVL (nivel por nivel):\n";`: Imprime un mensaje en la consola indicando que se mostrará el árbol convertido a AVL nivel por nivel.

- `printTree(avlRoot);`: Llama a la función `printTree`, pasando la raíz del árbol AVL (`avlRoot`). Esta función imprime el árbol en la consola, mostrándolo nivel por nivel.

- `printAVLTreeDot(avlRoot, "images/avl_tree.dot");`: Llama a la función `printAVLTreeDot`, pasando la raíz del árbol AVL (`avlRoot`) y el nombre del archivo DOT donde se guardará la descripción del árbol AVL. Esta función genera un archivo DOT que describe el árbol AVL.

- `cout << "Archivo DOT para AVL generado como 'images/avl_tree.dot'.\n";`: Informa al usuario que se ha generado un archivo DOT para el árbol AVL.

- `system("dot -Tpng images/avl_tree.dot -o images/avl_tree.png");`: Utiliza el comando `system` para invocar el programa `dot` de Graphviz, que convierte el archivo DOT en una imagen PNG. La imagen resultante se guarda en el directorio 'images', con el nombre 'avl_tree.png'.

- `cout << "Imagen del arbol AVL generada como 'images/avl_tree.png'.\n";`: Informa al usuario que se ha generado una imagen PNG del árbol AVL.

- `break;`: Termina el `case 'c'` y sale del bloque `switch`. Esto significa que después de completar la conversión y visualización del árbol AVL, el programa no ejecutará más código dentro del `switch` a menos que el usuario vuelva a seleccionar la opción `'c'` o alguna otra opción válida.

*****

case 'd': {
                            RBNode* rbRoot = convertToRB(root);
                            cout << "Arbol convertido a Rojo-Negro (nivel por nivel):\n";
                            printRBTree(rbRoot);
                            printRBTreeDot(rbRoot, "images/rb_tree.dot");
                            cout << "Archivo DOT para Rojo-Negro generado como 'images/rb_tree.dot'.\n";
                            system("dot -Tpng images/rb_tree.dot -o images/rb_tree.png");
                            cout << "Imagen del arbol Rojo-Negro generada como 'images/rb_tree.png'.\n";
                            break;

- `case 'd': {`: Si `subopcion` tiene el valor `'d'`, se ejecuta el bloque de código dentro de este `case`. Este bloque está diseñado para permitir al usuario convertir el árbol binario de búsqueda autobalanceado inicial a un árbol Rojo-Negro (también conocido como árbol AVL, aunque en este contexto parece referirse a un árbol Rojo-Negro genérico).

Dentro del `case 'd':`:

- `RBNode* rbRoot = convertToRB(root);`: Llama a la función `convertToRB`, pasando la raíz del árbol original (`root`). Esta función intenta convertir el árbol dado a un árbol Rojo-Negro y devuelve la raíz del árbol Rojo-Negro resultante. La nueva raíz se almacena en la variable `rbRoot`.

- `cout << "Arbol convertido a Rojo-Negro (nivel por nivel):\n";`: Imprime un mensaje en la consola indicando que se mostrará el árbol convertido a Rojo-Negro nivel por nivel.

- `printRBTree(rbRoot);`: Llama a la función `printRBTree`, pasando la raíz del árbol Rojo-Negro (`rbRoot`). Esta función imprime el árbol en la consola, mostrándolo nivel por nivel.

- `printRBTreeDot(rbRoot, "images/rb_tree.dot");`: Llama a la función `printRBTreeDot`, pasando la raíz del árbol Rojo-Negro (`rbRoot`) y el nombre del archivo DOT donde se guardará la descripción del árbol Rojo-Negro. Esta función genera un archivo DOT que describe el árbol Rojo-Negro.

- `cout << "Archivo DOT para Rojo-Negro generado como 'images/rb_tree.dot'.\n";`: Informa al usuario que se ha generado un archivo DOT para el árbol Rojo-Negro.

- `system("dot -Tpng images/rb_tree.dot -o images/rb_tree.png");`: Utiliza el comando `system` para invocar el programa `dot` de Graphviz, que convierte el archivo DOT en una imagen PNG. La imagen resultante se guarda en el directorio 'images', con el nombre 'rb_tree.png'.

- `cout << "Imagen del arbol Rojo-Negro generada como 'images/rb_tree.png'.\n";`: Informa al usuario que se ha generado una imagen PNG del árbol Rojo-Negro.

- `break;`: Termina el `case 'd'` y sale del bloque `switch`. Esto significa que después de completar la conversión y visualización del árbol Rojo-Negro, el programa no ejecutará más código dentro del `switch` a menos que el usuario vuelva a seleccionar la opción `'d'` o alguna otra opción válida.

******

  case 'e': {
                            cout << VERDE_T"Volviendo al menu principal...\n";
                            break;


- `case 'e': {`: Si `subopcion` tiene el valor `'e'`, se ejecuta el bloque de código dentro de este `case`. Este bloque está diseñado para permitir al usuario regresar al menú principal.

Dentro del `case 'e':`:

- `cout << VERDE_T"Volviendo al menu principal...\n";`: Imprime un mensaje en la consola indicando que el programa está volviendo al menú principal. El uso de `VERDE_T` sugiere que el mensaje se mostrará en verde, probablemente mediante algún mecanismo de coloración de texto en la consola.

- `break;`: Termina el `case 'e'` y sale del bloque `switch`. Esto significa que después de imprimir el mensaje, el programa no ejecutará más código dentro del `switch` a menos que el usuario vuelva a seleccionar la opción `'e'` o alguna otra opción válida.

****

 default: {
                            cout << MAGENTA_T"Opcion no valida. Por favor, ingrese una opcion valida.\n";
                            break;
                        }
                    }
                } while (subopcion != 'e');
                break;

Incluye un bloque `default` para manejar casos en los que ninguna de las opciones especificadas en los `case` coincide con la elección del usuario. También, hay un bucle `while` que continúa hasta que el usuario selecciona la opción `'e'` para volver al menú principal. Aquí te explico cada parte:

- `default: {`: Este bloque se ejecuta cuando ninguna de las condiciones especificadas en los `case` anteriores coincide con la elección del usuario. Es decir, si `subopcion` no es igual a ninguno de los valores especificados en los `case`, entonces se ejecuta el código dentro de este bloque `default`.

Dentro del `default:`:

- `cout << MAGENTA_T"Opcion no valida. Por favor, ingrese una opcion valida.\n";`: Imprime un mensaje en la consola indicando que la opción seleccionada no es válida y pidiendo al usuario que ingrese una opción válida. El uso de `MAGENTA_T` sugiere que el mensaje se mostrará en magenta, probablemente mediante algún mecanismo de coloración de texto en la consola.

- `break;`: Termina el bloque `default` y sale del bloque `switch`. Esto significa que después de imprimir el mensaje de error, el programa no ejecutará más código dentro del `switch` a menos que el usuario vuelva a seleccionar una opción válida.

Fuera del bloque `switch`, pero aún dentro del bucle `while`:

- `} while (subopcion!= 'e');`: Este es el final del bloque `switch` y también marca el final del bucle `while`. El bucle continuará ejecutándose siempre que `subopcion` no sea igual a `'e'`, lo que significa que el menú seguirá mostrándose y esperando una elección del usuario hasta que el usuario decida volver al menú principal seleccionando `'e'`.

- `break;`: Al final del bucle `while`, esta instrucción `break` asegura que, una vez que el usuario selecciona la opción `'e'` para volver al menú principal, el programa salga del bucle y posiblemente del menú principal, dependiendo de cómo esté estructurado el resto del programa.

*****

 case 2: {
                // Submenú para Grafos
                Graph graph;
                char subopcion;
                do {
                    cout << ROJO_T"\nSubmenu para Grafos\n";
                    cout << BLANCO_T"a. Ingrese la matriz de adyacencias\n";
                    cout << "b. Mostrar la visualizacion del grafo inicial\n";
                    cout << "c. Elija un algoritmo para encontrar el camino mas corto\n";
                    cout << "d. Elija un algoritmo para encontrar arboles de peso minimo\n";
                    cout << "e. Volver al menu principal\n";
                    cout << "Seleccione una opcion: ";
                    cin >> subopcion;

		system("cls");


- `case 2: {`: Si la variable `opcion` tiene el valor `2`, se ejecuta el bloque de código dentro de este `case`. Este bloque está diseñado para permitir al usuario interactuar con grafos.

Dentro del `case 2:`:

- Se crea una instancia de una clase `Graph` llamada `graph`. Esta clase representa un grafo y puede contener métodos para manipular y analizar el grafo.

- Se introduce un bucle `do-while` que presenta un submenú al usuario con varias opciones para trabajar con el grafo:

  - `a.` Permite al usuario ingresar la matriz de adyacencias para construir el grafo.
  - `b.` Muestra de forma visual el grafo inicial.
  - `c.` Ofrece al usuario la opción de elegir un algoritmo para encontrar el camino más corto en el grafo.
  - `d.` Ofrece al usuario la opción de elegir un algoritmo para encontrar árboles de peso mínimo en el grafo.
  - `e.` Regresa al menú principal.

- Después de mostrar el submenú, el programa solicita al usuario que seleccione una opción (`cin >> subopcion;`).

- `system("cls");` limpia la pantalla de la consola, preparándola para mostrar el resultado de la elección del usuario sin dejar el submenú visible.

*****

switch (subopcion) {
                        case 'a': {
                            string filepath;
                            cout << MAGENTA_T"Current repository path: adjancency_Matrix/matriz_de_adyacencias_30x30.txt\n";
                            cout << BLANCO_T"Ingrese la ruta absoluta del archivo de texto: ";                            
                            cin >> filepath;
                            graph.adjacencyMatrix = readAdjacencyMatrixFromFile(filepath);
                            break;
                        }

- `switch (subopcion) {`: Inicia una declaración `switch` que evalúa el valor de la variable `subopcion`. Dependiendo del valor de `subopcion`, se ejecutará un bloque de código correspondiente a un `case` específico.

- `case 'a': {`: Si `subopcion` tiene el valor `'a'`, se ejecuta el bloque de código dentro de este `case`. Este bloque está diseñado para permitir al usuario cargar una matriz de adyacencia desde un archivo de texto.

Dentro del `case 'a':`:

- Se declara una variable `string` llamada `filepath`. Esta variable almacenará la ruta absoluta del archivo de texto que contiene la matriz de adyacencia del grafo.

- `cout << MAGENTA_T"Current repository path: adjancency_Matrix/matriz_de_adyacencias_30x30.txt\n";`: Imprime un mensaje en la consola indicando la ruta predeterminada del archivo de matriz de adyacencia. El uso de `MAGENTA_T` sugiere que el mensaje se mostrará en magenta, probablemente mediante algún mecanismo de coloración de texto en la consola.

- `cout << BLANCO_T"Ingrese la ruta absoluta del archivo de texto: ";`: Solicita al usuario que ingrese la ruta absoluta del archivo de texto que contiene la matriz de adyacencia.

- `cin >> filepath;`: Lee la ruta ingresada por el usuario y la almacena en la variable `filepath`.

- `graph.adjacencyMatrix = readAdjacencyMatrixFromFile(filepath);`: Llama a la función `readAdjacencyMatrixFromFile`, pasando la ruta del archivo (`filepath`) como argumento. Esta función debería leer el contenido del archivo especificado y asignarlo a la propiedad `adjacencyMatrix` de la instancia `graph`. Asumimos que `graph` es una instancia de una clase o estructura que representa un grafo y tiene una propiedad `adjacencyMatrix` para almacenar su matriz de adyacencia.

- `break;`: Termina el `case 'a'` y sale del bloque `switch`. Esto significa que después de cargar la matriz de adyacencia desde el archivo, el programa no ejecutará más código dentro del `switch` a menos que el usuario vuelva a seleccionar la opción `'a'` o alguna otra opción válida.

*****

case 'b': {
                            generateDotFile(graph, "graph.dot");

                            ifstream checkFile("graph.dot");
                            if (checkFile.is_open()) {
                                checkFile.close();
                                if (system("dot -Tpng graph.dot -o graph.png") == 0) {
                                    cout << "Imagen del grafo generada como 'graph.png'." << endl;
                                } else {
                                    cerr << ROJO_T"Error: No se pudo generar la imagen del grafo." << endl;
                                }
                            } else {
                                cerr << ROJO_T"Error: El archivo DOT no se genero correctamente." << endl;
                            }
                            break;


- `case 'b': {`: Si `subopcion` tiene el valor `'b'`, se ejecuta el bloque de código dentro de este `case`. Este bloque está diseñado para permitir al usuario generar un archivo DOT para un grafo y luego convertir ese archivo DOT en una imagen PNG.

Dentro del `case 'b':`:

- `generateDotFile(graph, "graph.dot");`: Llama a la función `generateDotFile`, pasando la instancia del grafo (`graph`) y el nombre del archivo DOT que se generará (`"graph.dot"`). Esta función debería crear un archivo DOT que describe el grafo.

- `ifstream checkFile("graph.dot");`: Intenta abrir el archivo DOT recién creado para verificar si se generó correctamente. `ifstream` es un objeto de flujo de entrada para archivos, utilizado aquí para comprobar si el archivo existe y se abrió correctamente.

- `if (checkFile.is_open()) {`: Comprueba si el archivo DOT se abrió correctamente. Si es así, procede a cerrar el archivo y continuar con la siguiente verificación.

- `checkFile.close();`: Cierra el archivo DOT ya que solo necesitamos verificar su existencia y no realizar ninguna lectura o escritura adicional.

- `if (system("dot -Tpng graph.dot -o graph.png") == 0) {`: Utiliza el comando `system` para invocar el programa `dot` de Graphviz, que convierte el archivo DOT en una imagen PNG. La imagen resultante se guarda con el nombre `"graph.png"`. La condición `== 0` verifica si el comando se ejecutó sin errores.

- `cout << "Imagen del grafo generada como 'graph.png'." << endl;`: Si la conversión fue exitosa, imprime un mensaje informando al usuario que la imagen del grafo se generó correctamente.

- `cerr << ROJO_T"Error: No se pudo generar la imagen del grafo." << endl;`: Si hubo un error durante la conversión, imprime un mensaje de error en rojo.

- `else {`: Si el archivo DOT no se pudo abrir, indica un problema previo en la generación del archivo DOT.

- `cerr << ROJO_T"Error: El archivo DOT no se genero correctamente." << endl;`: Imprime un mensaje de error en rojo si el archivo DOT no se pudo abrir, lo cual implica que no se generó correctamente.

- `break;`: Termina el `case 'b'` y sale del bloque `switch`. Esto significa que después de intentar generar la imagen del grafo, el programa no ejecutará más código dentro del `switch` a menos que el usuario vuelva a seleccionar la opción `'b'` o alguna otra opción válida.

*****

case 'c': {
                            char subChoice;
                            do {
                                cout << ROJO_T"\nSubmenu para algoritmos de camino mas corto:\n" << endl;
                                cout << BLANCO_T"a. Dijkstra" << endl;
                                cout << "b. Floyd-Warshall" << endl;
                                cout << "c. Volver al menu principal" << endl;
                                cout << "Ingrese su eleccion: ";
                                cin >> subChoice;


- `case 'c': {`: Si `subopcion` tiene el valor `'c'`, se ejecuta el bloque de código dentro de este `case`. Este bloque está diseñado para permitir al usuario seleccionar un algoritmo de camino más corto para ejecutar sobre un grafo.

Dentro del `case 'c':`:

- Se introduce un bucle `do-while` que presenta un submenú al usuario con varias opciones para ejecutar algoritmos de camino más corto:

  - `a.` Permite al usuario ejecutar el algoritmo de Dijkstra.
  - `b.` Permite al usuario ejecutar el algoritmo de Floyd-Warshall.
  - `c.` Regresa al menú principal.

- Después de mostrar el submenú, el programa solicita al usuario que seleccione una opción (`cin >> subChoice;`).

Este diseño permite al usuario interactuar con algoritmos de camino más corto de manera flexible, ofreciendo opciones para ejecutar Dijkstra o Floyd-Warshall, y regresar al menú principal. Sin embargo, el código proporcionado solo muestra el submenú y espera la elección del usuario, sin implementar la lógica para ejecutar los algoritmos seleccionados. Para completar esta funcionalidad, sería necesario agregar bloques adicionales dentro del bucle `do-while` para manejar las elecciones del usuario y ejecutar los algoritmos correspondientes.

*****

switch (subChoice) {
                                    case 'a': {
                                        int startNode;
                                        cout << "Ingrese el nodo inicial para Dijkstra: ";
                                        cin >> startNode;
                                        dijkstra(graph, startNode);
                                        break;
                                    }


- `switch (subChoice) {`: Inicia una declaración `switch` que evalúa el valor de la variable `subChoice`. Dependiendo del valor de `subChoice`, se ejecutará un bloque de código correspondiente a un `case` específico.

- `case 'a': {`: Si `subChoice` tiene el valor `'a'`, se ejecuta el bloque de código dentro de este `case`. Este bloque está diseñado para permitir al usuario ejecutar el algoritmo de Dijkstra sobre un grafo.

Dentro del `case 'a':`:

- Se declara una variable `int` llamada `startNode`. Esta variable almacenará el identificador del nodo inicial desde el cual se ejecutará el algoritmo de Dijkstra.

- `cout << "Ingrese el nodo inicial para Dijkstra: ";`: Solicita al usuario que ingrese el número del nodo inicial desde el cual desea ejecutar el algoritmo de Dijkstra.

- `cin >> startNode;`: Lee el número ingresado por el usuario y lo almacena en la variable `startNode`.

- `dijkstra(graph, startNode);`: Llama a la función `dijkstra`, pasando la instancia del grafo (`graph`) y el identificador del nodo inicial (`startNode`) como argumentos. Esta función debería ejecutar el algoritmo de Dijkstra desde el nodo inicial especificado, calculando los caminos más cortos hacia todos los demás nodos del grafo.

- `break;`: Termina el `case 'a'` y sale del bloque `switch`. Esto significa que después de ejecutar el algoritmo de Dijkstra, el programa no ejecutará más código dentro del `switch` a menos que el usuario vuelva a seleccionar la opción `'a'` o alguna otra opción válida.

*****
case 'b': {
                                        floydWarshall(graph);
                                        break;
                                    }

- `case 'b': {`: Si `subChoice` tiene el valor `'b'`, se ejecuta el bloque de código dentro de este `case`. Este bloque está diseñado para permitir al usuario ejecutar el algoritmo de Floyd-Warshall sobre un grafo.

Dentro del `case 'b':`:

- `floydWarshall(graph);`: Llama a la función `floydWarshall`, pasando la instancia del grafo (`graph`) como argumento. Esta función debería ejecutar el algoritmo de Floyd-Warshall sobre el grafo, calculando los caminos más cortos entre todos los pares de nodos.

- `break;`: Termina el `case 'b'` y sale del bloque `switch`. Esto significa que después de ejecutar el algoritmo de Floyd-Warshall, el programa no ejecutará más código dentro del `switch` a menos que el usuario vuelva a seleccionar la opción `'b'` o alguna otra opción válida.

*****
case 'c': {
                                        cout << VERDE_T"Volviendo al menu principal." << endl;
                                        break;


- `case 'c': {`: Si `subChoice` tiene el valor `'c'`, se ejecuta el bloque de código dentro de este `case`. Este bloque está diseñado para permitir al usuario regresar al menú principal.

Dentro del `case 'c':`:

- `cout << VERDE_T"Volviendo al menu principal." << endl;`: Imprime un mensaje en la consola indicando que el programa está volviendo al menú principal. El uso de `VERDE_T` sugiere que el mensaje se mostrará en verde, probablemente mediante algún mecanismo de coloración de texto en la consola.

- `break;`: Termina el `case 'c'` y sale del bloque `switch`. Esto significa que después de imprimir el mensaje, el programa no ejecutará más código dentro del `switch` a menos que el usuario vuelva a seleccionar la opción `'c'` o alguna otra opción válida.

*****
default: {
                                        cout << ROJO_T"Opcion no valida. Por favor, ingrese una opcion valida." << endl;
                                        break;
                                    }
                                }
                            } while (subChoice != 'c');
                            break;
                        }

Incluye un bloque `default` para manejar casos en los que ninguna de las opciones especificadas en los `case` coincide con la elección del usuario. También, hay un bucle `while` que continúa hasta que el usuario selecciona la opción `'c'` para volver al menú principal. Aquí te explico cada parte:

- `default: {`: Este bloque se ejecuta cuando ninguna de las condiciones especificadas en los `case` anteriores coincide con la elección del usuario. Es decir, si `subChoice` no es igual a ninguno de los valores especificados en los `case`, entonces se ejecuta el código dentro de este bloque `default`.

Dentro del `default:`:

- `cout << ROJO_T"Opcion no valida. Por favor, ingrese una opcion valida." << endl;`: Imprime un mensaje en la consola indicando que la opción seleccionada no es válida y pidiendo al usuario que ingrese una opción válida. El uso de `ROJO_T` sugiere que el mensaje se mostrará en rojo, probablemente mediante algún mecanismo de coloración de texto en la consola.

- `break;`: Termina el bloque `default` y sale del bloque `switch`. Esto significa que después de imprimir el mensaje de error, el programa no ejecutará más código dentro del `switch` a menos que el usuario vuelva a seleccionar una opción válida.

Fuera del bloque `switch`, pero aún dentro del bucle `while`:

- `} while (subChoice!= 'c');`: Este es el final del bloque `switch` y también marca el final del bucle `while`. El bucle continuará ejecutándose siempre que `subChoice` no sea igual a `'c'`, lo que significa que el menú seguirá mostrándose y esperando una elección del usuario hasta que el usuario decida volver al menú principal seleccionando `'c'`.

- `break;`: Al final del bucle `while`, esta instrucción `break` asegura que, una vez que el usuario selecciona la opción `'c'` para volver al menú principal, el programa salga del bucle y posiblemente del menú principal, dependiendo de cómo esté estructurado el resto del programa.

*****
case 'd': {
                            char subChoice;
                            do {
                                cout << ROJO_T"\nSubmenu para algoritmos de arboles de peso minimo:\n" << endl;
                                cout << BLANCO_T"a. Kruskal" << endl;
                                cout << "b. Prim" << endl;
                                cout << "c. Volver al menu principal" << endl;
                                cout << "Ingrese su eleccion: ";
                                cin >> subChoice;

                                system("cls");


- `case 'd': {`: Si `subopcion` tiene el valor `'d'`, se ejecuta el bloque de código dentro de este `case`. Este bloque está diseñado para permitir al usuario seleccionar un algoritmo de árbol de peso mínimo para ejecutar sobre un grafo.

Dentro del `case 'd':`:

- Se introduce un bucle `do-while` que presenta un submenú al usuario con varias opciones para ejecutar algoritmos de árboles de peso mínimo:

  - `a.` Permite al usuario ejecutar el algoritmo de Kruskal.
  - `b.` Permite al usuario ejecutar el algoritmo de Prim.
  - `c.` Regresa al menú principal.

- Después de mostrar el submenú, el programa solicita al usuario que seleccione una opción (`cin >> subChoice;`).

- `system("cls");`: Limpia la pantalla de la consola, preparándola para mostrar el resultado de la elección del usuario sin dejar el submenú visible.

Este diseño permite al usuario interactuar con algoritmos de árboles de peso mínimo de manera flexible, ofreciendo opciones para ejecutar Kruskal o Prim, y regresar al menú principal. Sin embargo, el código proporcionado solo muestra el submenú y espera la elección del usuario, sin implementar la lógica para ejecutar los algoritmos seleccionados. Para completar esta funcionalidad, sería necesario agregar bloques adicionales dentro del bucle `do-while` para manejar las elecciones del usuario y ejecutar los algoritmos correspondientes.

*****

 switch (subChoice) {
                                    case 'a': {
                                        kruskal(graph);
                                        break;
                                    }


- `switch (subChoice) {`: Inicia una declaración `switch` que evalúa el valor de la variable `subChoice`. Dependiendo del valor de `subChoice`, se ejecutará un bloque de código correspondiente a un `case` específico.

- `case 'a': {`: Si `subChoice` tiene el valor `'a'`, se ejecuta el bloque de código dentro de este `case`. Este bloque está diseñado para permitir al usuario ejecutar el algoritmo de Kruskal sobre un grafo.

Dentro del `case 'a':`:

- `kruskal(graph);`: Llama a la función `kruskal`, pasando la instancia del grafo (`graph`) como argumento. Esta función debería ejecutar el algoritmo de Kruskal sobre el grafo, construyendo un árbol de peso mínimo.

- `break;`: Termina el `case 'a'` y sale del bloque `switch`. Esto significa que después de ejecutar el algoritmo de Kruskal, el programa no ejecutará más código dentro del `switch` a menos que el usuario vuelva a seleccionar la opción `'a'` o alguna otra opción válida.

*****
case 'b': {
                                        prim(graph);
                                        break;
                                    }


- `case 'b': {`: Si `subChoice` tiene el valor `'b'`, se ejecuta el bloque de código dentro de este `case`. Este bloque está diseñado para permitir al usuario ejecutar el algoritmo de Prim sobre un grafo.

Dentro del `case 'b':`:

- `prim(graph);`: Llama a la función `prim`, pasando la instancia del grafo (`graph`) como argumento. Esta función debería ejecutar el algoritmo de Prim sobre el grafo, construyendo un árbol de peso mínimo.

- `break;`: Termina el `case 'b'` y sale del bloque `switch`. Esto significa que después de ejecutar el algoritmo de Prim, el programa no ejecutará más código dentro del `switch` a menos que el usuario vuelva a seleccionar la opción `'b'` o alguna otra opción válida.

*****
case 'c': {
                                        cout << VERDE_T"\nVolviendo al menu principal." << endl;
                                        break;
                                    }


- `case 'c': {`: Si `subChoice` tiene el valor `'c'`, se ejecuta el bloque de código dentro de este `case`. Este bloque está diseñado para permitir al usuario regresar al menú principal.

Dentro del `case 'c':`:

- `cout << VERDE_T"\nVolviendo al menu principal." << endl;`: Imprime un mensaje en la consola indicando que el programa está volviendo al menú principal. El uso de `VERDE_T` sugiere que el mensaje se mostrará en verde, probablemente mediante algún mecanismo de coloración de texto en la consola.

- `break;`: Termina el `case 'c'` y sale del bloque `switch`. Esto significa que después de imprimir el mensaje, el programa no ejecutará más código dentro del `switch` a menos que el usuario vuelva a seleccionar la opción `'c'` o alguna otra opción válida.

*****
default: {
                                        cout << ROJO_T"\nOpcion no valida. Por favor, ingrese una opcion valida." << endl;
                                        break;
                                    }
                                }
                            } while (subChoice != 'c');
                            break;
Estas lineas incluyem un bloque `default` para manejar casos en los que ninguna de las opciones especificadas en los `case` coincide con la elección del usuario. También, hay un bucle `while` que continúa hasta que el usuario selecciona la opción `'c'` para volver al menú principal. Aquí te explico cada parte:

- `default: {`: Este bloque se ejecuta cuando ninguna de las condiciones especificadas en los `case` anteriores coincide con la elección del usuario. Es decir, si `subChoice` no es igual a ninguno de los valores especificados en los `case`, entonces se ejecuta el código dentro de este bloque `default`.

Dentro del `default:`:

- `cout << ROJO_T"\nOpcion no valida. Por favor, ingrese una opcion valida." << endl;`: Imprime un mensaje en la consola indicando que la opción seleccionada no es válida y pidiendo al usuario que ingrese una opción válida. El uso de `ROJO_T` sugiere que el mensaje se mostrará en rojo, probablemente mediante algún mecanismo de coloración de texto en la consola.

- `break;`: Termina el bloque `default` y sale del bloque `switch`. Esto significa que después de imprimir el mensaje de error, el programa no ejecutará más código dentro del `switch` a menos que el usuario vuelva a seleccionar una opción válida.

Fuera del bloque `switch`, pero aún dentro del bucle `while`:

- `} while (subChoice!= 'c');`: Este es el final del bloque `switch` y también marca el final del bucle `while`. El bucle continuará ejecutándose siempre que `subChoice` no sea igual a `'c'`, lo que significa que el menú seguirá mostrándose y esperando una elección del usuario hasta que el usuario decida volver al menú principal seleccionando `'c'`.

- `break;`: Al final del bucle `while`, esta instrucción `break` asegura que, una vez que el usuario selecciona la opción `'c'` para volver al menú principal, el programa salga del bucle y posiblemente del menú principal, dependiendo de cómo esté estructurado el resto del programa.

*****

 case 'e': {
                            cout << VERDE_T"\nVolviendo al menu principal." << endl;
                            break;
                        }


- `case 'e': {`: Si `subChoice` tiene el valor `'e'`, se ejecuta el bloque de código dentro de este `case`. Este bloque está diseñado para permitir al usuario regresar al menú principal.

Dentro del `case 'e':`:

- `cout << VERDE_T"\nVolviendo al menu principal." << endl;`: Imprime un mensaje en la consola indicando que el programa está volviendo al menú principal. El uso de `VERDE_T` sugiere que el mensaje se mostrará en verde, probablemente mediante algún mecanismo de coloración de texto en la consola.

- `break;`: Termina el `case 'e'` y sale del bloque `switch`. Esto significa que después de imprimir el mensaje, el programa no ejecutará más código dentro del `switch` a menos que el usuario vuelva a seleccionar la opción `'e'` o alguna otra opción válida.

*****

default: {
                            cout << ROJO_T"\nOpcion no valida. Por favor, ingrese una opcion valida." << endl;
                            break;
                        }
                    }
                } while (subopcion != 'e');
                break;
            }
Incluye un bloque `default` para manejar casos en los que ninguna de las opciones especificadas en los `case` coincide con la elección del usuario. También, hay un bucle `while` que continúa hasta que el usuario selecciona la opción `'e'` para volver al menú principal. Aquí te explico cada parte:

- `default: {`: Este bloque se ejecuta cuando ninguna de las condiciones especificadas en los `case` anteriores coincide con la elección del usuario. Es decir, si `subopcion` no es igual a ninguno de los valores especificados en los `case`, entonces se ejecuta el código dentro de este bloque `default`.

Dentro del `default:`:

- `cout << ROJO_T"\nOpcion no valida. Por favor, ingrese una opcion valida." << endl;`: Imprime un mensaje en la consola indicando que la opción seleccionada no es válida y pidiendo al usuario que ingrese una opción válida. El uso de `ROJO_T` sugiere que el mensaje se mostrará en rojo, probablemente mediante algún mecanismo de coloración de texto en la consola.

- `break;`: Termina el bloque `default` y sale del bloque `switch`. Esto significa que después de imprimir el mensaje de error, el programa no ejecutará más código dentro del `switch` a menos que el usuario vuelva a seleccionar una opción válida.

Fuera del bloque `switch`, pero aún dentro del bucle `while`:

- `} while (subopcion!= 'e');`: Este es el final del bloque `switch` y también marca el final del bucle `while`. El bucle continuará ejecutándose siempre que `subopcion` no sea igual a `'e'`, lo que significa que el menú seguirá mostrándose y esperando una elección del usuario hasta que el usuario decida volver al menú principal seleccionando `'e'`.

- `break;`: Al final del bucle `while`, esta instrucción `break` asegura que, una vez que el usuario selecciona la opción `'e'` para volver al menú principal, el programa salga del bucle y posiblemente del menú principal, dependiendo de cómo esté estructurado el resto del programa.

******
case 3: {
                cout << VERDE_T"\nSaliendo..." << endl;
                break;
            }
            default: {
                cout << ROJO_T"\nOpcion no valida. Por favor, seleccione una opcion valida." << endl;
                break;
            }
        }
    } while (opcion != 3);

    return 0;
}


- `case 3: {`: Este `case` se activa cuando el valor de `opcion` es `3`. Dentro de este bloque:

  - `cout << VERDE_T"\nSaliendo..." << endl;`: Imprime un mensaje en la consola indicando que el programa está a punto de salir. El uso de `VERDE_T` sugiere que el mensaje se mostrará en verde, probablemente mediante algún mecanismo de coloración de texto en la consola.

  - `break;`: Termina el `case 3` y sale del bloque `switch`. Esto significa que después de imprimir el mensaje, el programa no ejecutará más código dentro del `switch` a menos que el usuario vuelva a seleccionar la opción `3` o alguna otra opción válida.

- `default: {`: Este bloque se ejecuta cuando ninguna de las condiciones especificadas en los `case` anteriores coincide con la elección del usuario. Es decir, si `opcion` no es igual a `3`, entonces se ejecuta el código dentro de este bloque `default`.

  - `cout << ROJO_T"\nOpcion no valida. Por favor, seleccione una opcion valida." << endl;`: Imprime un mensaje en la consola indicando que la opción seleccionada no es válida y pidiendo al usuario que seleccione una opción válida. El uso de `ROJO_T` sugiere que el mensaje se mostrará en rojo, probablemente mediante algún mecanismo de coloración de texto en la consola.

  - `break;`: Termina el bloque `default` y sale del bloque `switch`. Esto significa que después de imprimir el mensaje de error, el programa no ejecutará más código dentro del `switch` a menos que el usuario vuelva a seleccionar una opción válida.

Fuera del bloque `switch`, pero aún dentro del bucle `while`:

- `} while (opcion!= 3);`: Este es el final del bloque `switch` y también marca el final del bucle `while`. El bucle continuará ejecutándose siempre que `opcion` no sea igual a `3`, lo que significa que el menú seguirá mostrándose y esperando una elección del usuario hasta que el usuario decida salir seleccionando `3`.

- `return 0;`: Al final del bucle `while`, esta instrucción `return 0;` indica que el programa ha terminado su ejecución exitosamente.
