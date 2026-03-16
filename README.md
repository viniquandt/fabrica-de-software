<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Descarte</title>
    <style>
        body {
            margin: 0;
            font-family: Arial, Helvetica, sans-serif;
            background: #f5f5f5;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .container {
            width: 600px;
            background: white;
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
            text-align: center;
        }

        h1 {
            color: #2f8f3a;
            margin-bottom: 10px;
        }

        h2 {
            color: #2f8f3a;
            margin-top: 20px;
            margin-bottom: 10px;
        }

        p {
            font-size: 16px;
            line-height: 1.5;
        }

        button {
            background: #c8eac7;
            border: none;
            padding: 12px;
            margin: 10px 0;
            width: 100%;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
        }

        button:hover {
            background: #b7e1b6;
        }

        input {
            width: 100%;
            padding: 10px;
            margin: 8px 0;
            border: none;
            background: #c8eac7;
            border-radius: 5px;
            font-size: 16px;
        }

        .tela {
            display: none;
        }

        .tela.ativa {
            display: block;
        }

        .sucesso {
            color: green;
            margin-top: 15px;
            font-weight: bold;
        }

        .erro {
            color: red;
            margin-top: 15px;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="container">
        
        <div id="inicio" class="tela ativa">
            <h1>Descarte</h1>
            <p>Sistema para descarte de resíduos</p>
            <button onclick="mostrarTela('localizar')">Localizar pontos de descarte</button>
            <button onclick="mostrarTela('agendar')">Agendar coleta de resíduos</button>
            <button onclick="mostrarTela('denuncia')">Registrar denúncia</button>
        </div>

        
        <div id="localizar" class="tela">
            <h2>Localizar pontos de descarte</h2>
            <p>Selecione o tipo de material:</p>
            <button onclick="mostrarTela('oleo')">Óleo de cozinha</button>
            <button onclick="mostrarTela('eletronicos')">Eletrônicos</button>
            <button class="voltar" onclick="mostrarTela('inicio')">&lt; Voltar</button>
        </div>

        
        <div id="oleo" class="tela">
            <h2>Óleo de Cozinha</h2>
            <p>O óleo de cozinha usado não deve ser descartado na pia, no vaso sanitário ou no lixo comum, pois pode causar entupimentos e contaminar o meio ambiente. O ideal é armazená-lo em uma garrafa plástica bem fechada e levá-lo até um ponto de coleta específico, onde será destinado corretamente para reciclagem ou reaproveitamento.</p>
            <button class="voltar" onclick="mostrarTela('localizar')">&lt; Voltar</button>
        </div>

        
        <div id="eletronicos" class="tela">
            <h2>Eletrônicos</h2>
            <p>Equipamentos eletrônicos, como celulares, computadores, pilhas e baterias, não devem ser descartados no lixo comum, pois contêm substâncias que podem prejudicar o meio ambiente. O correto é levá-los até pontos de coleta de lixo eletrônico ou locais de reciclagem especializados, onde serão desmontados e destinados de forma adequada.</p>
            <button class="voltar" onclick="mostrarTela('localizar')">&lt; Voltar</button>
        </div>

        
        <div id="agendar" class="tela">
            <h2>Agendar coleta de resíduos</h2>
            <input type="text" id="nome" placeholder="Nome">
            <input type="text" id="endereco" placeholder="Endereço">
            <input type="text" id="material" placeholder="Material para descarte">
            <button onclick="enviarAgendamento()">Enviar</button>
            <p id="mensagem" class="sucesso"></p>
            <p id="mensagemErro" class="erro"></p>
            <button class="voltar" onclick="mostrarTela('inicio')">&lt; Voltar</button>
        </div>

        
        <div id="denuncia" class="tela">
            <h2>Registrar Denúncia</h2>
            <input type="text" id="localDenuncia" placeholder="Local">
            <input type="text" id="descricao" placeholder="Descrição">
            <input type="file" id="anexar" accept="image/*">
            <button onclick="enviarDenuncia()">Enviar</button>
            <p id="mensagemDenuncia" class="sucesso"></p>
            <p id="mensagemErroDenuncia" class="erro"></p>
            <button class="voltar" onclick="mostrarTela('inicio')">&lt; Voltar</button>
        </div>
    </div>

    <script>
        function mostrarTela(id) {
            let telas = document.querySelectorAll(".tela");
            telas.forEach(t => t.classList.remove("ativa"));
            document.getElementById(id).classList.add("ativa");
            document.getElementById("mensagem").innerText = ""; // Limpa a mensagem de sucesso ao mudar de tela
            document.getElementById("mensagemErro").innerText = ""; // Limpa a mensagem de erro ao mudar de tela
            document.getElementById("mensagemDenuncia").innerText = ""; // Limpa a mensagem de sucesso da denúncia
            document.getElementById("mensagemErroDenuncia").innerText = ""; // Limpa a mensagem de erro da denúncia
        }

        function enviarAgendamento() {
            const nome = document.getElementById("nome").value;
            const endereco = document.getElementById("endereco").value;
            const material = document.getElementById("material").value;
            const mensagemErro = document.getElementById("mensagemErro");

            if (nome === "" || endereco === "" || material === "") {
                mensagemErro.innerText = "Preencha as opções acima"; // Mensagem de erro
                return;
            }

            document.getElementById("mensagem").innerText = "Agendamento realizado com sucesso!";
            mensagemErro.innerText = ""; // Limpa a mensagem de erro se o agendamento for bem-sucedido
        }

        function enviarDenuncia() {
            const localDenuncia = document.getElementById("localDenuncia").value;
            const descricao = document.getElementById("descricao").value;
            const mensagemErroDenuncia = document.getElementById("mensagemErroDenuncia");

            // Verifica se os campos estão preenchidos
            if (localDenuncia === "" || descricao === "") {
                mensagemErroDenuncia.innerText = "Preencha as opções acima"; // Mensagem de erro
                return;
            }

            document.getElementById("mensagemDenuncia").innerText = "Denúncia realizada com sucesso!";
            mensagemErroDenuncia.innerText = ""; // Limpa a mensagem de erro se a denúncia for bem-sucedida
        }
    </script>
</body>
</html>
