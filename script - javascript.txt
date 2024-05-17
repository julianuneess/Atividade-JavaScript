document.addEventListener('DOMContentLoaded', function () {
    const form = document.getElementById('passagemForm');
    const origemInput = document.getElementById('origem');
    const destinoInput = document.getElementById('destino');
    const quantidadeInput = document.getElementById('quantidade');
    const classeInput = document.getElementById('classe');
    const idaVoltaCheckbox = document.getElementById('ida-volta');

    const disponibilidadeCidades = [
        { cidade: 'Salvador', idaVoltaDisponivel: true },
        { cidade: 'Rio de Janeiro', idaVoltaDisponivel: false },
        { cidade: 'São Paulo', idaVoltaDisponivel: true },
        { cidade: 'Belo Horizonte', idaVoltaDisponivel: true }, 
        { cidade: 'Brasília', idaVoltaDisponivel: false }, 
        { cidade: 'Recife', idaVoltaDisponivel: true },
        { cidade: 'Fortaleza', idaVoltaDisponivel: true },
        { cidade: 'Manaus', idaVoltaDisponivel: false },
        { cidade: 'Curitiba', idaVoltaDisponivel: true },
        { cidade: 'Florianópolis', idaVoltaDisponivel: true }, 
        { cidade: 'Cuiabá', idaVoltaDisponivel: true }, 
        { cidade: 'Porto Alegre', idaVoltaDisponivel: false },
    ]; 

    form.addEventListener('submit', function (event) {
        event.preventDefault();

        const origem = origemInput.value.trim();
        const destino = destinoInput.value.trim();
        const quantidade = quantidadeInput.value.trim();
        const classe = classeInput.value.trim();
        const idaVolta = idaVoltaCheckbox.checked;

        if (origem === '' || destino === '' || quantidade === '' || classe === '') {
            alert('Por favor, preencha todos os campos.');
            return;
        }

        function verificarDisponibilidadeCidade(cidade) {
            const cidadeInfo = disponibilidadeCidades.find(info => info.cidade === cidade);
            if (cidadeInfo) {
                return cidadeInfo.idaVoltaDisponivel;
            } else {
                return false; 
            }
        }

        const idaVoltaDisponivelOrigem = verificarDisponibilidadeCidade(origem);
        const idaVoltaDisponivelDestino = verificarDisponibilidadeCidade(destino);

        if ((!idaVoltaDisponivelOrigem || !idaVoltaDisponivelDestino) && idaVolta) {
            alert('Passagens de ida e volta não estão disponíveis para a cidade de origem ou destino.');
            return;
        }

        if (origem === destino) {
            alert('A cidade de origem e destino devem ser diferentes.');
            return;
        }

        alert('Buscando dados...');
    });

    document.getElementById('random-destination-link').addEventListener('click', function (event) {
        window.location.href = 'lista-de-cidades.html';
    });
});
