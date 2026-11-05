# Requirements Document

## Introduction

Plataforma web com inteligência artificial que apoia mulheres a evoluírem na carreira em cloud. Ao abrir a página, a usuária responde a um questionário curto e acolhedor. A partir das respostas, a IA identifica o perfil, apresenta um leque de carreiras possíveis e monta um mapa de trajetória individual com trilhas de estudo, certificações, hackathons e vagas. Um chat com IA atua como mentora. A experiência inclui gamificação (pontos, conquistas, ranking opcional) e suporte a hábitos saudáveis de estudo (Pomodoro e pausas). Um calendário semanal mostra a disponibilidade de horários informada pela usuária, dividida pelos dias da semana, e distribui nela os blocos de estudo.

Os três pilares do produto são:

- **De onde você vem:** experiências e conhecimentos que a usuária já possui.
- **Onde você quer chegar:** carreira, especialização ou certificação desejada.
- **Como você vai chegar lá:** mapa com etapas, conteúdos, exercícios e oportunidades.

### Premissas

- Idioma da interface e do conteúdo: português do Brasil.
- Público-alvo: mulheres iniciantes em tecnologia, em transição de carreira, estudantes, profissionais em busca de certificações e pessoas buscando oportunidades.
- O foco de carreira é cloud, com áreas de Dados, Infraestrutura, Desenvolvimento, Segurança e IA.
- Não há cadastro obrigatório para responder ao questionário. A conta é pedida ao salvar o progresso.
- O catálogo de cursos, certificações, hackathons e competências é curado manualmente (arquivos versionados) na primeira versão. A IA seleciona e ordena itens do catálogo e não inventa links.

## Glossary

- **Sistema**: A plataforma web com inteligência artificial descrita neste documento.
- **Trilha**: Sequência personalizada de conteúdos, exercícios e atividades de estudo que leva a usuária à carreira objetivo.
- **Mapa de trajetória**: Representação visual da trilha em etapas ordenadas, com status e progresso de cada etapa.
- **Perfil**: Conjunto de informações geradas a partir das respostas do questionário e do currículo: tipo de jornada, nível por área, conhecimentos prévios, objetivos e lacunas.
- **Mentora**: Assistente de IA, acessível por chat, que orienta a usuária ao longo da jornada.
- **Bloco de estudo**: Intervalo de tempo agendado no calendário para uma atividade da trilha, um ciclo Pomodoro ou um simulado.
- **Disponibilidade**: Total de horas semanais e faixas de horário por dia da semana em que a usuária pode estudar.
- **Pomodoro**: Técnica de estudo com ciclos de foco e pausas curtas, com pausa longa a cada conjunto de ciclos.
- **Catálogo**: Base curada de cursos, certificações, hackathons, carreiras e competências, da qual a IA seleciona os itens recomendados.

## Requirements

### Requisito 1: Questionário inicial (triagem)

**História de usuária:** Como visitante, quero responder a um questionário simples ao abrir a página, para que a plataforma entenda meu momento e me indique caminhos.

#### Critérios de aceitação

1. QUANDO a usuária abrir a página inicial pela primeira vez, ENTÃO o sistema DEVE exibir uma tela de boas-vindas com o botão para iniciar o questionário, antes de qualquer outro conteúdo.
2. O sistema DEVE apresentar o questionário em etapas curtas, uma pergunta por tela, com barra de progresso e botões "Voltar" e "Continuar".
3. O questionário DEVE coletar: momento profissional (iniciando em tecnologia, migrando de carreira ou buscando especialização), situação de estudo (está na faculdade, não está, curso técnico, autodidata), experiência (nenhuma, estágio, até 2 anos, mais de 2 anos), objetivos profissionais, áreas de interesse e disponibilidade semanal de estudo (total de horas por semana e faixas de horário por dia da semana, conforme os critérios 4 a 7).
4. A pergunta de disponibilidade DEVE coletar o total de horas semanais de estudo e, para cada dia da semana (segunda a domingo), as faixas de horário em que a usuária pode estudar, escolhidas entre manhã, tarde e noite ou informadas como horário exato de início e fim.
5. A pergunta de disponibilidade DEVE oferecer o atalho "mesmo horário todos os dias úteis", que replica a faixa informada de segunda a sexta-feira e permite ajustar cada dia depois.
6. A usuária DEVE poder marcar qualquer dia da semana como "sem estudo", e o sistema DEVE excluir esse dia da distribuição de atividades.
7. SE a soma das faixas de horário informadas for menor que o total de horas semanais, ENTÃO o sistema DEVE avisar a usuária e pedir que ajuste o total ou as faixas antes de continuar.
8. O sistema DEVE permitir que a usuária marque conhecimentos e ferramentas que já possui a partir de uma lista por área, com nível (conheço o básico, uso no dia a dia, domino).
9. A usuária DEVE poder responder "ainda não sei" em perguntas de objetivo e interesse, e o sistema DEVE prosseguir normalmente.
10. O sistema DEVE oferecer o anexo opcional de currículo (PDF ou DOCX, até 5 MB). SE a usuária não anexar, ENTÃO o questionário DEVE continuar sem prejuízo.
11. QUANDO um currículo for anexado, ENTÃO o sistema DEVE extrair habilidades e experiências, mostrá-las para confirmação e permitir a edição antes de usá-las.
12. ENQUANTO o questionário estiver incompleto, o sistema DEVE guardar as respostas no navegador e permitir retomar de onde parou.
13. QUANDO a usuária concluir o questionário, ENTÃO o sistema DEVE mostrar um resumo das respostas, incluindo a disponibilidade por dia e horário, para revisão e edição antes de gerar o perfil.

