#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

int main() {
    cout << "¡Bienvenido al juego Mastermind!\n";
    cout << "Intenta adivinar la combinacion secreta de cuatro numeros.\n\n";

    int clave[4];
    bool adivinadas[4] = { false, false, false, false };

    cout << "¿Desea crear una combinacion aleatoria? (S para si/N para no): ";
    char opcion;
    cin >> opcion;

    if (opcion == 'S' || opcion == 's') {
        srand(time(0));
        cout << "\nSe ha creado una combinacion aleatoria.\n";
        for (int i = 0; i < 4; i++) {
            clave[i] = rand() % 10;
        }
    }
    else {
        cout << "\nIngrese la combinacion secreta de cuatro numeros: ";
        int combinacion;
        cin >> combinacion;
        for (int i = 3; i >= 0; i--) {
            clave[i] = combinacion % 10;
            combinacion /= 10;
        }
    }

    cout << "\n¡Comencemos el juego!\n";
    cout << "Tienes 10 intentos para adivinar la combinacion secreta.\n";
    cout << "Despues de cada intento, te daremos pistas sobre tu jugada.\n";

    cout << "\nCombinacion:\n";
    cout << "-----------------\n";
    for (int i = 0; i < 4; i++) {
        cout << "| " << "_ ";
    }
    cout << "|\n";
    cout << "-----------------\n";

    int jugadas[4];

    bool adivinoTodo = false;

    for (int intento = 1; intento <= 10; intento++) {
        cout << "\nIntento #" << intento << "\n";

        cout << "Ingresa tu jugada de cuatro numeros: ";
        int jugada;
        cin >> jugada;
        for (int i = 3; i >= 0; i--) {
            jugadas[i] = jugada % 10;
            jugada /= 10;
        }

        for (int i = 0; i < 4; i++) {
            if (jugadas[i] == clave[i]) {
                adivinadas[i] = true;
            }
        }

        cout << "\nCombinacion:\n";
        cout << "-----------------\n";
        for (int i = 0; i < 4; i++) {
            cout << "| ";
            if (adivinadas[i]) {
                cout << clave[i] << " ";
            }
            else if (find(clave, clave + 4, jugadas[i]) != clave + 4) {
                cout << "X ";
            }
            else {
                cout << "_ ";
            }
        }
        cout << "|\n";
        cout << "-----------------\n";

        adivinoTodo = true;
        for (int i = 0; i < 4; i++) {
            if (!adivinadas[i]) {
                adivinoTodo = false;
                break;
            }
        }

        if (adivinoTodo) {
            cout << "\n¡Felicitaciones! ¡Has adivinado la combinacion secreta en " << intento << " intentos!\n";
            break;
        }
    }

    if (!adivinoTodo) {
        cout << "\nLo siento, no has adivinado la combinación secreta.\n";
    }

    cout << "Gracias por jugar. ¡Hasta la próxima!\n";

    return 0;
}

