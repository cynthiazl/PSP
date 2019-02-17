***2º ejercicio para la evaluación***
****Consiste en extraer información de una web a elección del alumno, utilizando la técnica scrapping****

+ Código de la clase
```java
package sample;

import javafx.event.ActionEvent;
import javafx.fxml.FXML;
import javafx.scene.control.Label;
import org.jsoup.Connection;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;
import javafx.scene.control.TextArea;

import java.awt.*;
import java.lang.reflect.Array;

public class Controller {

    @FXML
    private TextArea mostrarResultados;

    @FXML
    private Label myTitle;

    @FXML
    void searchText(ActionEvent event) throws Exception {

        System.out.println("Holi");
        myTitle.setText("Esta información ha sido escrapeada de la web PcComponentes:");

        //Ofertas del día en Amazon
        Document doc = (Document) Jsoup.connect("https://www.pccomponentes.com/ofertas-especiales").get();

        //Los titulos
        String title = doc.title();

        //Array
        Elements contenedoresArticulos = doc.select("#articleListContent article");

        String resultado = "";

        for (Element contenedorArticulo : contenedoresArticulos){

            String nombreArticulo = contenedorArticulo.select("h3").text();
            String urlArticulo = "https://www.pccomponentes.com" + contenedorArticulo.select(".btn.btn-block.btn-primary").attr("href");
            String precioActual = contenedorArticulo.select(".tarjeta-articulo__precio-actual").text();
            String precioAnterior = contenedorArticulo.select(".tarjeta-articulo__pvp").text();
            String porcentajeDescuento = contenedorArticulo.select(".tarjeta-articulo__descuento").text();
            String estrellitas = contenedorArticulo.select(".rating-holder").text();


            resultado += nombreArticulo + "\n" + urlArticulo + "\n" + precioActual + "\n" + precioAnterior + "\n" +
                    porcentajeDescuento + "\n" + estrellitas + "\n" + "==================\n";



            System.out.println("ARTICULO EN OFERTA: " + nombreArticulo + "/n");

            System.out.println("Aqui tienes el link: " +urlArticulo);
            System.out.println("Precio actual del articulo: " + precioActual);
            System.out.println("Precio antiguo: " + precioAnterior);

            System.out.println("Porcentaje de descuento en el artículo: " + porcentajeDescuento);
            System.out.println("Estrellas: " +estrellitas);
            System.out.println("========================= ");
        }
        mostrarResultados.setText(resultado);
    }
}
```
____

***Imgaen de la interfaz con la información***

<img src="https://github.com/cynthiazl/PSP/blob/master/scrapping.png" width="350"/>

