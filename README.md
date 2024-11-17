# RESOLUÇÃO EXERCÍCIO 04

1. Assinale verdadeiro ou falso:

(F) Objetos são modelos para classes;

(F) Atributos de uma classe devem ser obrigatoriamente inicializados para que as classes compilem;

(V) Uma variável declarada dentro de um método deve ser inicializada para que a classe seja compilável;

(F) Uma variável que seja uma classe declarada em um método é automaticamente inicializada com undefined;

(V) Construtores são rotinas especiais que servem para inicializar e configurar os objetos no momento da instanciação;

(V) Construtores não possuem tipo de retorno e podem ou não ter parâmetros;

(V) Uma classe pode ter várias instâncias.


2. Suponha uma classe Hotel que sirva apenas para guardar a quantidade de solicitações de reservas feitas conforme abaixo:
``` typescript
class Hotel {
 quantReservas : number;
 adicionarReserva() : void {
 this.quantReservas++;
 }
}
```
Podemos afirmar que haverá um problema de compilação, pois a variável inteira não foi inicializada previamente? Justifique.
R= Sim, haverá um problema de compilação, pois as variáveis de instância precisam ser inicializadas no momento em que são declaradas ou dentro do construtor da classe antes de serem usadas. Analisando o código, quantReservas é declarado como uma variável do tipo number, mas não recebe um valor inicial. Portanto, na hora de incrementar this.quantReservas no método adicionarReserva, a variável estará indefinido, o que irá gerar um erro. 

3. Ainda sobre a classe do exemplo anterior, considere o código abaixo:
``` typescript
let hotel : Hotel = new Hotel(2); 
console.log(hotel.quantReservas); 
```
Adicione o construtor que aceite um parâmetro inteiro e faça a inicialização do atributo quantReservas.

R= 
``` typescript
class Hotel {
    quantReservas: number;

    constructor(quantReservas: number) {
      this.quantReservas = quantReservas;
    }

      adicionarReserva(): void {
      this.quantReservas++;
    }
  }

  let hotel: Hotel = new Hotel(2);
  console.log(hotel.quantReservas); 
  ```

4. Considere a classe Radio e as instruções que fazem seu uso abaixo: 
``` typescript
class Radio {
    volume: number;
    constructor(volume : number) {
      this.volume = volume;
    }
  }
  let r: Radio = new Radio();
  r.volume = 10;
```

Justifique o erro de compilação e proponha uma solução.

R= O erro ocorre pelo fato do construtor da classe Radio necessita de um parâmetro, o volume, no momento da instanciação. Porém, ao criar a instancia new Radio(), nenhum valor é passado. 

Uma forma de solucionar esse erro é definir um valor padrão para o parâmetro volume.
``` typescript
class Radio {
    volume: number;
  
    constructor(volume: number = 0) {
      this.volume = volume;
    }
  }
  
  let r: Radio = new Radio();
  r.volume = 10;
  console.log(r.volume); 
```

5. Considerando o uso da classe Conta apresentada em aula e seu uso abaixo:
``` typescript
class Conta {
    numero: String;
    saldo: number;
    
    constructor(numero: String, saldo: number) {
        this.numero = numero;
        this.saldo = saldo;
    }

    sacar(valor: number): void {
        this.saldo = this.saldo - valor;
    }
    
    depositar(valor: number): void {
        this.saldo = this.saldo + valor;
    }
    
    consultarSaldo(): number {
        return this.saldo;
    }

    transferir(contaDestino: Conta, valor: number): void {
        this.sacar(valor);
        contaDestino.depositar(valor);
    }
}

let c1: Conta = new Conta("1",100); 
let c2: Conta = new Conta("2",100); 
let c3: Conta; 
c1 = c2; c3 = c1; 
c1.sacar(10); 
c1.transferir(c2,50); 
console.log(c1.consultarSaldo()); 
console.log(c2.consultarSaldo()); 
console.log(c3.consultarSaldo());
```
a. Qual o resultado dos dois "prints"? Justifique sua resposta. 

