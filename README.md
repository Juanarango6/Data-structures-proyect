# Data-structures-proyect
//Data structures proyect

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

// PARTE DE ARBOLES 

Enumeración Color

// Enumeración para representar los colores en un árbol rojo-negro.
`enum Color { RED, BLACK };`
Define dos constantes, `RED` y `BLACK`, que representan los dos colores posibles en un árbol rojo-negro. Utilizados para mantener el árbol balanceado durante inserciones y eliminaciones.

Estructura TreeNode

    struct TreeNode {
       int val;          // Valor almacenado en el nodo.
       TreeNode* left;   // Puntero al hijo izquierdo.
       TreeNode* right;  // Puntero al hijo derecho.
    
    // Constructor que inicializa el valor del nodo y sus hijos a NULL.
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
    }

Representa un nodo en un árbol binario genérico. Contiene un valor `(val)`, y punteros a sus hijos izquierdo `(left)` y derecho `(right)`. El constructor inicializa el valor del nodo y establece ambos hijos a `NULL`.

    Estructura RBNode
      struct RBNode {
      int val;          // Valor almacenado en el nodo.
      Color color;      // Color del nodo (ROJO o NEGRO).
      RBNode* left;     // Puntero al hijo izquierdo.
      RBNode* right;    // Puntero al hijo derecho.
      RBNode* parent;   // Puntero al nodo padre.
    
    // Constructor que inicializa el valor del nodo, su color a ROJO, y sus hijos y padre a NULL.
    RBNode(int x) : val(x), color(RED), left(NULL), right(NULL), parent(NULL) {}
    };
Representa un nodo en un árbol rojo-negro. Incluye un campo color para indicar el color del nodo (rojo o negro) y un campo parent para referenciar al nodo padre. Permite implementar las reglas específicas del árbol rojo-negro.

    Función height
     int height(TreeNode* node) {
     if (node == NULL) return 0;
     return 1 + max(height(node->left), height(node->right));
    }
Calcula la altura de un nodo en un árbol AVL. La altura es la longitud del camino más largo desde ese nodo hasta una hoja. Fundamental para determinar el equilibrio del árbol.

Función isAVL

    bool isAVL(TreeNode* root) {
       if (root == NULL) return true;
       int leftHeight = height(root->left);
       int rightHeight = height(root->right);
       if (abs(leftHeight - rightHeight) > 1) return false;
       return isAVL(root->left) && isAVL(root->right);  
    }
Verifica si un árbol dado es un árbol AVL. Un árbol AVL es un árbol binario de búsqueda auto-balanceado, donde la diferencia de alturas entre los hijos de cualquier nodo no excede uno. Crucial para garantizar que el árbol permanezca balanceado después de inserciones y eliminaciones.

    Función rotateRight
      TreeNode* rotateRight(TreeNode* y) {
      TreeNode* x = y->left;
      TreeNode* T2 = x->right;
      x->right = y;
      y->left = T2;
      return x;
    }
Realiza una rotación simple a la derecha en un árbol AVL. La rotación gira el nodo y hacia la derecha, moviendo su subárbol izquierdo (x) a su posición original, y luego ajusta los punteros correspondientes. Retorna el nuevo nodo raíz del subárbol girado.

    Función rotateLeft
      TreeNode* rotateLeft(TreeNode* x) {
      TreeNode* y = x->right;
      TreeNode* T2 = y->left;
      y->left = x;
      x->right = T2;
      return y;
    }
Realiza una rotación simple a la izquierda en un árbol AVL. La rotación gira el nodo x hacia la izquierda, moviendo su subárbol derecho (y) a su posición original, y luego ajusta los punteros correspondientes. Retorna el nuevo nodo raíz del subárbol girado.

    Función getBalance
     int getBalance(TreeNode* node) {
     if (node == NULL) return 0;
     return height(node->left) - height(node->right);
    }
Obtiene el equilibrio de un nodo en un árbol AVL. La función calcula la diferencia de alturas entre el subárbol izquierdo y derecho del nodo. Un valor positivo indica que el subárbol izquierdo es más alto, mientras que un valor negativo indica que el subárbol derecho es más alto. Retorna el resultado de esta comparación.

Función insertAVL
    
    TreeNode* insertAVL(TreeNode* node, int key) {
    if (node == NULL)
        return new TreeNode(key);

    if (key < node->val)
        node->left = insertAVL(node->left, key);
    else if (key > node->val)
        node->right = insertAVL(node->right, key);
    else
        return node;

    int balance = getBalance(node);

    if (balance > 1 && key < node->left->val)
        return rotateRight(node);

    if (balance < -1 && key > node->right->val)
        return rotateLeft(node);

    if (balance > 1 && key > node->left->val) {
        node->left = rotateLeft(node->left);
        return rotateRight(node);
    }

    if (balance < -1 && key < node->right->val) {
        node->right = rotateRight(node->right);
        return rotateLeft(node);
    }

    return node;
    }
Inserta un nuevo nodo con clave key en el árbol AVL representado por node. Si el árbol resultante no es un árbol AVL válido después de la inserción, realiza las rotaciones necesarias para restaurarlo. Asegura que el árbol permanezca balanceado después de cada inserción.

Función insertBST

    TreeNode* insertBST(TreeNode* root, int key) {
    if (root == NULL)
        return new TreeNode(key);

    if (key < root->val)
        root->left = insertBST(root->left, key);
    else if (key > root->val)
        root->right = insertBST(root->right, key);

    return root;
    }
Inserta un nuevo nodo con clave key en el árbol binario de búsqueda (BST) representado por root. Si el árbol resultante no es un BST válido después de la inserción, realiza las inserciones necesarias para restaurarlo. Asegura que el árbol permanezca ordenado después de cada inserción.

