# Trabalho 2 — Deploy automático em VM

## Integrantes
Eduardo Vieira Martins da Silva
Isabelly Hipoliti Lucantonio

## Aplicação
CRUD de produtos com PHP 8.2, MySQL 8, Docker, Docker Compose e GitHub Actions.

### Funcionalidades
- Create: cadastrar produto.
- Read: listar produtos.
- Update: editar produto.
- Delete: excluir produto.
- Banco MySQL persistente em volume Docker.

## Executar
Na pasta do projeto:
```bash
docker compose up -d --build
docker compose ps
```
Acesse `http://localhost:8080`. Para acessar de outro computador, configure a VM em modo Bridge ou encaminhamento de porta no VirtualBox e acesse `http://IP_DA_VM:8080`.

Para parar:
```bash
docker compose down
```
O volume `mysql-dados` preserva os registros. Não use `docker compose down -v` se quiser manter os dados.

## Deploy automático
O arquivo `.github/workflows/deploy.yml` executa em todo `push` para `main` ou manualmente pela aba Actions. O workflow faz checkout, verifica Docker, executa `docker compose up -d --build` e testa a resposta da aplicação.

### Runner
No GitHub: **Settings → Actions → Runners → New self-hosted runner → Linux → x64**. Siga os comandos exibidos na página para configurar o runner na VM. O token é temporário: não o publique nem o envie em fotos. Mantenha o runner online para os workflows executarem. Para serviço persistente, siga as instruções `svc.sh` do próprio GitHub.

Prefira repositório privado ao usar self-hosted runner. Não publique tokens ou senhas reais.

## Informações para entrega
- Sistema: Ubuntu 26.04.1 LTS
- IP da VM: preencher com a saída de `hostname -I`
- Porta: `8080`
- URL: `http://IP_DA_VM:8080`

## Estrutura
```text
.github/workflows/deploy.yml
app/conexao.php
app/criar.php
app/editar.php
app/excluir.php
app/index.php
database/init.sql
Dockerfile
docker-compose.yml
README.md
```