### Requisito 2: Identificação de perfil por IA

**História de usuária:** Como usuária, quero que a plataforma entenda meu perfil e meus objetivos, para receber orientações que façam sentido para mim.

#### Critérios de aceitação

1. QUANDO a usuária confirmar o resumo, ENTÃO o sistema DEVE gerar um perfil com: tipo de jornada (iniciante, transição ou especialização), nível por área, conhecimentos prévios, objetivos e lacunas principais.
2. O sistema DEVE classificar a usuária como "crua" (sem base técnica) ou "com base" e adaptar a linguagem e as recomendações a essa classificação.
3. O sistema DEVE exibir o perfil gerado em linguagem simples e permitir que a usuária corrija qualquer item.
4. SE a chamada à IA falhar ou exceder 15 segundos, ENTÃO o sistema DEVE aplicar um perfil por regras determinísticas a partir das respostas e informar que a análise personalizada está indisponível no momento.
5. O sistema NÃO DEVE enviar nome, e-mail ou telefone do currículo ao modelo de IA.

### Requisito 3: Leque de carreiras

**História de usuária:** Como usuária, quero ver um leque de oportunidades de carreira compatíveis comigo, para escolher onde quero chegar.

#### Critérios de aceitação

1. QUANDO o perfil for confirmado, ENTÃO o sistema DEVE exibir de 3 a 6 carreiras recomendadas, cada uma com nome, resumo de uma frase, percentual de aderência ao perfil e motivo da recomendação.
2. O sistema DEVE cobrir as áreas Dados, Infraestrutura, Desenvolvimento, Segurança e IA e permitir explorar todas as carreiras do catálogo, não só as recomendadas.
3. QUANDO a usuária abrir uma carreira, ENTÃO o sistema DEVE exibir: descrição do dia a dia profissional, competências necessárias, linguagens, ferramentas e tecnologias, faixa de senioridade, grade curricular sugerida, certificações recomendadas e eventos relacionados (hackathons, comunidades).
4. O sistema DEVE destacar o que a usuária já domina e o que falta aprender para cada carreira.
5. A usuária DEVE poder escolher uma carreira como objetivo principal e trocá-la depois sem perder o histórico de progresso.

### Requisito 4: Mapa de trajetória e trilha personalizada

**História de usuária:** Como usuária, quero um mapa visual com etapas, para saber exatamente o que estudar e em que ordem.

#### Critérios de aceitação

1. QUANDO a usuária escolher uma carreira objetivo, ENTÃO o sistema DEVE gerar um mapa de trajetória com etapas ordenadas (por exemplo: Fundamentos, Prática, Especialização, Certificação, Portfólio, Oportunidades).
2. Cada etapa DEVE conter conteúdos, exercícios práticos, estimativa de horas e a marca de status (bloqueada, disponível, em andamento, concluída).
3. O sistema DEVE omitir ou marcar como "já dominado" os conteúdos correspondentes aos conhecimentos informados pela usuária.
4. A usuária DEVE poder validar um conhecimento por mini-teste de até 10 questões. SE ela atingir 70% ou mais, ENTÃO o sistema DEVE marcar o tópico como dominado e atualizar o mapa.
5. O sistema DEVE recomendar cursos gratuitos e pagos, identificando o tipo de cada um, e incluir vídeos, documentações e plataformas externas.
6. Todo curso ou material recomendado DEVE ter um link de acesso funcional que abra em nova aba.
7. O sistema DEVE oferecer uma visão "dia a dia" que exibe as atividades da trilha no Calendário semanal de estudos (Requisito 10), distribuídas conforme a disponibilidade semanal informada.
8. QUANDO a usuária concluir uma atividade, ENTÃO o sistema DEVE atualizar o mapa e o percentual de progresso imediatamente.
9. A IA DEVE selecionar apenas itens existentes no catálogo. SE um item recomendado não existir no catálogo, ENTÃO o sistema DEVE descartá-lo.

