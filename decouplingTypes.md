No desenvolvimento de software, a busca por um baixo acoplamento é essencial para criar sistemas flexíveis e de fácil manutenção, uma medida de qualidade do software.

O acoplamento, que representa a dependência entre os diversos módulos ou componentes de um sistema, pode tornar o código complexo e difícil de modificar quando não é adequadamente gerenciado.

Por isso, entender os diferentes tipos de acoplamento e suas implicações é fundamental para pessoas desenvolvedoras que desejam criar sistemas robustos e escaláveis.

Vamos explorar mais sobre o que é acoplamento e os diferentes tipos que podem ser encontrados no desenvolvimento de software.

O que é acoplamento?
Acoplamento, no contexto da engenharia de software, refere-se ao grau de dependência entre diferentes partes de um sistema. Quanto maior o acoplamento entre componentes, mais forte é a interdependência entre eles.

Alto acoplamento significa que os módulos estão intimamente conectados, assim, alterações em um dos módulos podem afetar os demais. Baixo acoplamento significa que os módulos são independentes, então as alterações em um módulo têm pouco impacto nos outros.

Existem diversos tipos de acoplamento que influenciam a estrutura e a manutenção de um sistema de software.

Principais tipos de acoplamento:
1 - Data Coupling (Acoplamento de Dados):

Ocorre quando um módulo depende apenas das estruturas de dados específicas de outro. Isso significa que os módulos são independentes uns dos outros e só há uma dependência nos tipos de dados sendo passados entre os módulos.

O acoplamento de dados é usado comumente em programação orientada a objetos e programação procedural.

class Usuario {
  constructor(private nome: string) {}

  getNome(): string {
    return this.nome;
  }
}

class GerenciadorUsuario {
  constructor(private usuario: Usuario) {}

  mostrarNomeUsuario(): void {
    console.log(this.usuario.getNome());
  }
}

// Utilização dos Módulos A e B
const usuario = new Usuario("Ana");
const gerenciadorUsuario = new GerenciadorUsuario(usuario);
gerenciadorUsuario.mostrarNomeUsuario();
COPIAR CÓDIGO
Neste exemplo, o GerenciadorUsuario depende diretamente do Usuario para funcionar corretamente, logo, qualquer alteração na estrutura ou comportamento da classe Usuario pode afetar diretamente o GerenciadorUsuario.

2 - Stamp Coupling (Acoplamento por Carimbo):

Refere-se a uma forma de acoplamento de dados na qual os módulos compartilham muitos campos em uma estrutura de dados complexa, mas cada módulo usa apenas um subconjunto desses campos.

// Módulo A
class Pedido {
  constructor(private id: number, private descricao: string, private valor: number) {}

  getId(): number {
    return this.id;
  }
}

// Módulo B
class GerenciadorPedido {
  constructor(private pedido: Pedido) {}

  mostrarIdPedido(): void {
    console.log(this.pedido.getId());
  }
}

// Utilização dos Módulos A e B
const pedido = new Pedido(1, "Produto A", 100);
const gerenciadorPedido = new GerenciadorPedido(pedido);
gerenciadorPedido.mostrarIdPedido();
COPIAR CÓDIGO
Neste exemplo, o GerenciadorPedido depende de um objeto Pedido que possui uma estrutura de dados complexa, mas apenas usa um subconjunto específico de campos desse objeto (id). Isso demonstra um acoplamento por carimbo.

3 - Control Coupling (Acoplamento de Controle):

Envolve a dependência entre módulos devido ao compartilhamento de informações de controle, como valores de flags ou indicadores que afetam o fluxo de execução do programa.

Quando os módulos se relacionam ou se comunicam de forma organizada, compartilhando dados de maneira coordenada, isso é conhecido como acoplamento de controle. Esse tipo de acoplamento implica que um módulo exerce controle sobre o fluxo de dados ou informações entre os demais, direcionando as instruções sobre como proceder.

// Módulo A 
class ProcessadorPagamento {
  processarPagamento(status: boolean): void {
    if (status) {
      console.log("Pagamento processado com sucesso.");
    } else {
      console.log("Falha ao processar pagamento.");
    }
  }
}

// Módulo B 
class CarrinhoCompras {
  constructor(private processador: ProcessadorPagamento) {}

