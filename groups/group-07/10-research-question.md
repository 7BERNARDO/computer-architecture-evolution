# 1. Como a arquitetura MIMD quebra o modelo tradicional de execução sequencial de código?

## 1.1 O Modelo Tradicional: O Fluxo de Controle Centralizado: 
    No modelo de computação tradicional — baseado na Arquitetura de Von Neumann e classificado como SISD (Single Instruction, Single Data) na Taxonomia de Flynn —, a execução é estritamente sequencial.
    O coração desse modelo é o Contador de Programa (PC - Program Counter), um registrador na CPU que armazena o endereço da próxima instrução a ser executada.
    A linearidade: O processador busca a instrução apontada pelo PC, executa-a, incrementa o PC para a próxima linha e repete o ciclo (Fetch-Decode-Execute). 
    O determinismo: Existe apenas uma única "linha do tempo". O estado das variáveis do programa muda em uma ordem previsível e exata, linha por linha.

## 1.2 A Quebra do Modelo pelo MIMD: Descentralização e Autonomia


    A arquitetura MIMD destrói essa linearidade ao introduzir Múltiplos Contadores de Programa independentes no sistema. Em vez de uma única CPU controlando tudo, temos múltiplos núcleos de processamento (ou múltiplos processadores) operando simultaneamente. 

    A quebra do modelo tradicional ocorre através de três pilares: 

    A. Autonomia de Instrução (Múltiplas Instruções) 
    
    Cada núcleo possui sua própria Unidade de Controle (UC) e seu próprio Contador de Programa (PC). Isso significa que, no exato mesmo ciclo de clock: 
    
     O Núcleo 1 pode estar executando uma instrução de desvio (if/else) em um sistema de login.

     O Núcleo 2 pode estar executando uma operação aritmética (sum) em um relatório de vendas. 

     O Núcleo 3 pode estar aguardando uma resposta de rede (I/O wait).

     Impacto: Não existe mais uma "receita passo a passo" centralizada. O fluxo de controle tornou-se distribuído e fragmentado.
    
    B. Autonomia de Dados (Múltiplos Dados)
    
    Cada fluxo de instrução opera sobre fluxos de dados completamente diferentes. Os núcleos podem acessar diferentes regiões da memória RAM ou memórias locais distintas (no caso de sistemas distribuídos).
    
     Impacto: O conceito de "estado do programa" muda. No modelo sequencial, o estado global é alterado de forma previsível. No MIMD, múltiplos processadores alteram partes diferentes do estado do sistema de forma simultânea e concorrente. 
    
    C. Assincronismo e Não-Determinismo 
    
    Os núcleos em uma arquitetura MIMD funcionam de forma assíncrona. Eles não esperam uns pelos outros para avançar. Fatores externos de hardware — como latência de acesso à memória cache (cache misses), interrupções do Sistema Operacional ou variações de temperatura no chip — fazem com que um núcleo execute suas tarefas ligeiramente mais rápido ou mais devagar que o outro a cada microssegundo. 
    
     Impacto: O tempo linear desaparece. Se você disparar a Tarefa A no Núcleo 1 e a Tarefa B no Núcleo 2, é impossível prever matematicamente qual linha de código terminará primeiro. O software torna-se não-determinista.

#### 1.3 O Paradoxo da Engenharia de Software no MIMD
    

   Para um Engenheiro de Software, o MIMD transfere a complexidade do hardware para o código. 
    
    Como o hardware MIMD quebrou a linha do tempo sequencial, o desenvolvedor é obrigado a recriar a ordem e a previsibilidade artificialmente no software quando os dados dependem uns dos outros. Se o Código A precisa de um dado que está sendo gerado pelo Código B em outro núcleo, o engenheiro não pode apenas "torcer" para que dê tempo. 
    
    É necessário programar utilizando mecanismos de sincronização (como Threads, barreiras, semáforos, locks ou passagem de mensagens). Se esses mecanismos falharem, o sistema sofre com problemas exclusivos do mundo paralelo, como as condições de corrida ou os deadlocks. 

## 2. Como a arquitetura MIMD quebra o modelo tradicional de execução sequencial de código?

## 3. Qual é a diferença prática entre MIMD de Memória Compartilhada (SMP) e Memória Distribuída (Clusters) na hora de programar?

## 4.  O que é o problema da "Coerência de Cache" em hardware MIMD e como ele afeta o software?

## 5. Como a Lei de Amdahl define o limite de performance de um software rodando em MIMD?

## 6. O que acontece se dois processadores tentarem alterar o mesmo dado na memória compartilhada?

## 7. Qual é o maior desafio ao programar para sistemas MIMD?

## 8. Onde a arquitetura MIMD é usada no dia a dia?

## 9. Qual é a principal vantagem da memória distribuída em relação à compartilhada?

## 10. O que pode ser a continuação da arquitetura MIMD ?