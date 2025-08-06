
Perfecto, Juan. Te hago una versión más sencilla y directa del programa, con lo que me pediste:

Solo uso Scanner, arreglos (String[][]) y tipos primitivos.

El menú es con **switch** dentro de un **while(true)**.

Se verifica:

Que no se repita el ID.

Que la entrada sea válida (cantidad y precio sean números).

Que el ID exista al buscar, modificar o eliminar.




---

✅ VENTAS: matriz ventas[100][4]

Cada fila representa una venta con:

1. ID


2. Producto


3. Cantidad


4. Precio unitario




---

✅ CÓDIGO EN JAVA (simple, directo, y bien organizado):

import java.util.Scanner;

public class VentasConVectores {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        String[][] ventas = new String[100][4]; // [ID, producto, cantidad, precio]
        int totalVentas = 0;

        while (true) {
            System.out.println("\n--- MENÚ ---");
            System.out.println("1. Crear venta");
            System.out.println("2. Listar ventas");
            System.out.println("3. Buscar por ID");
            System.out.println("4. Modificar venta");
            System.out.println("5. Eliminar venta");
            System.out.println("6. Calcular total");
            System.out.println("7. Salir");
            System.out.print("Elija opción: ");
            
            String opcion = sc.nextLine();

            switch (opcion) {
                case "1": // Crear venta
                    if (totalVentas >= ventas.length) {
                        System.out.println("No se pueden agregar más ventas.");
                        break;
                    }

                    System.out.print("Ingrese ID: ");
                    String id = sc.nextLine();

                    boolean repetido = false;
                    for (int i = 0; i < totalVentas; i++) {
                        if (ventas[i][0].equals(id)) {
                            repetido = true;
                            break;
                        }
                    }

                    if (repetido) {
                        System.out.println("Ese ID ya existe.");
                        break;
                    }

                    System.out.print("Producto: ");
                    String producto = sc.nextLine();

                    System.out.print("Cantidad: ");
                    String cantidad = sc.nextLine();
                    if (!esNumero(cantidad)) {
                        System.out.println("Cantidad inválida.");
                        break;
                    }

                    System.out.print("Precio unitario: ");
                    String precio = sc.nextLine();
                    if (!esDecimal(precio)) {
                        System.out.println("Precio inválido.");
                        break;
                    }

                    ventas[totalVentas][0] = id;
                    ventas[totalVentas][1] = producto;
                    ventas[totalVentas][2] = cantidad;
                    ventas[totalVentas][3] = precio;
                    totalVentas++;

                    System.out.println("Venta creada.");
                    break;

                case "2": // Listar
                    if (totalVentas == 0) {
                        System.out.println("No hay ventas.");
                    } else {
                        for (int i = 0; i < totalVentas; i++) {
                            System.out.println("ID: " + ventas[i][0] + ", Producto: " + ventas[i][1] +
                                    ", Cantidad: " + ventas[i][2] + ", Precio: " + ventas[i][3]);
                        }
                    }
                    break;

                case "3": // Buscar por ID
                    System.out.print("ID a buscar: ");
                    String buscar = sc.nextLine();
                    boolean encontrado = false;
                    for (int i = 0; i < totalVentas; i++) {
                        if (ventas[i][0].equals(buscar)) {
                            System.out.println("ID: " + ventas[i][0] + ", Producto: " + ventas[i][1] +
                                    ", Cantidad: " + ventas[i][2] + ", Precio: " + ventas[i][3]);
                            encontrado = true;
                            break;
                        }
                    }
                    if (!encontrado) System.out.println("No se encontró esa venta.");
                    break;

                case "4": // Modificar
                    System.out.print("ID a modificar: ");
                    String mod = sc.nextLine();
                    int posMod = -1;
                    for (int i = 0; i < totalVentas; i++) {
                        if (ventas[i][0].equals(mod)) {
                            posMod = i;
                            break;
                        }
                    }

                    if (posMod == -1) {
                        System.out.println("No se encontró ese ID.");
                        break;
                    }

                    System.out.print("Nuevo producto: ");
                    ventas[posMod][1] = sc.nextLine();

                    System.out.print("Nueva cantidad: ");
                    String nuevaCant = sc.nextLine();
                    if (!esNumero(nuevaCant)) {
                        System.out.println("Cantidad inválida.");
                        break;
                    }
                    ventas[posMod][2] = nuevaCant;

                    System.out.print("Nuevo precio: ");
                    String nuevoPrecio = sc.nextLine();
                    if (!esDecimal(nuevoPrecio)) {
                        System.out.println("Precio inválido.");
                        break;
                    }
                    ventas[posMod][3] = nuevoPrecio;

                    System.out.println("Venta modificada.");
                    break;

                case "5": // Eliminar
                    System.out.print("ID a eliminar: ");
                    String del = sc.nextLine();
                    int posDel = -1;
                    for (int i = 0; i < totalVentas; i++) {
                        if (ventas[i][0].equals(del)) {
                            posDel = i;
                            break;
                        }
                    }

                    if (posDel == -1) {
                        System.out.println("No se encontró esa venta.");
                        break;
                    }

                    // Mover hacia arriba para eliminar
                    for (int i = posDel; i < totalVentas - 1; i++) {
                        ventas[i] = ventas[i + 1];
                    }
                    totalVentas--;
                    System.out.println("Venta eliminada.");
                    break;

                case "6": // Calcular total
                    double total = 0;
                    for (int i = 0; i < totalVentas; i++) {
                        int cant = Integer.parseInt(ventas[i][2]);
                        double precioU = Double.parseDouble(ventas[i][3]);
                        total += cant * precioU;
                    }
                    System.out.println("Ingreso total: $" + total);
                    break;

                case "7":
                    System.out.println("Saliendo...");
                    return;

                default:
                    System.out.println("Opción inválida.");
                    break;
            }
        }
    }

    // Verifica si es número entero
    public static boolean esNumero(String texto) {
        try {
            Integer.parseInt(texto);
            return true;
        } catch (Exception e) {
            return false;
        }
    }

    // Verifica si es número decimal
    public static boolean esDecimal(String texto) {
        try {
            Double.parseDouble(texto);
            return true;
        } catch (Exception e) {
            return false;
        }
    }
}


---

✅ Este código:

Es simple, claro y solo con lo que estás viendo: Scanner, while, switch, arreglos, validación de entradas, etc.

Usa solo String[][] para representar las ventas.

Incluye funciones para validar si los datos son numéricos.



---

¿Te gustaría que te lo divida en partes o necesitas ayuda para pasarlo a JOptionPane en otra versión más adelante?

