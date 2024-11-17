      //Autor Luis MIguel Zocadagui Diaz

import java.util.*;

class Turno {
    String nombre;
    String cedula;
    String codigo;

    Turno(String nombre, String cedula, String codigo) {
        this.nombre = nombre;
        this.cedula = cedula;
        this.codigo = codigo;
    }

    @Override
    public String toString() {
        return "{" +
       //         "nombre='" + nombre + '\'' +
       //         ", cedula='" + cedula + '\'' +
                " '" + codigo + '\'' +
                '}';
    }
}

public class ControlDeTurnos {
    private static List<Turno> listaTurnos = new LinkedList<>();
    private static Queue<Turno> colaTurnos = new LinkedList<>();
    private static Stack<Turno> pilaTurnos = new Stack<>();
    private static int contadorTurnos = 0;
    private static final int MAX_TURNOS = 100;
    private static final String[] OPERARIOS = {"Ana Jimenez", "Alexander Diaz", "Carlos Rodriguez", "Marta Gonzalez", "Jorge Villamizar"};

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int opcion;

        //Bienvenida del menu al usuario
        
        do {
            System.out.println("BIENVENIDO a ServiUCompensar");           
            System.out.println("Menu de Control de Turnos, por favor seleccione la opcion deseada:");
            System.out.println("1. Solicitar nuevo turno");
            System.out.println("2. Asignar turno a operario de asesoria");
            System.out.println("3. Eliminar turno atendido");
            System.out.println("4. Salir");
            System.out.print("Seleccione por favor una opcion: ");
            System.out.println(""); 
            opcion = scanner.nextInt();
            scanner.nextLine(); 

            switch (opcion) {
                case 1:
                    solicitarNuevoTurno(scanner);
                    break;
                case 2:
                    asignarTurnoAOperario();
                    break;
                case 3:
                    eliminarTurnoAtendido();
                    break;
                case 4:
                    System.out.println("Muchas gracias por usar ServiUCompensar, espero que se haya solucionado su solicitud, Feliz Dia...");
                    break;
                default:
                    System.out.println("Opcion no valida, por favor Intente de nuevo.");
            }
        } while (opcion != 4);
    }

    //crear turno segun datos de usuario
    
    private static void solicitarNuevoTurno(Scanner scanner) {
    System.out.print("Perfecto, vamos a Crear su Nuevo Turno: ");
        System.out.print("Ingrese por favor su nombre: ");
        String nombre = scanner.nextLine();
        System.out.print("Ingrese por favor su numero de cedula: ");
        String cedula = scanner.nextLine();
        String codigo = generarCodigoTurno();
        Turno nuevoTurno = new Turno(nombre, cedula, codigo);
        listaTurnos.add(nuevoTurno);
        colaTurnos.add(nuevoTurno);
        pilaTurnos.push(nuevoTurno);
        System.out.println("Proceso Exitoso, su Turno es: "   + nuevoTurno);
        System.out.println("\n");     
        
    }

      // gernerar el codigo 
  
    
    private static String generarCodigoTurno() {
        contadorTurnos = (contadorTurnos % MAX_TURNOS) + 1;
        return String.format("T%03d", contadorTurnos);
    }

         // asignar el  el codigo a un agente
   
    
    private static void asignarTurnoAOperario() {
        if (colaTurnos.isEmpty()) {
            System.out.println("No hay turnos para asignar, intente nuevamente por favor. \n");
            return;
        }
        Turno turno = colaTurnos.poll();
        String operario = OPERARIOS[new Random().nextInt(OPERARIOS.length)];
        System.out.println("Su Turno " + turno.codigo + " se encuentra asignado a agente de asesoria: " + operario + "\n");
    }

          // eliminar el codigo 
  
    
    private static void eliminarTurnoAtendido() {
        if (pilaTurnos.isEmpty()) {
            System.out.println("No hay turnos para eliminar, intente nuevamente por favor. \n");
            return;
        }
        
        Turno turno = pilaTurnos.pop();
        listaTurnos.remove(turno);
        System.out.println("El Turno " + turno.codigo + " fue atendido y eliminado. \n");
        
   System.out.println("Muchas gracias por usar ServiUCompensar, espero que se haya solucionado su solicitud, Feliz Dia... \n");      
    }
}