R= O valor é 90 e eles possuem o mesmo valor pois apontam para o mesmo objeto.

b. O que acontece com o objeto para o qual a referência c1 apontava?

R= Não é possível acessar o objeto pois nenhuma variável está apontando para ele.

6. Crie uma classe chamada Saudacao que: 
* Contenha um atributo chamado texto e outro chamado destinatario, ambos String; 
* Crie um construtor que inicializa os dois atributos; 
* Crie um método obterSaudacao() que retorne a concatenação dos dois atributos. Ex: "Bom dia, João"; 
* Instancie uma classe Saudacao e teste seu método obterSaudacao().

``` typescript
class Saudacao {
    texto: string;
    destinatario: string;
  
    constructor(texto: string, destinatario: string) {
      this.texto = texto;
      this.destinatario = destinatario;
    }
  
    obterSaudacao(): string {
      return `${this.texto}, ${this.destinatario}`;
    }
  }
  
const saudacao = new Saudacao("Bom dia", "João");
console.log(saudacao.obterSaudacao());
```

7. Crie uma classe chamada Triangulo que:
* Possua 3 atributos inteiros representando os lados;
* Crie um método que retorna true se os lados formarem um triângulo de acordo com a regra: |b-c| < a < b+c;
* Crie 3 métodos: ehIsoceles(), ehEquilatero() e ehEscaleno() que retorne verdadeiro caso o triângulo seja um dos tipos relacionados ao nome do método. Eles devem chamar antes de tudo, o método da questão b. e retornar false se esse método já retornar false também;
* Instancie classes Triangulo de diferentes lados e seus métodos.

``` typescript
class Triangulo {
    ladoA: number;
    ladoB: number;
    ladoC: number;
  
    constructor(ladoA: number, ladoB: number, ladoC: number) {
      this.ladoA = ladoA;
      this.ladoB = ladoB;
      this.ladoC = ladoC;
    }
  
    formaTriangulo(): boolean {
      return (
        Math.abs(this.ladoB - this.ladoC) < this.ladoA && this.ladoA < this.ladoB + this.ladoC &&
        Math.abs(this.ladoA - this.ladoC) < this.ladoB && this.ladoB < this.ladoA + this.ladoC &&
        Math.abs(this.ladoA - this.ladoB) < this.ladoC && this.ladoC < this.ladoA + this.ladoB
      );
    }

    ehIsoceles(): boolean {
        if (!this.formaTriangulo()) return false;
        return (
            (this.ladoA === this.ladoB && this.ladoA !== this.ladoC) ||
            (this.ladoA === this.ladoC && this.ladoA !== this.ladoB) ||
            (this.ladoB === this.ladoC && this.ladoB !== this.ladoA)
        );
    }
    
    ehEquilatero(): boolean {
        if (!this.formaTriangulo()) return false;
        return this.ladoA === this.ladoB && this.ladoB === this.ladoC;
    }
    
    ehEscaleno(): boolean {
        if (!this.formaTriangulo()) return false;
        return this.ladoA !== this.ladoB && this.ladoB !== this.ladoC && this.ladoA !== this.ladoC;
    }
}

// Triângulo escaleno
const triangulo1 = new Triangulo(8, 9, 10);
console.log(`Forma triângulo: ${triangulo1.formaTriangulo()}`);
console.log(`É equilátero: ${triangulo1.ehEquilatero()}`);
console.log(`É isósceles: ${triangulo1.ehIsoceles()}`);
console.log(`É escaleno: ${triangulo1.ehEscaleno()}`);

// Triângulo equilátero
const triangulo2 = new Triangulo(9, 9, 9);
console.log(`Forma triângulo: ${triangulo2.formaTriangulo()}`);
console.log(`É equilátero: ${triangulo2.ehEquilatero()}`);
console.log(`É isósceles: ${triangulo2.ehIsoceles()}`);
console.log(`É escaleno: ${triangulo2.ehEscaleno()}`);

// Triângulo isósceles
const triangulo3 = new Triangulo(9, 9, 10);
console.log(`Forma triângulo: ${triangulo3.formaTriangulo()}`);
console.log(`É equilátero: ${triangulo3.ehEquilatero()}`);
console.log(`É isósceles: ${triangulo3.ehIsoceles()}`);
console.log(`É escaleno: ${triangulo3.ehEscaleno()}`);
```