Función convertToAVL

    TreeNode* convertToAVL(TreeNode* root) {
    if (root == NULL) return NULL;
    vector<int> nodes;
    queue<TreeNode*> q;
    q.push(root);
    while (!q.empty()) {
        TreeNode* node = q.front();
        q.pop();
        nodes.push_back(node->val);
        if (node->left!= NULL) q.push(node->left);
        if (node->right!= NULL) q.push(node->right);
    }
    TreeNode* avlRoot = NULL;
    for (int val : nodes) {
        avlRoot = insertAVL(avlRoot, val);
    }
    return avlRoot;
    }
Convierte un árbol binario de búsqueda `(BST)` en un árbol AVL. Primero, recorre el `BST` en orden y guarda todos los valores en un vector. Luego, utiliza estos valores para construir un nuevo árbol AVL, asegurando que el árbol resultante sea un AVL válido.

Funciones Auxiliares para Rojo-Negro
     
    Función leftRotate
     void leftRotate(RBNode*& root, RBNode*& pt) {
     RBNode* pt_right = pt->right;
     pt->right = pt_right->left;

    if (pt->right!= NULL)
        pt->right->parent = pt;

    pt_right->parent = pt->parent;

    if (pt->parent == NULL)
        root = pt_right;
    else if (pt == pt->parent->left)
        pt->parent->left = pt_right;
    else
        pt->parent->right = pt_right;

    pt_right->left = pt;
    pt->parent = pt_right;
    }
Realiza una rotación simple a la izquierda en un árbol rojo-negro. La rotación gira el nodo pt hacia la izquierda, moviendo su subárbol derecho (pt_right) a su posición original, y luego ajusta los punteros correspondientes.

Función rightRotate
   
    void rightRotate(RBNode*& root, RBNode*& pt) {
    RBNode* pt_left = pt->left;
    pt->left = pt_left->right;

    if (pt->left!= NULL)
        pt->left->parent = pt;

    pt_left->parent = pt->parent;

    if (pt->parent == NULL)
        root = pt_left;
    else if (pt == pt->parent->left)
        pt->parent->left = pt_left;
    else
        pt->parent->right = pt_left;

    pt_left->right = pt;
    pt->parent = pt_left;
    }
Realiza una rotación simple a la derecha en un árbol rojo-negro. La rotación gira el nodo pt hacia la derecha, moviendo su subárbol izquierdo `(pt_left)` a su posición original, y luego ajusta los punteros correspondientes.

Función balanceInsert
    
    void balanceInsert(RBNode*& root, RBNode*& pt) {
    RBNode* parent_pt = NULL;
    RBNode* grand_parent_pt = NULL;

    while ((pt!= root) && (pt->color!= BLACK) && (pt->parent->color == RED)) {
        parent_pt = pt->parent;
        grand_parent_pt = pt->parent->parent;

        if (parent_pt == grand_parent_pt->left) {
            RBNode* uncle_pt = grand_parent_pt->right;

            if (uncle_pt!= NULL && uncle_pt->color == RED) {
                grand_parent_pt->color = RED;
                parent_pt->color = BLACK;
                uncle_pt->color = BLACK;
                pt = grand_parent_pt;
            } else {
                if (pt == parent_pt->right) {
                    leftRotate(root, parent_pt);
                    pt = parent_pt;
                    parent_pt = pt->parent;
                }
                rightRotate(root, grand_parent_pt);
                swap(parent_pt->color, grand_parent_pt->color);
                pt = parent_pt;
            }
        } else {
            RBNode* uncle_pt = grand_parent_pt->left;

            if (uncle_pt!= NULL && uncle_pt->color == RED) {
                grand_parent_pt->color = RED;
                parent_pt->color = BLACK;
                uncle_pt->color = BLACK;
                pt = grand_parent_pt;
            } else {
                if (pt == parent_pt->left) {
                    rightRotate(root, parent_pt);
                    pt = parent_pt;
                    parent_pt = pt->parent;
                }
                leftRotate(root, grand_parent_pt);
                swap(parent_pt->color, grand_parent_pt->color);
                pt = parent_pt;
            }
        }
    }
    root->color = BLACK;
    }
Esta función se encarga de mantener el árbol rojo-negro balanceado después de insertar un nuevo nodo `(pt)`. Realiza varias comprobaciones y rotaciones para asegurar que todas las propiedades del árbol rojo-negro se mantengan. Las rotaciones y cambios de color son necesarios para evitar violaciones de las propiedades del árbol rojo-negro después de la inserción.

    Función insertRB
     RBNode* insertRB(RBNode* root, int val) {
     RBNode* pt = new RBNode(val);

    if (root == NULL) {
        pt->color = BLACK;
        return pt;
    }

    RBNode* current = root;
    RBNode* parent = NULL;

    while (current!= NULL) {
        parent = current;
        if (pt->val < current->val)
            current = current->left;
        else if (pt->val > current->val)
            current = current->right;
        else
            return root; // Duplicates are not allowed
    }

    pt->parent = parent;
    if (pt->val < parent->val)
        parent->left = pt;
    else
        parent->right = pt;

    balanceInsert(root, pt);

    return root;
    }
Esta función inserta un nuevo nodo con valor val en el árbol rojo-negro representado por root. Comienza buscando la posición correcta para el nuevo nodo siguiendo las mismas reglas que un árbol binario de búsqueda `(BST)`. Una vez que encuentra la posición, inserta el nuevo nodo y llama a balanceInsert para asegurar que el árbol permanezca balanceado según las propiedades del árbol rojo-negro.

