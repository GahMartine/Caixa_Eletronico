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
    int cedulas[NUM_CEDULAS]; //qntd de cada cedula disponivel
    int valores[NUM_CEDULAS] = {100, 50, 20, 10, 5, 2, 1}; //valores das eedulas
    int totalCedulas = 0; //total de cedulas disponivel

    //solicita quantidade de cedula
    printf("Digite a quantidade inicial de cedulas:\n");
    printf("Formato: R$100,00 | R$50,00\nR$20,00 | R$10,00\nR$5,00 | R$2,00 | R$1,00\n");
    for (int i = 0; i < NUM_CEDULAS; i++) {
        scanf("%d", &cedulas[i]);
        totalCedulas += cedulas[i]; //atualiza o total de cedulas
    }

    for (;;) {
        int operação;
        printf("\nEscolha uma operação:\n0: Saque\n1: Depósito\n2: Encerrar\n");
        scanf("%d", &operação);
        
        if (operação == -1) {
            printf("Operação concluida!\n");
            break; //encerra
        }

        if (operação == 0) { //saque
            int valorSaque;
            printf("Digite o valor para o saque: R$ ");
            scanf("%d", &valorSaque);
            
            int cedulasUsadas[NUM_CEDULAS] = {0}; //cedulas que foram utilizadas no saque
            for (int i = 0; i < NUM_CEDULAS; i++) {
                while (valorSaque >= valores[i] && cedulas[i] > 0) {
                    valorSaque -= valores[i]; //diminui o valor da cedula
                    cedulasUsadas[i]++; //conta a cedula utilizada
                    cedulas[i]--; //remove a cedula do caixa
                }
            }
            
            //verifica o saque
            if (valorSaque > 0) {
                printf("Saque de R$ %d não efetuado por falta de cedulas.\n", valorSaque);
                //reverte
                for (int i = 0; i < NUM_CEDULAS; i++) {
                    cedulas[i] += cedulasUsadas[i]; //adiciona as cedulas de volta
                }
            } else {
                int totalSacado = 0;
                for (int i = 0; i < NUM_CEDULAS; i++) {
                    totalSacado += cedulasUsadas[i] * valores[i]; //calcula o totol sacado
                }
                printf("Saque de R$ %d efetuado com sucesso.\n", totalSacado);
            }

        } else if (operação == 1) { //deposito
            printf("Digite a quantidade de cedulas para deposito:\n");
            printf("Formato: R$100,00 | R$50,00\nR$20,00 | R$10,00\nR$5,00 | R$2,00 | R$1,00\n");
            int deposito[NUM_CEDULAS];
            for (int i = 0; i < NUM_CEDULAS; i++) {
                scanf("%d", &deposito[i]);
                cedulas[i] += deposito[i]; //adiciona as cedulas depositadas ao caixa
            }
            printf("Deposito realizado com sucesso.\n");
        }

        //atualiza o total de cedulas
        totalCedulas = 0;
        for (int i = 0; i < NUM_CEDULAS; i++) {
            totalCedulas += cedulas[i]; //calcua o total de cedula
        }

        //exibe a quantidade atual de cedulas
        printf("\nR$100,00 | R$50,00\n R$20,00 | R$10,00\n R$5,00 | R$2,00 | R$1,00 Total\n");
        printf("Quantidade de cedulas: \n");
        for (int i = 0; i < NUM_CEDULAS; i++) {
            printf("%d ", cedulas[i]);
        }
        printf("Total de cedulas: %d\n", totalCedulas);
    }

    return 0;
}
