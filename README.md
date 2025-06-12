SQL
CREATE DATABASE SistemaReceitas;
USE SistemaReceitas;

-- Tabela de usuários
CREATE TABLE Usuario (
    id_usuario INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    senha VARCHAR(100) NOT NULL
);

-- Tabela de categorias de receitas
CREATE TABLE Categoria (
    id_categoria INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(50) NOT NULL
);

-- Tabela de receitas
CREATE TABLE Receita (
    id_receita INT AUTO_INCREMENT PRIMARY KEY,
    titulo VARCHAR(100) NOT NULL,
    descricao TEXT,
    tempo_preparo INT, -- minutos
    rendimento VARCHAR(50),
    id_usuario INT,
    id_categoria INT,
    FOREIGN KEY (id_usuario) REFERENCES Usuario(id_usuario),
    FOREIGN KEY (id_categoria) REFERENCES Categoria(id_categoria)
);

-- Tabela de ingredientes
CREATE TABLE Ingrediente (
    id_ingrediente INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL
);

-- Tabela associativa entre receitas e ingredientes
CREATE TABLE Receita_Ingrediente (
    id_receita INT,
    id_ingrediente INT,
    quantidade DECIMAL(6,2),
    unidade VARCHAR(20),
    PRIMARY KEY (id_receita, id_ingrediente),
    FOREIGN KEY (id_receita) REFERENCES Receita(id_receita),
    FOREIGN KEY (id_ingrediente) REFERENCES Ingrediente(id_ingrediente)
);

-- Tabela de etapas de preparo
CREATE TABLE Etapa_Preparo (
    id_etapa INT AUTO_INCREMENT PRIMARY KEY,
    id_receita INT,
    ordem INT,
    descricao TEXT,
    FOREIGN KEY (id_receita) REFERENCES Receita(id_receita)
);

-- Tabela de comentários
CREATE TABLE Comentario (
    id_comentario INT AUTO_INCREMENT PRIMARY KEY,
    id_receita INT,
    id_usuario INT,
    texto TEXT NOT NULL,
    data DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (id_receita) REFERENCES Receita(id_receita),
    FOREIGN KEY (id_usuario) REFERENCES Usuario(id_usuario)
);