Función convertToRB
    
    RBNode* convertToRB(TreeNode* root) {
    if (root == NULL) return NULL;
    vector<int> nodes;
    queue<TreeNode*> q;
    q.push(root);
    while (!q.empty()) {
        TreeNode* node = q.front();
        q.pop();
        nodes.push_back(node->val);
        if (node->left!= NULL) q.push(node->left);
        if (node->right!= NULL) q.push(node->right);
    }
    RBNode* rbRoot = NULL;
    for (int val : nodes) {
        rbRoot = insertRB(rbRoot, val);
    }
    return rbRoot;
    }
Convierte un árbol binario de búsqueda `(BST)` en un árbol rojo-negro `(RBTree)`. Primero, recorre el `BST` en orden y guarda todos los valores en un vector. Luego, utiliza estos valores para construir un nuevo árbol `RBTree`, asegurando que el árbol resultante sea un RBTree válido.

Función printRBTree

    void printRBTree(RBNode* root) {
    if (root == NULL) return;
    queue<RBNode*> q;
    q.push(root);
    while (!q.empty()) {
        RBNode* node = q.front();
        q.pop();
        cout << node->val << (node->color == RED? "R " : "B ") << " ";
        if (node->left!= NULL) q.push(node->left);
        if (node->right!= NULL) q.push(node->right);
    }
    cout << endl;
    }
Imprime el árbol rojo-negro `(RBTree)` en consola, mostrando los nodos y su color (rojo o negro).

Función printTree

    void printTree(TreeNode* root) {
    if (root == NULL) return;
    queue<TreeNode*> q;
    q.push(root);
    while (!q.empty()) {
        TreeNode* node = q.front();
        q.pop();
        cout << node->val << " ";
        if (node->left!= NULL) q.push(node->left);
        if (node->right!= NULL) q.push(node->right);
    }
    cout << endl;
    }
Imprime el árbol binario de búsqueda `(BST)` en consola, mostrando los nodos en orden.

Funciones generateDot
Existen dos sobrecargas de la función generateDot, una para árboles binarios de búsqueda `(BST)` y otra para árboles rojo-negros `(RBTree)`. Ambas escriben en un archivo DOT, describiendo la estructura del árbol para su posterior visualización con herramientas como Graphviz.

Funciones printBSTTreeDot, printAVLTreeDot, printRBTreeDot
Estas funciones generan archivos DOT para visualizar árboles binarios de búsqueda `(BST)`, árboles AVL y árboles rojo-negros `(RBTree)` respectivamente. Cada función toma un nodo raíz y un nombre de archivo como argumentos, y utiliza la función generateDot para escribir la representación DOT del árbol en el archivo especificado.

## // PARTE DE GRAFOS -------------------------------------------------------------------------------------------------------------------------

### // Estructura para representar un grafo

  **Estructura `Graph`:** Esta estructura representa un grafo. Dentro de esta estructura, se utiliza un `vector` de `vector`s de enteros (`vector<vector<int>>`) llamado `adjacencyMatrix`. 
  Este es un método común para representar grafos, donde cada fila y columna corresponden a un nodo del grafo, y el valor en la intersección indica si hay una arista entre esos dos nodos o cuál es su peso (si existe). 
  Un valor de 0 generalmente significa que no hay arista entre los nodos correspondientes.

```C++
// Estructura para representar un grafo
  struct Graph {
      vector<vector<int>> adjacencyMatrix;
  };
```

### // Estructura para representar una arista
  
  **Estructura `Edge`:** Esta estructura representa una arista en el grafo. Contiene tres miembros:
  **`src`:** Representa el nodo origen de la arista.
  **`dest`:** Representa el nodo destino de la arista.
  **`weight`:** Representa el peso de la arista, que puede ser utilizado para representar, por ejemplo, la distancia entre los nodos si el grafo representa una red de caminos o una red social.

```C++
// Estructura para representar una arista  
struct Edge {
    int src, dest, weight;
};
```
### // Función para imprimir la matriz de adyacencia

  La función printAdjacencyMatrix está diseñada para imprimir la matriz de adyacencia de un grafo. La matriz de adyacencia es una representación común de grafos en programación,
  donde cada fila y columna representan un nodo del grafo, y el valor en la intersección indica si hay una arista entre esos dos nodos o cuál es su peso.

  **Parámetro `matrix`:** La función recibe una referencia constante a un `vector` de `vector`s de enteros (`vector<vector<int>>`). Este parámetro representa la matriz de adyacencia del grafo.
  
  **Bucle externo:** El primer bucle `for` itera sobre cada fila de la matriz de adyacencia. Esto se logra utilizando un rango basado en `auto`,
  lo que permite iterar sobre cada fila sin necesidad de especificar explícitamente el tipo de dato.
 ** Bucle interno:** Dentro del bucle externo, hay otro bucle `for` que itera sobre cada elemento (valor) de la fila actual. Este bucle utiliza la sintaxis moderna de rango para iterar sobre todos los elementos de la fila.
  
  **Impresión de valores:** Para cada valor en la fila, se imprime el valor seguido de un espacio. Esto se hace usando `cout`, que es la salida estándar en C++.
  Al final de cada fila, se imprime un salto de línea (`endl`) para comenzar una nueva fila en la salida.

```C++
  // Función para imprimir la matriz de adyacencia
void printAdjacencyMatrix(const vector<vector<int>>& matrix) {
    for (const auto& row : matrix) { // Itera sobre cada fila de la matriz
        for (int value : row) { // Itera sobre cada elemento de la fila actual
            cout << value << " "; // Imprime el valor del elemento
        }
        cout << endl; // Cambia de línea después de imprimir toda la fila
    }
}
```

