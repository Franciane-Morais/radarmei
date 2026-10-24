# Radar MEI

**Responsável pelo projeto: Franciane de Morais Silva.**

Consulta auxiliar de licitações para microempreendedores, desenvolvida com apoio de ferramentas de inteligência artificial.

## Executar

Instale Node.js 22.13 ou superior. Abra esta pasta no terminal (PowerShell ou VS Code no Windows):

```bash
npm install
npm run dev
```

Acesse http://localhost:3000. Para encerrar, pressione Ctrl+C.

```bash
npm test
npm run typecheck
npm run build
npm start
```

O primeiro `npm install` gera `package-lock.json`; envie-o ao GitHub para registrar as versões instaladas. Nas próximas instalações, use `npm ci`.

## Enviar ao GitHub

1. Extraia o ZIP e abra a pasta `radar-mei`.
2. Crie um repositório chamado `radar-mei` na sua conta.
3. Use **Add file → Upload files** e envie o conteúdo da pasta, preservando a estrutura.
4. `README.md` e `package.json` devem aparecer na raiz do repositório. Inclua `.gitignore`.
5. Não envie `node_modules`, `.next`, arquivos `.env` ou credenciais. Não envie apenas o ZIP se quiser disponibilizar o código navegável.

Ou use Git, depois de criar um repositório vazio (substitua SEU_USUARIO):

```bash
git init
git add .
git commit -m "Projeto Radar MEI - Franciane de Morais Silva"
git branch -M main
git remote add origin https://github.com/SEU_USUARIO/radar-mei.git
git push -u origin main
```

Nenhum repositório foi criado automaticamente. Use a autenticação da sua própria conta.

## Estrutura e funcionalidades

| Arquivo | Função |
| --- | --- |
| `app/page.tsx` | Perfil de produtos, filtros, resultados e favoritos |
| `app/company-panel.tsx` | CNPJ e roteiro de documentos |
| `app/globals.css` | Layout e adaptação para celular |
| `app/layout.tsx` | Metadados e autoria |
| `app/api/tenders/route.ts` | Consulta de propostas abertas no PNCP |
| `app/api/company/route.ts` | Consulta cadastral pela BrasilAPI |
| `lib/product-filter.ts` | Categorias e correspondência de produtos |
| `lib/company.ts` | Validação de CNPJ e seleção dos dados |
| `tests/` | Testes das regras |

## Fontes e limitações

- PNCP: https://pncp.gov.br/api/consulta/swagger-ui/index.html
- BrasilAPI: https://brasilapi.com.br/docs — consulta por meio da Minha Receita, não diretamente e em tempo real na Receita Federal.
- Receita Federal: https://solucoes.receita.fazenda.gov.br/Servicos/cnpjreva/

As integrações atuais não exigem chaves e dependem de disponibilidade e conectividade com as fontes externas.

A busca carrega 50 registros por página. Os filtros de produtos, objeto, órgão e município atuam apenas nos registros carregados, não no universo inteiro do PNCP. A classificação por palavras no objeto não lê anexos. Editais mistos podem aparecer se incluírem um produto selecionado. Termos específicos são comparados literalmente após normalização de acentos e pontuação.

O cadastro do CNPJ não comprova regularidade fiscal nem habilitação. Alvarás, certidões, licenças e documentos não são consultados automaticamente. O roteiro mostra “não verificado” e distingue anotações feitas pelo usuário. O CNAE não determina sozinho a elegibilidade. O formato alfanumérico de CNPJ é validado, mas sua consulta automática ainda não é suportada neste projeto.

Perfil de produtos e favoritos são guardados no navegador. CNPJ, resultado e anotações ficam somente em memória durante a sessão da página. Ao consultar, o CNPJ é enviado à BrasilAPI. Não há contas, banco de usuários, notificações ou integração com diários oficiais.

## Aviso de responsabilidade

