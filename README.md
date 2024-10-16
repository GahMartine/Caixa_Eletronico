#include <stdio.h>

#define NUM_CEDULAS 7

/******************************************************************/
/* Aluno1: Gabriel Cesar Soares Martine - Número de matrícula: 8160085 */
/* Aluno2: Michel Douglas Cardoso - Número de matrícula: 8157129 */
/* Exercício-Programa 1 — Caixa Eletrônico */
/* Programação Avançada - 2024 - Professor: Bruno Perillo */
/* Compilador: GDB (DevC++ ou gcc) versão 1.0 */
/******************************************************************/

int main() {
    int cedulas[NUM_CEDULAS];
    int valores[NUM_CEDULAS] = {100, 50, 20, 10, 5, 2, 1};
    int totalCedulas = 0;

    printf("Digite a quantidade inicial de cédulas (100, 50, 20, 10, 5, 2, 1):\n");
    for (int i = 0; i < NUM_CEDULAS; i++) {
        scanf("%d", &cedulas[i]);
        totalCedulas += cedulas[i];
    }

    for (;;) { 
        int operacao;
        printf("Digite a operação (0: saque, 1: depósito, -1: encerrar): ");
        scanf("%d", &operacao);
        
        if (operacao == -1) {
            break;
        }

        if (operacao == 0) { 
            int valorSaque;
            printf("Digite o valor a ser sacado: R$ ");
            scanf("%d", &valorSaque);
            
            int cedulasUsadas[NUM_CEDULAS] = {0}; 
            for (int i = 0; i < NUM_CEDULAS; i++) {
                while (valorSaque >= valores[i] && cedulas[i] > 0) {
                    valorSaque -= valores[i];
                    cedulasUsadas[i]++;
                    cedulas[i]--; 
                }
            }
            
            if (valorSaque > 0) { 
                printf("Saque de R$ %d não realizado por falta de cédulas\n", valorSaque + (cedulasUsadas[0] * 100 + cedulasUsadas[1] * 50 + cedulasUsadas[2] * 20 + cedulasUsadas[3] * 10 + cedulasUsadas[4] * 5 + cedulasUsadas[5] * 2 + cedulasUsadas[6] * 1));
                
                for (int i = 0; i < NUM_CEDULAS; i++) {
                    cedulas[i] += cedulasUsadas[i]; 
                }
            } else {
                printf("Saque de R$ %d efetuado\n", (cedulasUsadas[0] * 100 + cedulasUsadas[1] * 50 + cedulasUsadas[2] * 20 + cedulasUsadas[3] * 10 + cedulasUsadas[4] * 5 + cedulasUsadas[5] * 2 + cedulasUsadas[6] * 1));
            }

        } else if (operacao == 1) { 
            printf("Digite a quantidade de cédulas para depósito (100, 50, 20, 10, 5, 2, 1):\n");
            int deposito[NUM_CEDULAS];
            for (int i = 0; i < NUM_CEDULAS; i++) {
                scanf("%d", &deposito[i]);
                cedulas[i] += deposito[i]; 
            }
        }

        totalCedulas = 0;
        for (int i = 0; i < NUM_CEDULAS; i++) {
            totalCedulas += cedulas[i];
        }

        printf("R$ 100 R$ 50 R$ 20 R$ 10 R$ 5 R$ 2 R$ 1 Total\n");
        printf("Quantidade de cédulas ");
        for (int i = 0; i < NUM_CEDULAS; i++) {
            printf("%d ", cedulas[i]);
        }
        printf("%d\n", totalCedulas);
    }

    return 0;
}
