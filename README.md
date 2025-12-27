// Jogo Batalha Naval – Tema 5

/*
Projeto desenvolvido em linguagem C++, utilizando matriz para representar
o tabuleiro do jogo Batalha Naval. O sistema posiciona os navios de forma
automática e permite que o jogador realize disparos informando linha e
coluna. O jogo informa acertos e erros e finaliza quando todos os navios
sao destruidos, conforme proposto no Tema 5 da disciplina.
*/

#include <iostream>
#include <cstdlib>
#include <ctime>

using namespace std;

// Constantes do jogo
const int TAM = 10;
const int NAVIOS = 5;

// Inicializa o tabuleiro com agua
void inicializarTabuleiro(char tabuleiro[TAM][TAM]) {
    for (int i = 0; i < TAM; i++) {
        for (int j = 0; j < TAM; j++) {
            tabuleiro[i][j] = '~';
        }
    }
}

// Posiciona os navios de forma aleatoria
void posicionarNavios(int navios[TAM][TAM]) {
    int colocados = 0;

    while (colocados < NAVIOS) {
        int linha = rand() % TAM;
        int coluna = rand() % TAM;

        if (navios[linha][coluna] == 0) {
            navios[linha][coluna] = 1;
            colocados++;
        }
    }
}

// Mostra o tabuleiro ao jogador
void mostrarTabuleiro(char tabuleiro[TAM][TAM]) {
    cout << "   ";
    for (int i = 0; i < TAM; i++) {
        cout << i << " ";
    }
    cout << endl;

    for (int i = 0; i < TAM; i++) {
        cout << i << "  ";
        for (int j = 0; j < TAM; j++) {
            cout << tabuleiro[i][j] << " ";
        }
        cout << endl;
    }
}

int main() {
    srand(time(NULL));

    char tabuleiro[TAM][TAM];
    int navios[TAM][TAM] = {0};

    int linha, coluna;
    int acertos = 0;
    int tentativas = 0;

    inicializarTabuleiro(tabuleiro);
    posicionarNavios(navios);

    cout << "=== JOGO BATALHA NAVAL ===" << endl;

    while (acertos < NAVIOS) {
        cout << endl;
        mostrarTabuleiro(tabuleiro);

        cout << "\nInforme a linha: ";
        cin >> linha;
        cout << "Informe a coluna: ";
        cin >> coluna;

        // Validacao de limites
        if (linha < 0 || linha >= TAM || coluna < 0 || coluna >= TAM) {
            cout << "Posicao invalida! Tente novamente.\n";
            continue;
        }

        // Verifica se ja foi tentado
        if (tabuleiro[linha][coluna] != '~') {
            cout << "Voce ja tentou essa posicao!\n";
            continue;
        }

        tentativas++;

        // Verifica acerto ou erro
        if (navios[linha][coluna] == 1) {
            cout << "ACERTOU um navio!\n";
            tabuleiro[linha][coluna] = 'X';
            acertos++;
        } else {
            cout << "ERROU!\n";
            tabuleiro[linha][coluna] = 'O';
        }
    }

    cout << "\nParabens! Voce destruiu todos os navios!\n";
    cout << "Total de tentativas: " << tentativas << endl;

    return 0;
}

cout << "\nFim de jogo. Todos os navios foram destruidos com sucesso.\n";