### Requisito 5: Mentora com IA (chat)

**História de usuária:** Como usuária, quero conversar com uma mentora de IA, para tirar dúvidas e receber orientação durante a jornada.

#### Critérios de aceitação

1. O sistema DEVE disponibilizar um chat acessível em todas as telas após o questionário, por um botão flutuante.
2. A mentora DEVE ter acesso ao perfil, à carreira objetivo e ao progresso da usuária para contextualizar as respostas.
3. A mentora DEVE responder em tom acolhedor e em português, com respostas curtas e opção de aprofundar.
4. A mentora DEVE responder dúvidas técnicas sobre os conteúdos da trilha, sugerir próximos passos e explicar por que uma recomendação foi feita.
5. Quando a mentora citar curso, certificação ou vaga, ela DEVE usar somente itens do catálogo ou das fontes de vagas integradas, com link.
6. QUANDO a pergunta fugir do escopo (carreira, estudos, cloud), ENTÃO a mentora DEVE redirecionar educadamente ao tema.
7. A mentora DEVE exibir sugestões de perguntas iniciais para quem não sabe o que perguntar.
8. SE a IA estiver indisponível, ENTÃO o chat DEVE exibir mensagem de erro amigável e permitir tentar de novo sem perder a conversa.
9. As respostas DEVEM ser exibidas em streaming, e a usuária DEVE poder interromper a geração.

### Requisito 6: Preparação para certificações

**História de usuária:** Como usuária, quero um plano de estudo para a certificação que desejo, para me preparar com segurança.

#### Critérios de aceitação

1. O sistema DEVE listar certificações de cloud por nível e área, com pré-requisitos, domínios do exame, duração, custo estimado e link oficial.
2. A IA DEVE recomendar certificações compatíveis com o perfil e a carreira objetivo.
3. QUANDO a usuária escolher uma certificação, ENTÃO o sistema DEVE criar um plano de estudo com data-alvo, distribuído por domínio do exame e pela disponibilidade semanal, com os blocos de estudo e os simulados agendados no Calendário semanal de estudos (Requisito 10).
4. O plano DEVE incluir materiais oficiais, cursos e simulados, cada um com link.
5. O sistema DEVE registrar o resultado dos simulados e exibir a evolução por domínio.
6. O sistema DEVE exibir o progresso até o exame (percentual do plano, dias restantes) e indicar quando a usuária está atrasada em relação à data-alvo, com opção de reajustar o plano.

### Requisito 7: Mapeamento de oportunidades

**História de usuária:** Como usuária, quero ver vagas e eventos compatíveis, para saber o que falta e aplicar.

#### Critérios de aceitação

1. O sistema DEVE integrar fontes públicas de vagas e exibir título, empresa, local/modalidade, competências exigidas e link da vaga original.
2. O sistema DEVE ordenar as vagas por compatibilidade com as habilidades da usuária e exibir o percentual de compatibilidade.
3. QUANDO a usuária abrir uma vaga, ENTÃO o sistema DEVE listar as competências que ela já possui e as que faltam, com atalho para adicionar o conteúdo correspondente ao mapa.
4. O sistema DEVE exibir hackathons, bootcamps e eventos relevantes à carreira objetivo, com data e link de inscrição.
5. SE uma fonte de vagas estiver indisponível, ENTÃO o sistema DEVE exibir as demais fontes e informar a falha de forma discreta.
6. O sistema DEVE permitir filtrar por modalidade (remoto, híbrido, presencial), senioridade e localização.

### Requisito 8: Gamificação e ranking

**História de usuária:** Como usuária, quero ganhar pontos e conquistas, para me manter motivada.

#### Critérios de aceitação

1. QUANDO a usuária concluir uma atividade, um mini-teste, um ciclo Pomodoro ou uma etapa, ENTÃO o sistema DEVE conceder pontos conforme uma tabela de pontuação fixa e exibir feedback visual imediato.
2. O sistema DEVE exibir pontos totais, nível, sequência de dias estudados e conquistas obtidas.
3. O sistema DEVE oferecer conquistas (por exemplo: primeira atividade, primeira etapa, sequência de 7 dias, certificação concluída) e metas de aprendizagem semanais.
4. O mapa de trajetória DEVE mostrar visualmente a posição atual, as etapas concluídas e as próximas.
5. O ranking DEVE ser opcional e desativado por padrão. A usuária DEVE poder entrar e sair dele a qualquer momento.
6. O ranking DEVE exibir somente apelido e pontos da semana, sem dados pessoais.
7. O sistema NÃO DEVE conceder pontos duplicados para a mesma atividade concluída.

