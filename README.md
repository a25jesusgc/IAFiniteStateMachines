# Exercicio IA Avanzada FSM

Para o exercicio creei unha nova escena chamada **WallsScene**. É moi semellante á outra pero cunhas paredes. Establecei a posicion dos *checkpoints*, do *SafePointRunawayState* e configurei e fixen *bake* do *NavMesh Surface* para que teña en conta os *NavMesh Modifier* das paredes.

Engadín un novo **State** chamado **Hold**. Este estado é un estado intermedio entre **Pursue** e **Patrol**. Cando está perseguindo ao xogador, se o perde de vista, en lugar de volver a patrullar inmediatamente, mantén a posición uns segundos ata volver a patrullar.

Para isto, creei a nova clase **Hold** que hereda de **State**. No seu *construtor* se lle *setea* o nome co **State** do *enum*. No método sobresctrito **Enter** activa o *trigger* para a animación *isIdle*, detén o axente con *agent.isStopped = true*, e establece os segundos de espera aleatoriamente entre 3 e 7 segundos.

No método sobresctrito **Update**, resta o tempo de espera ata que chegue a 0, momento no cal establece o seguinte estado a **Patrol** creando un novo obxecto **Patrol** e asignándollo ao **nextState** e cambia o *stage* a **Event.EXIT** para que se execute o método **Exit**.

Finalmente no método sobrescrito **Exit** *resetea* o *trigger* da animación *isIdle* e chama ao **Exit** do pai.

Para conectar isto cos outros estados, tiven que editar **Pursue**, cambiando que o **nextState** cando perde ao xogador de vista sexa **Hold** no lugar de **Patrol**.