8. Uma classe Equipamento com:

a. um atributo ligado (tipo boolean) 

b. dois métodos liga() e desliga(). O método liga torna o atributo ligado true e o método desliga torna o atributo ligado false. 

c. Crie um método chamado inverte(), que muda o status atual (se ligado, desliga...se desligado, liga) 

d. Crie um método que estaLigado() que retorna o valor do atributo ligado 

e. Altere o comportamento do método ligar() para caso o equipamento já esteja ligado, não ligue novamente. Faça o mesmo com o método desligar(). 

f. Instancie uma classe Equipamento e teste todos os seus métodos. 

R= 
``` typescript
class Equipamento {
    ligado: boolean;
  
    constructor() {
      this.ligado = false;
    }
    
    liga(): void {
        if (!this.ligado) {
        this.ligado = true;
        console.log("Equipamento ligado.");
        } else {
        console.log("O equipamento já está ligado.");
        }
    }

    desliga(): void {
        if (this.ligado) {
        this.ligado = false;
        console.log("Equipamento desligado.");
        } else {
        console.log("O equipamento já está desligado.");
        }
    }
    
    inverte(): void {
        this.ligado = !this.ligado;
        console.log(`Equipamento agora está ${this.ligado ? "ligado" : "desligado"}.`);
    }

    estaLigado(): boolean {
        return this.ligado;
    }
}

const equipamento1 = new Equipamento();

// Executando os métodos
equipamento1.liga();
console.log(`Está ligado? ${equipamento1.estaLigado()}`);

equipamento1.desliga();
console.log(`Está ligado? ${equipamento1.estaLigado()}`);

equipamento1.inverte();
console.log(`Está ligado? ${equipamento1.estaLigado()}`);

equipamento1.inverte();
console.log(`Está ligado? ${equipamento1.estaLigado()}`);
```

9. Altere a classe conta dos slides conforme as instruções abaixo: 
* Altere o método sacar de forma que ele retorne verdadeiro ou falso. Caso o saque deixe saldo negativo, o mesmo não será realizado, retornando falso; 
* Altere o método transferir() para que retorne também um valor lógico e que não seja feita a transferência caso o sacar() na conta origem não seja satisfeito; 
* Verifique as diferentes operações implementadas.

R= 
``` typescript
class Conta {
    numero: String;
    saldo: number;
    
    constructor(numero: String, saldo: number) {
        this.numero = numero;
        this.saldo = saldo;
    }

    sacar(valor: number): boolean {
        if (valor > this.saldo) {
          console.log("Saque não realizado: saldo insuficiente.");
          return false;
        }
        this.saldo -= valor;
        console.log(`Saque de R$${valor} realizado com sucesso.`);
        return true;
    }
    
    depositar(valor: number): void {
        this.saldo += valor;
        console.log(`Depósito de R$${valor} realizado com sucesso.`);
    }
    
    consultarSaldo(): number {
        return this.saldo;
    }

    transferir(contaDestino: Conta, valor: number): boolean {
        if (this.sacar(valor)) {
          contaDestino.depositar(valor);
          console.log(`Transferência de R$${valor} para a conta ${contaDestino.numero} realizada com sucesso.`);
          return true;
        }
        console.log(`Transferência de R$${valor} para a conta ${contaDestino.numero} não realizada: saldo insuficiente.`);
        return false;
    }
}

// Teste - classe Conta
let c1: Conta = new Conta("1", 500);
let c2: Conta = new Conta("2", 1000);

console.log(`Saldo inicial c1: R$${c1.consultarSaldo()}`);
console.log(`Saldo inicial c2: R$${c2.consultarSaldo()}`);

// Teste de saque
c1.sacar(100);
console.log(`Saldo c1 após saque: R$${c1.consultarSaldo()}`);
c1.sacar(300);
console.log(`Saldo c1 após tentativa de saque: R$${c1.consultarSaldo()}`);

// Teste de transferência
c1.transferir(c2, 60);
console.log(`Saldo c1 após transferência: R$${c1.consultarSaldo()}`);
console.log(`Saldo c2 após receber transferência: R$${c2.consultarSaldo()}`);

c1.transferir(c2, 40);
console.log(`Saldo c1 após tentativa de transferência: R$${c1.consultarSaldo()}`);
console.log(`Saldo c2 após tentativa de receber transferência: R$${c2.consultarSaldo()}`);
```

