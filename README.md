# Desafio-3-DIO.me
//Desenvolver uma calculadora no padrão “programador”, onde operações binárias, decimais, hexadecimais são realizadas.
#include <stdio.h>
#include <stdlib.h>

long long converterParaDecimal(char numero[], int base) {
    long long decimal = 0;
    int i = 0;
    int valor;

    while (numero[i] != '\0') {
        if (numero[i] >= '0' && numero[i] <= '9') {
            valor = numero[i] - '0';
        } else if (numero[i] >= 'A' && numero[i] <= 'F') {
            valor = numero[i] - 'A' + 10;
        } else if (numero[i] >= 'a' && numero[i] <= 'f') {
            valor = numero[i] - 'a' + 10;
        }

        decimal = decimal * base + valor;
        i++;
    }

    return decimal;
}

void converterParaOutraBase(long long decimal, int base) {
    char resultado[50];
    int indice = 0;

    while (decimal > 0) {
        int resto = decimal % base;
        resultado[indice++] = (resto < 10) ? resto + '0' : resto + 'A' - 10;
        decimal /= base;
    }

    for (int i = indice - 1; i >= 0; i--) {
        printf("%c", resultado[i]);
    }
    printf("\n");
}

int main() {
    char operador;
    char num1[50], num2[50];
    int base;
    long long decimal1, decimal2, resultadoDecimal;

    printf("Escolha a base para os números (2, 10, 16): ");
    scanf("%d", &base);

    printf("Digite um operador (+, -, *, /): ");
    scanf(" %c", &operador);

    printf("Digite dois operandos: ");
    scanf("%s %s", num1, num2);

    decimal1 = converterParaDecimal(num1, base);
    decimal2 = converterParaDecimal(num2, base);

    switch (operador) {
        case '+':
            resultadoDecimal = decimal1 + decimal2;
            printf("Resultado: ");
            converterParaOutraBase(resultadoDecimal, base);
            break;
        case '-':
            resultadoDecimal = decimal1 - decimal2;
            printf("Resultado: ");
            converterParaOutraBase(resultadoDecimal, base);
            break;
        case '*':
            resultadoDecimal = decimal1 * decimal2;
            printf("Resultado: ");
            converterParaOutraBase(resultadoDecimal, base);
            break;
        case '/':
            if (decimal2 != 0) {
                resultadoDecimal = decimal1 / decimal2;
                printf("Resultado: ");
                converterParaOutraBase(resultadoDecimal, base);
            } else {
                printf("Erro! Divisão por zero não é permitida.\n");
            }
            break;
        default:
            printf("Operador inválido.\n");
    }

    return 0;
}
