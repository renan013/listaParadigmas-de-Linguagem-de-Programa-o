# listaParadigmas-de-Linguagem-de-Programa-o# 1. Classes e Objetos Básicos
class Carro:
    def __init__(self, marca, modelo, ano):
        self.marca = marca
        self.modelo = modelo
        self.ano = ano

    def exibir_detalhes(self):
        print(f"Marca: {self.marca}, Modelo: {self.modelo}, Ano: {self.ano}")

carro1 = Carro("Toyota", "Corolla", 2020)
carro2 = Carro("Honda", "Civic", 2019)
carro3 = Carro("Ford", "Fusion", 2018)

carro1.exibir_detalhes()
carro2.exibir_detalhes()
carro3.exibir_detalhes()

# 2. Métodos (Acelerar e Frear)
class Carro:
    def __init__(self, marca, modelo, ano):
        self.marca = marca
        self.modelo = modelo
        self.ano = ano
        self.velocidade = 0

    def acelerar(self):
        self.velocidade += 10

    def frear(self):
        self.velocidade -= 10

    def exibir_velocidade(self):
        print(f"Velocidade atual: {self.velocidade} km/h")

carro = Carro("Toyota", "Corolla", 2020)
carro.acelerar()
carro.exibir_velocidade()
carro.frear()
carro.exibir_velocidade()

# 3. Encapsulamento
class ContaBancaria:
    def __init__(self, titular, saldo):
        self.__saldo = saldo
        self.titular = titular

    def depositar(self, valor):
        self.__saldo += valor

    def sacar(self, valor):
        if valor <= self.__saldo:
            self.__saldo -= valor
        else:
            print("Saldo insuficiente")

    def exibir_saldo(self):
        print(f"Saldo atual: {self.__saldo}")

conta = ContaBancaria("João", 1000)
conta.depositar(500)
conta.sacar(300)
conta.exibir_saldo()

# 4. Herança
class Animal:
    def som(self):
        pass

class Cachorro(Animal):
    def som(self):
        return "Latido"

class Gato(Animal):
    def som(self):
        return "Miau"

# 5. Polimorfismo
def emitir_som(animais):
    for animal in animais:
        print(animal.som())

cachorro = Cachorro()
gato = Gato()
animais = [cachorro, gato]
emitir_som(animais)

# 6. Composição
class Motor:
    def __init__(self, potencia):
        self.potencia = potencia

class CarroComMotor:
    def __init__(self, marca, modelo, ano, motor):
        self.marca = marca
        self.modelo = modelo
        self.ano = ano
        self.motor = motor

motor = Motor(1.8)
carro_motor = CarroComMotor("Toyota", "Corolla", 2020, motor)
print(f"Carro: {carro_motor.marca}, Motor: {carro_motor.motor.potencia}L")

# 7. Associação
class Escola:
    def __init__(self, nome):
        self.nome = nome
        self.professores = []

    def adicionar_professor(self, professor):
        self.professores.append(professor)

class Professor:
    def __init__(self, nome):
        self.nome = nome

escola = Escola("Escola A")
professor = Professor("Professor João")
escola.adicionar_professor(professor)
print(f"Escola: {escola.nome}, Professores: {[prof.nome for prof in escola.professores]}")

# 8. Agregação
class Empresa:
    def __init__(self, nome):
        self.nome = nome
        self.empregados = []

    def adicionar_empregado(self, empregado):
        self.empregados.append(empregado)

class Empregado:
    def __init__(self, nome, cargo, salario):
        self.nome = nome
        self.cargo = cargo
        self.salario = salario

empresa = Empresa("Empresa X")
empregado = Empregado("José", "Gerente", 5000)
empresa.adicionar_empregado(empregado)
print(f"Empresa: {empresa.nome}, Empregados: {[emp.nome for emp in empresa.empregados]}")

# 9. Interfaces/Protocolos
from abc import ABC, abstractmethod

class Imprimivel(ABC):
    @abstractmethod
    def imprimir(self):
        pass

class Relatorio(Imprimivel):
    def imprimir(self):
        print("Imprimindo relatório")

class Contrato(Imprimivel):
    def imprimir(self):
        print("Imprimindo contrato")

relatorio = Relatorio()
contrato = Contrato()
relatorio.imprimir()
contrato.imprimir()

# 10. Sobrecarga de Métodos (usando *args)
class Calculadora:
    def somar(self, *args):
        return sum(args)

