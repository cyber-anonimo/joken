# joken

<!-- js -->
const placar = {
    usuario: 0,
    computador: 0,
    partidas: 0
}

function alteraPlacar () {
   document.getElementById('placar-jogador').innerText    = placar.usuario; 
   document.getElementById('placar-computador').innerText = placar.computador;
   document.getElementById('numero-jogos').innerText      = placar.partidas;
}

function monitoraEscolhaDoUsuario () {
    let opcEscolhida = document.getElementById('combo-escolha').value;
    
    if (opcEscolhida == 'selecione') {
        document.getElementById('imgJogador1').src = "";
        return 0;
    }

    switch (opcEscolhida) {
        case 'pedra':
            document.getElementById('imgJogador1').src = "/images/pedra";
        break;
        case 'papel':
            document.getElementById('imgJogador1').src = "/images/papel"; 
        break;
        case 'tesoura':
            document.getElementById('imgJogador1').src = "/images/tesoura";
        break;
    }

}

function sorteiaJogadaComputador () {
    const numeroSorteado = parseInt(Math.random() * (4 - 1) + 1)
    switch (numeroSorteado) {
        case 1:
            document.getElementById('imgComputador').src = "/images/pedra";
            return 'pedra'
        case 2:
            document.getElementById('imgComputador').src = "/images/papel"; 
            return 'papel'
        case 3:
            document.getElementById('imgComputador').src = "/images/tesoura";
            return 'tesoura'
    }
}

function jogar () {
    placar.partidas++;
    const valorComputador = sorteiaJogadaComputador();
    const valorJogador    = document.getElementById('combo-escolha').value;

    if (valorComputador == valorJogador) {
        alert('Deu empate');
    } else if (valorJogador == 'pedra' && valorComputador == 'tesoura') {
        alert('Você Venceu');
        placar.usuario++;
    } else if (valorJogador == 'papel' && valorComputador == 'pedra') {
        alert('Você Venceu');
        placar.usuario++;
    } else if (valorJogador == 'tesoura' && valorComputador == 'papel') {
        alert('Você Venceu');
        placar.usuario++;
    } else {
        alert('Computador Venceu');
        placar.computador++;
    }
    alteraPlacar();
}

function reinicio () {
    placar.partidas = 0;
    placar.computador = 0;
    placar.usuario = 0;

    document.getElementById('imgComputador').src = '';
    document.getElementById('imgJogador1').src = '';
    document.getElementById('combo-escolha').value = 'selecione';
    alteraPlacar();
}

alteraPlacar();

<!-- html -->
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pedra|Papel|Tesoura</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <h1 id = "Jokenpô"><center>Jokenpô</center></h1>

    <div class="tela-jogo">
        <div class="caixa-jogo">
            <h3 class="titulo">Você</h3>
            <div>
                <select name="" id="combo-escolha" onchange="monitoraEscolhaDoUsuario()">
                    <option value="selecione" selected>Selecione</option>
                    <option value="pedra">Pedra</option>
                    <option value="papel">Papel</option>
                    <option value="tesoura">Tesoura</option>
                </select> 
                <br> 
                <img src= "" id="imgJogador1">  
            </div>
        </div>
        <div class="caixa-jogo">
            <h3 class="titulo">Placar</h3>

            <div class="placar-div">
                <table id="tabela">
                    <thead>
                        <th>Você</th>
                        <th>VS</th>
                        <th>Computador</th>
                    </thead>
                    <tbody>
                        <tr>
                            <td>
                                <span id="placar-jogador"></span>
                            </td>
                            <td>|</td>
                            <td>
                                <span id="placar-computador"></span>
                            </td>
                        </tr>
                        <tr>
                            <td colspan="3">Partidas Jogadas</td>
                        </tr>
                        <tr>
                            <td colspan="3">
                                <span id="jogadas"></span>
                            </td>
                        </tr>
                    </tbody>
                </table>
                <button class="botao-jogo" onclick="jogar()">Jogar</button>
                <button class="botao-jogo" onclick="reinicio()">Reiniciar</button>
            </div>

        </div>
        <div class="caixa-jogo">
            <h3 class="titulo">Computador</h3>

            <img id="imgComputador">
        </div>
    </div>

    <h3 id = "Mensagem"><font color= #ffffff>Mensagem</font></h3>

    <script src="app.js"></script>
</body>
</html>

<!-- css -->
#Jokenpô{
    background-color: gold;
}

body {
    background-color: darkgreen;
}

#Mensagem{
    background-color: darkred;
}

.tela-jogo {
    margin: 5%;
    background-color: #acacac;
    border: yellow dashed;    
    display: flex;
    flex-direction: row;
    justify-content: space-around;
}

#tabela {
    border-collapse: collapse;
    width: 100%;
}

#tabela td, #tabela th {
    border: 3px dashed yellow;
    padding: 8px;
    text-align: center;
    width: 80px;
    color: yellow;
    font-size: 20px;
}

.botao-jogo {
    width: 100%;
    color: yellow;
    font-size: 20px;
    background-color: black;
    margin-top: 5px;
    margin-bottom: 5px;
}

.botao-jogo:hover {
    background-color: #acacac;
}

.titulo {
    color: yellow;
    font-size: 26px;
    text-align: center;
}

#combo-escolha {
    color: yellow;
    background-color: black;
    font-size: 19px;
    padding: 3px;
}

#Mensagem{
    background-color: darkred;
}