### // Función para leer la matriz de adyacencia desde un archivo de texto

  La función `readAdjacencyMatrixFromFile` tiene como objetivo leer una matriz de adyacencia desde un archivo de texto y devolverla como un `vector` de `vectors` de enteros. 
  Esta función es especialmente útil cuando se trabaja con gráficos y se necesita cargar datos de un archivo para realizar análisis o manipulaciones.

  **Parámetro `filename`:** La función acepta un `string` que representa el nombre del archivo desde el cual se leerá la matriz de adyacencia.
  
  **Inicialización de la matriz:** Se inicializa un `vector` de `vector`s de enteros (`vector<vector<int>>`) vacío llamado `matrix` para almacenar la matriz de adyacencia leída del archivo.
  
  **Apertura del archivo :** Se intenta abrir el archivo con el nombre proporcionado. Si el archivo se abre correctamente, se procede a leerlo; De lo contrario, se informa de un error.
  
  **Lectura del archivo :** See lee el archivo línea por línea. Cada línea se procesa mediante un `stringstream` para convertirla en un formato que pueda ser fácilmente analizado.
  
  **Análisis de líneas y filas :** Cada línea se divide en valores separados por comas, que se agregan a un `vector` de enteros (`row`).
  Después de procesar todos los valores de una línea, esa fila se agrega a la matriz principal.
  
  **Cierre del archivo :** Una vez que se hayan leído todas las líneas del archivo, se cierra el archivo.
  
  **Retorno de la matriz :** Finalmente, la función devuelve la matriz de adyacencia leída del archivo.

  ```c++
  // Función para leer la matriz de adyacencia desde un archivo de texto
vector<vector<int>> readAdjacencyMatrixFromFile(const string& filename) {
    vector<vector<int>> matrix; // Vector vacío para almacenar la matriz de adyacencia
    ifstream file(filename); // Intenta abrir el archivo con el nombre dado
    if (file.is_open()) { // Verifica si el archivo se abrió correctamente
        string line; // Variable temporal para almacenar cada línea del archivo
        while (getline(file, line)) { // Lee cada línea del archivo
            stringstream ss(line); // Convierte la línea leída en un stream de entrada
            vector<int> row; // Vector para almacenar los valores de una fila
            int value; // Variable temporal para almacenar cada valor leído
            while (ss >> value) { // Extrae valores del stream hasta que no haya más
                row.push_back(value); // Agrega el valor extraído al vector de la fila
                if (ss.peek() == ',') // Comprueba si el siguiente carácter es una coma
                    ss.ignore(); // Ignora el carácter de coma si está presente
            }
            matrix.push_back(row); // Agrega la fila completa al vector de la matriz
        }
        file.close(); // Cierra el archivo después de leerlo completamente
    } else {
        cerr << "Error: No se pudo abrir el archivo." << endl; // Informa de error si el archivo no se pudo abrir
    }
    return matrix; // Devuelve la matriz de adyacencia leída
}
```
### // Función para leer el grafo desde un archivo de texto

Esta documentación proporciona una visión general de lo que hace la función, describe el parámetro de entrada (`filename`), y explica lo que la función devuelve (`un objeto Graph`). 
También menciona brevemente la expectativa sobre el formato del archivo de texto, aunque esto último dependería de la implementación específica de `readAdjacencyMatrixFromFile`

 ```c++
// Función para leer el grafo desde un archivo de texto
Graph readGraphFromFile(const string& filename) { //Nombre del archivo de texto que contiene la información del grafo.
    Graph graph;
    graph.adjacencyMatrix = readAdjacencyMatrixFromFile(filename);
    return graph; //Un objeto Graph que contiene la matriz de adyacencia del grafo leído.
}
 ```

### // Función para generar y guardar un archivo DOT para un grafo

La función `generateDotFile` que tiene como objetivo generar un archivo DOT para un grafo dado. Los archivos DOT son utilizados por herramientas como Graphviz para visualizar grafos. A continuación, se detalla el funcionamiento de esta función con comentarios explicativos:

```c++
// Función para generar y guardar un archivo DOT para un grafo
void generateDotFile(const Graph& graph, const string& filename) {
    ofstream dotFile(filename); // Intenta abrir el archivo con el nombre dado para escritura
    if (dotFile.is_open()) { // Verifica si el archivo se abrió correctamente
        dotFile << "graph G {" << endl; // Comienza la definición del grafo en el formato DOT
        for (int i = 0; i < graph.adjacencyMatrix.size(); ++i) { // Itera sobre cada nodo del grafo
            for (int j = i + 1; j < graph.adjacencyMatrix.size(); ++j) { // Itera sobre los posibles pares de nodos conectados
                if (graph.adjacencyMatrix[i][j]!= 0) { // Verifica si hay una arista entre los nodos i y j
                    dotFile << i << " -- " << j << " [label=\"" << graph.adjacencyMatrix[i][j] << "\"];" << endl; // Agrega la arista al archivo DOT
                }
            }
        }
        dotFile << "}" << endl; // Cierra la definición del grafo
        dotFile.close(); // Cierra el archivo
        cout << "Archivo DOT generado: " << filename << endl; // Informa que el archivo DOT fue generado exitosamente
    } else {
        cerr << "Error: No se pudo abrir el archivo DOT para escribir." << endl; // Maneja el caso en que el archivo no se pudo abrir
    }
}
```

