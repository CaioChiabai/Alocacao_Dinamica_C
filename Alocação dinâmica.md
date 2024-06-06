# Alocação dinâmica

A linguagem C possui apenas 4 funções para alocação dinâmica sendo todas elas disponíveis na biblioteca `<stdlib.h>` :

- `malloc()`;
- `calloc();`
- `realloc();`
- `free().`

E existe também o operador:

- `sizeof().`

# Sizeof

 Retorna o numero de bytes necessários para alocar um único elemento de um tipo de dado

- Exemplo de programa
    
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(){
    
        int x;
        x = sizeof(int);
        printf("%d", x);
    }
    //atribui o valor 4 a variavel x
    ```
    

No geral se define o tamanho das variáveis como:

`char: 1 byte`

`int: 4 bytes`

`float: 4 bytes`

`double: 8 bytes`

# Malloc

Serve para alocar memória durante a execução do programa. Ele faz o pedido de memória ao computador e retorna um ponteiro com o endereço do inicio do espaço alocado

- Funcionamento
    
    A função `malloc()` recebe como parâmetro a quantidade de bytes a ser alocada e retorna:
    
    - Null: em caso de erro;
    - Ponteiro para a primeira posição alocada
    
- Exemplos de Programa
    
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(){
    
    //Exemplo: criar um array de tamanho 50
    
        int *v;
        char *c;
        v = (int*)malloc(50 * (sizeof(int)));
        c = (char*)malloc(50 * (sizeof(char)));
    
        return 0;
    }
    ```
    
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(){
    
        int *p;
    
        p = (int*)malloc(5 * (sizeof(int)));
    
        if(p == NULL){
            printf("Erro de Memoria!!");
            exit(1); // termina o programa 
        }
    
        int i;
        for(i = 0; i < 5; i++){
            printf("Digite p[%d]: ", i);
            scanf("%d", &p[i]);
        }
    
        printf("\n");
    
        int y;
        for(y = 0; y < 5; y++){
            printf("p[%d] = %d \n", y, p[y]);
        }
    		
    		//libera a memoria alocada
        free(p);
    		
        return 0;
    }
    ```
    

# Calloc

Serve para alocar memoria durante a execução do programa. Ela faz o pedido de memoria ao computador e retorna um ponteiro com o endereço do inicio do espaço alocado

- Funcionamento
    
    A função `calloc()` recebe por parâmetro:
    
    - Número de elementos no array a ser alocado;
    - Tamanho de cada elemento do array.
    
    E retorna:
    
    - NULL: caso de erro;
    - Ponteiro para a primeira posição do array.
    
- Exemplos de Programa
    
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    
    // Serve para alocar memória durante a execução do programa.
    // Ele faz o pedido de memória ao computador e retorna um ponteiro 
    // com o endereço do inicio do espaço alocado.
    
    int main(){
    
        int *v;
        char *c;
    
    //Exemplo: criar um array de 50 inteiros (4 bytes cada)
        v = (int*) calloc (50, 4);
    
    //Exemplo: criar um array de 200 char (1 bytes cada)    
        c = (char*) calloc (200, 1);
    
        return 0;
    }
    ```
    

# Diferença Malloc e Calloc

```c
#include <stdio.h>
#include <stdlib.h>

//Diferenca de malloc e calloc
//Calloc sempre ao alocar a memoria coloca 0 nos espaços alocados

int main(){

    int *c, *m;
    c = (int*)malloc(5 * (sizeof(int)));
    m = (int*)calloc(5, sizeof(int));

    for(int i = 0; i < 5; i++){
        printf("Malloc m[%d]: %d  ", i, m[i]);
    }
    
    printf("\n");

    for(int j = 0; j < 5; j++){
        printf("Calloc c[%d]: %d  ", j, c[j]);
    }
    
    return 0;
}
```

# Realloc

Serve para alocar ou realocar memória durante a execução do programa. Ela faz o pedido de memoria ao computador e retorna um ponteiro com o endereço do inicio do espaço alocado

- Funcionamento
    
    A função `realloc()` recebe como parâmetro:
    
    - Ponteiro para um bloco de memória já alocada;
    - A quantidade de bytes a ser alocada.
    
    E retorna:
    
    - NULL: caso de erro;
    - Ponteiro para a primeira posição do array.
    
    Se o ponteiro para o bloco de memoria previamente alocado for Null, a função `realloc()`irá alocar memória da mesma forma que a função `malloc()`. Veja o programa 2 como exemplo.
    
- Exemplo de programa
    
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(){
    
        int *p;
    
    //Cria um array de 50 inteiros (200 bytes)
        p = (int*) malloc (50 * sizeof(int));
        
    //Aumenta o array para 100 inteiros (400 bytes)
        p = (int*) realloc (p, 100 * sizeof(int));
    
        free(p);
        return 0;
    }
    ```
    
    ```c
    #include <stdlib.h>
    
    //Se o ponteiro para o bloco de memoria previamente alocado
    //for Null, a função realloc() irá alocar memória da mesma
    //forma que a função malloc()
    
    int main(){
    
        int *p;
    
    //O comando abaixo
        p = (int*) realloc (NULL, 50 * sizeof(int));
        
    //Equivale a:
        p = (int*) malloc (50 * sizeof(int));
    
        free(p);
        return 0;
    }
    ```
    

# Alocação de Matrizes

Para alocar um array com mais de 1 dimensão precisamos utilizar o conceito de “ponteiro para ponteiro”:

- Ponteiro (1 nível): cria um vetor; `int *p;`
- Ponteiro para ponteiro (2 níveis): permite criar uma matriz; `int **p`
- Ponteiro para ponteiro para ponteiro (3 níveis): permite criar um array de três dimensões. `int ***p;`

E assim por diante.

- Int * → permite criar um array de int;
- int ** → permite criar um array de int*.
- Exemplo de programa
    
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(){
    
        int **p; // 2 '*'  = 2 níveis = 2 dimensões
        int i, j, N = 2;
    
        //Criar um array de ponteiros (int *)
        p = (int**) malloc (N * sizeof(int*));
    
        for(i = 0; i < N; i++){
            //Criar um array de int
            p[i] = (int*) malloc (N * sizeof(int));
            
            for(j = 0; j < N; j++){
                //Lê a matriz de inteiros
                scanf("%d", &p[i][j]);
            }
        }
    
    //Em um array de mais de uma dimensão, a memoria
    //é liberada na ordem inversa da alocação
    
        for(i = 0; i < N; i++){
            free(p[i]);
        }
    
        free(p);
        return 0;
    }
    ```
    
    