10. Crie uma classe chamada Jogador e nela: 
* Crie 3 atributos inteiros representando força, nível e pontos atuais; 
* Crie um construtor no qual os 3 parâmetros são passados e inicialize os respectivos atributos; 
* Crie um método chamado calcularAtaque. Nele, calcule e retorne o valor da multiplicação de força pelo nível. Esse resultado é o dano de ataque do jogador; 
* Crie um método chamado atacar em que é passado um outro jogador (atacado) como parâmetro. Nele e é feita a subtração do dano (método calcularAtaque) dos pontos do atacado; 
* Crie um método chamado estaVivo que retorna true caso o atributo pontos do jogador seja maior que zero e falso caso contrário. 
* Altere o método atacar para usar o método está vivo e desconsiderar a operação, ou seja, não atacar, caso o jogador passado por parâmetro não esteja vivo. 
* Crie um método chamado toString() que retorna a representação textual do jogador concatenando todos os seus atributos. 
* Avalie em com testes dois jogadores instanciados e inicializados através do construtor. Utilize o método de ataque de cada jogador e ao final, verifique qual jogador tem mais pontos.

R= 

``` typescript
class Jogador {
    nome: string
    forca: number;
    nivel: number;
    pontos: number;
  
    constructor(nome: string, forca: number, nivel: number, pontos: number) {
        this.nome = nome;
        this.forca = forca;
        this.nivel = nivel;
        this.pontos = pontos;
    }
  
    calcularAtaque(): number {
        return this.forca * this.nivel;
    }
  
    atacar(jogadorAtacado: Jogador): void {
        if (!jogadorAtacado.estaVivo()) {
            console.log(`${jogadorAtacado.nome} já está derrotado. Ataque ignorado.`);
            return;
        }
  
        const dano = this.calcularAtaque();
        jogadorAtacado.pontos -= dano;
    
        console.log(
            `${this} atacou ${jogadorAtacado.nome} causando ${dano} de dano.`
        );
  
        if (!jogadorAtacado.estaVivo()) {
            console.log(`${jogadorAtacado.nome} foi derrotado!`);
        }
    }
  
    estaVivo(): boolean {
        return this.pontos > 0;
    }
  
    toString(): string {
        return `Jogador ${this.nome} (Força: ${this.forca}, Nível: ${this.nivel}, Pontos: ${this.pontos})`;
    }
}
  
// Testando a classe Jogador
const jogador1 = new Jogador("Mago", 20, 4, 100);
const jogador2 = new Jogador("Arqueiro", 14, 6, 80);
  
console.log("Estado inicial dos jogadores:");
console.log(jogador1.toString());
console.log(jogador2.toString());
  
// Jogador 1 ataca Jogador 2
jogador1.atacar(jogador2);
  
// Jogador 2 ataca Jogador 1
jogador2.atacar(jogador1);
  
// Jogador 1 ataca Jogador 2
jogador1.atacar(jogador2);
  
// Verificando estado final
console.log("Estado final dos jogadores:");
console.log(jogador1.toString());
console.log(jogador2.toString());
  
// Comparando quem tem mais pontos
if (jogador1.pontos > jogador2.pontos) {
    console.log("Jogador 1 tem mais pontos!");
    } else if (jogador1.pontos < jogador2.pontos) {
    console.log("Jogador 2 tem mais pontos!");
    } else {
    console.log("Ambos os jogadores têm os mesmos pontos!");
}
```