**Parámetros**:
  `graph`: Una referencia constante al objeto `Graph` que representa el grafo cuyo archivo DOT se va a generar.
  `filename`: Una cadena que contiene el nombre del archivo DOT que se generará.

 **Proceso**:
  1. Se intenta abrir un archivo con el nombre especificado en el parámetro `filename` para escritura.
  2. Si el archivo se abre correctamente, se inicia la definición del grafo en el formato DOT con `"graph G {"`.
  3. Luego, se itera sobre cada posible par de nodos en el grafo. Para cada par de nodos `(i, j)` donde `i < j`, se verifica si hay una arista entre ellos mediante el valor en la posición `[i][j]` de la matriz de adyacencia del grafo.
  4. Si existe una arista (es decir, el valor no es 0), se agrega una línea al archivo DOT que representa esta arista, incluyendo el peso de la arista como etiqueta.
  5. Después de procesar todas las aristas, se cierra la definición del grafo con `"}` y se cierra el archivo.
  6. Finalmente, se informa que el archivo DOT fue generado exitosamente.

 **Manejo de errores**:
  Si el archivo no se pudo abrir para escritura, se emite un mensaje de error indicando que no se pudo abrir el archivo DOT para escribir.

Esta función es útil para generar archivos DOT de grafos, permitiendo su posterior visualización con herramientas como Graphviz, lo cual es invaluable para analizar y entender la estructura de los grafos.

###// Algoritmo de Floyd-Warshall para encontrar todas las distancias más cortas entre todos los pares de vértices

El código proporcionado implementa el algoritmo de Floyd-Warshall para calcular todas las distancias más cortas entre todos los pares de vértices en un grafo. Además, genera un archivo DOT para visualizar el resultado y, opcionalmente, una imagen PNG de ese grafo. A continuación, se detalla el funcionamiento de esta función con comentarios explicativos:

```c++
// Algoritmo de Floyd-Warshall para encontrar todas las distancias más cortas entre todos los pares de vértices
void floydWarshall(const Graph& graph) {
    int V = graph.adjacencyMatrix.size(); // Obtiene el número de vértices en el grafo
    vector<vector<int>> dist(V, vector<int>(V, numeric_limits<int>::max())); // Inicializa la matriz de distancias con infinito

    // Inicializar la matriz de distancias con los pesos de las aristas
    for (int i = 0; i < V; ++i) {
        for (int j = 0; j < V; ++j) {
            dist[i][j] = graph.adjacencyMatrix[i][j]; // Copia los pesos directos de las aristas
        }
    }

    // Actualizar las distancias mínimas entre todos los pares de vértices
    for (int k = 0; k < V; ++k) {
        for (int i = 0; i < V; ++i) {
            for (int j = 0; j < V; ++j) {
                if (dist[i][k]!= numeric_limits<int>::max() && dist[k][j]!= numeric_limits<int>::max() &&
                    dist[i][k] + dist[k][j] < dist[i][j]) {
                    dist[i][j] = dist[i][k] + dist[k][j]; // Actualiza la distancia mínima si es menor
                }
            }
        }
    }

    // Imprimir las distancias mínimas entre todos los pares de vértices
    cout << "Distancias mínimas entre todos los pares de vértices (Floyd-Warshall):" << endl;
    for (int i = 0; i < V; ++i) {
        for (int j = 0; j < V; ++j) {
            if (dist[i][j] == numeric_limits<int>::max())
                cout << "INF "; // Imprime INF si la distancia es infinita
            else
                cout << dist[i][j] << " "; // Imprime la distancia si no es infinita
        }
        cout << endl;
    }

    // Generar archivo DOT para visualizar el resultado de Floyd-Warshall
    ofstream dotFile("floyd_warshall.dot"); // Intenta abrir el archivo DOT para escritura
    if (dotFile.is_open()) {
        dotFile << "graph G {" << endl; // Comienza la definición del grafo en el formato DOT
        for (int i = 0; i < V; ++i) {
            for (int j = 0; j < V; ++j) {
                if (dist[i][j]!= numeric_limits<int>::max() && i!= j) { // Solo dibuja aristas no nulas
                    dotFile << i << " -- " << j << " [label=\"" << dist[i][j] << "\"];" << endl; // Dibuja la arista con su peso
                }
            }
        }
        dotFile << "}" << endl; // Cierra la definición del grafo
        dotFile.close(); // Cierra el archivo
        cout << "Archivo DOT generado para Floyd-Warshall: floyd_warshall.dot" << endl;

        // Verificar si el archivo DOT se ha generado correctamente
        ifstream checkFile("floyd_warshall.dot");
        if (checkFile.is_open()) {
            checkFile.close();
            // Generar la imagen PNG a partir del archivo DOT
            if (system("dot -Tpng floyd_warshall.dot -o floyd_warshall.png") == 0) {
                cout << "Imagen de Floyd-Warshall generada como 'floyd_warshall.png'." << endl;
            } else {
                cerr << "Error: No se pudo generar la imagen de Floyd-Warshall." << endl;
            }
        } else {
            cerr << "Error: El archivo DOT de Floyd-Warshall no se generó correctamente." << endl;
        }
    } else {
        cerr << "Error: No se pudo abrir el archivo DOT para escribir." << endl;
    }
}
```
Este función realiza lo siguiente:

1. **Inicialización**: Calcula el número de vértices en el grafo y crea una matriz de distancias inicializada con infinito (usando `numeric_limits<int>::max()`).

2. **Carga de pesos de aristas**: Copia los pesos de las aristas directas de la matriz de adyacencia del grafo a la matriz de distancias.

3. **Actualización de distancias**: Aplica el algoritmo de Floyd-Warshall para actualizar las distancias mínimas entre todos los pares de vértices.

4. **Impresión de resultados**: Imprime las distancias mínimas calculadas.

5. **Generación de archivo DOT**: Crea un archivo DOT que representa el grafo con las distancias mínimas encontradas.

6. **Generación de imagen PNG**: Utiliza Graphviz para generar una imagen PNG del grafo a partir del archivo DOT creado.

