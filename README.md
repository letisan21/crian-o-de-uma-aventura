# crian-o-de-uma-aventura
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aventura Interativa - Misturando HTML, CSS e JS</title>
    <style>
        /* Estilos Gerais */
        body {
            font-family: 'Arial', sans-serif;
            background-color: #2c3e50;
            color: #fff;
            text-align: center;
            padding: 30px;
        }

        h1 {
            font-size: 2em;
            margin-bottom: 20px;
            text-transform: uppercase;
        }

        #story {
            margin-bottom: 20px;
            font-size: 1.2em;
            line-height: 1.6;
        }

        #choices {
            margin-top: 20px;
        }

        .choice-btn {
            background-color: #2980b9;
            color: white;
            font-size: 1.1em;
            padding: 10px 20px;
            margin: 10px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s ease;
            width: 250px;
        }

        .choice-btn:hover {
            background-color: #3498db;
        }

        .choice-btn:focus {
            outline: none;
        }

        /* Animations */
        .fade-in {
            animation: fadeIn 1s ease-in-out;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }

        footer {
            margin-top: 50px;
            color: #95a5a6;
            font-size: 0.9em;
        }
    </style>
</head>
<body>

    <h1>Aventura Interativa</h1>
    <div id="story">
        <p>Você acorda em uma floresta densa. O som das folhas farfalhando ao vento é a única coisa que você consegue ouvir.</p>
    </div>

    <div id="choices">
        <button class="choice-btn fade-in" onclick="choose('leftPath')">Seguir pela estrada à esquerda</button>
        <button class="choice-btn fade-in" onclick="choose('rightPath')">Seguir pela estrada à direita</button>
    </div>

    <footer>&copy; 2024 Aventura Interativa</footer>

    <script>
        // Estrutura de dados da aventura
        const storyData = {
            start: {
                text: "Você acorda em uma floresta densa. O som das folhas farfalhando ao vento é a única coisa que você consegue ouvir.",
                choices: [
                    { text: "Seguir pela estrada à esquerda", next: "leftPath" },
                    { text: "Seguir pela estrada à direita", next: "rightPath" }
                ]
            },
            leftPath: {
                text: "Você seguiu pela estrada à esquerda e encontrou uma cabana misteriosa. O que você fará?",
                choices: [
                    { text: "Entrar na cabana", next: "enterCabin" },
                    { text: "Voltar para a floresta", next: "start" }
                ]
            },
            rightPath: {
                text: "Você seguiu pela estrada à direita e encontrou um rio turbulento. O que fazer?",
                choices: [
                    { text: "Tentar atravessar o rio", next: "crossRiver" },
                    { text: "Voltar para a floresta", next: "start" }
                ]
            },
            enterCabin: {
                text: "Dentro da cabana, você encontra um mapa antigo. Com o mapa, você escapa da floresta e ganha a aventura!",
                choices: [
                    { text: "Jogar novamente", next: "start" }
                ]
            },
            crossRiver: {
                text: "Você tentou atravessar o rio, mas a correnteza era forte demais e você não conseguiu chegar ao outro lado.",
                choices: [
                    { text: "Jogar novamente", next: "start" }
                ]
            }
        };

        // Função para exibir o texto da história e as escolhas
        function displayStory(storyNode) {
            const storyDiv = document.getElementById('story');
            const choicesDiv = document.getElementById('choices');

            // Limpar as escolhas anteriores
            choicesDiv.innerHTML = '';

            // Atualizar o texto da história
            storyDiv.innerHTML = `<p>${storyData[storyNode].text}</p>`;

            // Adicionar as novas escolhas
            storyData[storyNode].choices.forEach(choice => {
                const button = document.createElement('button');
                button.className = 'choice-btn fade-in';
                button.textContent = choice.text;
                button.onclick = () => choose(choice.next);
                choicesDiv.appendChild(button);
            });
        }

        // Função chamada quando uma escolha é feita
        function choose(nextNode) {
            displayStory(nextNode);
        }

        // Iniciar a história
        displayStory('start');
    </script>

</body>
</html>
