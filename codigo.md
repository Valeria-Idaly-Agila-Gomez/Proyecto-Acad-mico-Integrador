#include <stdio.h>
#include <stdlib.h>
float iva = 0.15;
// ===== PROTOTIPOS =====
void mostrarCatalogo();
void seleccionarProducto(int *producto, int *cantidad);
float obtenerPrecio(int producto);
float calcularSubtotal(int producto, int cantidad);
float calcularIVA(float subtotal);
float aplicarDescuento(float subtotal, int cantidad);
float calcularTotal(float subtotal, float iva, float descuento);
void generarFactura(float subtotal, float iva, float descuento, float total);
void gestionarPago(float total);

// ===== FUNCIONES =====

void mostrarCatalogo() {
    printf("\n===== CATALOGO DE ROPA =====\n");
    printf("1. Blusa ............. $10.00\n");
    printf("2. Pantalon .......... $20.00\n");
    printf("3. Medias ............ $2.50\n");
    printf("4. Chompa ............ $15.00\n");
    printf("5. Chaqueta .......... $18.00\n");
    printf("6. Short ............. $7.00\n");
    printf("7. Zapatos ........... $35.00\n");
    printf("8. Camisas ........... $15.00\n");
    printf("9. Camisetas ......... $8.00\n");
    printf("10. Pantalonetas ..... $9.00\n");
    printf("11. Calentadores ..... $15.00\n");
    printf("12. Faldas ........... $8.00\n");
}

void seleccionarProducto(int *producto, int *cantidad) {
    do {
        printf("\nSeleccione el producto (1-12): ");
        scanf("%d", producto);
    } while (*producto < 1 || *producto > 12);

    printf("Ingrese la cantidad: ");
    scanf("%d", cantidad);
}

float obtenerPrecio(int producto) {
    float precios[] = {
        10.00, 20.00, 2.50, 15.00, 18.00, 7.00,
        35.00, 15.00, 8.00, 9.00, 15.00, 8.00
    };
    return precios[producto - 1];
}

float calcularSubtotal(int producto, int cantidad) {
    return obtenerPrecio(producto) * cantidad;
}

float calcularIVA(float subtotal) {
    return subtotal * iva;   
}

float aplicarDescuento(float subtotal, int cantidad) {
    if (cantidad >= 10) {
        return subtotal * 0.10;
    }
    return 0;
}

float calcularTotal(float subtotal, float iva, float descuento) {
    return subtotal + iva - descuento;
}

void generarFactura(float subtotal, float iva, float descuento, float total) {
    printf("\n===== FACTURA =====\n");
    printf("Subtotal:      $%.2f\n", subtotal);
    printf("IVA (15%%):     $%.2f\n", iva);
    printf("Descuento:     $%.2f\n", descuento);
    printf("Total a pagar: $%.2f\n", total);
}

void gestionarPago(float total) {
    float pago;
    printf("\nIngrese el valor de pago: ");
    scanf("%f", &pago);

    if (pago > total) {
        printf("Vuelto: $%.2f\n", pago - total);
    } else if (pago == total) {
        printf("Pago exacto.\n");
    } else {
        printf("Faltan: $%.2f\n", total - pago);
    }
}

// ===== MAIN =====

int main() {
    int producto, cantidad;
    float subtotal, iva, descuento, total;
    char continuar;

    do {
        mostrarCatalogo();
        seleccionarProducto(&producto, &cantidad);

        subtotal = calcularSubtotal(producto, cantidad);
        iva = calcularIVA(subtotal);
        descuento = aplicarDescuento(subtotal, cantidad);
        total = calcularTotal(subtotal, iva, descuento);

        generarFactura(subtotal, iva, descuento, total);
        gestionarPago(total);

        printf("\nDesea realizar otra compra? (s/n): ");
        scanf(" %c", &continuar);

    } while (continuar == 's' || continuar == 'S');

    printf("\nSistema finalizado. Gracias por su compra.\n");
    return 0;
}
