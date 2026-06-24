# push-catus-store

Passo 1: Isolamento de Ambientes (Estratégia Blindada)

Em vez de tentar misturar históricos de repositórios diferentes na mesma pasta, você clonou os dois projetos em pastas separadas dentro de ~/Desktop/catus/:

    wake-gold-food-service (Origem: GitHub - com todo o seu código novo).

    goldfoodservice (Destino: GitLab - com a estrutura limpa da branch main/sprint15).

Passo 2: Sincronização Limpa via Terminal (rsync)

Você usou o poder do terminal para copiar apenas os arquivos de código de uma pasta para a outra, garantindo que a configuração oculta do Git de uma empresa não entrasse na outra.
Bash

rsync -av --delete --exclude='.git' wake-gold-food-service/theme/ goldfoodservice/

    Por que deu certo? A flag --exclude='.git' protegeu o repositório do GitLab, e a cópia limpou os arquivos antigos mantendo apenas o seu código atualizado pronto para o envio.

Passo 3: Organização de Branches no GitLab

Dentro da pasta goldfoodservice (GitLab), você salvou o progresso na main, alternou com segurança para a branch correta e trouxe todas as modificações usando o checkout pontual:
Bash

git switch sprint15
git checkout main -- .

Passo 4: O Ajuste de Identidade (Configuração Local)

Para garantir que os próximos commits fiquem com o carimbo profissional correto e não misture os e-mails das empresas, o segredo foi configurar o Git de forma local (apenas para aquela pasta):
Bash

git config user.name "Marcelo Vinicius Taparelli"
git config user.email "marcelo.taparelli@catus.com.br"

Passo 5: Forçar o Ajuste no Servidor (O Gran Finale)

Como o primeiro commit tinha subido com a assinatura trocada, você corrigiu o autor localmente e usou o push -f para atualizar o GitLab com o histórico limpo:
Bash

git commit --amend --author="Marcelo Vinicius Taparelli <marcelo.taparelli@catus.com.br>" --no-edit
git push origin sprint15 -f
