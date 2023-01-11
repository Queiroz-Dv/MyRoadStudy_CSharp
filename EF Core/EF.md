<h1 style="color: #FFFAF0"> 💻 Entity Framework Core </h1>

<div>
<fieldset style="border-style: outset">
    <legend  style="color: #00CED1">Introdução</legend>
    <p>O Entity Framework Core é a nova versão do Entity Framework 6.x.
        O EF Core é uma ferramenta ORM (<strong style="color: #00FFFF">Object Relational Mapping</strong>), ele abstrai os objetos <strong> ADO .NET </strong> e os comandos <strong>SQL</strong>
    </p>
</fieldset>
</div><br>

<div>
    <fieldset  style="border-style: outset">
        <legend style="color: #00CED1">ORM e Modelagem de Dados</legend>
        <strong style="color: #00FFFF">ORM</strong> é uma ferramenta para armazenar dados de objetos de domínio para o banco de dados relacional de forma automática e sucinta.
        <h2 style="color: #FFFAF0"> 🧩 Abordagens</h2>
        <ul>
            <li><strong>Code First:</strong></li>
            <p>
                Cria o banco de dados e tabelas usando a <i style="color: #7FFFD4">migração</i> com base nas <i style="color: #7FFFD4">conveções</i> e configuração fornecidas nas classes do seu domínio.
                Essa abordagem é útil no DDD(Domain Driven Design).
            </p>
            <li><strong>Database First:</strong></li>
            <p>
                Cria as classes de domínio e contexto com ase em um banco de dados eistente
                usando os comandos do EF Core.
                Com suporte limitado no EF Core; não suporta designer visual ou assistente.
            </p>
        </ul>
    </fieldset>
</div><br>

<div>
    <fieldset  style="border-style: outset">
        <legend  style="color: #00CED1"> O Modelo de Acesso a Dados</legend>
        <div>
        <p>
            No EF Core, o acesso a dados é executado usando um <i style="color: #7FFFD4">modelo</i>.
        </p>
        <p>
            Um modelo é composto de <i style="color: #7FFFD4">classes de entidade</i> e um <i style="color: #7FFFD4">contexto</i> derivado que representa uma sessão com o banco de dados, permitindo que você pesquise e salve dados.
        </p>
        </div>
        <session>
            <p>Podemos criar um modelo usando as seguintes abordagens:</p>
            <ol>
                <li>
                    Gerar um <i style="color: #7FFFD4">modelo</i> a partir de um <i style="color: #7FFFD4">banco de dados existente</i>;
                </li>
                <li>
                    Codificar manualmente um <i style="color: #7FFFD4">modelo</i> para corresponder ao seu banco de dados;
                </li>
                <li>
                    Usar o <i style="color: #7FFFD4">EF Migrations</i> para criar um banco de dados a partir do seu <i style="color: #7FFFD4">modelo</i><em>(e depois evoluí-lo conforme seu modelo muda ao longo do tempo).</em>
                </li>
            </ol>
        </session>
    </fieldset>
</div>
<div>
    <fieldset style="border-style: outset">
        <legend  style="color: #00CED1">Projeto em Code First</legend>
    <fieldset>
        <legend style="color: #FFFAF0">Definir o modelo de entidades</legend>
        <ul>
        <li> Criar a classe definindo as propriedades que vão representar o meu domínio</li>
        <li> Produto, Categoria, Cliente, Aluno, etc.</li>
        </ul>
    </fieldset>
    <br>
    <fieldset>
        <legend style="color: #FFFAF0">Definir a classe de contexto</legend>
        <ul>
        <li> <i style="color: #7FFFD4">Cria a classe que herda de</i> DbContext</li>
        <li> <i style="color: #7FFFD4">Mapear as entidades para as tabelas via propriedades</i> DbSet</li>
        <li><i style="color: #7FFFD4"> Usar o método</i> OnConfiguring<i style="color: #7FFFD4"> para definir o provedor e a string de conexcão</i></li>
        </ul>
    </fieldset>
    <br>
    <fieldset>
        <legend style="color: #FFFAF0">Usar o Migrations</legend>
        <ul>
        <li> add-migration</li>
        <li> Update-database</li>
        </ul>
    </fieldset>
    </fieldset>
</div>

## 🧭 Propriedades de Navegação

Uma **propriedade de navegação** é definida na **entidade principal ou dependente** que contém uma referência para a entidade relacionada.

```c#
public class Autor 
{
    public int AutorId {get; set;}
    public string Nome {get; set;}
    public string Sobrenome {get; set;}
    public ICollection<Livros> Livros {get; set;} // Propriedade de navegação de Coleção
}
```

```c#
public class Livro 
{
    public int LivroId {get; set;}
    public string Titulo {get; set;}
    public int AnoLancamento {get; set;}
    public Autor Autor {get; set;} // Propriedade de navegação de Referência
}
```

As propriedades de navegação permitem a **navegação da associação** entre os **tipos** via código: