System.out.print("Ingrese ID a modificar: ");
                    String modificar = sc.nextLine();
                    int posMod = -1;

                    for (int i = 0; i < totalVentas; i++) {
                        if (ids[i].equals(modificar)) {
                            posMod = i;
                            break;
                        }
                    }

                    if (posMod == -1) {
                        System.out.println("ID no encontrado.");
                        continue;
                    }

                    System.out.print("Nuevo producto: ");
                    productos[posMod] = sc.nextLine();

                    System.out.print("Nueva cantidad: ");
                    try {
                        cantidades[posMod] = Integer.parseInt(sc.nextLine());
                    } catch (Exception e) {
                        System.out.println("Cantidad inválida.");
                        continue;
                    }

                    System.out.print("Nuevo precio: ");
                    try {
                        precios[posMod] = Double.parseDouble(sc.nextLine());
                    } catch (Exception e) {
                        System.out.println("Precio inválido.");
                        continue;
                    }

                    System.out.println("Venta modificada.");
                    break;

                case "5":
                    System.out.print("Ingrese ID a eliminar: ");
                    String eliminar = sc.nextLine();
                    int posDel = -1;

                    for (int i = 0; i < totalVentas; i++) {
                        if (ids[i].equals(eliminar)) {
                            posDel = i;
                            break;
                        }
                    }

                    if (posDel == -1) {
                        System.out.println("ID no encontrado.");
                        continue;
                    }

                    // Desplazar todo para eliminar
                    for (int i = posDel; i < totalVentas - 1; i++) {
                        ids[i] = ids[i + 1];
                        productos[i] = productos[i + 1];
                        cantidades[i] = cantidades[i + 1];
                        precios[i] = precios[i + 1];
                    }

                    totalVentas--;
                    System.out.println("Venta eliminada.");
                    break;

                case "6":
                    double total = 0;
                    for (int i = 0; i < totalVentas; i++) {
                        total += cantidades[i] * precios[i];
                    }
                    System.out.println("Ingreso total: $" + total);
                    break;

                case "7":
                    System.out.println("Saliendo del programa...");
                    return;

                default:
                    System.out.println("Opción inválida.");
                    break;
            }
        }
    }
}