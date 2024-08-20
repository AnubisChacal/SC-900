---
created: 16-08-2024
tags:
  - Sc-900
---
# O modelo de camadas de segurança da Azure

É a camada mais interna e crítica, onde são aplicadas as proteções diretamente sobre os dados armazenados e processados. Isso inclui criptografia de dados em repouso, políticas de governança de dados e backup seguro.

![Pasted image 20240816104036.jpg](https://drive.google.com/file/d/13L_1P8LPzcD29BDn-VsKlVlZ2F6mnGFe/view?usp=sharing)

## Camada de dados -  Modelo OSI

A camada de enlace de dados é a segunda camada do modelo OSI e sua principal função é garantir que os dados sejam transferidos de maneira confiável entre dois nós diretamente conectados em uma rede. Essa camada se posiciona entre a camada física (responsável pela transmissão bruta de bits) e a camada de rede (responsável pelo roteamento dos dados entre redes diferentes).![[Pasted image 20240816104002.jpg]]

# Como a camada de dados funciona ?

A camada de **Dados** no modelo de camadas de segurança da Azure é a mais interna e crítica, pois se concentra diretamente na proteção dos dados armazenados e processados no ambiente da nuvem. Dado que os dados são frequentemente o alvo final de ameaças, essa camada é projetada para garantir que os dados permaneçam seguros, confidenciais e disponíveis apenas para usuários e sistemas autorizados. 
###### _A abordagem de defesa em profundidade em camadas conforme mostrado na imagem abaixo e se movimenta de fora para dentro:
![[Pasted image 20240816104801.png]]

# Ferramentas e metodologias para a proteção da camada de dados

### [Network security]([Network security concepts and requirements in Azure | Microsoft Learn](https://learn.microsoft.com/en-us/azure/security/fundamentals/network-overview))

O objetivo é garantir que apenas o tráfego legítimo seja permitido. O Azure inclui uma infraestrutura de rede robusta para dar suporte aos requisitos de conectividade de aplicativos e serviços.

**opções que o Azure oferece na área de segurança de rede**

- Azure networking
- Network access control
- Azure Firewall
- Secure remote access and cross-premises connectivity
- Availability
- Name resolution
- Perimeter network (DMZ) architecture
- Azure DDoS protection
- Azure Front Door
- Traffic manager
- Monitoring and threat detection

### [Access management]([Práticas recomendadas de segurança de identidade e acesso do Azure | Microsoft Learn](https://learn.microsoft.com/en-us/azure/security/fundamentals/identity-management-best-practices))

coleção de práticas recomendadas de segurança de controle de acesso e gerenciamento de identidade do Azure.
A base de praticas é retirada do [Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/active-directory/fundamentals/active-directory-whatis)

Para cada prática recomendada, o azure explica:

- Qual é a melhor prática
- Por que você deseja habilitar essa prática recomendada
- Qual pode ser o resultado se você não habilitar a prática recomendada?
- Alternativas possíveis às melhores práticas
- Como você pode aprender a habilitar as melhores práticas

### [Threat protection]([Proteção contra ameaças do Azure | Microsoft Learn](https://learn.microsoft.com/en-us/azure/security/fundamentals/threat-detection))

O Azure oferece funcionalidade interna de proteção contra ameaças por meio de serviços como Microsoft Entra ID, logs do Azure Monitor e Microsoft Defender para Nuvem. Essa coleção de serviços e recursos de segurança fornece uma maneira simples e rápida de entender o que está acontecendo em suas implantações do Azure.

O Microsoft Entra ID Protection é mais do que uma ferramenta de monitoramento e relatórios. Para proteger as identidades da sua organização, você pode configurar políticas baseadas em risco que respondem automaticamente aos problemas detectados quando um nível de risco especificado é atingido![[Pasted image 20240816111956.png]]

### [Information Protection]([What is Azure Information Protection (AIP)? | Microsoft Learn](https://learn.microsoft.com/en-us/azure/information-protection/what-is-information-protection))

A AIP (Proteção de Informações do Azure) fornece o serviço de criptografia, [Azure Rights Management](https://learn.microsoft.com/en-us/azure/information-protection/what-is-azure-rms), que é usado pela Proteção de Informações do Microsoft Purview e os seguintes recursos:

- [Rótulos de confidencialidade](https://learn.microsoft.com/en-us/purview/sensitivity-labels)
- [Cliente de Proteção de Informações do Microsoft Purview](https://learn.microsoft.com/en-us/purview/information-protection-client)
- [Verificador de Proteção de Informações do Microsoft Purview](https://learn.microsoft.com/en-us/purview/deploy-scanner)
- [SDK da Proteção de Informações da Microsoft](https://learn.microsoft.com/en-us/azure/information-protection/what-is-information-protection#microsoft-information-protection-sdk)

# Boa praticas aplicadas a camada de dados 

As boas práticas de segurança de dados na camada de segurança da Azure são fundamentais para garantir que os dados armazenados e processados no ambiente de nuvem estejam protegidos contra ameaças e acessos não autorizados

## [Criptografia de Dados em Repouso e em Trânsito]([Visão geral da criptografia do Azure | Microsoft Learn](https://learn.microsoft.com/pt-br/azure/security/fundamentals/encryption-overview))

- **[Repolso]([Visão geral da criptografia do Azure | Microsoft Learn](https://learn.microsoft.com/pt-br/azure/security/fundamentals/encryption-overview#encryption-of-data-at-rest))** - A azure recomenda que quando tratamos de dados em repolso seja executado a tratativa de criptografia desses dados do lado do cliente e do lado do serviço,  em ambas as situações a azure recomenda a criptografia do tipo [AES]([Advanced Encryption Standard – Wikipédia, a enciclopédia livre (wikipedia.org)](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard))
  
- **[Transito]([Visão geral da criptografia do Azure | Microsoft Learn](https://learn.microsoft.com/pt-br/azure/security/fundamentals/encryption-overview#encryption-of-data-in-transit))** - Quando tratamos de dados em trasinto a azure informa que quando os dados se movem entre data centers, fora dos limites físicos não controlados pela Microsoft (ou em nome da Microsoft), é utilizado o metodo de criptografia [MACsec]([802.1AE: Segurança MAC (MACsec) | (ieee802.org)](https://1.ieee802.org/security/802-1ae/))
	- Quando falomos de um cenario entre cliente e servidor a microsoft fornesse a metodologia do protocolo [TLS]([RFC 8446: The Transport Layer Security (TLS) Protocol Version 1.3 (rfc-editor.org)](https://www.rfc-editor.org/rfc/rfc8446))

> [!NOTE]
>  OBS.: Em alguns momentos dentro do ambiente de desenvolvimento ou infreestrutura pode ser sitado sobre o [protocolo SSL]([RFC 6101: The Secure Sockets Layer (SSL) Protocol Version 3.0 (rfc-editor.org)](https://www.rfc-editor.org/rfc/rfc6101)) e é importante salientar que o mesmo foi oficialmente considerado obsoleto a partir de 2015

## Gerenciamento de Identidade e Acesso (IAM)
