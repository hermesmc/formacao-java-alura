# Formação Java - Alura
Anotações do curso de formação Java feito no Alura.
Somente o objeto muda os atributos deste mesmo objeto, fica a dica.

## O que é Java?

Java é a linguagem de programação mais usada no mundo, segundo o famoso ranking da TIOBE. É uma linguagem orientada a objeto, multiplataforma e bastante completa por permitir a criação de um programa único para uso em diversas plataformas. A plataforma Java ganhou muitos mercados diferentes - da Web ao Desktop em grandes empresas e governos, passando por mobile e IoT. Mas o grande mercado Java hoje ainda é o back-end em sistemas Web.

## Documentação Java

https://docs.oracle.com/javase/8/docs/api/

## Indice

- Atalhos úteis do Eclipse
- Pacotes Java:
  - Java.lang
  - Java.util
  - Java.io
- Collections  

# Atalhos úteis do Eclipse
 - CTRL+1: Criar os métodos;
 - CTRL+3 e GCUF: Para criar o metodo contrutor; 
 - CTRL+3 e GGAS: Para criar os metodos Getters and Setters;
 - sysout + CTRL+ENTER = System.out.println();
 - main + CTRL+SPACE = 
 
 	public static void main(String[] args) {

	}
 - CTRL+SHIFT+F = formata o código (endentando)
 - foreach + CTRL+SPACE + ENTER = Gera um "for";
 
 Verificando a versão do Java no Eclipse:
 
 - Window - > Preferences -> Java -> Installed JRE's

# - java.lang
 É basicamente o pacote que te fornece classes fundamentais para começar a programar em JAVA, como String, Object, entre outras.
# - java.util
 Utilizada na manipulação de arrays