  finalizarCompra(status: boolean): void {
    this.processador.processarPagamento(status);
  }
}

// Utilização dos Módulos A e B
const processador = new ProcessadorPagamento();
const carrinho = new CarrinhoCompras(processador);
carrinho.finalizarCompra(true);
COPIAR CÓDIGO
Neste exemplo, o CarrinhoCompras depende do ProcessadorPagamento para determinar se a compra deve ser finalizada com sucesso ou não, com base no status do pagamento. Isso demonstra um acoplamento de controle.

4 - Common Coupling (Acoplamento Comum):

Ocorre quando dois ou mais módulos dependem de um terceiro módulo comum para realizar suas funções. Isso cria uma forte interdependência entre os módulos, tornando o sistema mais difícil de ser modularizado e mantido.

// Módulo A
class Log {
  registrarMensagem(mensagem: string): void {
    console.log(`[LOG] ${mensagem}`);
  }
}

// Módulo B
class ServicoAutenticacao {
  constructor(private log: Log) {}

  autenticarUsuario(): void {
    // Lógica de autenticação
    this.log.registrarMensagem("Usuário autenticado com sucesso.");
  }
}

// Utilização dos Módulos A e B
const log = new Log();
const servicoAutenticacao = new ServicoAutenticacao(log);
servicoAutenticacao.autenticarUsuario();
COPIAR CÓDIGO
Neste exemplo, o ServicoAutenticacao depende do Log para registrar mensagens de log durante o processo de autenticação. Ambos os módulos compartilham a mesma dependência do Log, demonstrando um acoplamento comum.

5 - Content Coupling (Acoplamento de Conteúdo):

É o tipo mais forte de acoplamento, onde um módulo depende diretamente da implementação interna de outro módulo, acessando e manipulando suas variáveis internas.

// Módulo A
class Calculadora {
  private resultado: number = 0;

  somar(a: number, b: number): void {
    this.resultado = a + b;
  }

  obterResultado(): number {
    return this.resultado;
  }
}

// Módulo B
class Logger {
  private calculadora: Calculadora;

  constructor(calculadora: Calculadora) {
    this.calculadora = calculadora;
  }

  registrarLog(): void {
    console.log(`Resultado da operação: ${this.calculadora.obterResultado()}`);
  }
}

// Utilização dos Módulos A e B
const calculadora = new Calculadora();
calculadora.somar(2, 3);
const logger = new Logger(calculadora);
logger.registrarLog();
COPIAR CÓDIGO
Neste exemplo, o Logger depende diretamente da implementação interna da classe Calculadora, usando e manipulando sua variável interna resultado. Isso demonstra um acoplamento de conteúdo, considerado o tipo mais forte.

Vantagens do baixo acoplamento
Maior facilidade de manutenção: o baixo acoplamento reduz o impacto das alterações de um módulo em outros módulos, facilitando a modificação ou substituição de componentes individuais sem afetar todo o sistema.
Modularidade aprimorada: o baixo acoplamento permite que os módulos sejam desenvolvidos e testados isoladamente, melhorando a modularidade e a reutilização do código.
Melhor escalabilidade: o baixo acoplamento facilita a adição de novos módulos e a remoção dos existentes, facilitando o dimensionamento do sistema conforme necessário.
Desvantagens do alto acoplamento
Maior complexidade: o alto acoplamento aumenta a interdependência entre os módulos, tornando o sistema mais complexo e difícil de entender.
Flexibilidade reduzida:o alto acoplamento dificulta modificar ou substituir componentes individuais sem afetar todo o sistema.
Modularidade diminuída: o alto acoplamento dificulta desenvolver e testar módulos isoladamente, reduzindo a modularidade e a reutilização do código.
Se você quiser se aprofundar no assunto, vou deixar algumas referências, em inglês, para que possa mergulhar no assunto:

Leituras Recomendadas:
Coupling and Cohesion – Software Engineering (Acoplamento e Coesão – Engenharia de Software)
Data Coupling - Types Of Coupling(Acoplamento de dados - Tipos de acoplamento)
Ao compreender os diferentes tipos de acoplamento e sua aplicação no desenvolvimento em TypeScript, você estará melhor preparado para projetar sistemas de software mais modularizados, flexíveis e de fácil manutenção, seguindo os princípios da SOLID, além de outros princípios de design de software.