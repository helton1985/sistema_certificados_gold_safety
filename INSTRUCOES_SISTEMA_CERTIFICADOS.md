# Sistema de Automação de Certificados - Gold Safety

## Visão Geral

Este sistema automatiza a geração de certificados PEMT (Plataforma Elevatória Móvel de Trabalho) baseado no modelo fornecido. O sistema permite:

- **Geração individual**: Criar um certificado por vez
- **Geração em lote**: Criar múltiplos certificados de uma vez e baixar em arquivo ZIP
- **Interface web intuitiva**: Fácil de usar, sem necessidade de conhecimento técnico
- **Campos personalizáveis**: Nome, CPF, treinamento, empresa, carga horária e data

## Campos Variáveis Identificados

Com base no modelo de certificado fornecido, os seguintes campos são automaticamente preenchidos:

1. **Nome Completo** (sempre em maiúsculo)
2. **CPF** (formato: 000.000.000-00)
3. **Treinamento** (padrão: "FORMAÇÃO DE SERGUANÇA EM PLATAFORMA ELEVATÓRIA MÓVEL DE TRABALHO - PEMT")
4. **Empresa** (padrão: "Johnson Controls Hitachi")
5. **Carga Horária** (padrão: "8 (oito) horas")
6. **Data** (formato: "15 de Julho de 2025")

## Funcionalidades

### 1. Certificado Individual
- Preencha os dados de um participante
- Clique em "Gerar Certificado"
- O PDF será baixado automaticamente

### 2. Certificados em Lote
- Configure as informações globais (treinamento, empresa, horas, data)
- Adicione participantes um por um (nome e CPF)
- Clique em "Gerar Todos os Certificados"
- Um arquivo ZIP com todos os certificados será baixado

## Estrutura do Projeto

```
certificate-generator/
├── src/
│   ├── main.py                 # Aplicação Flask principal
│   ├── routes/
│   │   ├── certificate.py      # Rotas para geração de certificados
│   │   └── user.py            # Rotas de usuário (template)
│   ├── models/
│   │   └── user.py            # Modelos de banco (template)
│   ├── static/
│   │   ├── index.html         # Interface web
│   │   └── certificado.pdf    # Modelo de certificado
│   └── database/
│       └── app.db             # Banco SQLite
├── venv/                      # Ambiente virtual Python
├── requirements.txt           # Dependências
└── README.md
```

## Como Executar Localmente

### Pré-requisitos
- Python 3.8 ou superior
- pip (gerenciador de pacotes Python)

### Passos para Instalação

1. **Navegue até o diretório do projeto:**
   ```bash
   cd certificate-generator
   ```

2. **Ative o ambiente virtual:**
   ```bash
   source venv/bin/activate  # Linux/Mac
   # ou
   venv\Scripts\activate     # Windows
   ```

3. **Instale as dependências:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Execute a aplicação:**
   ```bash
   python src/main.py
   ```

5. **Acesse no navegador:**
   ```
   http://localhost:5000
   ```

## Tecnologias Utilizadas

### Backend
- **Flask**: Framework web Python
- **ReportLab**: Geração de PDFs
- **PyPDF2**: Manipulação de PDFs existentes

### Frontend
- **HTML5/CSS3**: Interface responsiva
- **JavaScript**: Interatividade e comunicação com API
- **Design responsivo**: Funciona em desktop e mobile

## API Endpoints

### POST /api/certificate/generate
Gera um certificado individual.

**Payload:**
```json
{
  "name": "João Silva Santos",
  "cpf": "123.456.789-00",
  "training": "FORMAÇÃO DE SERGUANÇA EM PLATAFORMA ELEVATÓRIA MÓVEL DE TRABALHO - PEMT",
  "company": "Johnson Controls Hitachi",
  "hours": "8 (oito) horas",
  "date": "15 de Julho de 2025"
}
```

**Resposta:** Arquivo PDF para download

### POST /api/certificate/generate-batch
Gera múltiplos certificados em um arquivo ZIP.

**Payload:**
```json
{
  "participants": [
    {
      "name": "João Silva Santos",
      "cpf": "123.456.789-00",
      "training": "FORMAÇÃO DE SERGUANÇA EM PLATAFORMA ELEVATÓRIA MÓVEL DE TRABALHO - PEMT",
      "company": "Johnson Controls Hitachi",
      "hours": "8 (oito) horas",
      "date": "15 de Julho de 2025"
    }
  ]
}
```

**Resposta:** Arquivo ZIP com todos os certificados

## Personalização

### Alterando o Modelo de Certificado
1. Substitua o arquivo `src/static/certificado.pdf` pelo novo modelo
2. Ajuste as coordenadas no arquivo `src/routes/certificate.py` na função `generate_certificate()`

### Modificando Campos Padrão
Edite os valores padrão no arquivo `src/static/index.html` ou na função `generate_certificate()`.

## Solução de Problemas

### Erro de Importação PIL/_imaging
Se encontrar erros relacionados ao PIL/Pillow durante o deploy:
```bash
pip uninstall pillow
pip install pillow --upgrade
```

### Certificados não são gerados
1. Verifique se o arquivo `certificado.pdf` está na pasta `src/static/`
2. Confirme que todas as dependências estão instaladas
3. Verifique os logs do Flask para erros específicos

### Interface não carrega
1. Certifique-se de que o Flask está rodando na porta 5000
2. Verifique se não há bloqueios de firewall
3. Acesse diretamente: `http://localhost:5000`

## Melhorias Futuras

1. **Upload de planilha**: Permitir upload de arquivo Excel/CSV com lista de participantes
2. **Templates múltiplos**: Suporte a diferentes modelos de certificado
3. **Assinatura digital**: Integração com certificados digitais
4. **Histórico**: Manter registro dos certificados gerados
5. **Autenticação**: Sistema de login para controle de acesso

## Suporte

Para dúvidas ou problemas:
1. Verifique os logs do Flask no terminal
2. Confirme que todas as dependências estão instaladas
3. Teste primeiro com um certificado individual antes do lote

## Licença

Sistema desenvolvido para Gold Safety - Uso interno.