# - java-io
  Pacote responsável pelo controle de entrada e saída de dados.
  ## Formatação de números:
  - https://docs.oracle.com/javase/tutorial/java/data/numberformat.html
  
  ## Tratamento de caracteres especiais:
  - https://home.unicode.org/
  
  ## Serialização:
  Transformação do objeto java da JVM em um fluxo de bits/bytes e vice-versa. Bastante utilizado na comunicação entre máquinas virtuais java. 
  Classes para essa implementação:
  
    - java.io.ObjectOutputStream
    - java.io.ObjectInputStream
    
  ### Exemplo com tipo String:
		
  - Exemplo gravação de arquivo
 
         public class TesteSerializacao {
	        public static void main(String[] args) throws IOException, ClassNotFoundException {
	    
		      String nome = "Hermes Maruyama";				
		      ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("objeto.bin"));		
		      oos.writeObject(nome);
		      oos.close();
		      
	       }	      
	}	      
				
  - Exemplo leitura arquivo
		
        public class TesteSerializacao {
	        public static void main(String[] args) throws IOException, ClassNotFoundException {
	       
                 ObjectInputStream ois = new ObjectInputStream(new FileInputStream("objeto.bin"));
   	             String nomeLido = (String) ois.readObject();		
	             ois.close();
	             System.out.println(nomeLido);
		     
	         }
        }
	
  ### Exemplo outro objeto:
  
  Na classe utilizada para criar o objeto:
  
  inclua 
  
  - implements Serializable
  
  e 
  
   //utilizado para controlar a versão da classe, caso mude algum atributo com tipos incompatíveis o valor deve ser incrementado<br>
   - private static final long serialVersionUID = 1L; //Não obrigatório colocar explicitamente o atributo serialVersionUID, mas é boa prática.
  
  ### Collections
  
  https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html
  
  No codigo abaixo, estamos comparando o parametro tempo para ordenar o array. Array este composto pelo titulo da aula e seu tempo:
  
  	public static void main(String[] args) {
		Aula a1 = new Aula("Revisando ArrayLists", 18);
		Aula a2 = new Aula("Listas de objetos", 15);
		Aula a3 = new Aula("Relacionamentos de Listas e Objetos", 16);
		
		ArrayList<Aula> aulas = new ArrayList<>();
		aulas.add(a1);
		aulas.add(a2);
		aulas.add(a3); 
		
  	aulas.sort(Comparator.comparing(Aula::getTempo));
  
  CompareTo na classe aula:  
  
  	public int compareTo(Aula outraAula) {
		return this.titulo.compareTo(outraAula.titulo);
	}

  ## ArrayList X LinkedList
  
  - O ArrayList funciona muito bem em listas grandes que não vão sofrer alterações de posição dos registros. 
  - Já a LinkedList adiciona muito rápido elemestos na lista. MAs para buscar um determinado registro ela é mais lenta.
  
  ## List X Set
  
  As listas possuem indices e são mais lentas que os conjuntos(sets). A grande vantagem dos conjuntos é a veloidade. 
  Mas não permitem ser ordenadas e a consulta de elemento pelo indice.

  Em listas, ao redefinir o metodo equals, o método hash também deve ser sobreescrito:
  
  	@Override
	public boolean equals(Object obj) {
		//cast
		Aluno outro = (Aluno)obj;
		return this.nome.equals(outro.nome); 		
	}
	
	@Override
	public int hashCode() {
		return this.nome.hashCode();
	}
   Desta forma vpcê garante que na tabela de espalhamento o hash do nome será sempre o mesmo.	

   ## Código legado de coleções
   
   O  Iterator é um objeto que todas as coleções nos dão acesso, que serve para iterar entre os elementos dentro da coleção, selecionando sempre o próximo objeto da coleção.
   Um outro objeto antigo que pode ser citado é o Vector, que era utilizado antes da interface Collection existir (Collection existe desde o Java 1.2):

   Vector<Aluno> vetor = new Vector<>();

   Essa classe é muito antiga e se parece com o ArrayList, inclusive ela implementa List atualmente. A diferença é que ela pode ser utilizada por várias threads simultaneamente, chamado de thread safe. 
   
   TreeSet:  já ordena os seus elementos na hora da inserção. O critério da ordenação depende e pode ser definido através de um Comparator.
   
   Interface Map
   
   Essa interface permite associar um determinado registro a um valor. Sendo assim podemos pesquisar um número de matrícula, que não faz parte do hash, e localizá-lo.
   
   Cursos que merecem ser feitos:
    OO: Melhores técnicas com Java
    SOLID com Java
    Design Patterns Java I
    Design Patterns Java II

   ## Java 8
   
   Classes anônimas: são classes que, ao invés de serem declaras para fazerem coisas triviais e, principalmente, quando a classe não for aproveitada em outro lugar no código, são construídas no próprio new.
   
  Exempo:
   
   	Consumer<String> consumidor = new Consumer<String>() {
 		@Override
		public void accept(String s) {
			System.out.println(s);				
		}
   	};
   
  Lambdas: 
   
	palavras.forEach((String s) -> {
		System.out.println(s);		
	});
	
  Lambda mais simples ainda
      
	palavras.forEach(s -> System.out.println(s));	
	
  Metodo Referência - Method References
    
  Exemplos:
    
	palavras.sort((Comparator.comparing(s -> s.length())));
	System.out.println(palavras);

  OU 
	
	palavras.sort((Comparator.comparing(String::length)));
	System.out.println(palavras);	

  OU
  
	Consumer<String> impressor = System.out::println;
	palavras.forEach(impressor);   

## Design Pattern

Os Design Patterns, também conhecidos como Padrões de Projeto, foram criados pelo arquiteto Christopher Alexander, na década de 70. Durante esse período o arquiteto escreveu dois livros: “Pattern Language” e “Timeless Way of Building”. Esses livros foram o exemplo de como Christopher pensava no modo para documentar esses padrões.

O objetivo dos padrões de projeto, são tornar componentes reutilizáveis que facilitam a padronização, que permita agilidade para as soluções de problemas recorrentes no desenvolvimento do sistema.

## Utilizando datas

Utiizando a novas API de datas com alguns exemplos:

Data atual
	
	LocalDate hoje = LocalDate.now(); 
	
Data específica:

	LocalDate dataEspecifica = LocalDate.of(2016, 07, 01);

Formatando datas

	DateTimeFormatter dataFormatada = DateTimeFormatter.ofPattern("dd/MM/yyyy");
	System.out.println(olimpiadas.format(dataFormatada));
	
Data e hora atual(formatando data e hora):

	LocalDateTime agora = LocalDateTime.now();
	DateTimeFormatter dataFormatadaComHoras = DateTimeFormatter.ofPattern("dd/MM/yyyy hh:mm");
	System.out.println(agora.format(dataFormatadaComHoras));


