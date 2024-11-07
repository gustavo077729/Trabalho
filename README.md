# Trabalho
#include <stdio.h>
#include <stdlib.h>

struct filaElementos {
    int comeco, fim;
    int *elementos;
};

void iniciarFila(struct filaElementos *fila, int tamanho) {
    fila->comeco = 0;
    fila->fim = -1;
    fila->elementos = (int *)malloc(tamanho * sizeof(int)); 
    if (fila->elementos == NULL) {
        printf("Erro ao alocar memória para a fila.\n");
        exit(1); 
    }
}

void liberarFila(struct filaElementos *fila) {
    free(fila->elementos);  
    printf("Memória da fila liberada.\n");
}

int isFilaVazia(struct filaElementos *fila) {
    return fila->fim < fila->comeco;
}

void inserir(struct filaElementos *fila, int x) {
    if (fila->fim == 9) {  
        printf("Erro: Fila cheia. Não é possível adicionar mais elementos.\n");
    } else {
        fila->fim++;
        fila->elementos[fila->fim] = x;
    }
}

void consultar(struct filaElementos *fila) {
    if (isFilaVazia(fila)) {
        printf("Erro: A fila está vazia. Não há elementos para consultar.\n");
    } else {
        for (int i = fila->comeco; i <= fila->fim; i++) {
            printf("Elemento: %d\n", fila->elementos[i]);
        }
    }
}

void consultarComecoFila(struct filaElementos *fila) {
    if (isFilaVazia(fila)) {
        printf("Erro: A fila está vazia. Não há elementos para consultar.\n");
    } else {
        printf("Primeiro elemento da fila: %d\n", fila->elementos[fila->comeco]);
    }
}

void remover(struct filaElementos *fila) {
    if (isFilaVazia(fila)) {
        printf("Erro: A fila está vazia. Não há elementos para remover.\n");
    } else {
        fila->comeco++;
        
        if (fila->comeco > fila->fim) {
            fila->comeco = fila->fim = -1;  
        }
    }
}

void esvaziar(struct filaElementos *fila) {
    if (isFilaVazia(fila)) {
        printf("Erro: A fila está vazia. Não há elementos para esvaziar.\n");
    } else {
        fila->fim = -1; 
        printf("Fila esvaziada.\n");
    }
}

void lerEntrada(int *x) {
    int valid = 0;
    while (!valid) {
        printf("Informe um número: ");
        if (scanf("%d", x) == 1) {
            valid = 1; 
        } else {
            printf("Entrada inválida. Tente novamente.\n");
         
            while (getchar() != '\n');
        }
    }
}

int main() {
    int tamanho;
    printf("Digite o tamanho da fila: ");
    scanf("%d", &tamanho);

    struct filaElementos fila;
    iniciarFila(&fila, tamanho);  

    int x;
    for (int i = 0; i < tamanho; i++) {
        lerEntrada(&x); 
        inserir(&fila, x);  
    }

    printf("\nConsultando todos os elementos da fila:\n");
    consultar(&fila);

    printf("\nConsultando o primeiro elemento da fila:\n");
    consultarComecoFila(&fila);

    printf("\nRemovendo o primeiro elemento da fila:\n");
    remover(&fila);
    consultar(&fila);  

    printf("\nEsvaziando a fila:\n");
    esvaziar(&fila);
    consultar(&fila); 

    liberarFila(&fila);  

}
