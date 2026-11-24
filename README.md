# Autopilot Hash Generator

Programa para Windows com interface gráfica para **gerar o hash de hardware (Windows Autopilot)** de um
equipamento e **juntar vários CSVs** em um único arquivo, pronto para importar no
**Microsoft Intune / Entra ID**. Sem instalar nada: é um único `.exe`.

> **Versão 1.0.** Teste primeiro em uma máquina e confira se o CSV gerado importa no seu Intune.

## Baixar

Vá em [**Releases**](../../releases) e baixe o `Autopilot-Hash-Generator.exe`.

## Como usar

1. Dê duplo clique no `Autopilot-Hash-Generator.exe` e aceite o aviso de administrador do Windows.
2. Em **Gerar o hash deste equipamento**, escolha a pasta onde salvar (padrão `C:\temp`) e clique em **GERAR HASH**.
3. Para importar vários equipamentos de uma vez, use **Juntar CSVs para importação**: escolha a pasta onde
   estão os arquivos `.csv`, a pasta onde quer salvar, o nome do arquivo e clique em **JUNTAR CSVs**.
4. Importe o arquivo no Intune: *Dispositivos > Windows > Registro do Windows > Dispositivos do Windows
   Autopilot > Importar*.

## O que ele faz

- Detecta serial, fabricante, modelo e nome do computador.
- Gera o CSV `<serial>.csv` com o hash de hardware, com **Group Tag** opcional.
- Valida se o CSV realmente contém o hash antes de indicar sucesso.
- Junta todos os `.csv` de uma pasta em um único arquivo e remove seriais duplicados.
- Lembra as últimas pastas usadas.

## Requisitos

- Windows 10 ou 11, com conta de administrador local.
- Equipamento físico: em máquinas virtuais, ou sem suporte a WMI/MDM, o hash pode não ser gerado.

## Aviso do Windows / antivírus

O `.exe` **não é assinado digitalmente**, então o Windows pode mostrar "O Windows protegeu seu PC":
clique em **Mais informações > Executar assim mesmo**. Alguns antivírus também podem alertar, porque o
programa abre o PowerShell internamente. Confira o hash **SHA-256** da página da Release:

```
certutil -hashfile Autopilot-Hash-Generator.exe SHA256
```

## Privacidade

O programa funciona totalmente offline e não envia nenhum dado. O hash de hardware identifica o equipamento
no seu tenant: **não publique os CSVs gerados**.

## Feedback

Encontrou um problema ou tem uma sugestão? Abra uma **[Issue](../../issues)** e informe:
versão do Windows, o que você fez e a mensagem de erro (se houver).

## Créditos

O coletor de hash é o `Get-WindowsAutoPilotInfo.ps1` da Microsoft (licença MIT), incluído sem alterações.
Veja `THIRD-PARTY-NOTICES.txt`.

---
O código-fonte não é público neste repositório.
