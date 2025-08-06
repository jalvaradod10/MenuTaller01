
import java.util.Scanner;

public class MenuVentas {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Vectores para guardar cada parte de una venta
        String[] ids = new String[100];
        String[] productos = new String[100];
        int[] cantidades = new int[100];
        double[] precios = new double[100];
        int totalVentas = 0;

        while (true) {
            System.out.println("\n--- MENÚ DE VENTAS ---");
            System.out.println("1. Crear venta");
            System.out.println("2. Listar ventas");
            System.out.println("3. Buscar venta por ID");
            System.out.println("4. Modificar venta");
            System.out.println("5. Eliminar venta");
            System.out.println("6. Calcular total");
            System.out.println("7. Salir");
            System.out.print("Elige una opción: ");
            String opcion = sc.nextLine();

            switch (opcion) {
                case "1": // Crear venta
                    if (totalVentas >= 100) {
                        System.out.println("No se pueden agregar más ventas.");
                        continue;
                    }

                    System.out.print("Ingrese ID: ");
                    String nuevoId = sc.nextLine();
                    boolean existe = false;
                    for (int i = 0; i < totalVentas; i++) {
                        if (ids[i].equals(nuevoId)) {
                            existe = true;
                            break;
                        }
                    }
                    if (existe) {
                        System.out.println("Ese ID ya existe.");
                        continue;
                    }

                    System.out.print("Ingrese nombre del producto: ");
                    String producto = sc.nextLine();

                    System.out.print("Ingrese cantidad: ");
                    String cantidadStr = sc.nextLine();
                    if (!esEntero(cantidadStr)) {
                        System.out.println("Cantidad inválida.");
                        continue;
                    }

                    System.out.print("Ingrese precio unitario: ");
                    String precioStr = sc.nextLine();
                    if (!esDecimal(precioStr)) {
                        System.out.println("Precio inválido.");
                        continue;
                    }

                    // Guardar en vectores
                    ids[totalVentas] = nuevoId;
                    productos[totalVentas] = producto;
                    cantidades[totalVentas] = Integer.parseInt(cantidadStr);
                    precios[totalVentas] = Double.parseDouble(precioStr);
                    totalVentas++;

                    System.out.println("Venta guardada con éxito.");
                    break;

                case "2": // Listar ventas
                    if (totalVentas == 0) {
                        System.out.println("No hay ventas registradas.");
                        break;
                    }
                    System.out.println("Ventas registradas:");
                    for (int i = 0; i < totalVentas; i++) {
                        System.out.println("ID: " + ids[i] + ", Producto: " + productos[i] +
                                ", Cantidad: " + cantidades[i] +
                                ", Precio: " + precios[i]);
                    }
                    break;

                case "3": // Buscar venta
                    System.out.print("Ingrese el ID a buscar: ");
                    String buscarId = sc.nextLine();
                    boolean encontrado = false;
                    for (int i = 0; i < totalVentas; i++) {
                        if (ids[i].equals(buscarId)) {
                            System.out.println("Venta encontrada:");
                            System.out.println("Producto: " + productos[i] +
                                    ", Cantidad: " + cantidades[i] +
                                    ", Precio: " + precios[i]);
                            encontrado = true;
                            break;
                        }
                    }
                    if (!encontrado) {
                        System.out.println("No se encontró ese ID.");
                    }
                    break;

                case "4": // Modificar venta
                    System.out.print("Ingrese el ID a modificar: ");
                    String idMod = sc.nextLine();
                    int pos = -1;
                    for (int i = 0; i < totalVentas; i++) {
                        if (ids[i].equals(idMod)) {
                            pos = i;
                            break;
                        }
                    }
                    if (pos == -1) {
                        System.out.println("ID no encontrado.");
                        continue;
                    }

                    System.out.print("Nuevo producto: ");
                    productos[pos] = sc.nextLine();

                    System.out.print("Nueva cantidad: ");
                    String nuevaCantidad = sc.nextLine();
                    if (!esEntero(nuevaCantidad)) {
                        System.out.println("Cantidad inválida.");
                        continue;
                    }

                    System.out.print("Nuevo precio: ");
                    String nuevoPrecio = sc.nextLine();
                    if (!esDecimal(nuevoPrecio)) {
                        System.out.println("Precio inválido.");
                        continue;
                    }

                    cantidades[pos] = Integer.parseInt(nuevaCantidad);
                    precios[pos] = Double.parseDouble(nuevoPrecio);
                    System.out.println("Venta modificada.");
                    break;

                case "5": // Eliminar venta
                    System.out.print("Ingrese el ID a eliminar: ");
                    String idEliminar = sc.nextLine();
                    int posEliminar = -1;
                    for (int i = 0; i < totalVentas; i++) {
                        if (ids[i].equals(idEliminar)) {
                            posEliminar = i;
                            break;
                        }
                    }
                    if (posEliminar == -1) {
                        System.out.println("ID no encontrado.");
                        continue;
                    }

                    for (int i = posEliminar; i < totalVentas - 1; i++) {
                        ids[i] = ids[i + 1];
                        productos[i] = productos[i + 1];
                        cantidades[i] = cantidades[i + 1];
                        precios[i] = precios[i + 1];
                    }
                    totalVentas--;
                    System.out.println("Venta eliminada.");
                    break;

                case "6": // Calcular total
                    double total = 0;
                    for (int i = 0; i < totalVentas; i++) {
                        total += cantidades[i] * precios[i];
                    }
                    System.out.println("Total de ingresos: $" + total);
                    break;

                case "7": // Salir
                    System.out.println("Saliendo...");
                    return;

                default:
                    System.out.println("Opción inválida.");
                    break;
            }
        }
    }

    // Validar si es entero
    public static boolean esEntero(String s) {
        for (int i = 0; i < s.length(); i++) {
            if (!Character.isDigit(s.charAt(i))) return false;
        }
        return !s.isEmpty();
    }

    // Validar si es decimal
    public static boolean esDecimal(String s) {
        boolean punto = false;
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (c == '.') {
                if (punto) return false;
                punto = true;
            } else if (!Character.isDigit(c)) {
                return false;
            }
        }
        return !s.isEmpty();
    }
}