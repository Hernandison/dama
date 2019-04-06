
#include <stdio.h>
#include <stdlib.h>

char tabuleiro[8][8];
char usuarioAtual; // 'P' ou 'B'
void moverj1();

void montar()
{
    for(int i=0; i<8; i++)
    {
        for(int j=0; j<8; j++)
        {
            if(i <= 2)
            {
                //PRETO
                //par - impar - par
                if(i == 0 && j % 2 == 0)
                {
                    tabuleiro[i][j] = 'P';
                }
                else if(i == 1 && j % 2 != 0)
                {
                    tabuleiro[i][j] = 'P';
                }
                else if(i == 2 && j % 2 == 0)
                {
                    tabuleiro[i][j] = 'P';
                }
                else
                {
                    tabuleiro[i][j] = '\xDB';
                }

            }
            else if(i >= 5 && i <= 7)
            {
                //BRANCO
                //impar - par - impar
                if(i == 5 && j % 2 != 0)
                {
                    tabuleiro[i][j] = 'B';
                }
                else if(i == 6 && j % 2 == 0)
                {
                    tabuleiro[i][j] = 'B';
                }
                else if(i == 7  && j % 2 != 0)
                {
                    tabuleiro[i][j] = 'B';
                }
                else
                {
                    tabuleiro[i][j] = '\xDB';
                }
            }
            if(i == 3 && j % 2 == 0)
            {
                //linhas vazias
                tabuleiro[i][j] = '\xDB';
            }
            else if(i == 4 && j % 2 != 0)
            {
                tabuleiro[i][j] = '\xDB';
            }
        }
    }
}

void mostrar()
{
    for(int i=0; i<8; i++)
    {
        for(int j=0; j<8; j++)
        {
            printf("%c", tabuleiro[i][j]);
        }
        printf("\n");
    }
}

int estarDentroTabuleiro(int linha, int coluna)
{
    return (linha >= 0 && linha <= 7) &&
           (coluna >= 0 && coluna <= 7);
}

int verificarDiagonal(int linhaO, int colunaO, int linhaD, int colunaD)
{
    if(usuarioAtual == 'P')
    {
        int diferencaLdLo = linhaD - linhaO; // Positiva
        int diferencaCdCo = colunaD - colunaO;
        if(diferencaLdLo > 0)
        {
            diferencaCdCo = abs(colunaD - colunaO);
            return diferencaLdLo == diferencaCdCo;
        }

        return 0;
    }
    else if(usuarioAtual == 'B')
    {

    }

}

int main()
{

    montar();
    mostrar();
    int linhaO;
    int colunaO;
    int linhaD;
    int colunaD;

    printf("Usuario-P Digite a linha e coluna da Peça\n");
    scanf("%i", &linhaO);
    scanf("%i", &colunaO);
    usuarioAtual = 'P';
    printf("Usuario-P Digite a linha e coluna do Destino\n");
    scanf("%i", &linhaD);
    scanf("%i", &colunaD);
    //3.0 - Veirificar se estar dentro do Tabuleiro
    if( estarDentroTabuleiro(linhaO, colunaO) &&
            estarDentroTabuleiro(linhaD, colunaD))
    {
        //3.1 - Vericar se é Diagonal
        if(verificarDiagonal(linhaO, colunaO, linhaD, colunaD))
        {
            printf("MOVIMENTAÇÃO VÁLIDA: %c", usuarioAtual);
            //3.2 Verificar a Origem

            /*  if(verificarOrigem(linhaO, colunaO)){
               //3.3 Verificar o movimento para o destino
               verificarDestino(linhaO, colunaO);
              } */


        }
        else
        {
            printf("MOVIMENTAÇÃO INVÁLIDA para o usuário: %c", usuarioAtual);
        }
    }
    else
    {
        // Fora do Tabuleiro
        printf("Posição fora do Tabuleiro !!!\n");
    }


    return 0;
}

