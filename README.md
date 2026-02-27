# ♟️ Checkers Suite: Distributed Game Engine & UI

**📋 Sobre o Projeto
Este projeto trata-se de uma solução completa para o jogo de Damas, permitindo partidas em tempo real entre dois jogadores através de uma arquitetura distribuída.

O sistema evoluiu de uma interface de consola (Fase 1) para uma aplicação Desktop (Fase 2), mantendo a integridade do motor de jogo original e introduzindo persistência remota em MongoDB.

---

**🏗️ Arquitetura do Sistema
A aplicação segue o padrão MVVM (Model-View-ViewModel) e os princípios de Clean Architecture, garantindo que a lógica de negócio seja independente da base de dados e da interface.

*1. Motor de Jogo (tds.model)
O "Coração" do sistema, implementado com foco na imutabilidade e segurança de tipos:

Imutabilidade: Cada jogada gera um novo estado do tabuleiro (Board), facilitando o rastreio de estados e evitando efeitos secundários.

Lógica de Damas: Implementação integral das regras oficiais:

Movimentos simples e capturas obrigatórias.

Capturas múltiplas em cadeia.

Promoção de peças a Damas (Queens) com movimento livre diagonal.

Abstração Espacial: Uso de value classes para Row e Column e um sistema de coordenadas robusto em Square.

*2. Camada de Persistência (tds.storage)
Um sistema de armazenamento flexível que utiliza o Repository Pattern:

Abstração: Interface Storage<Key, Data> que permite trocar entre o sistema de ficheiros local (TextFileStorage) e o banco de dados remoto (MongoStorage) sem alterar o código da aplicação.

Serialização Customizada: Implementação de Serializer<T> para converter objetos complexos em strings otimizadas, garantindo que o estado do jogo seja persistido de forma eficiente no MongoDB.

*3. ViewModel e Concorrência (tds.viewmodel)
A AppViewModel gere o estado da UI e as comunicações assíncronas:

Reatividade: Utilização de mutableStateOf do Compose para atualizações automáticas da interface.

Polling Assíncrono: Implementação de waitForOtherSide via Kotlin Coroutines. O sistema verifica o servidor em segundo plano sem bloquear a interface do utilizador, sincronizando a jogada do oponente automaticamente.

---

**🎨 Interfaces de Utilizador
Desktop (Compose Multiplatform)
A interface gráfica oferece uma experiência moderna e intuitiva:

Perspetiva Dinâmica: O tabuleiro inverte-se automaticamente para o jogador das peças pretas, garantindo que cada utilizador vê o jogo da sua perspetiva.

Feedback Visual: Diálogos de erro (ErrorDialog), barra de estado em tempo real (StatusBar) e destaque de peças selecionadas.

Menu de Opções: Suporte para "Show Targets" (ajuda visual) e "Auto-refresh".

Consola (CLI)
Uma aplicação robusta de linha de comandos que processa ordens como START <id>, PLAY <from> <to> e REFRESH, demonstrando a versatilidade do motor de jogo.

---

**🛠️ Stack Tecnológica
Linguagem: Kotlin 1.9+

UI Framework: Jetpack Compose Multiplatform

Base de Dados: MongoDB (NoSQL)

Gestão de Dependências: Gradle

Assincronismo: Kotlin Coroutines

---

**🚀 Como Executar
Pré-requisitos:

Java JDK 17 ou superior.

MongoDB: Configurar a variável de ambiente MONGO_CONNECTION com a sua Connection String.

---

Tabuleiro 8x8 com casas pretas e brancas.

Peças Brancas (w) iniciam o jogo.

Captura Obrigatória: Se um salto estiver disponível, o jogador deve realizá-lo.

Damas: Peças que atingem a última linha são promovidas, ganhando a capacidade de mover várias casas em qualquer direção diagonal.

Condição de Vitória: O jogo termina quando um jogador captura todas as peças adversárias ou bloqueia todos os seus movimentos.

---
