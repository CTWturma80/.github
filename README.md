# WEG OS – Sistema de Gestão de Ordens de Serviço e Ocorrências

Projeto Integrador – Java + MySQL

## Descrição Geral
Este repositório organiza os projetos desenvolvidos pelos grupos da turma para a Situação de Aprendizagem Integrada 
**WEG OS**.  
O objetivo é implementar um sistema completo de **gestão de Ordens de Serviço (OS)** para manutenções industriais, utilizando **Java**, **POO**, **exceções personalizadas**, **JDBC** e **MySQL**.

Cada grupo possui seu próprio repositório dentro desta organização, com autonomia para criar o modelo de classes e soluções, mantendo as regras de negócio definidas neste documento.


# 1. Objetivo do Sistema
O sistema deve permitir o gerenciamento de:

- Usuários (Técnico, Supervisor, Gerente)  
- Máquinas e setores  
- Ordens de Serviço (preventivas, corretivas e preditivas)  
- Custos das manutenções  
- Ocorrências automáticas geradas por repetição de OS corretivas  
- Relatórios por perfil de acesso  

A dor fícticia é o controle atual da empresa WEG ser manual. O novo sistema elimina erros, reduz retrabalho e melhora a rastreabilidade das manutenções.


# 2. Funcionalidades Obrigatórias

## 2.1 Cadastro e Login de Usuários
Controle de permissões:

|     Perfil     |                          Permissões                         |
|----------------|-------------------------------------------------------------|
| **Técnico**    | Executa e encerra OS atribuídas                             |
| **Supervisor** | Abre OS; acompanha OS do setor; trata Ocorrências pendentes |
| **Gerente**    | Acesso total, cria usuários, consulta todos os relatórios   |


# 2.2 Gestão de Máquinas
- Cadastro de máquina  
- Status (funcionando, parada, manutenção)  
- Relacionamento com setor  
- Listagem por setor  


# 2.3 Ordens de Serviço
Tipos:  
- **Corretiva**  
- **Preventiva**  
- **Preditiva**  

Campos obrigatórios: técnico, máquina, setor, tipo, custos, status, datas etc.


# 3. Regra de Negócio: Ocorrências

## 3.1 Geração Automática
Criar uma Ocorrência quando:
- A mesma máquina no mesmo setor registrar **3 OS corretivas** e **não existir OS Preditiva ativa**

Status inicial: **Pendente**


## 3.2 Supervisor – Fila de Ocorrências
Supervisor visualiza apenas ocorrências pendentes do seu setor.

Ação obrigatória:

Gerar OS Preditiva.

Após gerar, a ocorrência muda para **Em Tratamento** e some da lista.


## 3.3 Gerente – Relatório Completo
Relatório com todas as ocorrências, filtros por setor, supervisor e status.  
A ocorrência tratada aparece como **Em Tratamento**, vinculada à OS preditiva.


## 3.4 Ciclo de Vida da Ocorrência
A ocorrência permanece em **Em Tratamento** até a OS preditiva ser concluída.  
Após isso, muda automaticamente para **Concluída**.


# 4. Estrutura Obrigatória de Pacotes
model/ → Classes principais + interfaces
exception/ → Exceções personalizadas
database/ → Conexão JDBC
repository/ → CRUD
util/ → Funções auxiliares
view/ → Menus (console)
main/ → Método main()


# 5. Etapas do Desenvolvimento

### 5.1 Configuração Inicial
- Criar banco MySQL, tabelas e conexão JDBC.  
- Montar a estrutura de pacotes e modelos básicos.

### 5.2 Autenticação e Perfis
- Implementar login, CRUD de usuários e permissões por função.

### 5.3 Cadastro e Gestão de Recursos
- CRUD de máquinas, setores e ordens de serviço.  
- Atualizar o status das máquinas conforme as OS.

### 5.4 Regra de Ocorrências
- Detectar 3 OS corretivas → gerar Ocorrência automaticamente.  
- Supervisor gera OS Preditiva → ocorrência entra em tratamento.  
- Encerrar OS Preditiva → ocorrência é concluída.

### 5.5 Relatórios
- Consultas e filtros para Gerente (OS, máquinas e ocorrências).

### 5.6 Interface por Console
- Menus por perfil e validação das entradas do usuário.

### 5.7 Testes e Documentação
- Testar regras, CRUDs e fluxos.  
- Atualizar README, script SQL e entregar a versão final.
