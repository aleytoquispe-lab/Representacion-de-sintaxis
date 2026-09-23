// Importa el framework UIKit con todos los elementos de la interfaz de usuario
import UIKit

// Define la clase del controlador de pantalla, heredando de UIViewController
class ViewController: UIViewController {

    // Conexión al campo de texto del capital ingresado por el usuario
    @IBOutlet weak var txtCapital: UITextField!
    // Conexión al campo de texto de la tasa de interés anual
    @IBOutlet weak var txtInteresAnual: UITextField!
    // Conexión al campo de texto del tiempo en años
    @IBOutlet weak var txtAnios: UITextField!

    // Conexión a la etiqueta donde se muestra la cuota mensual calculada
    @IBOutlet weak var lblCuotaMensual: UILabel!
    // Conexión a la etiqueta donde se muestra el monto total acumulado
    @IBOutlet weak var lblMontoTotal: UILabel!

    // Método de ciclo de vida que se ejecuta al cargar la pantalla en memoria
    override func viewDidLoad() {
        // Ejecuta la lógica por defecto de la clase base UIViewController
        super.viewDidLoad()
        // Establece el texto inicial por defecto de la cuota mensual
        lblCuotaMensual.text = "Cuota mensual: $0.00"
        // Establece el texto inicial por defecto del monto total
        lblMontoTotal.text = "Monto total: $0.00"
    }

    // Acción de la interfaz que se activa al presionar el botón de calcular
    @IBAction func calcularPrestamo(_ sender: Any) {
        // Convierte el texto de txtCapital a Double; si está vacío o es inválido, asigna 0
        let P = Double(txtCapital.text ?? "") ?? 0
        // Convierte el texto de txtInteresAnual a Double; si falla, asigna 0
        let tasaAnual = Double(txtInteresAnual.text ?? "") ?? 0
        // Convierte el texto de txtAnios a Double; si falla, asigna 0
        let anios = Double(txtAnios.text ?? "") ?? 0

        // Valida que todos los datos ingresados sean estrictamente mayores a 0
        if P <= 0 || tasaAnual <= 0 || anios <= 0 {
            // Muestra mensaje de alerta si algún dato es incorrecto o menor/igual a 0
            lblCuotaMensual.text = "Ingresa valores válidos mayores a 0"
            // Borra el texto de la etiqueta del monto total en caso de error
            lblMontoTotal.text = ""
            // Interrumpe y sale de la función para evitar hacer cálculos erróneos
            return
        }

        // 3. Calcular tasa mensual (r) y número total de pagos (n)
        // Convierte el porcentaje de interés anual a una tasa decimal mensual (r)
        let r = (tasaAnual / 100) / 12
        // Multiplica los años por 12 para obtener el total de meses/pagos (n)
        let n = anios * 12

        // 4. Aplicar fórmula de cuota mensual: M = P * [ r * (1+r)^n / ((1+r)^n - 1) ]
        // Eleva (1 + r) a la potencia n usando la función pow()
        let factor = pow(1 + r, n)
        // Aplica la fórmula de amortización para calcular el pago mensual (M)
        let M = P * ((r * factor) / (factor - 1))

        // 5. Calcular el monto total a pagar
        // Multiplica la cuota mensual por la cantidad total de meses
        let montoTotal = M * n

        // 6. Mostrar resultados formateados a 2 decimales
        // Formatea la cuota mensual a 2 decimales (%.2f) y la asigna a la etiqueta
        lblCuotaMensual.text = String(format: "Cuota mensual: $%.2f", M)
        // Formatea el monto total a 2 decimales (%.2f) y lo asigna a la etiqueta
        lblMontoTotal.text = String(format: "Monto total a pagar: $%.2f", montoTotal)
    }
}
