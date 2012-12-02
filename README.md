DSL-Redaccion de Cuestionarios
===============================


Práctica de Laboratorio #12 (Virtual): DSL: Redacción de Cuestionarios I (Sin Contexto)


 Esta práctica es virtual. 
Use los recursos disponibles en la nube (google+ chat y hangouts, foros y mensajes de moodle, mail, github, etc) para consultar cualquier duda.

 
Encontrará la versión mas actualizada de la descripción de esta práctica en los apuntes de la asignatura en la sección:


Práctica: DSL: Redacción de Cuestionarios I (Sin Contexto)
 
del capítulo 



Reflexión y Metaprogramación
 Observe que el enlace a la práctica puede quedar obsoleto ya que los apuntes están en permanente construcción.
 


Práctica: DSL: Redacción de Cuestionarios I (Sin Contexto) 
Se trata de escribir un programa que redacte cuestionarios. En principio, sólo soportaremos preguntas del tipo selección múltiple:
 
1. ¿En que año Cristobal Colón descubrió América?
1 - 1942
2 - 1492
3 - 1808
4 - 1914
Su respuesta:
 Debe definir una clase Quiz que soporte un pequeño lenguaje en el que las preguntas puedan ser especificadas. El constructor de Quiz va seguido de un bloque al que pasa como argumento el objeto e que representa al examen:
 
quiz = Quiz.new("Cuestionario de PFS 10/12/2011") do |e|
  e.question '¿En que año Cristobal Colón descubrió América?',
    e.wrong =>'1942',
    e.right =>'1492',
    e.wrong =>'1808',
    e.wrong =>'1914'
  
  a = rand(10)
  b = rand(10)
  e.question "#{a}+#{b} = ",
    e.wrong =>"44",
    e.wrong =>"#{a + b + 2}",
    e.right =>"#{a + b}",
    e.wrong =>"#{a + b - 2}"
end

puts quiz
puts "************************"
quiz.run
 El programa anterior podría producir una salida parecida a esta: 

MacBookdeCasiano:chapter8ReflectionandMetaprogramming casiano$ ruby Quiz.rb 
Cuestionario de PFS 10/12/2011

¿En que año Cristobal Colón descubrió América?

  1 -  1942
  2 -  1492
  3 -  1808
  4 -  1914


0+8 = 

  1 -  44
  2 -  10
  3 -  8
  4 -  6


************************
Cuestionario de PFS 10/12/2011

¿En que año Cristobal Colón descubrió América?

  1 -  1942
  2 -  1492
  3 -  1808
  4 -  1914

Su respuesta: 3
0+8 = 

  1 -  44
  2 -  10
  3 -  8
  4 -  6

Su respuesta: 1
0 respuestas correctas de un total de 2.
MacBookdeCasiano:chapter8ReflectionandMetaprogramming casiano$


 •Los cuestionarios deberían tener un método to_s que devuelve una String conteniendo el examen en texto plano
 •Los cuestionarios deberían tener un método run que formulará cada una de las preguntas del cuestionario y mostrara el porcentaje de aciertos
 •Puede que le interese crear tres clases, una para las respuestas (Answer), otra para las preguntas (Question) y una para el cuestionario (Quiz)
 •Hay un problema con la llamada al método question:   question '¿En que año Cristobal Colón descubrió América?',
    wrong =>'1942',
    right =>'1492',
    wrong =>'1808',
    wrong =>'1914'
 si el segundo argumento es un hash y las claves son :wrong y :right se va a producir una colisión y el último valor sobreescribirá a los anteriores. ¿Como resolverlo? Una posible forma de hacerlo es escribiendo métodos wrong y right como sigue:  def wrong
    @counter += 1
    [@counter, WRONG]
  end
 
•Escriba un método to_html que genere una página describiendo el examen. Use ERB.
 •Opcionalmente puede incluir hojas de estilo, javascript, etc. en el HTML generado
 •Use TDD con RSpec 
•Use Unit Testing 
•Use Continuous Integration (Travis) 
•Use Continuous Testing (Guard) 
•Documente su gema (véase RDOC::Markup o RDOC o YARD). 
•Cree una gema ull-etsii-aluXX-quiz 
•Publique la gema en RubyGems.org 
•Indique la URL de su repositorio en GitHub y la URL en RubyGems.org 
