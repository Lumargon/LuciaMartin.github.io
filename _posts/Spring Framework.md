##Spring Framework ¿Qué es y para qué sirve?

Java, es un lenguaje de programación orientado a objetos (POO), que es usado por miles de millones de dispositivos, desde computadoras hasta parquímetros, pero hoy en día, uno de sus mayores usos es para el creciente mundo de la web, y esto se debe a que es una herramienta de uso diario en el area del desarrollo web.

Con el exponencial aumento de la complejidad en todos los sistemas web, tanto gráficamente, como en temas de seguridad, la comunidad programadora se ha visto obligada a diseñar “ayudas” para no tener que repetir código y reducir en tiempo y espacio el desarrollo de estas aplicaciones, así como por ejemplo, en la electrónica cada vez dispositivos más pequeños son más potentes, en la programación se busca lo mismo cada día.

Spring es un framework del lenguaje de programacion java, y un framework en programación es el resultado de la evolucion de la ingenieria del software, estos son creados por programadores para programadores, con la finalidad de estandarizar el trabajo, resolver, agilizar y manejar los problemas y complejidades que van apareciendo en el mundo de la programación, a medida las exigencias van creciendo.

Spring nos permite desarrollar aplicaciones de manera más rápida, eficaz y corta, saltándonos tareas repetitivas y ahorrándonos lineas de código.

##Inversion de Control (IOC) e Inyección de dependencia (DI) en Spring


Inversión de control es un término que siempre ha generado bastante confusión en la comunidad. Pero lo que hay que saber es que es una expresión que se usa para referirse al cambio en el flujo de ejecución y vida de los objetos con respecto a la programación tradicional, básicamente de lo que se trata es de invertir la forma en que se controla la aplicación, lo qué antes dependía del programador, como por ejemplo, el orden en que se llaman los métodos para darle un comportamiento particular a la aplicación, ahora depende completamente de otro ente, en este caso, el framework, todo esto con la finalidad de crear aplicaciones más complejas y con funcionamientos más encapsulados y automáticos.


La inyección de dependencia, es un tipo de inversion de control, donde el manejo de las propiedades de un objeto son inyectadas a través de un constructor, un setter, un servicio, etc. Creando de esta manera un control diferente para un comportamiento más conveniente en nuestra aplicación, como se mencionó anteriormente.

abiendo esto, una de las caracteristicas principales de spring framework es el Spring container. El Spring Container es un IoC Container (Contenedor de Inversion de control, por sus siglas en inglés), estos son frameworks o partes de un framework, en este caso, que se encargan de realizar inyección de dependencia sin la necesidad de realizar la definición en java (o el lenguaje de POO que estemos utilizando) a través de archivos de metadata, por ejemplo un xml.


Este IOC container se encargará de crear los objetos, relacionarlos, configurarlos y manejar su ciclo de vida completo, desde la creación de estos hasta su destrucción, es por esto que se usa el término Inversion of control en spring, porque como dijimos anteriormente, el Spring container será el que controle una gran parte de la creación de los objetos y de la inyección de dependencia en estos.


##Un ejemplo breve

Vamos a mostrar un ejemplo muy breve de como funciona el Spring container. Imaginemos que tenemos un proyecto llamado Universidad, en el cual vamos a tener una clase Estudiante.java



package com.universidad
 
public class EstudianteBean{
   private String nombre; 
   private String apellido; 
   private String dni; 
 
   public String getNombre(){ 
   return nombre;
   } 
 
   public void setNombre(String nombre){ 
   this.nombre = nombre;
   } 
 
   public String getApellido(){
   return apellido; 
   } 
 
   public void setApellido(String apellido){
   this.apellido = apellido;
   } 
 
   public String getDni(){
   return dni; 
   }
 
  public void setDni(String dni){
  this.dni = dni; 
  } 
 
  public void mostrarEstudianteActual(){
  System.out.println(nombre+" "+apellido+", es el estudiante actual");
  }
 
}




Nuestro proyecto Universidad utiliza Spring framework, por lo tanto, en la configuración de este se debería encontrar un archivo xml que se encargará del control de ciertos objetos (Spring IOC Container). Este archivo, que ahora llamaremos springconfig.xml debería lucir de esta manera




<!DOCTYPE beans PUBLIC "-//PRING//DTD// BEAN 2.0//ES" 
"http://www.springframework.org/dtd/spring-beans-2.0.dtd">
<beans>
 <bean id="estudiante" class="com.universidad.EstudianteBean">
 <property name="nombre" value="Juan">
 <property name="apellido" value="Perez">
 <property name="dni" value="95.445.123">
 </bean>
</beans>




Si miramos detalladamente se puede notar que la etiqueta “bean” dentro de este xml hace referencia a mi clase EstudianteBean.java, el parametro “class” apunta a su dirección en mi proyecto y con el “id” le doy un nombre para poder identificarlo.

La etiqueta “property” apunta a las variables de mi clase y con “value” puedo introducirles un valor directamente. El Spring Container puede acceder y modificar objetos de la mi clase EstudianteBean a través de sus metodos get y set.

Spring nos permite, a través de estos archivos de configuración en XML, crear una especie de catálogo para cada uno de los beans que tengamos y así poder llamarlos y manipularlos cuando queramos desde otras clases sin necesidad de instanciarlos una y otra vez.


Algo que a simple vista pudiera verse un poco tedioso y complejo, pero cuando se trata de enormes aplicaciones con cientos y cientos de clases estos frameworks son lo que ha permitido al mundo del desarrollo de software crecer y evolucionar.



##¿Cuándo Spring empieza a controlar?

Ahora se procede a mostrar como implementa Spring, su control sobre los objetos en mi proyecto Universidad de la siguiente manera;



package com.universidad 
 
import org.springframework.beans.factory.BeanFactory;
import org.springframework.beans.factory.xml.XmlBeanFactory;
import org.springframework.core.io.ClassPathResource;
import org.springframework.core.io.Resource;
 
public class UniversidadLogic{ 
   
  public static void main(String[] args){
      Resource recurso = new ClassPathResource("springconfig.xml");
      BeanFactory factory = new XmlBeanFactory(recurso);
 
      EstudianteBean estudianteBean = (EstudianteBean)factory.getBean("estudiante");
       
      estudianteBean.mostrarEstudianteActual();
   }
}