Este proceso permite visualizar gráficamente el grafo con las distancias mínimas calculadas por el algoritmo de Floyd-Warshall, facilitando la comprensión de la estructura del grafo y las relaciones entre sus vértices.


###// Función para el algoritmo de Dijkstra

Se implementa el algoritmo de Dijkstra para encontrar las distancias mínimas desde un nodo inicial a todos los demás nodos en un grafo. 
Además, genera un archivo DOT para visualizar el resultado y, opcionalmente, una imagen PNG de ese grafo.

```c++
// Función para el algoritmo de Dijkstra
void dijkstra(const Graph& graph, int startNode) {
    int numNodes = graph.adjacencyMatrix.size(); // Obtiene el número total de nodos en el grafo
    vector<int> dist(numNodes, numeric_limits<int>::max()); // Inicializa la matriz de distancias con infinito
    vector<bool> visited(numNodes, false); // Vector para marcar los nodos visitados

    dist[startNode] = 0; // La distancia desde el nodo inicial hasta sí mismo es 0

    for (int count = 0; count < numNodes - 1; ++count) { // Itera hasta menos uno porque el nodo inicial ya está marcado
        int minDist = numeric_limits<int>::max(); // Busca el nodo con la distancia mínima no visitada
        int minIndex = -1;

        // Encuentra el nodo no visitado con la distancia mínima
        for (int i = 0; i < numNodes; ++i) {
            if (!visited[i] && dist[i] < minDist) {
                minDist = dist[i];
                minIndex = i;
            }
        }

        if (minIndex == -1) // Si no se encuentra ningún nodo no visitado, termina el algoritmo
            break;

        visited[minIndex] = true; // Marca el nodo encontrado como visitado

        // Actualiza las distancias de los nodos adyacentes al nodo seleccionado
        for (int i = 0; i < numNodes; ++i) {
            if (!visited[i] && graph.adjacencyMatrix[minIndex][i] && // Verifica si hay una arista y si el nodo no visitado
                dist[minIndex]!= numeric_limits<int>::max() && // Evita comparaciones con infinito
                dist[minIndex] + graph.adjacencyMatrix[minIndex][i] < dist[i]) { // Actualiza la distancia si es menor
                dist[i] = dist[minIndex] + graph.adjacencyMatrix[minIndex][i];
            }
        }
    }

    // Imprime las distancias mínimas desde el nodo inicial
    cout << "Distancias mínimas desde el nodo " << startNode << " (Dijkstra):" << endl;
    for (int i = 0; i < numNodes; ++i) {
        cout << "Nodo " << i << ": " << dist[i] << endl;
    }

    // Genera archivo DOT para visualizar el resultado de Dijkstra
    ofstream dotFile("dijkstra.dot"); // Intenta abrir el archivo DOT para escritura
    if (dotFile.is_open()) {
        dotFile << "graph G {" << endl; // Comienza la definición del grafo en el formato DOT
        for (int i = 0; i < numNodes; ++i) {
            if (dist[i]!= numeric_limits<int>::max() && i!= startNode) { // Solo dibuja aristas no nulas
                dotFile << startNode << " -- " << i << " [label=\"" << dist[i] << "\"];" << endl; // Dibuja la arista con su peso
            }
        }
        dotFile << "}" << endl; // Cierra la definición del grafo
        dotFile.close(); // Cierra el archivo
        cout << "Archivo DOT generado para Dijkstra: dijkstra.dot" << endl;

        // Verifica si el archivo DOT se ha generado correctamente
        ifstream checkFile("dijkstra.dot");
        if (checkFile.is_open()) {
            checkFile.close();
            // Genera la imagen PNG a partir del archivo DOT
            if (system("dot -Tpng dijkstra.dot -o dijkstra.png") == 0) {
                cout << "Imagen de Dijkstra generada como 'dijkstra.png'." << endl;
            } else {
                cerr << "Error: No se pudo generar la imagen de Dijkstra." << endl;
            }
        } else {
            cerr << "Error: El archivo DOT de Dijkstra no se generó correctamente." << endl;
        }
    } else {
        cerr << "Error: No se pudo abrir el archivo DOT para escribir." << endl;
    }
}
```

Este código realiza lo siguiente:

1. **Inicialización**: Prepara los vectores `dist` y `visited` para almacenar las distancias mínimas desde el nodo inicial a todos los demás nodos y marcar los nodos visitados, respectivamente.

2. **Ejecución del algoritmo de Dijkstra**: Implementa el algoritmo de Dijkstra para encontrar las distancias mínimas desde el nodo inicial a todos los demás nodos en el grafo.

3. **Impresión de resultados**: Imprime las distancias mínimas desde el nodo inicial a todos los demás nodos.

4. **Generación de archivo DOT**: Crea un archivo DOT que representa el grafo con las distancias mínimas encontradas por el algoritmo de Dijkstra.

5. **Generación de imagen PNG**: Utiliza Graphviz para generar una imagen PNG del grafo a partir del archivo DOT creado.

Este proceso permite visualizar gráficamente el grafo con las distancias mínimas calculadas por el algoritmo de Dijkstra, facilitando la comprensión de la estructura del grafo y las relaciones entre sus vértices.

// FUNCIÓN FIND
```c++
int find(vector<int>& parent, int i) {
    if (parent[i] == -1)
        return i;
    return find(parent, parent[i]);
}
```
Busca la raíz del conjunto al que pertenece un nodo específico en un grafo o árbol. Utiliza el algoritmo de búsqueda recursiva para encontrar el ancestro común más cercano (ACM) de un nodo dado, lo cual representa la raíz del conjunto al que pertenece ese nodo.

