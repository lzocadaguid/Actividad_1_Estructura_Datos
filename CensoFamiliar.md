import java.util.Scanner;

public class CalculoSubsidiosPublicos {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // inicamos generando la bienvenida al aplicativo         
        System.out.println("Buen Dia. Bienvenido al programa para calcular el subsidio de servicios publicos\n");
        
        // preguntamos la cantidad de familias 

        System.out.print("por favor ingrese la cantidad de familias: ");
        int numFamilias = scanner.nextInt();

        // Declarar para poder almacenar los valores de agua, luz, gas y estrato, en este caso lo dejaremos tipo double
        double[] agua = new double[numFamilias];
        double[] luz = new double[numFamilias];
        double[] gas = new double[numFamilias];
        int[] estrato = new int[numFamilias];

        // Ingresar los valores por cada una de las familias
        for (int i = 0; i < numFamilias; i++) {
            System.out.println("Familia " + (i + 1) + ":");
            System.out.print("Ingrese por favor el valor del agua: ");
            agua[i] = scanner.nextDouble();
            System.out.print("Ingrese por favor el valor de la luz: ");
            luz[i] = scanner.nextDouble();
            System.out.print("Ingrese por favor el Valor del gas: ");
            gas[i] = scanner.nextDouble();
            System.out.print("Ingrese por favor el estrato:");
            estrato[i] = scanner.nextInt();
        }

             System.out.println("Gracias\n");       
             
        // ahora vamos a calcular y mostrar el total a pagar con los descuentos aplicados
        for (int i = 0; i < numFamilias; i++) {
            double descuentoAgua = calcularDescuento(agua[i], estrato[i]);
            double descuentoLuz = calcularDescuento(luz[i], estrato[i]);
            double descuentoGas = calcularDescuento(gas[i], estrato[i]);

            double totalAgua = agua[i] - descuentoAgua;
            double totalLuz = luz[i] - descuentoLuz;
            double totalGas = gas[i] - descuentoGas;

            System.out.println("perfecto a continuacion encontrara los resultados del calculo:\n");           
            System.out.println("La Familia Numero " + (i + 1) + " Obtuvo:");
            System.out.println("Total a pagar por agua: " + totalAgua);
            System.out.println("Total a pagar por luz: " + totalLuz);
            System.out.println("Total a pagar por gas: " + totalGas);
                   }

         System.out.println("Muchas gracias, tenga usted un feliz dia");
         
        scanner.close();
    }

    
    
    // este es el metodo para calcular el descuento según el estrato ingresado
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
