/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package roundrobin;

import java.util.Scanner;

/**
 *
 * @author ESPINOSA
 */
public class Roundrobin {

    /**
     * @param args the command line arguments
     */
    static Scanner teclado = new Scanner(System.in);

    public static void main(String[] args) {
        // TODO code application logic here

        String datos[] = new String[]{"a", "b", "c"};
        int tiempo[] = new int[datos.length];
        int numero = datos.length;

   
        RoundRobin(datos, tiempo, numero);

    }

    public static void insertar(String datos[], int tiempo[], int numero) {
        for (int i = 0; i < numero; i++) {
            System.out.print("inserte el tiempo en el proceso [" + datos[i] + "]:");
            tiempo[i] = teclado.nextInt();
        }
    }

    public static int quantum(int tiempo[], int numero) {
        int resultado = 0;
        for (int i = 0; i < numero; ++i) {
            resultado += tiempo[i];
        }
        resultado /= numero;
        return resultado;
    }

    public static void RoundRobin(String datos[], int tiempo[], int numero) {
        insertar(datos, tiempo, numero);
        int Quantum = quantum(tiempo, numero);
        System.out.println("El quantum es: " + Quantum);
        int tiempoFinal = 0;
        float sumatoria = 0.0f;
        int contador = 0;
        int i = 0;
        do {
            
            int Tiempo = tiempo[i] != 0 ? tiempo[i] -= Quantum : ++i;
            if (tiempo[i] > 0) {
                tiempoFinal += Quantum;
            } else {
                tiempoFinal += Quantum + tiempo[i];
                sumatoria += tiempoFinal;
                System.out.println("el tiempo de proceso de " + datos[i] + ": " + tiempoFinal);

               contador++;
            }
            if ( i< numero-1){ ++i;}
            
        } while (contador < numero);
        sumatoria /= numero;
        System.out.print("Tiempo promedio de los procesos es: " + sumatoria);
    }
}