calc = Calculadora()
print(calc.somar(1, 2))
print(calc.somar(1, 2, 3))

# 11. Classes Abstratas
class Funcionario(ABC):
    @abstractmethod
    def calcular_salario(self):
        pass

class FuncionarioHorista(Funcionario):
    def calcular_salario(self):
        return "Salário por hora"

class FuncionarioAssalariado(Funcionario):
    def calcular_salario(self):
        return "Salário fixo"

func_horista = FuncionarioHorista()
func_assalariado = FuncionarioAssalariado()
print(func_horista.calcular_salario())
print(func_assalariado.calcular_salario())

# 12. Sobrecarga de Operadores
class Produto:
    def __init__(self, nome, preco):
        self.nome = nome
        self.preco = preco

    def __add__(self, other):
        return self.preco + other.preco

produto1 = Produto("Produto A", 50)
produto2 = Produto("Produto B", 30)
print(produto1 + produto2)

# 13. Métodos Estáticos
class Matematica:
    @staticmethod
    def fatorial(n):
        if n == 0:
            return 1
        else:
            return n * Matematica.fatorial(n-1)

print(Matematica.fatorial(5))

# 14. Singleton
class Configuracao:
    __instance = None

    def __new__(cls):
        if Configuracao.__instance is None:
            Configuracao.__instance = super(Configuracao, cls).__new__(cls)
        return Configuracao.__instance

config1 = Configuracao()
config2 = Configuracao()
print(config1 == config2)  # True

# 15. Exceções Personalizadas
class SaldoInsuficienteException(Exception):
    pass

class ContaBancariaComExcecao:
    def __init__(self, saldo):
        self.saldo = saldo

    def sacar(self, valor):
        if valor > self.saldo:
            raise SaldoInsuficienteException("Saldo insuficiente")
        self.saldo -= valor

conta_excecao = ContaBancariaComExcecao(1000)
try:
    conta_excecao.sacar(1500)
except SaldoInsuficienteException as e:
    print(e)
import java.util.ArrayList;
import java.util.List;

// 1. Classes e Objetos Básicos
class Carro {
    String marca;
    String modelo;
    int ano;

    Carro(String marca, String modelo, int ano) {
        this.marca = marca;
        this.modelo = modelo;
        this.ano = ano;
    }

    void exibirDetalhes() {
        System.out.println("Marca: " + this.marca + ", Modelo: " + this.modelo + ", Ano: " + this.ano);
    }
}

