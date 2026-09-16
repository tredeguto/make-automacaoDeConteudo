# 🎭 Automação de Curadoria e Geração de Conteúdo Cultural

Este projeto é um fluxo automatizado construído no **Make.com** para ler feeds de notícias e artigos do setor cultural, gerar redações otimizadas para redes sociais via **Gemini AI**, classificar a necessidade de imagem real vs. gerada por IA e enviar o resultado para aprovação final por e-mail.

---

## 📌 Funcionalidades

- **Curadoria via RSS**: Lida a partir de uma planilha do Google Sheets com links e fontes de notícias.
- **Redação Inteligente**: Utiliza o **Gemini 3.5 Flash** para estruturar legendas com ganchos, hashtags e citações automáticas de fonte.
- **Classificação Automática**: Usa o **Gemini 3.5 Flash Lite** para determinar se a pauta exige a foto original do feed (`REAL`) ou se pode utilizar uma imagem conceitual gerada por IA (`GERAR`).
- **Geração de Imagens**: Integração com a API do Pollinations AI para pautas conceituais.
- **Armazenamento e Notificação**: Salva as imagens geradas/baixadas no Google Drive e envia um e-mail em HTML para o curador aprovar o conteúdo.

---

## 🛠️ Arquitetura do Fluxo

```text
[Google Sheets] ➔ [RSS Reader] ➔ [Gemini: Redação] ➔ [Google Sheets: Catalogar]
                                        │
                                        ▼
                                [Gemini: Classificador]
                                        │
                     ┌──────────────────┴──────────────────┐
                     ▼                                     ▼
             [Branch 1: REAL]                      [Branch 2: GERAR]
            Download Imagem RSS                   Requisição Pollinations AI
                     │                                     │
                     └──────────────────┬──────────────────┘
                                        ▼
                              [Google Drive: Upload]
                                        │
                                        ▼
                              [Gmail: Enviar Aprovação]
