```sql
-- Criar Banco de Dados ExpressoLanches
IF NOT EXISTS (SELECT * FROM sys.databases WHERE name = 'ExpressoLanches')
BEGIN
    CREATE DATABASE ExpressoLanches;
END
GO

-- Utilizar o Banco de Dados ExpressoLanches
USE ExpressoLanches;
GO

-- Tabela de Categorias
IF NOT EXISTS (SELECT * FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_NAME = 'Categorias')
BEGIN
    CREATE TABLE Categorias (
        CategoriaID INT PRIMARY KEY,
        NomeCategoria VARCHAR(255) NOT NULL
    );
END
GO

-- Tabela de Fornecedores
IF NOT EXISTS (SELECT * FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_NAME = 'Fornecedores')
BEGIN
    CREATE TABLE Fornecedores (
        FornecedorID INT PRIMARY KEY,
        NomeFornecedor VARCHAR(255) NOT NULL,
        CNPJ VARCHAR(14) NOT NULL,
        Endereco VARCHAR(255) NOT NULL,
        Telefone VARCHAR(15) NOT NULL
    );
END
GO

-- Tabela de Clientes
IF NOT EXISTS (SELECT * FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_NAME = 'Clientes')
BEGIN
    CREATE TABLE Clientes (
        ClienteID INT PRIMARY KEY,
        NomeCliente VARCHAR(255) NOT NULL,
        CPF VARCHAR(11) NOT NULL,
        Endereco VARCHAR(255) NOT NULL,
        Email VARCHAR(255) NOT NULL,
        Telefone VARCHAR(15) NOT NULL
    );
END
GO

-- Tabela de Produtos
IF NOT EXISTS (SELECT * FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_NAME = 'Produtos')
BEGIN
    CREATE TABLE Produtos (
        ProdutoID INT PRIMARY KEY,
        NomeProduto VARCHAR(255) NOT NULL,
        Preco DECIMAL(10,2) NOT NULL,
        Estoque INT NOT NULL,
        CategoriaID INT,
        FornecedorID INT,
        FOREIGN KEY (CategoriaID) REFERENCES Categorias(CategoriaID),
        FOREIGN KEY (FornecedorID) REFERENCES Fornecedores(FornecedorID)
    );
END
GO

-- Tabela de Pedidos
IF NOT EXISTS (SELECT * FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_NAME = 'Pedidos')
BEGIN
    CREATE TABLE Pedidos (
        PedidoID INT PRIMARY KEY,
        ClienteID INT,
        DataPedido DATETIME NOT NULL,
        StatusPedido VARCHAR(50) NOT NULL,
        FOREIGN KEY (ClienteID) REFERENCES Clientes(ClienteID)
    );
END
GO

-- Tabela de Itens de Pedido
IF NOT EXISTS (SELECT * FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_NAME = 'ItensPedido')
BEGIN
    CREATE TABLE ItensPedido (
        ItemID INT PRIMARY KEY,
        PedidoID INT,
        ProdutoID INT,
        Quantidade INT NOT NULL,
        PrecoUnitario DECIMAL(10,2) NOT NULL,
        FOREIGN KEY (PedidoID) REFERENCES Pedidos(PedidoID),
        FOREIGN KEY (ProdutoID) REFERENCES Produtos(ProdutoID)
    );
END
GO


```

![Captura de tela 2023-11-12 213148](https://github.com/rubenslyra/expresso-lanches/assets/37023108/098fa2b0-2e77-45f8-91f2-50ffc12acf63)

