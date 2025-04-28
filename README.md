<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Loja Bombeiro Civil</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #fff;
            margin: 0;
            padding: 20px;
            color: #333;
        }
        header {
            background-color: #c40000;
            color: #fff;
            padding: 20px;
            text-align: center;
            border-radius: 8px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 12px;
            text-align: center;
        }
        th {
            background-color: #f7b500;
            color: #000;
        }
        tr:nth-child(even) {
            background-color: #f2f2f2;
        }
        footer {
            margin-top: 40px;
            text-align: center;
            font-size: 14px;
            color: #777;
        }
        .formulario {
            margin-top: 30px;
            background-color: #f9f9f9;
            padding: 20px;
            border-radius: 8px;
        }
        .formulario input, .formulario select {
            width: 100%;
            padding: 10px;
            margin-top: 10px;
            margin-bottom: 20px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        .formulario button {
            background-color: #c40000;
            color: white;
            padding: 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            width: 100%;
            font-size: 16px;
        }
        .formulario button:hover {
            background-color: #a30000;
        }
    </style>
</head>
<body>

<header>
    <h1>Loja Virtual - Equipamentos para Bombeiro Civil</h1>
</header>

<table>
    <thead>
        <tr>
            <th>Produto</th>
            <th>Preço</th>
            <th>Tamanhos/Numeração</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Calça</td>
            <td>R$ 180,00</td>
            <td>36, 38, 40, 42, 44, 46, 48, 50, 52</td>
        </tr>
        <tr>
            <td>Coturno</td>
            <td>R$ 250,00</td>
            <td>37, 38, 39, 40, 41, 42, 43, 44</td>
        </tr>
        <tr>
            <td>Gandola</td>
            <td>R$ 215,00</td>
            <td>P, M, G, GG, XG</td>
        </tr>
        <tr>
            <td>Camisa Acochoada</td>
            <td>R$ 90,00</td>
            <td>P, M, G, GG, XG</td>
        </tr>
        <tr>
            <td>Porta-Treco</td>
            <td>R$ 90,00</td>
            <td>Tamanho Único</td>
        </tr>
        <tr>
            <td>Cinto Tático</td>
            <td>R$ 50,00</td>
            <td>Ajustável</td>
        </tr>
        <tr>
            <td>Gorro (Pala)</td>
            <td>R$ 45,00</td>
            <td>Tamanho Único</td>
        </tr>
    </tbody>
</table>

<section class="formulario">
    <h2>Realizar Pedido</h2>
    <form id="pedidoForm">
        <label for="produto">Produto:</label>
        <select id="produto" required>
            <option value="Calça">Calça</option>
            <option value="Coturno">Coturno</option>
            <option value="Gandola">Gandola</option>
            <option value="Camisa Acochoada">Camisa Acochoada</option>
            <option value="Porta-Treco">Porta-Treco</option>
            <option value="Cinto Tático">Cinto Tático</option>
            <option value="Gorro (Pala)">Gorro (Pala)</option>
        </select>

        <label for="tamanho">Tamanho/Número:</label>
        <select id="tamanho" required>
        </select>

        <label for="nome">Seu Nome:</label>
        <input type="text" id="nome" placeholder="Digite seu nome" required>

        <button type="submit">Enviar Pedido</button>
    </form>
</section>

<footer>
    <p>Entre em contato para pedidos e disponibilidade de tamanhos! &#128293;</p>
</footer>

<script>
    const tamanhos = {
        "Calça": ["36", "38", "40", "42", "44", "46", "48", "50", "52"],
        "Coturno": ["37", "38", "39", "40", "41", "42", "43", "44"],
        "Gandola": ["P", "M", "G", "GG", "XG"],
        "Camisa Acochoada": ["P", "M", "G", "GG", "XG"],
        "Porta-Treco": ["Tamanho Único"],
        "Cinto Tático": ["Ajustável"],
        "Gorro (Pala)": ["Tamanho Único"]
    };

    const produtoSelect = document.getElementById('produto');
    const tamanhoSelect = document.getElementById('tamanho');

    function atualizarTamanhos() {
        const produto = produtoSelect.value;
        tamanhoSelect.innerHTML = '';
        tamanhos[produto].forEach(function(tam) {
            const option = document.createElement('option');
            option.value = tam;
            option.textContent = tam;
            tamanhoSelect.appendChild(option);
        });
    }

    produtoSelect.addEventListener('change', atualizarTamanhos);
    atualizarTamanhos();

    document.getElementById('pedidoForm').addEventListener('submit', function(event) {
        event.preventDefault();

        var produto = document.getElementById('produto').value;
        var tamanho = document.getElementById('tamanho').value;
        var nome = document.getElementById('nome').value;

        var mensagemTexto = `Pedido Loja Bombeiro Civil\nProduto: ${produto}\nTamanho: ${tamanho}\nNome: ${nome}`;

        // Cria o arquivo txt para download
        var blob = new Blob([mensagemTexto], { type: 'text/plain' });
        var link = document.createElement('a');
        link.href = window.URL.createObjectURL(blob);
        link.download = `Pedido_${nome.replace(/\s+/g, '_')}.txt`;
        link.click();

        // Depois abre o WhatsApp
        var mensagemWhatsApp = `Olá, gostaria de realizar um pedido!%0AProduto: ${produto}%0ATamanho: ${tamanho}%0ANome: ${nome}`;
        var telefone = '558799865141';

        setTimeout(function() {
            window.open(`https://api.whatsapp.com/send?phone=${telefone}&text=${mensagemWhatsApp}`, '_blank');
        }, 500);
    });
</script>

</body>
</html>
