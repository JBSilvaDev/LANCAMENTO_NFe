
# LANCAMENTO_NFe - Automação de Lançamento de Notas Fiscais Eletrônicas

Este projeto de automação, desenvolvido com UiPath no padrão REFramework, tem como objetivo automatizar o processo de leitura de e-mails, extração de dados de faturas em PDF, lançamento dessas informações em um sistema "Contoso Invoicing" e consolidação dos dados em uma planilha Excel.

**link do repositório:** https://github.com/JBSilvaDev/LANCAMENTO_NFe

## Funcionalidades Principais

*   **Leitura de E-mails**: Acessa uma caixa de e-mail (IMAP) para buscar faturas.
    *   Filtra e-mails por assunto ("Fatura").
    *   Salva anexos em formato PDF na pasta `Data\Attachments`.
    *   Move os e-mails processados para a pasta `Processed_Invoices` na caixa de entrada.
*   **Processamento de PDFs**:
    *   Converte faturas em PDF para texto.
    *   Extrai informações cruciais (Data, Nome da Conta, E-mail de Contato, Valor Total) utilizando Expressões Regulares (Regex).
    *   **Recurso Adicional**: Para informações detalhadas sobre as expressões regulares utilizadas, acesse o e-book no repositório: [https://github.com/JBSilvaDev/Regex](https://github.com/JBSilvaDev/Regex)
*   **Lançamento no Sistema Contoso Invoicing**:
    *   Interage com a aplicação desktop "Contoso Invoicing" (`legacyinvoicingapp.exe`).
    *   Preenche automaticamente os campos de lançamento com os dados extraídos do PDF.
    *   Define o status da fatura como "Invoiced" (Faturado) e recupera o ID gerado pelo sistema.
*   **Consolidação de Dados**:
    *   Registra todos os dados processados (incluindo o ID do Contoso) em uma tabela de dados em memória.
    *   Após o processamento de todas as faturas, exporta e anexa esses dados a uma planilha Excel de reconciliação (`Data\Output\Reconciliation.xlsx`).
*   **Organização de Arquivos**:
    *   Renomeia os arquivos PDF e TXT processados com um carimbo de data/hora (`AAAAMMDDhhmmss_NomeOriginal.pdf/.txt`).
    *   Move os arquivos PDF e TXT renomeados para a pasta `Data\Processed` para manter um registro organizado.

## Pré-requisitos

*   **UiPath Studio**: Para executar e desenvolver o projeto.
*   **Sistema Contoso Invoicing**: A aplicação desktop `legacyinvoicingapp.exe` deve estar instalada e acessível.
*   **Acesso à Caixa de E-mail**: Credenciais de IMAP para a caixa de e-mail que recebe as faturas.

## Configuração

1.  **Credenciais de E-mail**:
    *   Abra o arquivo `Data\Config.xlsx`.
    *   Na planilha `Constants`, insira os valores para `Email` e `SenhaApp` (senha de aplicativo, se estiver usando autenticação de dois fatores ou aplicativos de terceiros).
    *   Certifique-se de que `Porta` e `ServerGoogleIMAP` (ou o servidor IMAP correspondente) estejam configurados corretamente.

2.  **Configurações do Projeto**:
    *   Outras configurações podem ser ajustadas na planilha `Settings` do `Config.xlsx`, conforme necessário para o ambiente.

## Como Executar

1.  Abra o projeto no UiPath Studio.
2.  Verifique se todas as dependências estão resolvidas (podem ser restauradas automaticamente ou manualmente através do Gerenciador de Pacotes).
3.  Execute o arquivo `Main.xaml`.

O robô iniciará o processo, lendo e-mails, processando faturas e atualizando o sistema e a planilha de reconciliação.

*Este RPA foi criado como parte do desafio do curso "Automatize Processos com Erimatéia".*
