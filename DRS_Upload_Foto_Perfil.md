# 🧾 Documento de Requisitos de Software (DRS)

**Projeto:** Sistema de Cadastro de Usuários  
**Módulo / Área:** Upload de Foto de Perfil  
**Tipo:** Feature  
**Autor:** Equipe de Desenvolvimento  
**Data:** 11/11/2025  
**Versão:** v1.0

---

## 1. 📋 Resumo
Implementar a funcionalidade de upload de foto de perfil no cadastro de usuários, permitindo validação de tamanho e formato da imagem.

## 2. 🎯 Objetivo / Problema
Usuários não conseguem alterar sua foto de perfil. Essa limitação impacta a personalização da conta e a experiência do usuário.

## 3. 🔍 Escopo

**Inclui:**
- Implementação do endpoint `/api/usuarios/foto`
- Validação de formato (JPEG/PNG)
- Salvamento em Azure Blob Storage

**Não inclui:**
- Edição ou recorte de imagens
- Integração com CDN

## 4. ⚙️ Requisitos Funcionais (RF)

| ID | Descrição | Prioridade | Critério de Aceite |
|----|------------|-------------|--------------------|
| RF-01 | O sistema deve permitir o upload de fotos de até 2MB. | Alta | Ao tentar enviar uma foto >2MB, o sistema deve exibir mensagem de erro. |
| RF-02 | O sistema deve aceitar apenas formatos JPEG e PNG. | Média | Uploads em outros formatos devem ser rejeitados. |
| RF-03 | O sistema deve armazenar a imagem no Azure Blob Storage. | Alta | URL gerada deve ser acessível via SAS Token válido. |

## 5. 🧱 Requisitos Não Funcionais (RNF)

| ID | Descrição | Categoria |
|----|------------|------------|
| RNF-01 | O tempo de upload não deve ultrapassar 10 segundos. | Performance |
| RNF-02 | O endpoint deve requerer autenticação JWT. | Segurança |
| RNF-03 | A aplicação deve registrar logs de erro no Application Insights. | Observabilidade |

## 6. 🔄 Fluxo da Solução

1. Usuário envia a imagem via formulário.  
2. Front-end converte para base64 e envia via POST.  
3. Back-end valida tamanho e formato.  
4. Imagem é armazenada no Blob Storage.  
5. URL de acesso é retornada ao front-end.

## 7. 🧪 Critérios de Teste / Casos de Uso

| Caso | Descrição | Resultado Esperado |
|------|------------|--------------------|
| CT-01 | Upload de imagem PNG de 1.5MB | Upload realizado com sucesso. |
| CT-02 | Upload de imagem de 3MB | Erro: “Tamanho máximo permitido é 2MB.” |
| CT-03 | Upload sem token JWT | Erro: “Acesso não autorizado.” |

## 8. ⚠️ Impacto / Dependências
Depende do módulo de autenticação e do serviço Azure Storage.

## 9. 🔧 Tarefas Técnicas

| Nº | Descrição | Responsável | Status |
|----|------------|--------------|--------|
| 1 | Criar endpoint `/api/usuarios/foto` | Desenvolvedor | Pendente |
| 2 | Implementar validação de tamanho/formato | Desenvolvedor | Pendente |
| 3 | Criar SAS Token temporário para upload | DevOps | Pendente |

## 10. 🧩 Planos de Deploy / Rollback

- **Deploy:** via Azure DevOps Pipeline em ambiente Dev > Homolog > Prod  
- **Rollback:** restaurar versão anterior da API e limpar cache de CDN

## 11. ✅ Homologação e Validação

- **Ambiente de testes:** https://dev.sistema.com  
- **Responsável pela validação:** QA - Maria Silva  
- **Data prevista para homologação:** 20/11/2025

## 12. 📦 Release Notes

- Adicionada funcionalidade de upload de foto de perfil.  
- Corrigido erro 415 ao enviar arquivos PNG.  
- Melhorada mensagem de validação de tamanho de arquivo.

## 13. 📚 Referências

- Documentação da API: https://api.sistema.com/docs  
- Tarefa no Azure DevOps: #4587  
- Design no Figma: https://figma.com/file/XXXX
