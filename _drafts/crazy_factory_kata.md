# Crazy Factory Kata: Introducing Testing some modern testing concepts

Durante el curso que dimos en TGSOL (Madrid) durante este mes de mayo, tuvimos la posibilidad de introducir
diferentes conceptos del mundo del desarrollo de software a ingenieros de red. Gran parte de la formación
giró en torno a las prácticas de Integración Continua, sus claves y sus ventajas. 

Como la gran mayoría de asistentes no tenían un perfil de desarrollo sino que hasta el momento su experiencia estaba
centrada en el mundo de los sistemas de telecomunicaciones, el primer reto fue introducir los sistemas de control de
versiones que se usan hoy en día, y, en particular, git como estándar de facto que es.

Una importante lección aprendida durante la preparación de esta formación (y durante la propia) ha sido la 
necesidad de adaptar los contenidos al nivel y al contexto de los asistentes. En el caso particular de Git, me costó un
poco conectar con ellos y transmitir de forma clara los mecanismos básicos del add-commit.

Como la formación duró dos días, entre el primero y el segundo tuve la oportunidad de adaptarme un poco. Para el segundo día
de la formación contaba inicialmente con un ejercicio en el que los asistentes, agrupados por parejas y éstas, a su vez,
por grupos, tuviesen que compartir uno o varios repositorios en los que debían completar el código faltante para hacer
pasar los tests.

En el momento de cambiar este ejercicio para adaptarlo a un público con poca experiencia de desarrollo, improvisé un poco.
Así es como surgió la _CrazyFactoryKata_.

Este código se compone de tres clases (componentes, cada una de las cuales cuenta con sus tests unitarios) y de una cuarta
clase que depende (utiliza) las primeras tres. El código de las clases componentes está incompleto, de modo que sus tests
unitarios fallan. Cada pareja (o grupo) debe corregir una de estas clases, haciendo pasar así sus tests. Por ejemplo, el
test (fallido) de la Smasher es:

```
class Smasher {
	public int smash(int amountOfHamsters) {
		// TODO: Complete This
		return 0;
	}
}

class SmasherTest {
	@Test
	public void should_smash_hamsters_for_real() {
		assertThat(new Smasher().smash(10)).isEqualTo(5);
	}
}
```

Obviamente, como se trata de una kata de introducción al testing de código compartido mediante repositorios, 
la solución es muy simple. Sin embargo, existe una ambigüedad accidental en este ejemplo: basta con escribir un 
`return 5` para hacer pasar este test.

La cuarta clase que existe en el código es una integración de las tres anteriores, y lo que es especialmente interesante
es que los tests de esta cuarta clase no pasan con _cualquier implementación_ de las tres primeras.