**Parámetros**:
  `vector<int>& parent`: Referencia al vector que contiene los índices de los nodos padres. El valor -1 indica que el nodo es la raíz de su propio conjunto.
  `int i`: Índice del nodo cuya raíz se desea encontrar.
  Retorno: Entero que representa la raíz del conjunto al que pertenece el nodo i.

// FUNCIÓN unionSets
```c++
void unionSets(vector<int>& parent, int x, int y) {
    int xSet = find(parent, x);
    int ySet = find(parent, y);
    parent[xSet] = ySet;
}
```
Une dos conjuntos en un solo conjunto mediante la operación de unión. Se utiliza para combinar componentes conectados en un grafo o árbol.

**Parámetros**:
  `vector<int>& parent`: Referencia al vector que contiene los índices de los nodos padres. El valor -1 indica que el nodo es la raíz de su propio conjunto.
  `int x`: Índice del primer nodo cuyo conjunto se desea unir.
  `int y`: Índice del segundo nodo cuyo conjunto se desea unir.
  Efecto secundario: Modifica el vector `parent` para reflejar la nueva estructura de conjuntos después de la unión.

// FUNCIÓN compareEdges
```c++
bool compareEdges(const Edge& a, const Edge& b) {
    return a.weight < b.weight;
}
```
Compara dos aristas basándose en su peso. Se utiliza para ordenar las aristas de un grafo según su peso antes de aplicar el algoritmo de Kruskal.

**Parámetros**:
  `const Edge& a`: Referencia al vector que contiene los índices de los nodos padres. El valor -1 indica que el nodo es la raíz de su propio conjunto.
  `const Edge& b`: Índice del primer nodo cuyo conjunto se desea unir.
  Retorno: Valor booleano que indica si el peso de la arista a es menor que el peso de la arista b. Se utiliza para ordenar las aristas en orden ascendente de peso.

//ALGORITMO KRUSKAL
  ```c++
void kruskal(const Graph& graph) {
    int V = graph.adjacencyMatrix.size();
    vector<Edge> result(V - 1); // Árbol de expansión mínima tendrá (V - 1) aristas
    vector<int> parent(V, -1);  // Vector de padres para representar los conjuntos

    vector<Edge> edges; // Lista de aristas ordenadas por peso
    for (int i = 0; i < V; ++i) {
        for (int j = i + 1; j < V; ++j) {
            if (graph.adjacencyMatrix[i][j]!= 0) {
                edges.push_back({i, j, graph.adjacencyMatrix[i][j]});
            }
        }
    }
    // Ordenar las aristas por peso
    sort(edges.begin(), edges.end(), compareEdges);

    int edgeCount = 0;
    int i = 0;
    while (edgeCount < V - 1 && i < edges.size()) {
        Edge nextEdge = edges[i++];
        int x = find(parent, nextEdge.src);
        int y = find(parent, nextEdge.dest);
        if (x!= y) {
            result[edgeCount++] = nextEdge;
            unionSets(parent, x, y);
        }
    }
}
```
Implementación del algoritmo de Kruskal para encontrar un árbol de expansión mínima (AEM) en un grafo no dirigido ponderado. El algoritmo selecciona aristas disjuntas en orden creciente de peso hasta que se alcanza el número máximo de aristas que puede tener un árbol conexo, es decir, (V - 1) aristas donde V es el número de vértices.

**Parámetros**:
  `const Graph& graph`: Grafo no dirigido ponderado del cual se desea encontrar el AEM.
  Efecto secundario: Construye un vector `result` que contiene las aristas del AEM y modifica el vector `parent` para reflejar la estructura de conjuntos final después de 
  realizar todas las uniones necesarias.

###// Imprimir el Árbol de Expansión Mínima
```c++
cout << "Arbol de expansion minima (Kruskal):" << endl;
for (int i = 0; i < V - 1; ++i) {
    cout << result[i].src << " -- " << result[i].dest << " [peso=" << result[i].weight << "]" << endl;
}
```
Este fragmento de código imprime el árbol de expansión mínima (AEM) encontrado por el algoritmo de Kruskal. Para cada arista en el AEM, muestra el origen (src), el destino (dest) y el peso de la arista (weight). Esto permite visualizar la estructura del AEM directamente en la consola.

###// Generar Archivo DOT para Visualizar el Resultado de Kruskal
```c++
ofstream dotFile("kruskal.dot");
if (dotFile.is_open()) {
    dotFile << "graph G {" << endl;
    for (int i = 0; i < V - 1; ++i) {
        dotFile << result[i].src << " -- " << result[i].dest << " [label=\"" << result[i].weight << "\"];" << endl;
    }
    dotFile << "}" << endl;
    dotFile.close();
    cout << "Archivo DOT generado para Kruskal: kruskal.dot" << endl;
```
Este bloque de código genera un archivo DOT `kruskal.dot` que describe el AEM encontrado por el algoritmo de Kruskal. El archivo DOT es un formato estándar utilizado para describir gráficos en programas de diagramación como Graphviz. Para cada arista en el AEM, agrega una línea en el archivo DOT que conecta el origen y el destino de la arista, etiquetada con el peso de la arista.

###// Verificar si el Archivo DOT se ha Generado Correctamente
```c++
ifstream checkFile("kruskal.dot");
if (checkFile.is_open()) {
    checkFile.close();
    // Generar la imagen PNG a partir del archivo DOT
    if (system("dot -Tpng kruskal.dot -o kruskal.png") == 0) {
        cout << "Imagen de Kruskal generada como 'kruskal.png'." << endl;
    } else {
        cerr << "Error: No se pudo generar la imagen de Kruskal." << endl;
    }
} else {
    cerr << "Error: El archivo DOT de Kruskal no se generó correctamente." << endl;
}
```
Después de generar el archivo DOT, este fragmento verifica si el archivo se ha creado correctamente abriendo el archivo `kruskal.dot` y luego intenta convertirlo a una imagen PNG utilizando Graphviz `dot`. Si la conversión es exitosa, imprime un mensaje indicando que la imagen fue generada. En caso contrario, muestra un mensaje de error.

