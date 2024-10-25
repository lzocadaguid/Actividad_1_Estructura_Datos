import java.util.Scanner;

public class CensoFamiliar {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Preguntar la cantidad de familias
        System.out.print("Ingrese la cantidad de familias: ");
        int cantidadFamilias = scanner.nextInt();

        // Declarar arreglos para almacenar los valores de agua, luz, gas y estrato
        double[] agua = new double[cantidadFamilias];
        double[] luz = new double[cantidadFamilias];
        double[] gas = new double[cantidadFamilias];
        int[] estrato = new int[cantidadFamilias];

        // Ingresar los valores para cada familia
        for (int i = 0; i < cantidadFamilias; i++) {
            System.out.println("Familia " + (i + 1) + ":");
            System.out.print("Valor del agua: ");
            agua[i] = scanner.nextDouble();
            System.out.print("Valor de la luz: ");
            luz[i] = scanner.nextDouble();
            System.out.print("Valor del gas: ");
            gas[i] = scanner.nextDouble();
            System.out.print("Estrato: ");
            estrato[i] = scanner.nextInt();
        }

        // Calcular y mostrar el total a pagar con descuentos aplicados
        for (int i = 0; i < cantidadFamilias; i++) {
            double descuentoAgua = calcularDescuento(agua[i], estrato[i]);
            double descuentoLuz = calcularDescuento(luz[i], estrato[i]);
            double descuentoGas = calcularDescuento(gas[i], estrato[i]);

            double totalAgua = agua[i] - descuentoAgua;
            double totalLuz = luz[i] - descuentoLuz;
            double totalGas = gas[i] - descuentoGas;

            System.out.println("Familia " + (i + 1) + ":");
            System.out.println("Total a pagar por agua: " + totalAgua);
            System.out.println("Total a pagar por luz: " + totalLuz);
            System.out.println("Total a pagar por gas: " + totalGas);
        }

        scanner.close();
    }

    // Método para calcular el descuento según el estrato
    public static double calcularDescuento(double valor, int estrato) {
        double descuento = 0;
        if (estrato == 1) {
            descuento = valor * 0.20;
        } else if (estrato == 2) {
            descuento = valor * 0.15;
        } else if (estrato >= 3) {
            descuento = valor * 0.09;
        }
        return descuento;
    }
}
