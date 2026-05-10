# Sprint-Computer-Organization-and-Architecture
Repositório para realização das sprints de Computer Organization and Architecture - (Prof: Marcus Grilo)

1 - ChargeGrid Intelligence
Desafio FIAP + GoodWe Challenge 2026 | Sprint 1 – Computer Organization and Architecture

2 - Integrantes:

Alan Junio Araujo de Souza - RM 574112
Arthur Vettorazzo de Souza - RM 569445
Brayan Barbosa Dos Santos - RM 573682
Giovanne Gomes Petenuci - RM 574091
Gustavo Zibini Belizario - RM 561376
Luiz Otávio Brito Freixo - RM 569977

3 - Problema apresentado:

Sistemas de eletropostos frequentemente utilizam software de alto nível e hardware genérico, o que pode gerar: 
-Consumo desnecessário de energia 
-Baixa eficiência no processamento de dados (ex: autenticação, controle de carga) 
-Desperdício de recursos computacionais 

4 - Justificativa proposta:
  
A solução ChargeGrid Intelligence justifica-se pela necessidade de transformar eletropostos comuns em unidades de gestão energética inteligente. Ao integrar hardware de baixo consumo (ESP32), protocolos de comunicação industriais (OCPP e MODBUS) e inteligência artificial, o projeto permite que a infraestrutura reaja dinamicamente à demanda e à geração de energia solar disponível (via API GoodWe). Essa abordagem não apenas evita custos excedentes, mas também otimiza a experiência do usuário através da tarifação dinâmica e garante a sustentabilidade da operação, alinhando-se aos pilares de eficiência energética e inovação tecnológica.

5 - Proposta de Solução:

A arquitetura da plataforma foi desenhada como um ecossistema integrado que opera em três camadas interdependentes, priorizando a eficiência energética através do processamento de baixo nível:

Unidade de Processamento Local (Edge): Baseada no microcontrolador ESP32, esta camada física utiliza um módulo de controle otimizado em baixo nível (Assembly) para gerenciar operações críticas, como a leitura instantânea de sensores e a autenticação de usuários. O uso de instruções otimizadas do processador reduz os ciclos de CPU necessários, resultando em um consumo energético mínimo.

Camada de Integração (Backend): Atua como o núcleo de orquestração de dados, conectando carregadores via protocolo OCPP, medidores elétricos industriais via MODBUS e consumindo a API da GoodWe para monitorar a geração solar disponível.

Inteligência Preditiva (IA): Camada analítica responsável por processar os dados coletados para a previsão de demanda energética, aplicando regras de tarifação dinâmica e realizando a detecção proativa de anomalias elétricas.

6 - Arquitetura Utilizada:

A arquitetura do projeto fundamenta-se nos paradigmas de IoT e Edge Computing, com foco em hardware eficiente:

Arquitetura de Processamento (RISC): O sistema utiliza o microcontrolador ESP32, baseado em uma arquitetura de conjunto de instruções reduzido (RISC). Essa escolha permite uma execução mais rápida das instruções, otimizando o uso do pipeline do processador e minimizando conflitos de cache.

Eficiência por Instrução: A implementação de rotinas críticas em Assembly permite um controle rigoroso sobre os ciclos de clock, garantindo que o monitoramento de energia seja realizado com o menor número possível de instruções por segundo, reduzindo o aquecimento e o consumo do sistema.

Protocolos e Integração: Utilização de OCPP para carregadores e MODBUS para medidores industriais, integrando-se nativamente ao ecossistema de APIs da GoodWe para telemetria solar.

7 - Trechos de Código (Demonstração de Baixo Nível):

Embora a lógica principal de integração e IA opere em alto nível (Python), o controle de hardware no modelo de Edge Computing requer extrema eficiência no uso de ciclos de processamento.

O trecho conceitual em Assembly abaixo ilustra a base algorítmica executada na camada física. O objetivo desta rotina é ler a potência atual do medidor, compará-la com o limite do contrato e sinalizar o carregador para reduzir a carga caso o limite seja ultrapassado.

Snippet de código
; Lógica conceitual para verificação de limite de potência contratada
; Registradores utilizados:
; EAX = Armazena a potência atual lida do medidor
; EBX = Armazena o limite de potência contratada da distribuidora

Ler_Sensor:
    MOV EAX, [Memoria_Medidor]  ; Carrega a leitura de potência atual para o registrador EAX
    MOV EBX, [Limite_Contrato]  ; Carrega o limite máximo permitido para o registrador EBX

Verificar_Demanda:
    CMP EAX, EBX                ; Compara a potência atual (EAX) com o limite (EBX)
    JLE Operacao_Normal         ; Se EAX for menor ou igual (Jump if Less or Equal), pula para Operacao_Normal

Reduzir_Carga:
    MOV ECX, 1                  ; O valor 1 representa o sinal de "Alerta/Redução"
    MOV [Pino_Sinalizacao], ECX ; Envia o sinal para o hardware do carregador reduzir a potência
    JMP Finalizar_Ciclo         ; Pula para o fim do ciclo

Operacao_Normal:
    MOV ECX, 0                  ; O valor 0 representa "Operação Normal" (sem restrição)
    MOV [Pino_Sinalizacao], ECX ; Mantém o carregador operando em potência máxima

Finalizar_Ciclo:
    ; Retorna ao início do loop de monitoramento contínuo
    
Explicação da Lógica:
A instrução CMP (Compare) avalia instantaneamente se o consumo ultrapassou o teto. Se estiver seguro, a instrução JLE direciona o fluxo para manter o carregamento normal. Caso contrário, o sistema altera o registrador de sinalização (ECX recebe 1), o que pode acender o LED de alerta no totem ou limitar o fornecimento elétrico do carregador via hardware.

8 - Impactos Esperados:

Sustentabilidade Financeira: Mitigação de multas por ultrapassagem de demanda e otimização de receita via tarifação dinâmica.

Eficiência Energética: Maximização do uso de energia solar e redução da sobrecarga na rede elétrica convencional.

Inovação via Edge Computing: Respostas em milissegundos para controle de carga, menor dependência da nuvem e redução do consumo de banda.

*Relação com Sustentabilidade e Energias Renováveis:

Sustentabilidade na Arquitetura (Green Code): A combinação de arquitetura RISC com código otimizado resulta em "Código Verde", onde menos instruções executadas significam menor consumo de energia pelo próprio hardware de gestão.

Otimização da Matriz Energética: Integração com a API GoodWe para incentivar o carregamento durante picos de geração fotovoltaica, promovendo o uso de fontes limpas.

Estabilidade e Smart Grid: Proteção da infraestrutura local e apoio à expansão resiliente da mobilidade elétrica.

9 - Link pitch:

https://_____________________