###// Cerrar el Archivo DOT y Manejo de Errores
```c++
} else {
    cerr << "Error: No se pudo abrir el archivo DOT para escribir." << endl;
}
```
Este último bloque maneja el caso en el que no se pudo abrir el archivo DOT para escritura. Imprime un mensaje de error indicando que hubo un problema al intentar crear el archivo DOT.

// Algoritmo de Prim para encontrar un árbol de expansión mínima
```c++
void prim(const Graph& graph) {
    int V = graph.adjacencyMatrix.size();
    vector<int> key(V, numeric_limits<int>::max()); // Vector para almacenar la clave de cada vértice
    vector<bool> inMST(V, false); // Vector para marcar los vértices ya incluidos en el MST
    vector<int> parent(V, -1); // Vector para almacenar el padre de cada vértice en el MST
    key[0] = 0; // Inicializar la clave del primer vértice a 0
    parent[0] = -1; // Establecer el padre del primer vértice como -1, indicando que es la raíz

    for (int count = 0; count < V - 1; ++count) { // Iterar hasta encontrar V - 1 aristas
        int minKey = numeric_limits<int>::max(); // Inicializar la clave mínima a infinito
        int u = -1; // Inicializar el vértice u como -1

        for (int v = 0; v < V; ++v) { // Buscar el vértice con la clave mínima aún no considerada
            if (!inMST[v] && key[v] < minKey) {
                minKey = key[v];
                u = v;
            }
        }

        inMST[u] = true; // Marcar el vértice u como incluido en el MST

        for (int v = 0; v < V; ++v) { // Actualizar las claves de los vértices adyacentes a u
            if (graph.adjacencyMatrix[u][v] &&!inMST[v] && graph.adjacencyMatrix[u][v] < key[v]) {
                parent[v] = u;
                key[v] = graph.adjacencyMatrix[u][v];
            }
        }
    }
}
```
Implementación del algoritmo de Prim para encontrar un árbol de expansión mínima (AEM) en un grafo ponderado conexo. El algoritmo construye el AEM añadiendo gradualmente aristas que conectan vértices no incluidos en el MST actual, siempre elegiendo la arista con el peso mínimo que conecta un vértice fuera del MST con uno dentro.

**Parámetros**:
  `const Graph& graph`: Grafo ponderado conexo del cual se desea encontrar el AEM.
  Efecto secundario: Construye un vector `parent` que contiene el padre de cada vértice en el MST, y un vector `key` que almacena la distancia mínima desde el vértice 
  inicial hasta cada vértice. Además, mantiene un vector `inMST` que marca los vértices ya incluidos en el MST.

// Imprimir el árbol de expansión mínima (Prim)
```c++
cout << "Arbol de expansion minima (Prim):" << endl;
for (int i = 1; i < V; ++i) {
    cout << parent[i] << " -- " << i << " [peso=" << graph.adjacencyMatrix[i][parent[i]] << "]" << endl;
}
```
Este fragmento de código imprime el árbol de expansión mínima (AEM) encontrado por el algoritmo de Prim. Para cada arista en el AEM, muestra el origen `parent[i]`, el destino `i`, y el peso de la arista `graph.adjacencyMatrix[i][parent[i]]`. Esto permite visualizar la estructura del AEM directamente en la consola.

// Generar archivo DOT para visualizar el resultado de Prim
```c++
ofstream dotFile("prim.dot");
if (dotFile.is_open()) {
    dotFile << "graph G {" << endl;
    for (int i = 1; i < V; ++i) {
        dotFile << parent[i] << " -- " << i << " [label=\"" << graph.adjacencyMatrix[i][parent[i]] << "\"];" << endl;
    }
    dotFile << "}" << endl;
    dotFile.close();
    cout << "Archivo DOT generado para Prim: prim.dot" << endl;
```
Este bloque de código genera un archivo DOT `prim.dot` que describe el AEM encontrado por el algoritmo de Prim. El archivo DOT es un formato estándar utilizado para describir gráficos en programas de diagramación como Graphviz. Para cada arista en el AEM, agrega una línea en el archivo DOT que conecta el origen y el destino de la arista, etiquetada con el peso de la arista.

// Verificar si el archivo DOT se ha generado correctamente
```c++
ifstream checkFile("prim.dot");
if (checkFile.is_open()) {
    checkFile.close();
    // Generar la imagen PNG a partir del archivo DOT
    if (system("dot -Tpng prim.dot -o prim.png") == 0) {
        cout << "Imagen de Prim generada como 'prim.png'." << endl;
    } else {
        cerr << "Error: No se pudo generar la imagen de Prim." << endl;
    }
} else {
    cerr << "Error: El archivo DOT de Prim no se generó correctamente." << endl;
}
```
Después de generar el archivo DOT, este fragmento verifica si el archivo se ha creado correctamente abriendo el archivo `prim.dot` y luego intenta convertirlo a una imagen PNG utilizando Graphviz `dot`. Si la conversión es exitosa, imprime un mensaje indicando que la imagen fue generada. En caso contrario, muestra un mensaje de error.

// Cerrar el archivo DOT y manejo de errores
```c++
} else {
    cerr << "Error: No se pudo abrir el archivo DOT para escribir." << endl;
}
```
Este último bloque maneja el caso en el que no se pudo abrir el archivo DOT para escritura. Imprime un mensaje de error indicando que hubo un problema al intentar crear el archivo DOT.

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
