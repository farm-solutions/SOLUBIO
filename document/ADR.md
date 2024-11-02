
# Arquivo de Decisão Arquitetural (ADR)

## Título: Arquitetura para Chatbot da Dra. Jô

### Contexto
A Solubio deseja implementar um chatbot que atenda a diversas necessidades dos clientes e prospects, como renegociações, consultas de faturamento, geração de boletos, suporte/manutenção, entre outras. A solução deve ser escalável, garantir um atendimento de qualidade, reduzir o tempo de resposta e melhorar a experiência do usuário. Além disso, é importante considerar a conformidade com a Lei Geral de Proteção de Dados (LGPD) e oferecer uma solução que permita futuras expansões, caso o número de usuários aumente.

### Decisão
Optou-se por uma arquitetura em nuvem baseada em microserviços, com integração de um modelo de Processamento de Linguagem Natural (NLP) para melhor compreensão das solicitações dos usuários. A arquitetura usa serviços da AWS para escalabilidade, segurança e monitoramento. Componentes importantes incluem o AWS Route 53, API Gateway, AWS Cognito, AWS Lambda, AWS DynamoDB e AWS Bedrock com um modelo de NLP (GPT). Também foram considerados sistemas externos para RAG (Recuperação de Documentos Assistida por IA) e gerenciamento de APIs externas.

### Justificativa
1. **Escalabilidade**: A arquitetura em nuvem permite expandir rapidamente conforme a necessidade, garantindo que o chatbot atenda um volume crescente de interações.
2. **Facilidade de Integração**: Com o uso de AWS API Gateway, o sistema pode integrar-se facilmente a outros sistemas, fornecendo uma camada de abstração para chamadas externas.
3. **Segurança**: O uso do AWS Cognito para autenticação assegura que apenas usuários autorizados tenham acesso a determinados serviços. O AWS Secrets Manager será utilizado para armazenar de maneira segura as credenciais de acesso a APIs externas.
4. **Redução no Tempo de Resposta**: A arquitetura em microserviços, combinada com o uso de AWS Lambda para processamento, otimiza o tempo de resposta do sistema.
5. **LGPD**: O uso de serviços como DynamoDB para gestão de contexto e RDS PostgreSQL para informações de auditoria e histórico de interações assegura que os dados dos clientes sejam tratados de acordo com as leis de privacidade.

### Implicações
- **Custo Mensal**: Cada componente AWS pode ter um custo associado. Como o projeto é inicial e tem um crédito de $50 para testes, espera-se que a AWS forneça as necessidades básicas para o MVP. Futuramente, os custos devem ser reavaliados conforme o uso e a escalabilidade.
- **Manutenção Contínua**: A arquitetura baseada em IA e NLP precisa de constante monitoramento e atualização. A precisão das respostas pode diminuir com o tempo se os dados de treinamento não forem atualizados regularmente.
- **Experiência do Usuário**: É crucial que o chatbot forneça respostas rápidas e úteis, evitando repetições ou respostas ambíguas, o que impacta diretamente a satisfação do cliente.

### Alternativas Consideradas
1. **Chatbot baseado em regras**: Essa alternativa foi descartada, pois limitar-se a respostas predefinidas restringiria a flexibilidade e adaptabilidade necessárias para atender a múltiplas demandas de clientes e prospects.
2. **Hospedagem On-premises**: Consideramos uma arquitetura local, mas a descartamos devido a desafios de escalabilidade, custo de manutenção de infraestrutura e a necessidade de atualizações constantes.

### Consequências
- **Positivas**: Espera-se que o chatbot ofereça um suporte eficaz e imediato aos clientes, aumentando a satisfação e otimizando o atendimento. A Solubio poderá escalar a solução conforme a base de clientes cresce.
- **Negativas**: O modelo baseado em IA pode ter um custo de manutenção mais alto devido a necessidade de atualização contínua de dados e melhorias no modelo NLP.

### Resultados Esperados
- **Redução de Custo Operacional**: Automatização de tarefas repetitivas, como consultas de faturas e renegociações, reduz a necessidade de atendimento humano.
- **Melhora na Satisfação do Cliente**: Respostas rápidas e precisas aumentam a experiência positiva do usuário.
- **Eficiência e Escalabilidade**: A arquitetura em nuvem permite que o sistema cresça conforme a demanda, com componentes como o AWS Lambda e o DynamoDB ajustando-se automaticamente ao volume de solicitações.
