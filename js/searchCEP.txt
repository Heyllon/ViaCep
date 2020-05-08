//Instanciando o Botão
let btnCEP = document.querySelector('button');

//Obtendo a ação realização no click do botão
btnCEP.addEventListener('click', function () {

  let cep = document.querySelector('#cep').value;

  let api = `https://viacep.com.br/ws/${cep}/json/`;

  let request = new XMLHttpRequest();
  request.open('GET', api);

  request.onload = function () {
    console.dir(JSON.parse(request.responseText));
    console.log(JSON.parse(request.responseText).logradouro);
    console.log(JSON.parse(request.responseText).bairro);
    console.log(JSON.parse(request.responseText).uf);

    //Transforma o JSON retornado em um objeto do JavaScript
    let address = JSON.parse(request.responseText);

    //Pega o objeto retorno e adiciona na DIV do HTML
    let street = document.querySelector('#street');
    street.innerHTML = `<strong>Logradouro:</strong> ` + address.logradouro;

    let district = document.querySelector('#district');
    district.innerHTML = `<strong>Bairro:</strong> ` + address.bairro;

    let city = document.querySelector('#city');
    city.innerHTML = `<strong>Cidade:</strong> ` + address.localidade;

    //obtendo o valor do produto
    var vlrprod = document.getElementById('vlrp')
    var vlrDoFrete = document.getElementById('vlrDoFrete')
    var valor = Number(vlrprod.value)

    //Calculo da porcentagem por UF
    switch(address.uf){
      case 'SP':
        var porcentagem = Number(vlrprod.value * 0.3)
        break
      case 'DF':
        var porcentagem = Number(vlrprod.value * 0.55)
        break
      case 'GO':
        var porcentagem = Number(vlrprod.value * 0.55)
        break
      case 'MT':
        var porcentagem = Number(vlrprod.value * 0.65)
        break
      case 'MS':
        var porcentagem = Number(vlrprod.value * 0.6)
        break
      case 'RS':
        var porcentagem = Number(vlrprod.value * 0.6)
        break
      case 'SC':
        var porcentagem = Number(vlrprod.value * 0.5)
        break
      case 'PR':
        var porcentagem = Number(vlrprod.value * 0.4)
        break
      case 'ES':
        var porcentagem = Number(vlrprod.value * 0.7)
        break
      case 'MG':
        var porcentagem = Number(vlrprod.value * 0.8)
        break
      case 'BA':
        var porcentagem = Number(vlrprod.value * 0.9)
        break
      case 'SE':
        var porcentagem = Number(vlrprod.value * 0.85)
        break
      case 'AL':
        var porcentagem = Number(vlrprod.value * 0.9)
        break
      case 'PE':
        var porcentagem = Number(vlrprod.value * 0.95)
        break
      case 'PB':
        var porcentagem = Number(vlrprod.value * 0.95)
        break
      case 'RN':
        var porcentagem = Number(vlrprod.value * 1.40)
        break
      case 'CE':
        var porcentagem = Number(vlrprod.value * 1.00)
        break
      case 'PI':
        var porcentagem = Number(vlrprod.value * 1.40)
        break
      case 'MA':
        var porcentagem = Number(vlrprod.value * 1.45)
        break
      case 'TO':
        var porcentagem = Number(vlrprod.value * 0.85)
        break
      case 'RN':
        var porcentagem = Number(vlrprod.value * 1.40)
        break
      case 'AP':
        var porcentagem = Number(vlrprod.value * 1.45)
        break
      case 'PA':
        var porcentagem = Number(vlrprod.value * 1.45)
        break
      case 'RR':
        var porcentagem = Number(vlrprod.value * 1.40)
        break
      case 'AM':
        var porcentagem = Number(vlrprod.value * 1.30)
        break
      case 'AC':
        var porcentagem = Number(vlrprod.value * 1.45)
        break
      case 'RO':
        var porcentagem = Number(vlrprod.value * 1.40)
        break
      default:
        vlrDoFrete.innerHTML = '[ERRO] UF nao encontrada.'
        break
    }

    //Formula de calculo de frete
    valor = parseFloat(vlrprod.value) + parseFloat(porcentagem) 

    //apresentando o valor do final frete
    vlrDoFrete.innerHTML = `O valor do Frete é <strong>${valor.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' })}</strong>`;

  }

  //console.log(cep);
  request.send();

});