public class Main {
    public static void main(String[] args) {
        // 1. Classes e Objetos Básicos
        Carro carro1 = new Carro("Toyota", "Corolla", 2020);
        Carro carro2 = new Carro("Honda", "Civic", 2019);
        Carro carro3 = new Carro("Ford", "Fusion", 2018);

        carro1.exibirDetalhes();
        carro2.exibirDetalhes();
        carro3.exibirDetalhes();

        // 2. Métodos (Acelerar e Frear)
        CarroComVelocidade carro = new CarroComVelocidade("Toyota", "Corolla", 2020);
        carro.acelerar();
        carro.exibirVelocidade();
        carro.frear();
        carro.exibirVelocidade();

        // 3. Encapsulamento
        ContaBancaria conta = new ContaBancaria("João", 1000);
        conta.depositar(500);
        conta.sacar(300);
        conta.exibirSaldo();

        // 4. Herança
        Animal cachorro = new Cachorro();
        Animal gato = new Gato();

        // 5. Polimorfismo
        List<Animal> animais = new ArrayList<>();
        animais.add(c
        // 5. Polimorfismo
        animais.add(cachorro);
        animais.add(gato);
        emitirSom(animais);

        // 6. Composição
        Motor motor = new Motor(1.8);
        CarroComMotor carroMotor = new CarroComMotor("Toyota", "Corolla", 2020, motor);
        System.out.println("Carro: " + carroMotor.marca + ", Motor: " + carroMotor.motor.potencia + "L");

        // 7. Associação
        Escola escola = new Escola("Escola A");
        Professor professor = new Professor("Professor João");
        escola.adicionarProfessor(professor);
        System.out.println("Escola: " + escola.nome + ", Professores: " + escola.getNomesProfessores());

        // 8. Agregação
        Empresa empresa = new Empresa("Empresa X");
        Empregado empregado = new Empregado("José", "Gerente", 5000);
        empresa.adicionarEmpregado(empregado);
        System.out.println("Empresa: " + empresa.nome + ", Empregados: " + empresa.getNomesEmpregados());

        // 9. Interfaces/Protocolos
        Imprimivel relatorio = new Relatorio();
        Imprimivel contrato = new Contrato();
        relatorio.imprimir();
        contrato.imprimir();

        // 10. Sobrecarga de Métodos
        Calculadora calc = new Calculadora();
        System.out.println(calc.somar(1, 2));
        System.out.println(calc.somar(1, 2, 3));

        // 11. Classes Abstratas
        Funcionario funcHorista = new FuncionarioHorista();
        Funcionario funcAssalariado = new FuncionarioAssalariado();
        System.out.println(funcHorista.calcularSalario());
        System.out.println(funcAssalariado.calcularSalario());

        // 12. Sobrecarga de Operadores
        Produto produto1 = new Produto("Produto A", 50);
        Produto produto2 = new Produto("Produto B", 30);
        System.out.println(produto1.somarPrecos(produto2));

        // 13. Métodos Estáticos
        System.out.println(Matematica.fatorial(5));

        // 14. Singleton
        Configuracao config1 = Configuracao.getInstance();
        Configuracao config2 = Configuracao.getInstance();
        System.out.println(config1 == config2); // True

        // 15. Exceções Personalizadas
        ContaBancariaComExcecao contaExcecao = new ContaBancariaComExcecao(1000);
        try {
            contaExcecao.sacar(1500);
        } catch (SaldoInsuficienteException e) {
            System.out.println(e.getMessage());
        }
    }

    // 2. Métodos (Acelerar e Frear)
    static class CarroComVelocidade extends Carro {
        int velocidade = 0;

        CarroComVelocidade(String marca, String modelo, int ano) {
            super(marca, modelo, ano);
        }

        void acelerar() {
            this.velocidade += 10;
        }

        void frear() {
            this.velocidade -= 10;
        }

        void exibirVelocidade() {
            System.out.println("Velocidade atual: " + this.velocidade + " km/h");
        }
    }

    // 4. Herança
    static abstract class Animal {
        abstract String som();
    }

    static class Cachorro extends Animal {
        String som() {
            return "Latido";
        }
    }

    static class Gato extends Animal {
        String som() {
            return "Miau";
        }
    }

    // 5. Polimorfismo
    static void emitirSom(List<Animal> animais) {
        for (Animal animal : animais) {
            System.out.println(animal.som());
        }
    }

    // 6. Composição
    static class Motor {
        double potencia;

        Motor(double potencia) {
            this.potencia = potencia;
        }
    }

    static class CarroComMotor extends Carro {
        Motor motor;

        CarroComMotor(String marca, String modelo, int ano, Motor motor) {
            super(marca, modelo, ano);
            this.motor = motor;
        }
    }

    // 7. Associação
    static class Escola {
        String nome;
        List<Professor> professores = new ArrayList<>();

        Escola(String nome) {
            this.nome = nome;
        }

        void adicionarProfessor(Professor professor) {
            this.professores.add(professor);
        }

        List<String> getNomesProfessores() {
            List<String> nomes = new ArrayList<>();
            for (Professor professor : professores) {
                nomes.add(professor.nome);
            }
            return nomes;
        }
    }

    static class Professor {
        String nome;

        Professor(String nome) {
            this.nome = nome;
        }
    }

    // 8. Agregação
    static class Empresa {
        String nome;
        List<Empregado> empregados = new ArrayList<>();

        Empresa(String nome) {
            this.nome = nome;
        }

        void adicionarEmpregado(Empregado empregado) {
            this.empregados.add(empregado);
        }

        List<String> getNomesEmpregados() {
            List<String> nomes = new ArrayList<>();
            for (Empregado empregado : empregados) {
                nomes.add(empregado.nome);
            }
            return nomes;
        }
    }

    static class Empregado {
        String nome;
        String cargo;
        double salario;

        Empregado(String nome, String cargo, double salario) {
            this.nome = nome;
            this.cargo = cargo;
            this.salario = salario;
        }
    }

    // 9. Interfaces/Protocolos
    interface Imprimivel {
        void imprimir();
    }

    static class Relatorio implements Imprimivel {
        public void imprimir() {
            System.out.println("Imprimindo relatório");
        }
    }

    static class Contrato implements Imprimivel {
        public void imprimir() {
            System.out.println("Imprimindo contrato");
        }
    }

    // 10. Sobrecarga de Métodos
    static class Calculadora {
        int somar(int a, int b) {
            return a + b;
        }

        int somar(int a, int b, int c) {
            return a + b + c;
        }
    }

    // 11. Classes Abstratas
    static abstract class Funcionario {
        abstract String calcularSalario();
    }

    static class FuncionarioHorista extends Funcionario {
        String calcularSalario() {
            return "Salário por hora";
        }
    }

    static class FuncionarioAssalariado extends Funcionario {
        String calcularSalario() {
            return "Salário fixo";
        }
    }

    // 12. Sobrecarga de Operadores
    static class Produto {
        String nome;
        double preco;

        Produto(String nome, double preco) {
            this.nome = nome;
            this.preco = preco;
        }

        double somarPrecos(Produto outroProduto) {
            return this.preco + outroProduto.preco;
        }
    }

    // 13. Métodos Estáticos
    static class Matematica {
        static int fatorial(int n) {
            if (n == 0) {
                return 1;
            } else {
                return n * fatorial(n - 1);
            }
        }
    }

    // 14. Singleton
    static class Configuracao {
        private static Configuracao instance;

        private Configuracao() {}

        public static Configuracao getInstance() {
            if (instance == null) {
                instance = new Configuracao();
            }
            return instance;
        }
    }

    // 15. Exceções Personalizadas
    static class SaldoInsuficienteException extends Exception {
        public SaldoInsuficienteException(String mensagem) {
            super(mensagem);
        }
    }

    static class ContaBancariaComExcecao {
        private double saldo;

        ContaBancariaComExcecao(double saldo) {
            this.saldo = saldo;
        }

        void sacar(double valor) throws SaldoInsuficienteException {
            if (valor > this.saldo) {
                throw new SaldoInsuficienteException("Saldo insuficiente");
            }
            this.saldo -= valor;
        }
    }
}
package main

import (
    "fmt"
)

// 1. Classes e Objetos Básicos
type Carro struct {
    Marca  string
    Modelo string
    Ano    int
}

func (c Carro) ExibirDetalhes() {
    fmt.Printf("Marca: %s, Modelo: %s, Ano: %d\n", c.Marca, c.Modelo, c.Ano)
}

// 2. Métodos (Acelerar e Frear)
type CarroComVelocidade struct {
    Marca     string
    Modelo    string
    Ano       int
    Velocidade int
}

func (c *CarroComVelocidade) Acelerar() {
    c.Velocidade += 10
}

func (c *CarroComVelocidade) Frear() {
    c.Velocidade -= 10
}

func (c CarroComVelocidade) ExibirVelocidade() {
    fmt.Printf("Velocidade atual: %d km/h\n", c.Velocidade)
}

func main() {
    // 1. Classes e Objetos Básicos
    carro1 := Carro{"Toyota", "Corolla", 2020}
    carro2 := Carro{"Honda", "Civic", 2019}
    carro3 := Carro{"Ford", "Fusion", 2018}

    carro1.ExibirDetalhes()
    carro2.ExibirDetalhes()
    carro3.ExibirDetalhes()

    // 2. Métodos (Acelerar e Frear)
    carro := CarroComVelocidade{Marca: "Toyota", Modelo: "Corolla", Ano: 2020}
    carro.Acelerar()
    carro.ExibirVelocidade()
    carro.Frear()
    carro.ExibirVelocidade()

    // 3. Encapsulamento
    conta := NovaContaBancaria("João", 1000)
    conta.Depositar(500)
    conta.Sacar(300)
    conta.ExibirSaldo()
}

// 3. Encapsulamento
type ContaBancaria struct {
    titular string
    saldo   float64
}

func NovaContaBancaria(titular string, saldo float64) *ContaBancaria {
    return &ContaBancaria{titular: titular, saldo: saldo}
}

func (c *ContaBancaria) Depositar(valor float64) {
    c.saldo += valor
}

func (c *ContaBancaria) Sacar(valor float64) {
    if valor <= c.saldo {
        c.saldo -= valor
    } else {
        fmt.Println("Saldo insuficiente")
    }
}

func (c ContaBancaria) ExibirSaldo() {
    fmt.Printf("Saldo atual: %.2f\n", c.saldo)
}

// 4. Herança e Polimorfismo simulados em Go
type Animal interface {
    Som() string
}

type Cachorro struct{}

func (Cachorro) Som() string {
    return "Latido"
}

type Gato struct{}

func (Gato) Som() string {
    return "Miau"
}

func EmitirSom(animais []Animal) {
    for _, animal := range animais {
        fmt.Println(animal.Som())
    }
}

.        
