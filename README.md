package com.mycompany.ingresos;


import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.util.Scanner;

public class Ingresos {

      public static void main(String[] args) {
        // Crear un objeto Scanner para leer la entrada del usuario
        Scanner scanner = new Scanner(System.in);
        int opcion;

        // Bucle do-while para mostrar el menú hasta que el usuario elija salir
        do {
            // Mostrar el menú de opciones
            System.out.println("\nMenú de Registro de Ingresos");
            System.out.println("1. Registrar Ingreso");
            System.out.println("2. Ver Registros");
            System.out.println("3. Salir");
            System.out.print("Seleccione una opción: ");

            // Leer la opción seleccionada por el usuario
            opcion = scanner.nextInt();
            scanner.nextLine(); // Consumir el salto de línea después de leer el entero

            // Switch para manejar la opción seleccionada
            switch (opcion) {
                case 1:
                    registrarIngreso(scanner); // Llamar al método para registrar un ingreso
                    break;
                case 2:
                    verRegistros(); // Llamar al método para ver los registros
                    break;
                case 3:
                    System.out.println("Saliendo del programa..."); // Mensaje de salida
                    break;
                default:
                    System.out.println("Opción no válida. Intente de nuevo."); // Mensaje para opción no válida
            }
        } while (opcion != 3); // Continuar hasta que el usuario elija salir

        // Cerrar el objeto Scanner
        scanner.close();
    }

    // Método para registrar un nuevo ingreso
    private static void registrarIngreso(Scanner scanner) {
        System.out.println("\nRegistro de Ingresos");
        System.out.println("Por favor, ingrese los datos del ingreso:");

        // Leer los datos del ingreso
        System.out.print("Correlativo del ingreso: ");
        String correlativo = scanner.nextLine();

        System.out.print("ID de la cuenta bancaria: ");
        String idCuenta = scanner.nextLine();

        System.out.print("Monto del ingreso: ");
        String monto = scanner.nextLine();

        System.out.print("Descripción del ingreso: ");
        String descripcion = scanner.nextLine();

        System.out.print("Fecha de registro del ingreso (dd/mm/yyyy): ");
        String fecha = scanner.nextLine();

        // Formatear los datos del ingreso en una línea de texto
        String registro = String.format("%s,%s,%s,%s,%s", correlativo, idCuenta, monto, descripcion, fecha);

        // Escribir el registro en el archivo "Ingresos.txt"
        try (BufferedWriter writer = new BufferedWriter(new FileWriter("Ingresos.txt", true))) {
            writer.write(registro);
            writer.newLine(); // Añadir una nueva línea para el siguiente registro
            System.out.println("Registro guardado exitosamente.");
        } catch (IOException e) {
            // Manejar errores al escribir en el archivo
            System.err.println("Error al escribir en el archivo: " + e.getMessage());
        }
    }

    // Método para ver los registros existentes
    private static void verRegistros() {
        System.out.println("\nRegistros de Ingresos:");

        // Leer y mostrar los registros del archivo "Ingresos.txt"
        try (BufferedReader reader = new BufferedReader(new FileReader("Ingresos.txt"))) {
            String linea;
            while ((linea = reader.readLine()) != null) {
                System.out.println(linea);
            }
        } catch (IOException e) {
            // Manejar errores al leer el archivo
            System.err.println("Error al leer el archivo: " + e.getMessage());
        }
    }
    
}