Ferramenta auxiliar independente para facilitar a pesquisa de quem tem pouca familiaridade com licitações. Pode apresentar erros, omissões e dados desatualizados por mudanças nos sistemas de origem. Não garante exatidão, completude, atualização ou habilitação. Confirme informações, documentos, prazos e retificações nas fontes oficiais.

O site reúne e relaciona dados de terceiros. Não assume responsabilidade pelo conteúdo produzido pelos portais de origem nem por decisões baseadas exclusivamente na consulta, respeitadas as responsabilidades previstas na legislação aplicável. O aviso não representa isenção absoluta de responsabilidade.

## Hospedagem

Esta edição usa Next.js e servidor Node.js para execução fora do ambiente original. O código funcional foi preservado, e os comandos de execução foram adaptados. Identificadores privados da hospedagem anterior não estão incluídos.

**GitHub armazena o código; GitHub Pages sozinho não executa as rotas de API deste projeto.** Use hospedagem compatível com Next.js e backend Node.js. Não use exportação estática sem substituir o backend.

## Estado das integrações

Os testes automatizados validam regras locais, sem depender das fontes externas. A consulta PNCP não respondeu nos testes anteriores. A fonte de CNPJ respondeu ao teste direto, mas houve falha no teste pela interface. As integrações não estão plenamente validadas de ponta a ponta em produção. A aplicação informa falhas e não usa editais fictícios.

## Autoria e licença

Projeto sob responsabilidade de **Franciane de Morais Silva**, conforme identificação fornecida. Esta edição traz essa identificação no README, nos metadados e no rodapé do site.

Nenhuma licença de código aberto foi escolhida neste pacote. Publicar no GitHub não equivale a conceder licença de reutilização. As dependências mantêm suas próprias licenças.

## Localizar no mapa

A seção Mapa permite pesquisar uma instituição por nome, cidade e UF. Os editais com órgão e município informados incluem um link para localizar o órgão. Os links abrem uma pesquisa externa no Google Maps, não um endereço confirmado nem um mapa incorporado. Podem existir várias unidades. Confira o endereço antes de visitar; estar no mapa não comprova oportunidade aberta ou compra local. A busca não depende da resposta do PNCP.

Arquivos: `app/map-search.tsx` e `lib/maps.ts`. Não exige chave do Google Maps.

## Organização em páginas

- `/`: início e atalhos.
- `/editais`: perfil de produtos, busca e favoritos.
- `/mapa`: localização de instituições.
- `/minha-empresa`: CNPJ e conferência de documentos.
- `/como-usar`: orientações, fontes e limites.

Favoritos e perfil permanecem no navegador. Resultados de busca, CNPJ e anotações são temporários e podem ser perdidos ao mudar de página.

## Maria — aplicativo web para tablet

Acesse `/assistente`. Inclui personagem CSS animada, orientações por assuntos, transcrição Web Speech (quando suportada), leitura de respostas por speechSynthesis e instalação PWA. Não é IA generativa, APK, assistente do sistema Android ou serviço em segundo plano. Não realiza consultas em nome da pessoa.

No Chrome do Android, abra o endereço HTTPS da aplicação e use Instalar no tablet ou o menu Instalar aplicativo / Adicionar à tela inicial. A instalação depende do suporte e dos critérios do navegador; a publicação privada exige conta autorizada. Nenhum teste em tablet físico foi realizado nesta entrega.

Microfone somente após consentimento e ação da pessoa. Áudio pode ser processado pelo serviço de reconhecimento do navegador. Transcrição exige revisão e envio manual. Conversa não é persistida nem enviada a um provedor de IA. Não informe dados sensíveis. A voz é escolhida entre as disponíveis no aparelho; não há voz feminina garantida. O microfone e a leitura são interrompidos ao ocultar a página ou sair dela.

O service worker não armazena páginas privadas nem respostas de APIs. Sem rede, exibe aviso em novas navegações; não oferece consultas offline. Manifesto em `public/manifest.webmanifest`, ícones em `public/icons/`. HTTPS necessário em produção.

Verificação adicional: `node --test tests/assistant.test.ts` (Node 22.13+ com suporte a TypeScript).
