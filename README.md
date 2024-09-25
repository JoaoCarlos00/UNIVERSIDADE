# ETAPA 5 AC1

Criação de uma classe para um universidade aprovar ou desaprovar o aluno

## 🚀 Enunciados

Uma conceituada universidade calcula a nota final de seus alunos de duas formas a depender da quantidade de avaliações.

Até 2 avaliações a nota final será a média aritmética das notas. Caso tenha 3 notas será a média ponderada, onde a segunda nota tem o dobro do peso da primeira e a terceira tem o dobro do peso da segunda.

Caso haja 4 notas, ac1, ac2, ag e af, a nota final será dada pela equação:

MF = (ac1 * 0,15) + (ac2 * 0,30) + (ag * 0,10) + (af * 0,45).

Nessa mesma universidade, um aluno será aprovado se sua nota for >= 5 e possuir ao menos 75% de presença. Contudo, nas disciplinas no formato EAD, não há presença e a aprovação será apenas baseada na nota, com o mesmo valor de corte das disciplinas presenciais.

Crie a classe aluno que implementa essas funções e os atributos que julgar necessários. Além disso, crie construtores e um método que imprime o nome, RA, nota final e situação (Aprovado/Reprovado).

Para entrega desta atividade, crie um repositório remoto com o nome UNIVERSIDADE, preencha o README.MD conforme o modelo apresentado em aula.

### 📋 Códigos

public class Aluno { //Criação da Classe e de seus Atributos
    private String nome;
    private String ra;
    private double[] notas;
    private double presenca;
    private boolean isEAD; // Aqui é para saber se o aluno é do presencial ou ela faz via EAD

    public Aluno(String nome, String ra, boolean isEAD) { //Metodo constructor para controlar os atributos
        this.nome = nome;
        this.ra = ra;
        this.isEAD = isEAD;
        this.notas = new double[4]; // Para até 4 notas caso seja necessário
        this.presenca = 0.0; // Presença inicial
    }

    public void setNotas(double... notas) { //Metodo para definir as notas
        if (notas.length > 4) {
           System.out.println("Número máximo de notas é 4.");
        }
        this.notas = notas;
    }

    public void setPresenca(double presenca) { // Metodo para definir a presença do aluno
        this.presenca = presenca;
    }

    public double calcularNotaFinal() { //Metodo para calcular a nota final do aluno com base nos criterios colocados pela universidade
        int numNotas = 0;
        for (double nota : notas) {
            if (nota != 0) {
                numNotas++;
            }
        }

        switch (numNotas) {
            case 1:
            case 2:
                return calcularMediaAritmetica();
            case 3:
                return calcularMediaPonderada();
            case 4:
                return calcularMediaComPesos();
            default:
                return 0.0; // Em caso de não houver notas
        }
    }

    private double calcularMediaAritmetica() { //Media Aritmetica pois existem somente 2 notas
        double soma = 0.0;
        for (double nota : notas) {
            soma += nota;
        }
        return soma / notas.length; // Media das notas fornecidas
    }

    private double calcularMediaPonderada() {
        double peso1 = 1;
        double peso2 = 2;
        double peso3 = 2;
        double soma = (notas[0] * peso1) + (notas[1] * peso2) + (notas[2] * peso3);
        return soma / (peso1 + peso2 + peso3); // Media ponderada pois existem 3 notas
    }

    private double calcularMediaComPesos() { 
        return (notas[0] * 0.15) + (notas[1] * 0.30) + (notas[2] * 0.10) + (notas[3] * 0.45); //Equaçao da media com 4 notas
    }

    public String situacao() { //Condiçao para o aluno ser aprovado com base na presença dele
        double notaFinal = calcularNotaFinal();
        if (isEAD) {
            return notaFinal >= 5 ? "Aprovado" : "Reprovado";
        } else {
            return (notaFinal >= 5 && presenca >= 75) ? "Aprovado" : "Reprovado";
        }
    }

    public void SituacaoDoAluno() { //Modelo Visual de como sera rodado as informações fornecidas pela universidade
        System.out.println("Nome: " + nome);
        System.out.println("RA: " + ra);
        System.out.println("Nota Final: " + calcularNotaFinal());
        System.out.println("Situação: " + situacao());
    }

    public static void main(String[] args) {
        Aluno aluno = new Aluno("João Carlos", "248152", false);
        aluno.setNotas(7.0, 8.0, 6.0, 9.0);
        aluno.setPresenca(80.0); // 80% de presença
        aluno.SituacaoDoAluno();
    }
}

### 🔧 Instalação

* Explicação de como deve ser utilizado o projeto

## 🛠️ Construído com

Ferramentas utilizadas e bibliotecas

* IDE Eclipse

## 📌 Versão

* **Versão 1.0** caso seja atualizado manter a descrição inicial e inserir uma nova linha com descrição da atualização.
* **Versão 1.1** - *Refatoração* *data 09/09/24*

## ✒️ Autores

João Carlos Ferreira de Araujo RA 248152 -- AC1 de Programação Orientada à Objetos