### Requisito 9: Organização de estudos, Pomodoro e bem-estar

**História de usuária:** Como usuária, quero organizar meus estudos de forma saudável, para estudar com constância sem me sobrecarregar.

#### Critérios de aceitação

1. O sistema DEVE oferecer um temporizador Pomodoro com padrão de 25 minutos de foco e 5 de pausa, e pausa longa de 15 minutos a cada 4 ciclos, com durações configuráveis.
2. O temporizador DEVE continuar contando corretamente se a aba ficar em segundo plano e DEVE notificar o fim de cada ciclo com aviso sonoro e visual que a usuária possa desativar.
3. DURANTE as pausas, o sistema DEVE sugerir ações de bem-estar (alongar, beber água, respirar, olhar ao longe) com exercício guiado curto.
4. SE a usuária estudar mais de 3 horas seguidas, ENTÃO o sistema DEVE sugerir uma pausa mais longa.
5. O sistema DEVE apresentar o cronograma semanal personalizado por meio do Calendário semanal de estudos (Requisito 10), sem manter um cronograma separado.
6. A usuária DEVE poder ver o histórico de atividades concluídas, registrado a partir das marcações feitas no Calendário semanal de estudos.
7. A usuária DEVE poder registrar como se sente (check-in de humor) e, QUANDO indicar cansaço ou ansiedade, ENTÃO o sistema DEVE sugerir reduzir a carga da semana e oferecer reajustar o Calendário semanal de estudos.
8. O sistema NÃO DEVE usar mensagens de culpa ou pressão ao detectar dias sem estudo. As mensagens DEVEM ser de incentivo.

### Requisito 10: Calendário semanal de estudos

**História de usuária:** Como usuária, quero ver no calendário os horários que tenho livres em cada dia da semana e os estudos distribuídos neles, para saber exatamente quando estudar cada coisa.

#### Critérios de aceitação

1. QUANDO a usuária confirmar o resumo do questionário, ENTÃO o sistema DEVE criar o calendário semanal de estudos com a disponibilidade informada no Requisito 1, dividida por dia da semana e faixa de horário.
2. O sistema DEVE oferecer as visões "semana" e "dia" e permitir alternar entre elas e navegar entre semanas.
3. O sistema DEVE exibir a disponibilidade como faixas de tempo destacadas visualmente, de modo que as faixas disponíveis e os dias sem estudo sejam distinguíveis.
4. O sistema DEVE distribuir nas faixas disponíveis os blocos de estudo originados das atividades da trilha (Requisito 4), dos ciclos Pomodoro (Requisito 9) e dos simulados de certificação (Requisito 6).
5. O sistema DEVE manter a soma dos blocos planejados em cada semana menor ou igual ao tempo disponível informado, e em cada dia menor ou igual às faixas daquele dia.
6. SE as atividades pendentes não couberem no tempo disponível da semana, ENTÃO o sistema DEVE manter o excedente fora do calendário, na lista "a agendar", e informar a usuária.
7. O sistema DEVE exibir o total de horas planejadas e o total de horas disponíveis da semana, e de cada dia na visão "dia".
8. O sistema DEVE destacar o tempo livre ainda não ocupado por blocos dentro das faixas disponíveis.
9. A usuária DEVE poder editar a disponibilidade (dias, faixas de horário e total semanal) diretamente no calendário, com as mesmas opções do Requisito 1.
10. QUANDO a disponibilidade for alterada, ENTÃO o sistema DEVE reagendar automaticamente os blocos ainda não concluídos dentro das novas faixas e exibir o resultado para a usuária desfazer.
11. A usuária DEVE poder mover blocos para outro horário ou dia e redimensionar a duração de um bloco.
12. SE a usuária mover ou redimensionar um bloco para fora das faixas disponíveis, ENTÃO o sistema DEVE pedir confirmação e, quando confirmado, marcar o bloco como "fora da disponibilidade" sem contá-lo no tempo disponível.
13. SE um bloco se sobrepuser a outro bloco, ENTÃO o sistema DEVE impedir a sobreposição e sugerir o horário livre mais próximo.
14. A usuária DEVE poder marcar um bloco como concluído, e o sistema DEVE atualizar o progresso do mapa (Requisito 4) e conceder pontos conforme o Requisito 8.
15. QUANDO um bloco não for concluído até o fim do seu horário, ENTÃO o sistema DEVE marcá-lo como "pendente" e oferecer reagendá-lo nas próximas faixas livres, com mensagem de incentivo (Requisito 9, critério 8).
16. QUANDO a usuária estiver atrasada em relação à data-alvo de uma certificação (Requisito 6, critério 6), ENTÃO o sistema DEVE oferecer reajustar o calendário para recuperar o atraso dentro da disponibilidade.
17. O sistema DEVE exibir horários no fuso horário do dispositivo da usuária e DEVE manter os blocos nos mesmos horários locais quando houver mudança de horário de verão ou de fuso.
18. ONDE a usuária escolher exportar, o sistema DEVE gerar um arquivo .ics com os blocos agendados, compatível com Google Agenda e Outlook.
19. FOR ALL blocos exportados, importar o arquivo .ics DEVE produzir blocos com o mesmo título, data, horário de início e duração (propriedade de ida e volta).
20. O sistema DEVE permitir a navegação completa pelo calendário por teclado, incluindo mover e redimensionar blocos por atalhos, e DEVE descrever cada bloco (título, dia, horário e status) a leitores de tela, conforme o Requisito 12.
21. O calendário DEVE ser responsivo, exibindo a visão "dia" por padrão em telas de até 600 px de largura e a visão "semana" nas demais.
22. O sistema DEVE tratar os estados de carregamento, vazio (sem disponibilidade informada) e erro do calendário, com mensagem clara e ação de recuperação.

