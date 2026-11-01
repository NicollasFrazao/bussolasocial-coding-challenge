1.  **Objetivo**
    *   Desenvolver um módulo que simule um carrinho de compras básico, calculando o valor final de uma compra com base nos itens adicionados e na forma de pagamento escolhida.

2.  **Descrição**
    *   Implemente um módulo (pode ser uma classe, função ou conjunto de funções) que contenha a lógica para calcular o valor total de uma compra com base nos itens adicionados ao carrinho e no método de pagamento. 

    *   Não é necessário implementar nenhuma integração com banco de dados, APIs, ou gateways de pagamento; foque apenas na lógica e nos cálculos necessários.

    *   Tente fazer algum teste automatizado(Teste unitário).

3.  **Entrega**
    *   Formato: Faça o upload do seu código em um repositório público no GitHub e envie o link por e-mail.

    *   Prazo: O desafio deve ser entregue em até 1 semana.

4.  **Especificações da Implementação**
    *   Linguagem de programação: Utilize a linguagem da sua preferência.

    *   Função ou Classe Principal: Crie uma função ou classe que receba como entrada uma lista de itens e o método de pagamento escolhido. A função ou classe deve retornar o valor final da compra.

    *   Métodos de Pagamento: Implemente três métodos de pagamento:
        *   Pix (pagamento à vista)

        *   Cartão de Crédito à Vista (1x)

        *   Cartão de Crédito Parcelado (de 2 a 12 parcelas)

    *   No código, utilize a função ou classe principal para calcular o valor final da compra para cada uma das três formas de pagamento mencionadas.

    *   Observação: Existem várias maneiras de implementar o desafio; não há resposta certa ou errada. Escolha a solução que melhor demonstre suas habilidades técnicas.

    *   Dúvidas: Fique à vontade para entrar em contato se tiver alguma dúvida.

5.  **Regras de negócio**
    *   Estrutura dos Itens: Cada item no carrinho deve conter:
        *   Nome

        *   Preço unitário

        *   Quantidade

    *   Formas de pagamento aceitas:
        *   Pix (à vista)

        *   Cartão de Crédito à Vista (1x)

        *   Cartão de Crédito Parcelado (de 2 a 12 parcelas)

    *   Dados de Pagamento com Cartão: No caso de pagamento com cartão de crédito, inclua os seguintes dados de entrada:
        *   Nome do titular do cartão

        *   Número do cartão de crédito

        *   Data de validade do cartão

        *   Código de segurança (CVV)

    *   Regras de Descontos e Juros:
        *   Desconto para Pagamento à Vista: Para pagamentos à vista (Pix ou Cartão de Crédito à Vista), aplique um desconto de 10% sobre o valor total da compra.

        *   Juros para Pagamento Parcelado: Para pagamentos com Cartão de Crédito Parcelado, aplique uma taxa de juros de 1% ao mês sobre o valor total da compra.

            *   Para o cálculo do valor total com juros compostos, utilize a seguinte fórmula:

                *   `M = P*(1 + i)^n`

                *   Onde:
                    *   `M` é o montante final, ou seja, o valor total da compra com juros aplicados.

                    *   `P` é o principal, ou seja, o valor inicial (total da compra sem juros).

                    *   `i` é a taxa de juros por período, que deve ser expressa em decimal. No caso de 1% ao mês, seria 0,01.

                    * `n` é o número de períodos (número de meses, no caso de uma taxa mensal).

        * O cálculo do valor final da compra deve ser feito considerando a forma de pagamento selecionada, aplicando descontos e acréscimos conforme descrito nas regras de negócio.