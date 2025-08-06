Scanner sc = new Scanner(System.in);

        String[] ids = new String[100];
        String[] productos = new String[100];
        int[] cantidades = new int[100];
        double[] precios = new double[100];
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
                case "1":
                    if (totalVentas >= 100) {
                        System.out.println("No se pueden agregar más ventas.");
                        continue;
                    }

                    System.out.print("Ingrese ID: ");
                    String id = sc.nextLine();

                    // Verificar que no se repita
                    boolean repetido = false;
                    for (int i = 0; i < totalVentas; i++) {
                        if (ids[i].equals(id)) {
                            repetido = true;
                            break;
                        }
                    }

                    if (repetido) {
                        System.out.println("Ese ID ya existe.");
                        continue;
                    }

                    System.out.print("Producto: ");
                    String producto = sc.nextLine();

                    System.out.print("Cantidad: ");
                    int cantidad;
                    try {
                        cantidad = Integer.parseInt(sc.nextLine());
                    } catch (Exception e) {
                        System.out.println("Cantidad inválida.");
                        continue;
                    }

                    System.out.print("Precio unitario: ");
                    double precio;
                    try {
                        precio = Double.parseDouble(sc.nextLine());
                    } catch (Exception e) {
                        System.out.println("Precio inválido.");
                        continue;
                    }

                    ids[totalVentas] = id;
                    productos[totalVentas] = producto;
                    cantidades[totalVentas] = cantidad;
                    precios[totalVentas] = precio;
                    totalVentas++;

                    System.out.println("Venta registrada.");
                    break;

                case "2":
                    if (totalVentas == 0) {
                        System.out.println("No hay ventas registradas.");
                    } else {
                        for (int i = 0; i < totalVentas; i++) {
                            System.out.println("ID: " + ids[i] +
                                    ", Producto: " + productos[i] +
                                    ", Cantidad: " + cantidades[i] +
                                    ", Precio: " + precios[i]);
                        }
                    }
                    break;

                case "3":
                    System.out.print("Ingrese ID a buscar: ");
                    String buscar = sc.nextLine();
                    boolean encontrado = false;
                    for (int i = 0; i < totalVentas; i++) {
                        if (ids[i].equals(buscar)) {
                            System.out.println("ID: " + ids[i] +
                                    ", Producto: " + productos[i] +
                                    ", Cantidad: " + cantidades[i] +
                                    ", Precio: " + precios[i]);
                            encontrado = true;
                            break;
                        }
                    }

                    if (!encontrado) {
                        System.out.println("Venta no encontrada.");
                    }
                    break;