### Requisito 11: Contas e persistência do progresso

**História de usuária:** Como usuária, quero salvar meu progresso, para continuar de qualquer dispositivo.

#### Critérios de aceitação

1. QUANDO a usuária pedir para salvar o progresso, ENTÃO o sistema DEVE oferecer cadastro e login por e-mail e senha ou por provedor social.
2. QUANDO a usuária criar a conta, ENTÃO o sistema DEVE migrar as respostas e o progresso locais para a conta.
3. A usuária DEVE poder baixar e excluir todos os seus dados, incluindo o currículo, a partir de uma tela de configurações.
4. O sistema DEVE coletar consentimento explícito antes de processar o currículo e antes de entrar no ranking, em conformidade com a LGPD.
5. O sistema DEVE armazenar o currículo criptografado e removê-lo automaticamente após a extração das habilidades, a menos que a usuária peça para mantê-lo.

### Requisito 12: Experiência de uso, visual e acessibilidade

**História de usuária:** Como usuária, quero uma interface confortável, divertida e fácil de ler, para usar a plataforma sem esforço.

#### Critérios de aceitação

1. A interface DEVE ser responsiva e funcionar em telas de 360 px a 1920 px de largura, com prioridade para o uso em celular.
2. O visual DEVE usar paleta suave, cantos arredondados, ilustrações e microanimações leves, sem excesso de elementos por tela.
3. O texto DEVE usar linguagem simples, parágrafos curtos, tamanho mínimo de fonte de 16 px no corpo e espaçamento confortável entre linhas.
4. O sistema DEVE atender ao nível AA da WCAG 2.1: contraste mínimo de 4,5:1, navegação completa por teclado, rótulos para leitores de tela e foco visível.
5. O sistema DEVE respeitar a preferência `prefers-reduced-motion` e oferecer modo escuro.
6. Termos técnicos DEVEM ter explicação curta ao toque ou passagem do mouse (glossário).
7. A primeira tela útil DEVE carregar em até 3 segundos em conexão 4G.
8. Cada tela DEVE ter uma única ação principal em destaque.
9. Estados de carregamento, vazio e erro DEVEM ser tratados em todas as telas, com mensagens claras e uma ação de recuperação.

### Requisito 13: IA responsável e qualidade das recomendações

**História de usuária:** Como usuária, quero confiar nas recomendações, para investir meu tempo nelas.

#### Critérios de aceitação

1. O sistema DEVE informar de forma visível que o conteúdo é gerado por IA e que as recomendações são sugestões.
2. O sistema DEVE explicar o motivo de cada recomendação principal (carreira, certificação, vaga).
3. O sistema DEVE verificar periodicamente os links do catálogo e sinalizar para revisão os links quebrados.
4. A usuária DEVE poder avaliar cada recomendação (útil ou não) e o sistema DEVE registrar essa avaliação para melhoria.
5. O sistema NÃO DEVE usar atributos pessoais sensíveis (idade, raça, religião, orientação sexual, saúde) para classificar ou limitar recomendações de carreira.
6. O sistema DEVE aplicar limite de requisições por usuária à IA para controlar custo e abuso.
