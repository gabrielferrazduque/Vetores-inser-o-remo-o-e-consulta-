# Vetores-inser-o-remo-o-e-consulta-
Vetores (inserção, remoção e consulta)
#include <stdio.h>

#define MAX 50

// Função para realizar inserção ordenada
void inserirOrdenado(int vetor[], int *tamanho, int valor) {
    if (*tamanho == MAX) {
        printf("O vetor está cheio!\n");
        return;
    }
    
    int i;
    for (i = *tamanho - 1; (i >= 0 && vetor[i] > valor); i--) {
        vetor[i + 1] = vetor[i]; // Desloca os elementos
    }
    
    vetor[i + 1] = valor; // Insere o valor na posição correta
    (*tamanho)++;
}

// Função para imprimir o vetor
void imprimirVetor(int vetor[], int tamanho) {
    printf("Vetor: ");
    for (int i = 0; i < tamanho; i++) {
        printf("%d ", vetor[i]);
    }
    printf("\n");
}

// Função para busca binária
int buscaBinaria(int vetor[], int tamanho, int valor) {
    int inicio = 0, fim = tamanho - 1, meio;

    while (inicio <= fim) {
        meio = (inicio + fim) / 2;
        if (vetor[meio] == valor)
            return meio;
        else if (vetor[meio] < valor)
            inicio = meio + 1;
        else
            fim = meio - 1;
    }

    return -1; // Não encontrado
}

// Função para remover um valor do vetor
void removerValor(int vetor[], int *tamanho, int valor) {
    int posicao = buscaBinaria(vetor, *tamanho, valor);

    if (posicao == -1) {
        printf("Elemento não encontrado.\n");
        return;
    }

    // Desloca os elementos à direita para a esquerda
    for (int i = posicao; i < *tamanho - 1; i++) {
        vetor[i] = vetor[i + 1];
    }

    (*tamanho)--;
    printf("Elemento removido com sucesso.\n");
}

int main() {
    int vetor[MAX];
    int tamanho, valor, opcao;

    printf("Digite o tamanho do vetor (entre 3 e 50): ");
    do {
        scanf("%d", &tamanho);
    } while (tamanho < 3 || tamanho > 50);

    // Preenchimento do vetor
    for (int i = 0; i < tamanho; i++) {
        printf("Digite o valor %d: ", i + 1);
        scanf("%d", &valor);
        inserirOrdenado(vetor, &tamanho, valor);
    }

    do {
        printf("\nMenu:\n");
        printf("1. Imprimir vetor\n");
        printf("2. Consultar posição de um elemento\n");
        printf("3. Remover elemento\n");
        printf("4. Inserir elemento\n");
        printf("5. Sair\n");
        printf("Escolha uma opção: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                imprimirVetor(vetor, tamanho);
                break;
            case 2:
                printf("Digite o valor a ser consultado: ");
                scanf("%d", &valor);
                int posicao = buscaBinaria(vetor, tamanho, valor);
                if (posicao != -1)
                    printf("Elemento encontrado na posição %d\n", posicao);
                else
                    printf("Elemento não encontrado.\n");
                break;
            case 3:
                printf("Digite o valor a ser removido: ");
                scanf("%d", &valor);
                removerValor(vetor, &tamanho, valor);
                break;
            case 4:
                printf("Digite o valor a ser inserido: ");
                scanf("%d", &valor);
                inserirOrdenado(vetor, &tamanho, valor);
                break;
            case 5:
                printf("Saindo...\n");
                break;
            default:
                printf("Opção inválida!\n");
        }
    } while (opcao != 5);

    return 0;
}
