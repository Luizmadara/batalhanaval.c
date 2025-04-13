#include <stdio.h>

#define TAMANHO_TABULEIRO 10
#define TAMANHO_NAVIO 3
#define AGUA 0
#define NAVIO 3

// Função para inicializar o tabuleiro com água (0)
void inicializarTabuleiro(int tabuleiro[TAMANHO_TABULEIRO][TAMANHO_TABULEIRO]) {
    for (int i = 0; i < TAMANHO_TABULEIRO; i++) {
        for (int j = 0; j < TAMANHO_TABULEIRO; j++) {
            tabuleiro[i][j] = AGUA;
        }
    }
}

// Função para imprimir o tabuleiro
void exibirTabuleiro(int tabuleiro[TAMANHO_TABULEIRO][TAMANHO_TABULEIRO]) {
    for (int i = 0; i < TAMANHO_TABULEIRO; i++) {
        for (int j = 0; j < TAMANHO_TABULEIRO; j++) {
            printf("%d ", tabuleiro[i][j]);
        }
        printf("\n");
    }
}

// Função para verificar se é possível posicionar o navio sem sair dos limite e sem sobreposição
int podePosicionar(int tabuleiro[TAMANHO_TABULEIRO][TAMANHO_TABULEIRO], int linha, int coluna, char orientacao) {
    for (int i = 0; i < TAMANHO_NAVIO; i++) {
        int x = linha + (orientacao == 'V' ? i : 0);
        int y = coluna + (orientacao == 'H' ? i : 0);

        if (x >= TAMANHO_TABULEIRO || y >= TAMANHO_TABULEIRO || tabuleiro[x][y] != AGUA) {
            return 0; // Fora do tabuleiro ou sobreposição
        }
    }
    return 1; // Válido
}

// Função para posicionar o navio no tabuleiro
void posicionarNavio(int tabuleiro[TAMANHO_TABULEIRO][TAMANHO_TABULEIRO], int linha, int coluna, char orientacao) {
    for (int i = 0; i < TAMANHO_NAVIO; i++) {
        int x = linha + (orientacao == 'V' ? i : 0);
        int y = coluna + (orientacao == 'H' ? i : 0);
        tabuleiro[x][y] = NAVIO;
    }
}

int main() {
    int tabuleiro[TAMANHO_TABULEIRO][TAMANHO_TABULEIRO];

    // Inicializa o tabuleiro com água
    inicializarTabuleiro(tabuleiro);

    // Coordenadas iniciais dos navios
    int linhaHorizontal = 2, colunaHorizontal = 4; // Navio horizontal começa na linha 2, coluna 4
    int linhaVertical = 5, colunaVertical = 7;     // Navio vertical começa na linha 5, coluna 7

    // Verifica se é possível posicionar os navios
    if (podePosicionar(tabuleiro, linhaHorizontal, colunaHorizontal, 'H')) {
        posicionarNavio(tabuleiro, linhaHorizontal, colunaHorizontal, 'H');
    } else {
        printf("Erro ao posicionar o navio horizontal.\n");
    }

    if (podePosicionar(tabuleiro, linhaVertical, colunaVertical, 'V')) {
        posicionarNavio(tabuleiro, linhaVertical, colunaVertical, 'V');
    } else {
        printf("Erro ao posicionar o navio vertical.\n");
    }

    // Exibe o tabuleiro final
    printf("Tabuleiro final:\n");
    exibirTabuleiro(tabuleiro);

    return 0;
}
